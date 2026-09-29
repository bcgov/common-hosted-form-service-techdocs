[Home](index) > [Capabilities](Capabilities) > **Accessibility** 
***  
## Our Approach 
Accessibility is important because it empowers everyone to use the forms you'll build with CHEFS. It ensures equal access and inclusion, enabling individuals to use forms on an equal footing. By making forms accessible, such as providing clear instructions and appropriate labels, we empower people to fully engage and participate. Accessibility not only benefits all users but also improves their experience and ensures compliance with accessibility standards. It fosters an inclusive environment where everyone can confidently and independently interact with CHEFS forms.  

Our goal is to go above the minimum compliance requirement level AA of the Web Content Accessibility Guidelines 2.1 ([WCAG 2.1](https://www.w3.org/TR/WCAG21/)).

## Our commitment  

We are committed to meeting your needs no matter how you use the service. We understand that people may have different needs for accommodation. To make sure we can be inclusive of everyone, we want to learn from you.

### Tell us how we’re doing
To tell us about accessibility issues on Submit, you can:

* Reach out to us through our [CHEFS Exchange Lab - Teams Channel](https://teams.microsoft.com/l/channel/19%3a34b9d4b4deb54eebaa9be8bc1ccf02f7%40thread.tacv2/CHEFS%2520(Exchange%2520Lab%2520Team)?groupId=bef8086f-20c7-43a4-bd07-29ce764e818c&tenantId=6fdb5200-3d0d-4a8a-b036-d3685e359adc)
* Create an issue on our [public GitHub repository](https://github.com/bcgov/common-hosted-form-service/issues/new?assignees=&labels=&projects=&template=bug_report.md&title=)  

We will work with you to:

* Understand issues you’ve encountered and how they impact you
* Log all bugs in our product backlog and address them with high priority.
* Resolve issues as soon as we can 

> We are grateful for your feedback and insights.

## Accessibility Topics  

- [Form Multilanguage Support](Form-Multilanguage) 
- [Screen Reader Support](Accessibility#screen-reader-support)
- [Building Accessible Form.io Forms](Accessibility#building-accessible-formio-forms)

### Screen Reader Support  
  
The form components used in CHEFS already include accessibility features. [ARIA](https://en.wikipedia.org/wiki/WAI-ARIA) attributes make labels, tooltips, and descriptions accessible to screen readers and other tools. However, form developers still need to be mindful of accessibility principles to create truly inclusive experiences. The built-in accessibility features of CHEFS form components allow form developers to focus on other accessibility considerations.

As an example, the Vox screen reader for the Chrome browser will read this component:

![image](images/accessibility.png)

as _"This is the label. This is the tooltip. This is the description. Within: This is the placeholder. Edit text"_. Note that the user does not need to hover, etc, to “pop up” the tooltip to have it read out.

### Building Accessible Form.io Forms

Form.io provides accessibility features, but accessible forms also depend on component configuration and the application hosting them. Adding ARIA attributes alone does not ensure WCAG compliance. Form developers must consider labels, instructions, keyboard interaction, validation, and visual presentation.

#### Labels and instructions

Provide a meaningful label for every field. Complete each component's Label setting and keep labels visible wherever possible. In the rendered form, each label should be programmatically associated with its input.

Use ARIA where needed. Prefer an associated HTML label. Use `aria-labelledby` to reference existing label text, or `aria-label` when a visible label cannot be used and the control's purpose is otherwise clear. These attributes provide an accessible name; they do not display a label to sighted users.

Provide clear instructions. Explain required fields, expected formats, and any input restrictions. Use component descriptions for persistent guidance, and verify that the rendered input references relevant help text through `aria-describedby`.

Do not use placeholders as labels. Placeholder text disappears when users enter a value. Keep essential instructions available throughout completion of the form.

#### Component selection and configuration

Form.io's accessibility guidance identifies components and settings suitable for accessible forms. Complete relevant labels and descriptions, and review the guidance when selecting components.

For Select components, use the HTML5 widget; Form.io lists Select using Choices.js among components with accessibility limitations. For wizard forms, use the Classic Wizard Header. The Vertical header may require significant customization.

Components such as Data Grid, Edit Grid, Signature, and custom components require particular attention because Form.io excludes them from its Accessibility Compliance Module's supported component set. Review alternatives and test the actual interaction before using them.

#### Optional Accessibility Compliance Module

Form.io offers a separately licensed Accessibility Compliance Module that changes builder and renderer behaviour. It supports improvements to focus management, screen reader announcements, validation messages, and ARIA attributes. These features require intentional configuration and do not automatically make the host application accessible.

The module must be imported and registered at the application level. Some features—including accessible tooltips, Date/Time interactions, and Modal Edit windows—require both the module and Form.io's USWDS template. Confirm which modules and templates the CHEFS deployment includes before relying on these features.

#### Verify the completed form

Before publishing, test the form within CHEFS:

* Complete and submit it using only the keyboard, checking focus visibility and navigation order.
* Use a screen reader to check field names, descriptions, required states, and validation feedback.
* Trigger validation errors and confirm users can identify and correct them.
* Check conditional fields and wizard navigation.
* Review contrast, zoom behaviour, and whether instructions remain readable.

Repeat these checks after changes to components, templates, or the Form.io renderer.

For further details, see the [Form.io accessibility documentation](https://help.form.io/dev/accessibility).

***
[Terms of Use](Terms-of-Use) | [Privacy](Privacy) | [Security](Security) | [Service Agreement](Service-Agreement) | [Accessibility](Accessibility)