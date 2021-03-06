# Welcome to Pivot.js

Pivot.js is a simple way for you to get to your data.  It allows for the
creation of highly customizable unique table views from your browser.

> In data processing, a pivot table is a data summarization tool found in
> data visualization programs such as spreadsheets or business intelligence
> software. Among other functions, pivot-table tools can automatically sort,
> count, total or give the average of the data stored in one table or
> spreadsheet. It displays the results in a second table (called a "pivot
> table") showing the summarized data.

In our case, results (or the pivot-table) will be displayed as an HTML table
pivoting from the input data (CSV or JSON). Without further ado let's get to usage.

## View an [example](http://rjackson.github.com/pivot.js/) or view the [Docs](http://rjackson.github.com/pivot.js/docs/index.html#!/api/Pivot) for more information.

#Usage

Step one is to initialize the pivot object.  It expects the following attributes:

* `csv` - which should contain a valid string of comma separated values.  It is
  __important to note__ that you must include a header row in the CSV for pivot
  to work properly  (you'll understand why in a minute).
* `json` - which should contain a valid JSON string. At this time this string
  must be an array of arrays, and not an array of objects (storing the field
  names with each row consumes significantly more space).
* `fields` - which should be an array of objects.  This is used to instruct
  pivot on how to interact with the fields you pass in.  It keys off of the
  header row names.  And is formated like so:

```javascript
 [ {name: 'header-name', type: 'string', optional_attributes: 'optional field' },
 {name: 'header-name', type: 'string', optional_attributes: 'optional field' }]

```
(<small>See more about fields in Section below</small>)

* `filters` (default is empty) - which should contain any filters you would like to restrict your data to.  A filter is defined as an object like so:

```javascript
{zip_code: '34471'}

```

Those are the options that you should consider.  There are other options that are well covered in the spec.

A valid pivot could then be set up from like so.

```javascript

var field_definitions = [{name: 'last_name',   type: 'string',   filterable: true},
        {name: 'first_name',        type: 'string',   filterable: true},
        {name: 'zip_code',          type: 'integer',  filterable: true},
        {name: 'pseudo_zip',        type: 'integer',  filterable: true },
        {name: 'billed_amount',     type: 'float',    labelable: false,},
        {name: 'last_billed_date',  type: 'date',     filterable: true}

// from csv data:
var csv_string  =  "last_name,first_name,zip_code,billed_amount,last_billed_date\n" +
                   "Jackson,Robert,34471,100.00,\"Tue, 24 Jan 2012 00:00:00 +0000\"\n" +
                   "Jackson,Jonathan,39401,124.63,\"Fri, 17 Feb 2012 00:00:00 +0000\""

pivot.init({csv: csv_string, fields: field_definitions});

// from json data:
var json_string = '[["last_name","first_name","zip_code","billed_amount","last_billed_date"],' +
                    ' ["Jackson", "Robert", 34471, 100.00, "Tue, 24 Jan 2012 00:00:00 +0000"],' +
                    ' ["Smith", "Jon", 34471, 173.20, "Mon, 13 Feb 2012 00:00:00 +0000"]]'

pivot.init({json: json_string, fields: field_definitions});

```

# Wiki

* [Filters](https://github.com/rjackson/pivot.js/wiki/Filters)
* [Labels](https://github.com/rjackson/pivot.js/wiki/Labels) 
* [Summaries](https://github.com/rjackson/pivot.js/wiki/Summaries) 
* [Integrating with jQuery](https://github.com/rjackson/pivot.js/wiki/Integrating-with-jQuery)
* [Contribute](https://github.com/rjackson/pivot.js/wiki/Contributing)
* [DOCS](http://rjackson.github.com/pivot.js/docs/index.html#!/api/Pivot)

# Blergs

* [Introducing Pivot.js](http://jonathan-jackson.net/2012/04/10/introducing-pivotjs) - Jonathan Jackson

# Date Processing

Dates are stored internally as milliseconds since the epoch.  Dates to be
parsed from CSV will use Date.parse so make sure that the format you use
will be recongnized by your target browser.  Please use a shim library if
you need to ensure proper parsing regardless of browser implementation.

See [here](https://github.com/csnover/js-iso8601) for an example.

(ISO8601 dates are still not handled properly by Safari 5.1 or IE8.)


# Authors

Pivot.js is the work of Robert Jackson and Jonathan Jackson.

## License

This software is licensed under a modified BSD license.

See LICENSE for more details.