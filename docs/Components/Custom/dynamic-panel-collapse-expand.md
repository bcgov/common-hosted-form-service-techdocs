[Home](index) > [Components](Components) > [How-To Guides](how-to-guides) > **Dynamic Panel Collapse and Expand**
***

## Examples
> Dynamic Panel Collapse and Expand lets you show or hide form sections based on radio button selection.
> Try a working example<br>
> [View example](https://submit.digital.gov.bc.ca/app/form/submit?f=119cdfa6-88e8-4744-935f-acc2f3c4dab0)

## How do I make it?  

1. **Create a Panel Component**  
   Add a Panel component to your form. This panel will be shown or hidden based on user interaction. Assign it a `Key`, for example: `collapseExpandPanel`.

2. **Add Form Fields Inside the Panel**  
   Place any input components (e.g., Name, Email) inside the panel.

3. **Add a Radio Button Component**  
   Create a Radio button component outside the panel with values like:
   - Collapse
   - Expand  
   Give this component a `Key`, e.g., `expandcollapsepanel`.

4. **Add Advanced Logic**  
   Navigate to the Logic tab and click **Add Logic**. Use the following configuration:
   
   - **Logic Name**: `expand hide panel`
   - **Type**: `Javascript`
   - **Text Area**: Paste the below JavaScript:
     ```javascript
     // Get the panel component by its key
     const panel = instance.root.getComponent('collapseExpandPanel');

     if (panel) {
       // Determine if it should be collapsed based on radio selection
       const shouldCollapse = data.expandcollapsepanel === 'collapse';

       // Apply collapse state
       panel.collapsed = shouldCollapse;

       // Redraw the panel to reflect changes
       panel.redraw();
     }
     ```

5. **Preview the Form**  
   Try selecting **Collapse** or **Expand** in the radio options. The panel should collapse or expand accordingly.

---

This logic gets the panel component and toggles its `collapsed` property. Based on the radio selection, the panel will either be shown or hidden. This logic can also be reused with other input types or conditions to control panel visibility dynamically.

You can also modify properties like `disabled`, `hidden`, `label`, `tooltip`, and `description` dynamically at runtime using similar JavaScript logic.

NOTE: Don’t use redraw() unless absolutely necessary, especially for large forms—it’s expensive.
***
[Terms of Use](Terms-of-Use) | [Privacy](Privacy) | [Security](Security) | [Service Agreement](Service-Agreement) | [Accessibility](Accessibility)
