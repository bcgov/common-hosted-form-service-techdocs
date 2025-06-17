[Home](index) > [Components](Components) > [Custom](Custom) > **Dynamic Select Lists**
***

## Examples
> Try a working example<br>
> [View example](https://submit.digital.gov.bc.ca/app/form/submit?f=29700227-dbaa-478b-b4c0-e39feeba3f43)

> Download this example file and [import](Importing-and-exporting-form-designs) it into your design<br>
> [example__dynamic_select_lists_schema.json](../examples/example_dynamic_select_lists_schema.json){:download="example_dynamic_select_lists_schema.json"}

Change content of select list drop-downs with some advanced settings. For instance, the make and model of a car, or in this case information selecting primary or secondary colours.
***

## Advance select list configurations (Tutorial)
<!-- **[Back to top](#top)** -->

Use Advanced Fields for this tutorial.

### JSON data for colour type
This example uses sample colour JSON data stored in an initial select list. A user's selection then passes information along to subsequent form fields. 

Enter JSON data on the Data tab for the first select list. 
* Data > Data Source Type: Raw JSON
* Data > Data Source Raw JSON:
```json
[
  {
    "type": "primary",
    "colours": [
      {
        "code": {
          "hex": "#000",
          "rgba": [
            255,
            255,
            255,
            1
          ]
        },
        "type": "primary",
        "colour": "black",
        "category": "hue"
      },
      {
        "code": {
          "hex": "#FFF",
          "rgba": [
            0,
            0,
            0,
            1
          ]
        },
        "colour": "white",
        "category": "value"
      },
      {
        "code": {
          "hex": "#FF0",
          "rgba": [
            255,
            0,
            0,
            1
          ]
        },
        "type": "primary",
        "colour": "red",
        "category": "hue"
      },
      {
        "code": {
          "hex": "#00F",
          "rgba": [
            0,
            0,
            255,
            1
          ]
        },
        "type": "primary",
        "colour": "blue",
        "category": "hue"
      },
      {
        "code": {
          "hex": "#FF0",
          "rgba": [
            255,
            255,
            0,
            1
          ]
        },
        "type": "primary",
        "colour": "yellow",
        "category": "hue"
      }
    ]
  },
  {
    "type": "secondary",
    "colours": [
      {
        "code": {
          "hex": "#0F0",
          "rgba": [
            0,
            255,
            0,
            1
          ]
        },
        "type": "secondary",
        "colour": "green",
        "category": "hue"
      }
    ]
  }
]
```
* Data > Item Type: `<span>{{ item.type }}</span>`
* API > Property Name: `colourType`
* If done correctly, the preview window will show the JSON data in the select list drop-down.

### Dynamic list for colour choice
With the first select list working, you can now start on the dynamic list. Choosing primary or secondary from the first select list will send all colours of that type to the second select list.

* Data > Data Source Type: Custom 
* Data > Custom Values: `values = data.colourType.colours;`
* Data > Item Type: `<span>{{ item.colour }}</span>`
* API > Property Name: `colourChoice`
* The form must be saved and previewed to see the dynamic list work.

### Display colour information
Now that someone filling out the form has selected a colour, we can display the colour's information from the same JSON data.

* Create a new Text Field
* Display > Disabled: Checked
* Data > Calculated Value: `value = data.colourChoice.colour || 'undefined';`

Use JavaScript to format data, for example the rgba array can be joined with commas:
* Data > Calculated Value: `value = data.colourChoice.code.rgba.join() || 'undefined';`
[//]: # (Cascading Region-Subregion-Facility Dropdown Example)


### Cascading Region-Subregion-Facility Dropdown Example

#### Sample Region JSON

Here is a sample JSON structure used in the Region select list. It contains nested subregions and facilities:

```json
[
  {
    "name": "Vancouver Island",
    "area_km2": 32134,
    "population": 870000,
    "subregions": [
      {
        "name": "South Island",
        "climate": "Temperate",
        "facilities": [
          {
            "name": "Royal Jubilee Hospital",
            "type": "Healthcare",
            "address": "1952 Bay St, Victoria, BC"
          },
          {
            "name": "University of Victoria",
            "type": "Education",
            "address": "3800 Finnerty Rd, Victoria, BC"
          }
        ],
        "major_city": "Victoria"
      }
    ]
  },
  {
    "name": "Lower Mainland",
    "area_km2": 37800,
    "population": 2800000,
    "subregions": [
      {
        "name": "Metro Vancouver",
        "climate": "Oceanic",
        "facilities": [
          {
            "name": "Vancouver General Hospital",
            "type": "Healthcare",
            "address": "899 W 12th Ave, Vancouver, BC"
          },
          {
            "name": "UBC Main Campus",
            "type": "Education",
            "address": "2329 West Mall, Vancouver, BC"
          }
        ],
        "major_city": "Vancouver"
      }
    ]
  },
  {
    "name": "Kootenay",
    "area_km2": 57000,
    "population": 150000,
    "subregions": [
      {
        "name": "West Kootenay",
        "climate": "Mountain",
        "facilities": [
          {
            "name": "Kootenay Lake Hospital",
            "type": "Healthcare",
            "address": "3 View St, Nelson, BC"
          },
          {
            "name": "Selkirk College",
            "type": "Education",
            "address": "301 Frank Beinder Way, Castlegar, BC"
          }
        ],
        "major_city": "Nelson"
      }
    ]
  }
]
```

#### How Data Flows Between Select Lists

In this cascading dropdown configuration, each select list passes its selected data to the next through the global `data` object. Here’s how the relationship works:

#### 1. Region Select
- **Property Name**: `regionData`
- When a region is selected, its full object (including nested subregions and facilities) is stored as `data.regionData`.

#### 2. Subregion Select
- Dynamically accesses `data.regionData.subregions`.
- JavaScript logic ensures this field only loads subregions for the selected region:
  ```javascript
  if(data.regionData && data.regionData.subregions){
    values = JSON.parse(JSON.stringify(data.regionData.subregions));
  }
  ```

#### 3. Facility Select
- Depends on the selected subregion.
- It uses the subregion’s facilities from `data.subRegion`:
  ```javascript
  if(data.subRegion && data.subRegion.facilities){
    values = JSON.parse(JSON.stringify(data.subRegion.facilities));
  }
  ```

This mechanism allows for a seamless cascading experience where each dropdown filters based on the previous selection.

Save and preview the form to see the cascading dropdowns in action.

### Conditional logic
Show and hide form fields with [conditional logic](Conditional-forms-fields).

<!-- **[Back to top](#top)** -->
***
[Terms of Use](Terms-of-Use) | [Privacy](Privacy) | [Security](Security) | [Service Agreement](Service-Agreement) | [Accessibility](Accessibility)