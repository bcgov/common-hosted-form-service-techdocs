# Enterprise CHEFS and CSTAR

*Technical Documentation — Tenant Management, User Access, and CHEFS Integration*

---

## 1. Overview

Enterprise CHEFS (Common Hosted Forms | Enterprise) is an extension of the classic CHEFS platform that enables team-based, tenant-scoped form management. It works in close integration with CSTAR (Connected Services, Team Access, and Roles), which is the identity and access management system that governs who has access to what, and with what permissions.

In the Enterprise CHEFS model, forms are organized under tenants. A tenant is a dedicated workspace for a ministry, team, or initiative. Access to forms within a tenant is controlled by group memberships and service roles managed in CSTAR.

---

## 2. Landing Page and Login

### 2.1 Landing Page

When a user navigates to the Enterprise CHEFS URL, they land on a page that introduces both Enterprise CHEFS and CSTAR. The page provides two entry points: **Go to CHEFS**, which takes the user into the forms application, and **Go to CSTAR**, which takes the user to the CSTAR tenant management portal.

The landing page also displays an important notice for BCeID users: BCeID users must log in to CSTAR before using Enterprise CHEFS. This step ensures that their account is discoverable by tenant admins, who need to find and add them to a tenant or group.

### 2.2 Logging In

Users log in by clicking the Login button on the landing page. Authentication is done through IDIR. Form designers, form owners, and other users who need to create or manage forms must use their IDIR credentials to log in.

Once authenticated, an API call is made to CSTAR to fetch all tenants the logged-in user belongs to. This happens silently in the background immediately after login.

---

## 3. Tenant Selection in Enterprise CHEFS

### 3.1 Default State — Personal CHEFS

After logging in, the application defaults to Personal CHEFS. The top navigation bar displays **Common Hosted Forms | Personal**, and the top-right dropdown shows Personal CHEFS selected. This is the classic CHEFS experience — forms are personal and not associated with any tenant.

If the user does not belong to any tenants in CSTAR, the experience is identical to Personal CHEFS and there is no visible difference.

### 3.2 Tenant Dropdown

If the user belongs to one or more tenants, those tenants are listed in the dropdown in the top-right corner of the application, alongside Personal CHEFS. The user can click on any tenant from this list to switch into that tenant's context.

The dropdown lists all tenants the user is a member of in CSTAR. Personal CHEFS always appears as the default option at the top of the list.

### 3.3 Selecting a Tenant

When the user selects a tenant from the dropdown, the application switches context to that tenant. The navigation bar updates to show **Common Hosted Forms | Enterprise**, and the forms listed under the Forms page are now the forms that belong to the selected tenant.

Upon tenant selection, the following happens behind the scenes:

- An API call is made to CSTAR to retrieve all groups the logged-in user belongs to within that tenant.
- The roles assigned to each of those groups are fetched and aggregated into a combined set of permissions for the user.
- Those aggregated roles are applied across all forms in the tenant, determining what the user can see and do on each form.

---

## 4. Roles and Permissions

### 4.1 How Roles Work

Roles in Enterprise CHEFS come from CSTAR. A user can be a member of multiple groups within a tenant, and each group can have one or more service roles assigned to it from the Enterprise CHEFS connected service. When a user selects a tenant, all roles from all of their groups are aggregated and applied uniformly across all forms in that tenant.

For example, if a user belongs to two groups — one with the reviewer role and another with the submitter role — they will have both reviewer and submitter permissions on all forms within that tenant.

### 4.2 Available Roles

The following roles are available in Enterprise CHEFS, listed from most restricted to most permissive:

| Role | Description |
| --- | --- |
| `form_submitter` | Can submit forms. |
| `submission_reviewer` | Can review form submissions. |
| `submission_approver` | Can approve form submissions. |
| `form_designer` | Can create and design forms. |
| `form_admin` | Highest level of access. Can perform all actions including creating forms, managing settings, and viewing all submissions. |

