[Home](../index) > [Group Forms](index) > **Features and Use Cases**
***

## About Page

Users log in to CHEFS as usual — there is no separate landing page or gateway for Group Forms. After logging in, the user lands on the **About** page, which now includes a promo box introducing multi-tenancy:

- A summary of who Group Forms is a good fit for (managing many forms across programs or environments, multiple administrators or reviewers, frequent staffing changes, centralized access management, or adopting other connected services such as Notify)
- A **Login to CSTAR to Get Started** button for team leads and administrators who want to set up a tenant

![Screenshot: About page showing the CHEFS multi-tenancy promo box and Login to CSTAR to Get Started button](images/group-forms-landing.png)

> **Note:** Group Forms is only available to IDIR-authenticated users. BCeID users are not supported for tenants and cannot use Group Forms.

## Logging In

Users authenticate into CHEFS through IDIR or BCeID as usual. Once authenticated, an API call is made to CSTAR to fetch all tenants the logged-in user belongs to.

---

## My Forms vs Group Forms

### Default State — My Forms

After logging in, the application defaults to My Forms. The top-right dropdown shows **My Forms** selected, with no tenant context banner. This is the classic CHEFS experience — forms are personal and not associated with any tenant.

If the user does not belong to any tenants in CSTAR, the experience is identical to My Forms with no visible difference.

![Screenshot: Navigation bar showing My Forms mode](images/my-forms.png)

### Switching to a Tenant

If the user belongs to one or more tenants, those tenants are listed in the top-right dropdown under a **Group Forms** section, below the default **My Forms** option. Clicking a tenant switches the application to that tenant's context.

When a tenant is selected:

- A context banner showing the tenant's name appears below the navigation bar
- The Forms page title updates to **Group Forms**, and now lists forms that belong to the selected tenant
- CSTAR is called in the background to retrieve the user's groups and roles within that tenant
- The user's access to individual forms is determined by which groups have been assigned to each form

![Screenshot: Top-right tenant dropdown with My Forms and Group Forms sections](images/tenant-dropdown.png)

![Screenshot: Navigation bar and context banner showing Group Forms mode after tenant selection](images/group-forms.png)
---

## Roles and Permissions

Roles come from CSTAR groups, and access to a form is determined by group association. A user must belong to a group that has been assigned to a specific form in order to access it. Their roles on that form are derived from the roles assigned to those matching groups in CSTAR.

**Example:** A user in a `reviewers` group will only see and access forms that have the `reviewers` group assigned to them. Their role on those forms is whatever role the `reviewers` group holds in CSTAR (e.g. `submission_reviewer`).

### Available Roles

The following roles are available in Group Forms, from most restricted to most permissive:

| Role | Description |
| --- | --- |
| `form_submitter` | Can submit forms. |
| `submission_reviewer` | Can review form submissions. |
| `submission_approver` | Can approve form submissions. |
| `form_designer` | Can create and design forms. |
| `form_admin` | Full access — create forms, manage settings, and view all submissions. |

> **Note:** Roles are scoped per-form based on group association. A user only has access to forms where at least one of their CSTAR groups has been assigned by a `form_admin`.

> Note: Only users with the `form_admin` role can create new forms within a tenant.

---

## Managing Forms

### Forms Page

Once a tenant is selected, the Forms page displays all forms belonging to that tenant. The available actions on each form depend on the roles the user holds through their group assignments on that form. Just like My Forms, based on the user's roles, different pages and links will be made available on the individual form page.

### Group Management

Users with the `form_admin` role can manage which CSTAR groups are associated with a specific form. This is done through the **Group Management** page, accessible from within the form's management options.

The page presents two panels:

- **Available Groups** — all groups defined in CSTAR for the tenant that are not yet assigned to this form
- **Assigned Groups** — groups currently associated with this form

Groups can be moved between panels using the transfer control between them. Click **Save** to apply the changes.

![Screenshot: Group Management page showing Available Groups and Assigned Groups panels for a form](images/form-group-association.png)

> **Note:** Only users with the `form_admin` role can assign or remove groups from a form.

### Form Access — Specific Groups

When configuring a form, a `form_admin` can control who can access it using the **Form Access** setting. In Group Forms, in addition to the standard access options available in My Forms, the form can be restricted to **Specific Groups**.

The available options are:

- **Public (anonymous)** — anyone can access the form without logging in
- **Log-in Required** — any authenticated user can access the form
- **Specific Groups** — only users who belong to a CSTAR group that has been assigned to this form can access it

When **Specific Groups** is selected, a user's effective roles on the form are aggregated from all their CSTAR groups that are assigned to that form. For example, if a user belongs to both a `reviewers` group and a `submitters` group, and both are assigned to the form, they will hold the combined roles of both groups on that form.

![Screenshot: Form Access dropdown showing Specific Groups option selected](images/form-access-specific-groups.png)

### Draft Sharing with Specific Groups

CHEFS allows submitters to save a draft and share it with other users so they can collaborate on completing the form before final submission. See [Sharing a Submission](https://developer.gov.bc.ca/docs/default/component/chefs-techdocs/Capabilities/Form-Management/Sharing-a-submission/) for general draft sharing behaviour.

In Group Forms, a `form_admin` can enable the **Share draft with form group members only** setting under **Form Functionality**. When this is enabled, a submitter can only share their draft with users who are members of one of the form's authorized groups. Attempting to share with a user outside those groups will show an error.

![Screenshot: Form Functionality settings with Share draft with form group members only checked](images/specific-group-members-only-draft-sharing.png)

![Screenshot: Error shown when attempting to share a draft with a user not in the form's authorized groups](images/draft-sharing-specific-groups.png)

---

## End-to-End Flow

The following summarizes the full flow from login to form access:

1. Log in to CHEFS as usual via IDIR.
2. Land on the About page, which lands in My Forms mode and shows the multi-tenancy promo box.
3. CSTAR is called to retrieve all tenants the user belongs to.
4. If the user belongs to no tenants, the experience is identical to My Forms.
5. If the user belongs to one or more tenants, those tenants appear in the top-right dropdown under Group Forms, with My Forms as the default.
6. Select a tenant — the application switches to Group Forms mode for that tenant.
7. CSTAR is called to retrieve the user's groups and roles within that tenant.
8. The tenant's forms are displayed; the user can access forms where at least one of their groups has been assigned, with roles derived from those group assignments.
9. The user can submit, review, approve, manage, or design forms depending on their roles on each specific form.

***
[Terms of Use](../About/Terms-of-Use) | [Privacy](../About/Privacy) | [Security](../About/Security) | [Service Agreement](../About/Service-Agreement) | [Accessibility](../Capabilities/Accessibility)
