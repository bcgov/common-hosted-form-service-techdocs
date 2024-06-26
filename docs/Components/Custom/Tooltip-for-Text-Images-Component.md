[Home](index) > [Components](Components) > [Custom](Custom) > **Tooltip**
***

##  Examples
> Try a working example<br>
> [View example](https://submit.digital.gov.bc.ca/app/form/submit?f=697d4f58-766c-427d-a6f6-2925f056d8da)

> Download this example file and [import](Importing-and-exporting-form-designs) it into your design<br>
> [example_tooltip_for_text_images_component_schema.json](../examples/example_tooltip_for_text_images_component_schema.json){:download="example_tooltip_for_text_images_component_schema.json"}
***

## Tooltip (Tutorial)

By default, most of the form.io components such as the ‘Number’ and ‘Text’ fields have a tooltip capability which displays information when a user hovers their cursor over it. 

![tooltip1](images/tt1.png)

To add a tooltip to a component, simply click on Settings (gear icon), and add the tooltip text in the ‘Tooltip’ field under the ‘Display’ tab.

![tooltip2](images/tt2.png)


However, some fields such as the ‘Text/Images Component' do not have this capability. This limits CHEFS’ ability to display tooltips next to standalone text such as a heading. This limitation can be overcome by using an ‘HTML Component' and adding form.io’s own tooltip HTML class.

![tooltip3](images/tt3.png)


To achieve this, add an ‘HTML Element Component’ to your form and click on the Settings (gear) icon. Enter the following HTML code into the ‘Content’ field, replacing ‘HTML Tooltip’ with your custom text. 

![tooltip4](images/tt4.png)

```
<h1 class="col-form-label" ref="label" style="font-size: 1.5em">
  HTML Tooltip
  <i data-tooltip="This is a long tooltip containing important information." 
    class="fa fa-question-circle text-muted" tabindex="0" ref="tooltip" 
    aria-expanded="false" style="font-size: 20px"></i>
</h1>
```

<!-- **[Back to top](#top)** -->

***
[Terms of Use](Terms-of-Use) | [Privacy](Privacy) | [Security](Security) | [Service Agreement](Service-Agreement) | [Accessibility](Accessibility)