### 4.3 How Roles Affect the UI

The actions visible to a user on each form depend on their aggregated roles. For example:

- A user with only reviewer or submitter roles will see a **Submissions** link on forms but will not see the **Manage** link.
- A user with the `form_admin` role will see all available options — Manage, Submissions, and the ability to create new forms.
- Only users with the `form_admin` role can create new forms within a tenant.

> **Note:** All aggregated roles are applied equally across all forms within the selected tenant. There is currently no per-form role assignment.

---

## 5. Managing Forms in Enterprise CHEFS

### 5.1 Forms Page

Once a tenant is selected, the Forms page displays all forms that belong to that tenant. The page shows each form's title and available actions based on the user's roles. For users with the `form_admin` role, both a **Manage** link and a **Submissions** link appear next to each form.

### 5.2 Manage Form

Clicking the **Manage** link on a form opens the Manage Form page. This page works the same way as in Personal CHEFS and provides access to:

- **Form Settings** — general configuration for the form.
- **API Key** — for integrating the form with external systems.
- **CDOGS Template** — for document generation.
- **External APIs** — for connecting to external data sources.
- **Print Configuration** — for print layout settings.
- **Form Design History** — shows all versions of the form and their published status.

Only one version of a form can be published at a time. Once a version is published, it is no longer editable. A new version must be created to make further changes.

---

## 6. Features Not Yet Available

The following features are currently disabled in Enterprise CHEFS and are planned for future sprints:

- **Team Management** — the team management page is currently disabled. It will be replaced by group-based management tied to CSTAR groups.
- **Draft Sharing for a Specific Team** — the ability to share a draft form with a specific team is currently disabled. This will eventually be replaced by group-based form access controls.

> **Note:** These features are works in progress and will be enabled in upcoming releases as the CSTAR integration matures.

---

## 7. End-to-End Flow Summary

The following summarizes the full flow from login to form access:

1. The user navigates to the Enterprise CHEFS URL and lands on the introductory landing page.
2. The user clicks Login and authenticates via IDIR.
3. After login, an API call is made to CSTAR to retrieve all tenants the user belongs to.
4. If the user belongs to no tenants, the application behaves identically to Personal CHEFS.
5. If the user belongs to one or more tenants, those tenants appear in the top-right dropdown. Personal CHEFS is selected by default.
6. The user selects a tenant from the dropdown. The application switches to Enterprise mode for that tenant.
7. An API call is made to CSTAR to retrieve all groups the user belongs to within that tenant, and all associated roles are aggregated.
8. The forms for the selected tenant are displayed. The user's aggregated roles determine which actions are visible on each form.
9. The user can interact with forms based on their permissions — submitting, reviewing, approving, managing, or designing forms depending on their role.

---

## 8. Managing Access in CSTAR

### 8.1 Requesting a Tenant

Tenants are created through CSTAR. Any user can request a new tenant by clicking **Request New Tenant** on the CSTAR Tenants dashboard. The request requires a tenant name, a ministry or organization, and a description. Once submitted, the request goes to an operations admin for approval.

### 8.2 Adding Users and Creating Groups

Once a tenant is approved and active, the tenant owner can add users to the tenant and create groups. Groups are used to organize users and assign them service roles from Enterprise CHEFS. Users added to a group inherit all roles assigned to that group.

### 8.3 Connecting Enterprise CHEFS to a Tenant

Enterprise CHEFS must be added as a connected service to a tenant in CSTAR before roles can be assigned. This is done from the **Connected Services** tab on the Tenant Details page in CSTAR. Once Enterprise CHEFS is connected, its roles become available for assignment to groups within that tenant.

### 8.4 Assigning Roles to Groups

Roles are assigned to groups from the **Service Roles** tab on the Group Details page in CSTAR. The tenant admin clicks **Edit**, selects the desired roles from the Enterprise CHEFS connected service, and saves. All members of that group will then have those roles when accessing Enterprise CHEFS under the tenant.
