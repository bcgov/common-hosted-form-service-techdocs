[Home](index) > [Capabilities](Capabilities) > [Form Management](Form-Management) > **Accessing forms**
***

<!-- On this page:
- [To set form access](#to-set-form-access)
- [To use Log in Required with BCeID](#to-use-log-in-required-with-bceid) -->

## To set form access

You can choose from three levels of access for your form – **Public**, **Log-in Required**, and **Specific Team Members**.

Each option comes with its own set of considerations.

![img](images/chefs-form-access-fig5.png)
![img](images/chefs-form-access-fig1.png)

**Public (anonymous)**

The public option gives anyone access to your from, whether inside or outside government. 
Choose Public if you want to run an anonymous survey.

Some of the limitations when choosing Public as your access level are:
* The submitted cannot attach file uploads to their submission.
* The submitter cannot save their submission to finish later.
* The submitter cannot share their submission with others before they submit.

**Log-in required**

Requiring a submitter to log in limits your form to anyone with a **BC Services Card**, **Basic BCeID**, **Business BCeID**, **IDIR**, or **IDIR MFA** username and password. 

Requiring a log in enables several features for submitters. 
Submitters can:
* Save their submission and finish it later.
* Share their submission with colleagues.
* Use workflows.
* Review all their previous submissions. 

Requiring a login has some limitations:
* You can only select one of: BC Services Card, Basic BCeID, Business BCeID, or IDIR; you cannot allow multiple. **Note:** IDIR and IDIR MFA are treated as the same identity group - enabling IDIR also grants access to IDIR MFA users.
* Users often find getting a BCeID confusing.

**Specific Team Members**

If you only want a small group of people to access your form, choose **Specific Team Members**. 
To invite team members:

1. Click **My Forms**.
2. From your list of forms, click **Manage** for the form you want to update.
3. Click **Team Management** on the **Manage Form** page.

![img](images/chefs-form-access-fig2.png)


4. Under **Team Management**, check the box in the **Submitter** column for any user in the table you want to have access.

![img](images/chefs-form-access-fig3.png)

> **Note**: If there is no one on your team list, you will need to add them. [Learn how to add a user to your team](Managing-admin-teams).

To set the access for a new form:
1.	Click **Create a New Form**.
2.	In the **Form Access** section under **Form Settings**, select the appropriate level of access to your form.
3.	Finish selecting your form settings.
4.	Click **Continue**.

To update access to an existing form:
1.	Click **My Forms**.
2.	From your list of forms, click **Manage** for the form you want to update.
3.	Click **Edit** in the **Form Settings** header.

![img](images/chefs-form-access-fig4.png)

4.	In the **Form Access** section under **Form Settings**, choose the new access level you want to use.
5.	Click **Update** to accept the change.

## To use Log in Required with BCeID
<!-- **[Back to top](#top)** -->

If you decide to use **Basic BCeID** or **Business BCeID** for your form access, you must notify the Identity Information Management (IDIM) team by email (IDIM.Consulting@gov.bc.ca). They need to know which forms are using the BCeID service and allocate appropriate resources. 
You should provide them the following in your notification:

* Program area or initiative that owns the CHEFS form
* Contact Email address
* Estimate of how many submissions the form may receive per year

There are a few steps that IDIM will follow up and work with you on including a self-assessment and a signed service agreement:

* Submission of a BCeID onboarding self assessment to IDIM.Consulting@gov.bc.ca ( Client responsibility ) 
* Participation in Client | BCeID onboarding kickoff meeting ( Joint Client | IDIM responsibility ) 
* Client Supplementary Service added to Schedule B of the CHEFS Service Agreement ( Joint Client | IDIM responsibility) 
* Review and sign-off of Updated Service Agreement(s) (Client responsibility) 
* Creation of Online Service Directory (OSD) entries in BCeID application as part of your audit record (Client responsibility) 
* Submission of your project’s communications / invitations to the Public (that mention BCeID) submitted to IDIM.Consulting@gov.bc.ca for review and sign-off (Client responsibility) 
* Notify IDIM Consulting what your target Production Go-Live | BCeID account First Users date is - (please notify them if previously disclosed dates are moved or changed) (Client responsibility) 
* Provide estimates of BCeID end user account volumes (by BCeID account type) a) at launch and b) after the first year of operation - (please notify them if previously disclosed end user BCeID account volumes change) (Client responsibility) 
 
[Learn more about BCeID](https://www.bceid.ca/)

## To use Log in Required with BC Services Card

If your form is needing to trust that the name information provided is authentic, using an MFA protected, privacy protecting, and zero cost BC Government digital identity service without needing a username and password, look to the BC Services Card Account. To use BC Services Card Account for your form access, you must notify the Identity Information Management (IDIM) team by email ([IDIM.Consulting@gov.bc.ca](mailto:IDIM.Consulting@gov.bc.ca)). They need to know which forms use the BC Services Card Account and allocate appropriate resources. You should provide them the following in your notification:

* Program area or initiative that owns the CHEFS form
* Contact Email address
* Estimate of how many submissions the form may receive per year

There are a few steps that IDIM will follow up and work with you on:

* Participation in Client and BC Services Card Account onboarding kickoff meeting 
* Privacy Impact Assessment Update and checklist
* Submission of your project’s communications and/or invitations to the Public (that mention BC Services Card) submitted to [IDIM.Consulting@gov.bc.ca](mailto:IDIM.Consulting@gov.bc.ca) for review and sign-off
* Notify IDIM Consulting what your target Production Go-Live date and First Users date is with expected volumes - (please notify them if previously disclosed dates are moved or changed) 
* Additional forms created for a similar purpose and similar customer base may not have to go past the kickoff step but IDIM Consulting will advise you on that.

Learn more about [BC Services Card Account](https://id.gov.bc.ca/account/) 

Additional forms created for a similar purpose and similar customer base may not have to go past the self-assessment step but IDIM Consulting will advise you on that. 

> **Note:** BCeID and BC Services Card Account users cannot be added to your form as an administrator. See [Managing admin teams](Managing-admin-teams) for more details on how to add administrators to your form.

<!-- **[Back to top](#top)** -->

## IDIR with Multi-Factor Authentication (IDIR MFA)

CHEFS supports two IDIR login methods that are treated as equivalent for form access purposes:

| Login method | Identity provider hint | When to use |
|---|---|---|
| **IDIR** | `idir` | Standard IDIR login (no MFA required) |
| **IDIR MFA** | `azureidir` | IDIR login enforced through Azure AD with MFA |

### For form designers

When you configure a form to allow **IDIR** access, both IDIR and IDIR MFA users can submit and manage the form. You do not need to add IDIR MFA as a separate identity provider - the two are treated as the same identity group under the canonical code `idir`.

![img](images/chefs-form-access-fig1.png)

### For form users

When accessing a form or logging in from the CHEFS home page, you will see two IDIR login buttons:

- **IDIR** — redirects to the standard IDIR Keycloak login
- **IDIR MFA** — redirects to the Azure AD IDIR login, which enforces multi-factor authentication

![img](images/idir-mfa-and-idir-as-option.png)

Choose **IDIR MFA** for stronger authentication. Both options give you the same access to IDIR-enabled forms.

***
[Terms of Use](Terms-of-Use) | [Privacy](Privacy) | [Security](Security) | [Service Agreement](Service-Agreement) | [Accessibility](Accessibility)