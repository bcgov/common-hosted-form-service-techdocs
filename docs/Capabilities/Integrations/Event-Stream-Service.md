[Home](index) > [Capabilities](Capabilities) > [Integrations](Integrations) > **CHEFS Event Stream Service** 
***  
# CHEFS Event Stream Service

CHEFS is adding an Event Streaming Service which allows Form Owners to consume and process real-time data about the forms (ex. a new version of the form has been published) and submissions. 

Currently, Form Owners can configure event notifications via webhook (see [Event Subscription](./Event-Subscription.md)). These events are elementary, with metadata providing the IDs and event types. Generally, once the event notification is received the external application/service calls back to CHEFS via the CHEFS API to retrieve the full event data (form schema, submission data). This approach works but unnecessarily loads the CHEFS API service, degrading performance for all forms. More significantly, the logic for when and why an event is fired is directly coded into CHEFS. This is unsustainable as each external application may have different requirements for why an event is fired - a callback to CHEFS API is needed to determine if the event should be processed. 

Moving forward, CHEFS will fire events (with encrypted payloads) and allow the consumers to define the logic for processing on their end. An Event Streaming Service allows multiple consumers to process the same event. For instance, the Form Owner can process the submission data, while a metrics reporter can add a count to their submissions totals, another service can analyze service loads by sector.

This initial phase will introduce the Event Streaming Service as a component of CHEFS, with the intention that it grows, matures, and becomes a Common Component.

**Table of content:**

