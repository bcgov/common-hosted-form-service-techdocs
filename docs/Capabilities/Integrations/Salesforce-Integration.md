[Home](index) > [Capabilities](Capabilities) > [Integrations](Integrations) > **Salesforce Integration** 
***

Salesforce is one of many ways to work with form submission data.  

## Salesforce Integration using Named Credentials and External Services

By creating a new Salesforce External service you can work with the submission data.

### CHEFS Form Information

You will need this information about your form:
- The `formId` and `formVersionId`. One way to retrieve them is to "Manage" your form and in the table at the bottom click "Version 1" (or the version you want). The URL in the new browser window will contain ".../preview?f={formId}&v={formVersionId}"
- Your form's [API Key](../Data-Management/Generating-API-keys)

### Named Credentials in salesforce

**Named Credentials** allow Salesforce to manage authentication for calls to external systems. This simplifies the process of calling an external APIs by securely storing authentication details and abstracting the complexity of API authentication.

**Steps to Create Named Credentials:**

1. **Navigate to:** Setup > Named Credentials
2. **Click on:** New Named Credential
3. **Fill in the Details:**
   - **Label:** Enter a name for the credential (e.g., "CHEFSAPICredential").
   - **Name:** This is automatically populated based on the label.
   - **URL:** Enter the base URL of the external API as `https://submit.digital.gov.bc.ca/app/api/v1`
   - **Identity Type:** Select `Named Principal`
   - **Authentication Protocol:** Select `Basic Authentication`.
   - **Username:** Enter the API username. It will be `formId` in our case.
   - **Password:** "Password" will be set to your form [API Key](../Data-Management/Generating-API-keys)

4. **Save:** This securely stores the authentication details for accessing the external API.

### External Services in salesforce 

**External Services** in Salesforce allow you to connect to external APIs using a declarative approach.

**Steps to Create an External Service:**

1. **Navigate to:** Setup > External Services
2. **Click on:** New External Service
3. On the Select an API Source page, select whether you’re importing an API spec From Mulesoft Anypoint Platform, or From API Specification. Since we're using CHEFS spec here, select From API Specification.
4. **Fill in the Details:**
   - **Service Name:** Enter a name for the external service (e.g., "CHEFSAPIService").
   - **Named Credential:** Select the named credential you created earlier i.e. `CHEFSAPICredential`
   - **Service Schema:** Select `Relative URL`.
   - **URL**: Enter `/api-spec.yaml`, provides the Open API specification for all CHEFS API's. Any API's with Authorization as Basic Auth can be integrated with the salesforce External Services. Following are some of useful API's
        - Enter `/forms/{formId}/versions/{formVersionId}/submissions` to get the submissions for a version of your form - you will need to replace `{formId}` and `{formVersionId}` with the values for your form. 
        - Enter `/submissions/{formSubmissionId}/status` to get the statuses for each submission - you will need to replace `{formSubmissionId}` with the `id` value for each submission.

5. **Save & Next:** Salesforce will parse the OpenAPI specification and generate Apex actions.
6. You can now integrate and work with CHEFS data using the newly added External Service in your Apex code, Flow Builder, Process Builder, or any other Salesforce components that support External Service.

***
[Terms of Use](Terms-of-Use) | [Privacy](Privacy) | [Security](Security) | [Service Agreement](Service-Agreement) | [Accessibility](Accessibility)
