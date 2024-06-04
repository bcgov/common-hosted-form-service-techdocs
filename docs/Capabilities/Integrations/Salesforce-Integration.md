[Home](index) > [Capabilities](Capabilities) > [Integrations](Integrations) > **Salesforce Integration** 
***

Salesforce is one of many ways to work with form submission data.  

## Salesforce Integration

By creating a new Salesforce query you can work with the submission data.

### CHEFS Form Information

You will need this information about your form:
- The `formId` and `formVersionId`. One way to retrieve them is to "Manage" your form and in the table at the bottom click "Version 1" (or the version you want). The URL in the new browser window will contain ".../preview?f={formId}&v={formVersionId}"
- Your form's [API Key](../Data-Management/Generating-API-keys)

### Salesforce Configuration: Submissions

- Use Salesforce to `Get data` from a URL or `Web` location
- Use the URL `https://submit.digital.gov.bc.ca/app/api/v1/forms/{formId}/versions/{formVersionId}/submissions` to get the submissions for a version of your form - you will need to replace `{formId}` and `{formVersionId}` with the values for your form
- The type of authentication to use is "Basic".
- "User name" will be set to your `formId`
- "Password" will be set to your API Key

### Salesforce Configuration: Submission Statuses

It is also possible to get the list of statuses for each submission.

- Use Salesforce to `Get data` from a URL or `Web` location
- Use the URL `https://submit.digital.gov.bc.ca/app/api/v1/submissions/{formSubmissionId}/status` to get the statuses for each submission - you will need to replace `{formSubmissionId}` with the `id` value for each submission 
- The type of authentication to use is "Basic".
- "User name" will be set to your `formId`
- "Password" will be set to your API Key

***
[Terms of Use](Terms-of-Use) | [Privacy](Privacy) | [Security](Security) | [Service Agreement](Service-Agreement) | [Accessibility](Accessibility)