- [NATS.io](#natsio)
- [CHEFS Stream](#chefs-stream)
- [Encryption](#encryption)
- [Onboarding](#onboarding)

## nats.io
<a id="natsio"></a>
[NATS](https://nats.io) is a connective technology built for the ever increasingly hyper-connected world. It is a single technology that enables applications to securely communicate across any combination of cloud vendors, on-premise, edge, web and mobile, and devices. NATS consists of a family of open-source products that are tightly integrated but can be deployed easily and independently. NATS is being used globally by thousands of companies, spanning use-cases including microservices, edge computing, mobile, IoT and can be used to augment or replace traditional messaging.

NATS has been successfully used by many other projects within the BC Government. It can be scaled horizontally and runs without the need for a paid operator (e.g., [Kafka](https://kafka.apache.org)). 

NATS has official clients in multiple mainstream languages so Form Owners shouldn't have to adopt a new language to write their event consumers.

### Event Stream
The CHEFS Event Stream is implemented as a [NATS JetStream](https://docs.nats.io/nats-concepts/jetstream). 

JetStream offers many benefits over a traditional publisher/subscriber relationship: replay policies, durability, bulk handling, starting from a specific sequence, and starting from a specific date.

As stream producers, we can set retention limits, such as the maximum message age and the maximum number of messages in the stream.


### Consumers
NATS allows a variety of consumer types and this is required reading: [JetStream Consumers](https://docs.nats.io/nats-concepts/jetstream/consumers).

**IMPORTANT** - currently, access is limited to WebSockets. Please ensure your client can use WebSockets! Some reading: [getting-started-nats-ws](https://nats.io/blog/getting-started-nats-ws/) and [here](https://github.com/nats-io/nats.ws).

**ALSO IMPORTANT** - The allowed encrypted message size is < 1 Mb. Encryption dramatically adds to the message size, meaning raw json included in the payload (ie. submission data) should be under 50kb. You will receive an error attribute in your event payload if the overall message is too large.

### Credentials
Consumers will use connect using [NKeys](https://docs.nats.io/running-a-nats-service/configuration/securing_nats/auth_intro/nkey_auth). 

> With NKeys the server can verify identities without ever storing or ever seeing private keys. The authentication system works by requiring a connecting client to provide its public key and digitally sign a challenge with its private key. The server generates a random challenge with every connection request, making it immune to playback attacks. The generated signature is validated against the provided public key, thus proving the identity of the client. If the public key is known to the server, authentication succeeds.

CHEFS will **not** store the private key (seed). Once it is delivered to you and your team, it is up to you to store it securely.

## CHEFS Stream
<a id="chefs-stream"></a>
CHEFS will publish events to a stream named: `CHEFS`.

Under this stream will be two major subject prefixes: 

1. `PUBLIC.forms`
2. `PRIVATE.forms`


Consumers specify which subjects they wish to process and often use wildcards. For example, a consumer can specify `PUBLIC.forms.>` and `PRIVATE.forms.submissions.>`. This would consume ALL public forms events and only private submission events.

`PUBLIC.forms` can be consumed by any client. These events will contain only metadata and no personal/private information. 

`PRIVATE.forms` can be consumed by any client but not fully understood. The payloads of these events will contain encrypted data. Only known and approved clients will have the key to decrypt the private information (ex., a form submission).

`PRIVATE.forms` events will generally be a superset of the `PUBLIC.forms` events with the extra encrypted information in the payloads. As the system evolves, there may be more types of `PUBLIC.forms` events that contain different types of metadata (e.g., metrics on Ministry, whether the form is API enabled, etc.).


### Events

As stated, the two major subjects are `PUBLIC.forms` and `PRIVATE.forms`; these will be further specified as follows:

`PUBLIC|PRIVATE.<domain>.<class>.<type>.<form id>`

- domain = `forms`
- class = `schema` or `submission`.
- type = `created`, `deleted`, `modified` and more
- form id = the id of the form firing these events


Using wildcards a consumer could listen for events on a specific form id or a specific type (i.e. only listen to submission created events across any form).


- `PUBLIC.forms.schema.published.<form id>`
- `PUBLIC.forms.schema.unpublished.<form id>`
- `PUBLIC.forms.submission.created.<form id>`
- `PUBLIC.forms.submission.modified.<form id>`
- `PUBLIC.forms.submission.deleted.<form id>`

More events to come.

### Event Metadata
The event metadata contains data from the subject (domain, class, type, form id) which will allow subject specific processing if the consumer/listener/subscriber is using wildcard subjects.

Other metadata will be provided as needed per type and only if the data is *NOT* considered private.

| Attribute | Notes |
| --- | --- |
| `source` | `chefs` - where did this event originate? |
| `domain` | `forms` - top level classification for event |
| `class` | `submission` or `schema` - secondary classification for event |
| `type` | `created`, `deleted`, `modified` - tertiary classification for event |
| `formId` | uuid - CHEFS form id. Form that originates the event |
| `formVersionId` | uuid - CHEFS form version id. Only if value exists at time of event. |
| `submissionId` | uuid - CHEFS submission id. Only applies for `submission` class events. |
| `draft` | boolean - For `submission` class events, the submission.draft value |

**IMPORTANT** - Ensure you filter your event messages against your expected `source`. Events from Pull Request and Dev environments will use the same server but will have different `source`: (e.g., `pr-1444` and `chefs-dev`).

An example to show the overall structure of an event message is: 

```json
{
  meta: {
    source: 'chefs',
    domain: 'forms',
    class: 'submission'
    type: 'modified',
    formId: <uuid>,
    formVersionId: <uuid>,
    submissionId: <uuid>,
    draft: false,
  },
  payload: {
    data: <encrypted>
  }

```

See [Custom Form Metadata](./Form-Metadata.md) for information about form metadata passed in the `meta` section of the event message.

### NATS Message Metadata

NATS messages contain very valuable metadata that consumers should leverage for optimal processing. Each message on the stream will have a [sequence number](https://github.com/nats-io/nats.docs/blob/803d660c33496c9b7ba42360945be58621bbba0b/nats-concepts/seq_num.md) and a timestamp. Consumers can schedule batch consumption based on the sequence or timestamp of their last processed event. 

### Example Consumer
Please review our [demo code](https://github.com/bcgov/common-hosted-form-service/blob/main/event-stream-service/pullConsumer.js) trivialized example of a [pull consumer](https://docs.nats.io/nats-concepts/jetstream/consumers). It is up to the external application that consumes/listens to the events to decide how to set up their consumer. This is one way in one language (JavaScript). Please review the documentation about [consumers](https://docs.nats.io/nats-concepts/jetstream/consumers) and review the approved [examples](https://natsbyexample.com) for more information.

The example will ask for a batch of messages every 5 seconds - illustrating some basic pull behaviour. We can see as it processes the messages that there is a sequence number (`m.seq`) and a timestamp (`m.info.timestampNanos`) which we could leverage for different [delivery policies](https://docs.nats.io/nats-concepts/jetstream/consumers#deliverpolicy) such as get all messages since X sequence number.

Of note is checking for errors when processing the event messages. As noted above, if CHEFS attempts to put too large of a message in the Event Stream, an error will be sent instead. You should track the IDs and use the appropriate CHEFS API to download the data directly.

**Do not use our demo code for your client! Simplified example only!**

## Encryption
<a id="encryption"></a>

To securely facilitate the transmission of sensitive data between systems, CHEFS will encrypt the payloads for `PRIVATE.forms` events. 

Initially, CHEFS will encrypt the payload using an `aes-256-gcm` that requires a  `sha256` hash as a key (256 bits/32 bytes/64 characters).

CHEFS will use the [cryptr](https://github.com/MauriceButler/cryptr) JavaScript library. External applications are not required to use Node.js/JavaScript but must test their implementation or library.

The Form Designer will have to `enable` private messages and encryption. CHEFS can generate a key, or the Form Designer can provide it. In either case, only CHEFS and the Form Designer should know the key. The Form Designer should store the key securely and make it accessible to their application/service/system following best practices.

Since the Form Designer can specify the key, they can use the same key for all of their forms. This will simplify processing in their systems. Plans for CHEFS include a grouping of forms, which also alleviates the complexity of mapping 1-to-1 key-to-form.

## Onboarding
<a id="onboarding"></a>

As a prerequisite to onboarding, you will need credentials: an Account Name and a Password. IDIR users can generate credentials [here](https://ess-app.apps.silver.devops.gov.bc.ca/gencreds). You must save the password securely and share it only with your development and/or DevOps team members who require it. Do **NOT** share the password with the Event Stream Service team or the CHEFS team. The password is not recoverable, nor does it persist elsewhere. If it is lost, generate a new set of credentials.


To leverage the Event Stream Service, please fill out the [Event Stream Service request form](https://submit.digital.gov.bc.ca/app/form/submit?f=9c85b764-291a-459e-8b81-a0583d5ea7bc).

Enter your Ministry, Organization, or Initiative and your Account Name. Add contact emails for yourself and your technical team and an estimated date for promotion to our Production environment (submit.digital.gov.bc.ca). The support team will inform you when your account is active in each environment: Development, Test and Production. The same account can be used in all environments.

The account will first be activated in the Development and Test environments so you can test your consumer client and workflows. The credentials will be emailed to you and your technical team. The CHEFS team will **not** retain your password; please follow your privacy and security policies to save your password.




