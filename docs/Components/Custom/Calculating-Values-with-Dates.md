[Home](index) > [Components](Components) > [Custom](Custom) > **Calculating Values with Dates**
***

## Examples
> Try a working example<br>
> [View example](https://submit.digital.gov.bc.ca/app/form/submit?f=ea72822f-209e-4509-85be-0ab525846969)

> Download this example file and [import](Importing-and-exporting-form-designs) it into your design<br>
> [example_counting_days_between_two_dates_schema.json](../examples/example_counting_days_between_two_dates_schema.json){:download="example_counting_days_between_two_dates_schema.json"}

***
## Number of days between two dates.  

**IMPORTANT NOTE**: for the following example, if you have your fields inside of a layout component then you have to reference them using the following
```row.startDateTime``` instead of ```data.startDateTime```  

Here is the code you will need:

``` 
const date1String = data.startDateTime; // date string 1, change "startDateTime" to the name of your first date field  
const date2String = data.endDateTime; // date string 2, change "endDateTime" to the name of your second date field  
const date1 = new Date(date1String); //changes the data types from strings to dates  
const date2 = new Date(date2String); 

// Calculate the difference between the two dates in milliseconds and converts the date to a number  
const diffInMs = date2 - date1;  

// Convert the difference in milliseconds to days  
const diffInDays = Math.floor(diffInMs / (1000 * 60 * 60 * 24));  
value = diffInDays; // assigns the calculated number of days to the value that will be displayed in the field  
```

For the text field that you want the calculated number of days between two dates to show on, perform the following steps:  
1. Go into the field settings, on the data tab, scroll to the bottom and expand the calculated values section, and paste the code above into the javaScript section.   
2. The names of your two Date Time fields must match the ones in the javaScript code (```startDateTime``` and ```endDateTime```).  To set those names go to the API tab of the settings for each Date Time field. Alternatively you can modify the javaScript code to make them each match the "property name" showing on the API tab.   
3. Save your form design and try it out in the preview mode.  

_Note for developers_: It appears that the data type for the Date/Time field that returns with data.dateTime is a string. So it first has to be converted back to a date before you can simple subtract the two dates and take advantage of javaScript's automatic converting from date to number.  

## Autopopulate a Date/Time field with the value 1 Year Later than another Date/Time field
<!-- **[Back to top](#top)** -->

Here is the code you will need:
```  
// get the value of the original Date/Time field
var originalDateTime = new Date(data.endDateTime);

// add one year to the original Date/Time value
var oneYearLater = new Date(originalDateTime.setFullYear(originalDateTime.getFullYear() + 1));

// format the new Date/Time value as a string in the format 'YYYY-MM-DDTHH:mm'
var formattedDateTime = oneYearLater.toISOString().slice(0, 16);

// set the value of the new Date/Time field to the formatted string
value = formattedDateTime;  
```  
For the Date/Time field that you want the calculated value "1 year later" than your other Date/Time field, perform the following steps:  
1. Go into the field settings, on the data tab, scroll to the bottom and expand the calculated values section, and paste the code above into the javaScript section.   
2. The name of your Date/Time field used to calculate must match the ones in the javaScript code (```endDateTime```).  To set this value go to the API tab of the settings and type endDateTime into Property Name field. Alternatively you can modify the javaScript code value "endDateTime" to make it match the "property name" you selected for your Date/Time field on the API tab.   
3. Save your form design and try it out in the preview mode.   

***
[Terms of Use](Terms-of-Use) | [Privacy](Privacy) | [Security](Security) | [Service Agreement](Service-Agreement) | [Accessibility](Accessibility)
