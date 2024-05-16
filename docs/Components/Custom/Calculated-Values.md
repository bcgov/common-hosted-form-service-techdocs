[Home](index) > [Components](Components) > [Custom](Custom) > **Calculated Values**
***

## Examples 
Calculated values allows you to create fields that get filled in for you based on what the user inputs elsewhere.
Use the advanced field of the control you wish to populate with a calculated value.

<!-- **[Back to top](#top)** -->

> Try a working example<br>
> [View example](https://submit.digital.gov.bc.ca/app/form/submit?f=081d9df3-b601-461b-99e7-a26a46331b0c&sampleParameter=1234567)

> Download this example file and [import](Importing-and-exporting-form-designs) it into your design<br>
> [example_calculated_values_schema.json](../examples/example_calculated_values_schema.json){:download="example_calculated_values_schema.json"}
***

## Calculated Values (Tutorial)

<!-- **On the page:**
* [Data](#data)
* [Calculated Values](#calculated-values)  -->

## Data
<!-- **[Back to top](#top)** -->

To designate which data values for a selection should be used for calculated values in other fields, use the Data tab.

This option is available in both basic and advanced controls.

### Select list example
Drag and drop a `Select List` component into the designer and add some values on the `Data` tab. The label can be what you want the user to see, and the value can be what you would like to be accessible to calculate from in other fields.

![](images/conditional_select_list.png) 

## Calculated Values
<!-- **[Back to top](#top)** -->

### JavaScript
On the field you wish to display the calculated value, navigate to the `Data` tab.

![](images/data_tab.png) 

On the Data tab, scroll down to `Calculated Value` and expand the field. There are some useful help references there.

In the `JavaScript` section enter your calculation for the field you wish to display.

![value = data.myTestRadio * 10;](images/calculated_js.png)

With this example you could add up an assigned value for a set of radio buttons and assign each question a weighting:
`value = (data.questionAbc * 5) +  (data.questionDef * 5) +  (data.questionGhi * 5) +  (data.questionJkl * 5)`

You can use this section to create complex calculated values using JavaScript, by referencing one or more existing fields on your form with the data `data.*` variable. You can calculate numerical values, build String values, do conditional logic and much more.

If you need to know the field name for a field you wish to base a calculated value on, look at the API tab and the Property Name box for the name.

![](images/conditional_property_name.png)

### Capture query parameter
To automatically populate a form field with query parameters attached to the URL, go to the Data tab, locate and expand the Custom Default Value section. Then, in the JavaScript segment, input the calculation corresponding to the field you intend to exhibit, in our case something similar. 

![](images/query_parameter_javascript.jpg)

One factor to bear in mind is the potential for someone to modify the query parameter in the URL, potentially impersonating a similar value. If this poses a concern, it may be advisable to assign a unique and difficult-to-guess random identifier (such as a UUID) to each parameter. Subsequently, utilize this random identifier within the URL.

***
[Terms of Use](Terms-of-Use) | [Privacy](Privacy) | [Security](Security) | [Service Agreement](Service-Agreement) | [Accessibility](Accessibility)

