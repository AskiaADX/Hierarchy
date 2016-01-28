# Hierarchy V1.1.0

This ADC should be apply on chapter and uses merged question to store the result of the selections.

It uses a specific database format generated by the following page

http://www.askia.com/Downloads/dev/adc/hierarchy/CSVConverter.html

This page convert a CSV file to a Javascript database.        

## Tested in

* Chrome
* Firefox
* Safari
* Internet Explorer
* Opera
          
## Dependencies:

- Javascript database generated with 
http://www.askia.com/Downloads/dev/adc/hierarchy/CSVConverter.html

## Properties   

### General

#### Javascript database file path (database) [REQUIRE]

Path of the Javascript database file to include in the document.
This property is dynamic, we recommend the usage of the ??ResPath?? and include the javascript file in the survey resources.

The file must be generated with 
http://www.askia.com/Downloads/dev/adc/hierarchy/CSVConverter.html

It contains the following code format:

       Hierarchy.databases["name_of_database"] = {/* Database information */ };

Example:

       Hierarchy.databases["vehicles"] = {
           /* Definition of levels */
           "levels" : [
               {
                   "id" : "brand_id",
                   "name" : "brand",
                   "liveValues" : ["brand_id"]
               },
               {
                    "id" : "model_id",
                    "name" : "model",
                    "liveValues" : ["model_id", "model_code"]
               },
               {
                    "id" : "version_id",
                    "name" : "version"
               },
               {
                    "id" : "option_id",
                    "name" : "option"
               }
           ],
           /* Map name / index of table headers */
           "header" : {
               "brand_id" : 0, 
               "brand" : 1, 
               "model_id" : 2, 
               "model" : 3, 
               "model_code" : 4, 
               "version_id" : 5, 
               "version" : 6, 
               "option_id" : 7, 
               "option" : 8, 
               "id" : 9, 
               "code" : 10
           }, 
           /* Records. Array of lines which contains an array of columns 
              lines[columns[]] 
           */
           "records" : [
               ["1", "CITROEN", "7", "C2", "Mo1", "24", "VU", "1", "CDV", "1", "A1"],
               ["1", "CITROEN", "9", "C4", "Mo1", "24", "VU", "1", "CDV", "2", "A2"],
               ["1", "CITROEN", "8", "C3", "Mo1", "24", "VU", "1", "CDV", "3", "A3"],
               ["2", "FIAT", "20", "Ducato 30", "Mo11", "19", "van", "2", "LCV", "11", "A11"],
               ["2", "FIAT", "21", "Ducato 33", "Mo11", "19", "van", "2", "LCV", "12", "A12"],
               ["2", "FIAT", "22", "Ducato 35", "Mo11", "10", "light van", "2", "LCV", "13", "A13"]
           ]
       };


#### Database name (databaseName) [REQUIRE]

Name of the database as it appear in the Javascript database file

#### Values to save (values) [REQUIRE]

Name of fields separate with coma and surround by quotes or double-quotes.
It indicates the fields to save on the latest level selection.

Example:

       "id", "code", "brand_id", "model_id", "model_code", "version_id", "option_id"

#### HTML Ids prefix (prefix) [OPTIONAL]

Prefix of all HTML input Ids where the values will be saved.
It may be use if you have several instance of the Hierarchy ADC into the same page.

Example:
   If the field to save is "brand_id" and the prefix is "vehicle_", you must have and HTML input in your page with the id="vehicle_brand_id"

#### Display name of level (levelNames) [REQUIRE]

Label of the dropdown for each levels. 
Each level must have a display names even if it's an empty name.
All names must be surrounded by a double-quotes and separate with coma.

It is require to generate the right number of dropdown

Example:

        "Brands", "Models", "Versions"
        or if you have four levels
        "", "", "", "" 

#### Text of first dropdown option (blankOptions) [OPTIONAL]

Text of the first dropdown options for each levels.
All textes must be surrounded by a double-quotes and separate with coma.

Example:

       "Please select a brands", "Please select a models", "Please select a versions"

#### Orientation (orientation) [REQUIRE]

Horizontal or vertical dropdowns orientation.

Default: Vertical

#### Horizontal space (horizontalSpace) [REQUIRE]
 
Size of the horizontal space between dropdown (pixel by default).
Works with the horizontal orientation

Default: 15px

#### Width of inputs (inputsWidth) [REQUIRE]

Indicates the width (including the unit) to use for the both the search input and the dropdown list.

Default: 300px

#### Dropdown size (dropDownSize) [REQUIRE]

Indicates the size of the dropdown list. It's the number of options visible before the scroll.

Default: 10


#### Not supported browser text (notSupportedBrowser) [REQUIRE]

Message to display to the non-supported browser

Default: Sorry this page uses Javascript code, please enable it


### Search

#### Use search (useSearch) [OPTIONAL]

Add the input search

Possible values:

* 0 - No search
* 1 - Auto-generate search
* 2 - Custom search input

Default: 1

#### Id of the custom search input (customSearchId) [OPTIONAL]

Id of the custom search input (when useSearch=2)

Default: ''

#### Label of search input (searchLabel) [OPTIONAL]

Text to use in the label of the search input

#### Search fields (searchIn) [OPTIONAL]

Name of fields separate with coma and surround by quotes or double-quotes.
It's require when using search.
It indicates in which fields to search.

Example:
     
       "brand", "model"

#### Search at beginning (searchAtBeginning) [OPTIONAL]

Search at the beginning of the field value

Default: Yes


#### Separator of words in input search (searchSeparator) [OPTIONAL]

Separator of words in the input search.

Example: 
   
     If the separator is "+", the respondent have to enter it to search in different places:

     "citroen + c2"

     Will search "citroen" AND "c2"

Default: +

#### Min characters (minChars)

Minimum number of characters entered before to trigger the search.

Default: 2


### Behaviours

#### Display first level items (firstLevelVisible)

Display first level items

Default: No

#### Auto select when 1 result found (autoSelect)

Auto select when only one result is found

Default: No

#### Sub-levels visibility (visibility)

Visibility of sub-levels when not activated.

It could be: "Visible", "Hidden" or "Disabled"

Default: Visible

#### Max results (maxResults)

Maximum number of results to display in the dropdown.
Set 0 for unlimited results.

This option is useful if you have a huge database.

Default: 0

