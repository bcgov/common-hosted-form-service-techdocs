[Home](index) > [Capabilities](Capabilities) > [Integrations](Integrations) > **Power BI Integration** 
***

Microsoft Power BI is one of many ways to work with form submission data. The web version of Power BI doesn't have the features needed to retrieve submissions, so download Power BI from the Microsoft Store.

## Power BI Query

By creating a new Power BI query you can work with the submission data.

You will need this information about your CHEFS form:
- `formId`   - To put in the datasource URL and to use as the username in for the basic authorization.  
- `API Key`  - To use as the password for the basic authorization. Instructions are available for [Generating API Keys](../Data-Management/Generating-API-keys)  
- `formVersionId` (optional) - If you want to filter to one version.
- `formSubmissionId` (optional) - If you want to get just one submission of a form.  

### To get all submissions for a CHEFS Form 
For the datasource, use the URL: `https://submit.digital.gov.bc.ca/app/api/v1/forms/{formId}/export?format=json`
replace `{formId}` with yours

### To get submissions for just one form version
- You will need the `formVersionId`. One way to retrieve them is to "Manage" your form and in the table at the bottom click "Version 1" (or the version you want).
- The URL in the new browser window will contain ".../preview?f={formId}&v={formVersionId}"
- to get the submissions for a version of your form - you will need to replace `{formId}` and `{formVersionId}` with these values from your form

### Query Configuration: Submissions  
__Open PowerBI Desktop version.__
- In the ribbon at the top of Power BI click `Get data` and select `Web`  
- depending on whether you want all submissions or just submission from one version, or just one submission, you will need to use a different URL for each:
  - ALL Submissions: `https://submit.digital.gov.bc.ca/app/api/v1/forms/{formId}/export?format=json`
  - Form Version Specific: `https://submit.digital.gov.bc.ca/app/api/v1/forms/{formId}/versions/{formVersionId}/submissions`
  - Submission Specific: `https://submit.digital.gov.bc.ca/app/api/v1/submissions/{formSubmissionId}/
- Choose "Basic" for the authorization type, with "User name" set to your `formId` and "Password" set to your API Key

### Query Configuration: Submission Statuses

It is also possible to get the list of statuses for each submission.

- In the ribbon at the top of Power BI click `Get data` and select `Web`
- Use the URL `https://submit.digital.gov.bc.ca/app/api/v1/submissions/{formSubmissionId}/status` to get the statuses for each submission - you will need to replace `{formSubmissionId}` with the `id` value for each submission 
- Choose "Basic" for the authorization type, with "User name" set to your `formId` and "Password" set to your API Key

***
[Terms of Use](Terms-of-Use) | [Privacy](Privacy) | [Security](Security) | [Service Agreement](Service-Agreement) | [Accessibility](Accessibility)
