[Home](index) > [Capabilities](Capabilities) > [Functionalities](Functionalities) > **Submit to Email**
***

# Submit to Email

> **EXPERIMENTAL**
>
> Submit to Email is now available on the entire CHEFS platform. It is still marked with an "experimental" icon in the form settings while the CHEFS team gathers feedback. Please share your experience through the [CHEFS Teams channel](https://teams.microsoft.com/l/channel/19%3A34b9d4b4deb54eebaa9be8bc1ccf02f7%40thread.tacv2/CHEFS%20(Exchange%20Lab%20Team)?groupId=bef8086f-20c7-43a4-bd07-29ce764e818c&tenantId=6fdb5200-3d0d-4a8a-b036-d3685e359adc).

## Overview

Submit to Email lets a form owner send a formatted copy of every submission to one or more email recipients automatically. CHEFS renders the submission through a document template you supply (a CDOGS template), zips the rendered document together with any files the submitter attached, and delivers the package by email after the submission is received.

This is useful when:

- The submission needs to reach a shared mailbox or a downstream team as soon as it arrives.
- You want a portable, human-readable record of each submission (rendered document + attachments) rather than a link back into CHEFS.
- You need to hand off submission content to a system or reviewer who does not have a CHEFS account.

---

## Before you begin

You need two things ready:

1. **A document template** for the rendered submission. This is the same kind of CDOGS template used for [Download a submission with custom format (CDOGS)](CDOGS-Template-Upload). If you have not built one yet, follow that page first.
2. **One or more recipient email addresses**. These are the people or shared mailboxes that will receive the package for every submission.

---

## Enabling the feature

1. Open your form's **Settings**.
2. In the **Form Functionality** panel, tick the checkbox labelled **"Email submission package with document template"**. An "experimental" icon next to the label indicates the feature is still marked experimental.
3. Add at least one **recipient email address**. Press Enter, space, or comma between addresses to add more than one.
4. Select the **document template** that will be used to render each submission.
5. Save the form settings.

The recipient list and the document template are both required when the feature is enabled. CHEFS blocks Save if either is missing, because a package job without them can only ever fail.

---

## How delivery works

After a submission is received, CHEFS queues a background job that:

1. Renders the submission through the selected document template.
2. Collects any files the submitter attached.
3. Chooses a delivery mode based on the size of the package:
   - **Inline attachment.** If the rendered document is small enough and the total attachment size and count are within platform limits, the package is sent as attachments on the email.
   - **Download link.** If any of those limits are exceeded, CHEFS instead stores the package as a zip in submission storage and emails the recipients a download link.

The submitter's completion experience is unchanged; the package email is sent to the recipient list you configured, not to the submitter.

### Package delivery limits

The current platform-wide limits that decide inline vs link delivery:

- Rendered document up to **5 MB**.
- Total attachments up to **10 MB**.
- At most **10 attachments** on a single submission.

A submission that exceeds any of these is still delivered; it just arrives as a link to a stored zip instead of inline.

---

## Retries and failures

Package jobs are processed in the background and retried on transient failures (for example, a temporary email service outage). A job that keeps failing for a permanent reason (bad template, invalid recipient address) is marked as failed and stops retrying. Fix the underlying setting on the form and future submissions will send normally; previously failed jobs are not automatically re-sent.

---

## Privacy and data handling

Submissions can contain sensitive information. Before enabling this feature, confirm:

- The recipient mailbox is appropriate to receive the submission content in email form.
- The recipients understand they are receiving copies of every submission, including any attachments.
- Your Privacy Impact Assessment (PIA) covers sending submission content outside CHEFS by email.

If you are not sure, review [Privacy and data collection](Privacy-and-data-collection) or ask through the CHEFS Teams channel before turning the feature on for a live form.

---

## FAQ

**Does the submitter receive the package?**
No. The package is sent to the recipient list configured on the form, not to the submitter. The submitter still sees the normal completion page.

**Can I change the template after the form is live?**
Yes. Update the selected template in Form Settings and Save. New submissions use the new template; previously delivered emails are not re-sent.

**What happens if I remove all recipients?**
CHEFS will not let you save the settings with the feature enabled and no recipients. Either add a recipient, or uncheck the feature to disable it.

**What happens if a submission exceeds the size limits?**
The package is delivered as a stored zip with a download link in the email instead of as inline attachments. Nothing is dropped.

**Is this feature available on all forms?**
Yes, on the entire CHEFS platform. The "experimental" icon indicates the feature is still marked experimental while feedback is collected; there is no separate request or allowlist required.

***
[Terms of Use](Terms-of-Use) | [Privacy](Privacy) | [Security](Security) | [Service Agreement](Service-Agreement) | [Accessibility](Accessibility)
