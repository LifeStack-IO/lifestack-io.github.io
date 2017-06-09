---
label: snippets
layout: post
title: Embed IMPORTRANGE in Formulas
short_title: __IMPORTRANGE__ in Formulas
author:
  name: jd
tags:
- google
- sheet
category: functions
lead: How to embed the IMPORTRANGE function within other functions in Google Sheets.
published: true
---
{% include lead.md %}

### Introduction

Having mastered using the [importrange]({{ site.baseurl }}{% link _snippets/google_sheet_importrange.md %}) function to link together disparate spreadsheets, you can also use it as part of a larger formula to provide lookup functionality, without having to import an entire range of data.

### Method

Consider the (simplified) situation where you use a code to identify _something_ from a lookup table in a separate spreadsheet. The formulas below assume that this table will be in the first sheet, otherwise, you will need to prefix the range reference with the sheet name (e.g. _A:A_ becomes __Sheet1__!A:A).

|---
| Code | Name
|:-|:-
| A1 | Widget Type A (Model 1)
| A3 | Widget Type A (Model 3)
| A5 | Widget Type A (Model 5)
| B2 | Widget Type B (Model 2)
| B4 | Widget Type B (Model 4)
| B6 | Widget Type B (Model 6)

By using an embedded [importrange][1] you can access the 'name' of a particular part, by the code, in a separate spreadsheet, using the formula below. This assumes that your code is in the first column (second row) of your spreadsheet (A2).

{% highlight puppet %}
INDEX(IMPORTRANGE("SPREADSHEET_ID OR SPREADSHEET_URL", "B:B"), MATCH(A2, IMPORTRANGE("SPREADSHEET_ID OR SPREADSHEET_URL", "A:A"), 0), 1)
{% endhighlight %}{:class="formula"}

Whilst you can use [importrange][1] as part of any formula you wish, although you should read the caveats below first!

### Caveats

###### Authorisation

When you use first connect to a sheet using [importrange][1] you will get an 'N/A' error until you perform a simple authorisation. To do this, simply hover over the cell and wait for a message to appear. This should say something like '_You need to connect these sheets_' and include an '__Allow Access__' button. Once you click this button, you are authorising the first sheet to connect to the second sheet (as you). This alleviates the need to grant any other users of the first sheet access to the second sheet (useful if you just want to provide a simple filtered view). However, if you use an embedded version of the function, you won't get the same prompt message, just an error. You need, therefore, to do an initial range import to set up the authorisation before you start writing more complex formulas. Use a function such as this to kick start the process (you can delete it after one run, although you might need to re-run it in the future if you ever need to delete the user which granted the original authorisation).

{% highlight puppet %}
IMPORTRANGE("SPREADSHEET_ID OR SPREADSHEET_URL", "A1")
{% endhighlight %}{:class="formula"}

###### Performance

This technique works well for small scale and infrequent lookups (up to a few hundred rows), but you will see significant performance issues if you try to use it on larger datasets. In these cases, it is __much__ faster to [import an entire range][1] into a 'spare' sheet of the current spreadsheet and perform lookups against that.

[1]: https://support.google.com/docs/answer/3093340 "How to use the IMPORTRANGE function"