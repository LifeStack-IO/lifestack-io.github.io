---
label: snippets
layout: post
title: Filtering data quickly and easily using the QUERY Function
short_title: __Quick Filters__ for better sheets
author:
  name: jd
tags:
- google
- sheet
category: functions
lead: How to create simple '_drop-down_' filters in sheets to easily and quickly filter an imported range of data rows.
published: true
date: 2017-11-27
---
{% include lead.md %}

### Introduction

Viewing large datasets is something to which a tabular spreadsheet is brilliantly suited. You can use column [filters][1] or [filter views][1] to help highlight or focus on relevant rows, but sometimes these can be quite clunky for end-users. Filter views are also not available on mobile devices/apps, limiting their use.

### Filtering Imported Data

If you have a relatively complex spreadsheet that generated a final output that you wish to share with others, a good way of doing this is by using the [importrange]({{ site.baseurl }}{% link _snippets/google_sheet_importrange.md %}) and [query]({{ site.baseurl }}{% link _snippets/google_sheet_query.md %}) functions. You can create a new sheet, grant others edit permissions to it, and use it to present data from your original __complex__ sheet to them. Remember that filters _live_ within the sheet itself, so sometimes it's annoying having other people filter your sheet! Providing them with an output sheet using [range imports][2] removes this problem, as the filter is on the imported range in the new sheet, not in your source sheet. It also hides away the complexity of your spreadsheet from people who don't need to see all the inner workings, and it can speed things up as well because the importing of ranges doesn't seem to trigger a recalculation of the source sheet. So, if you have a lot of complex formulas that generate a final table - this technique will make it fast and responsive, while still preserving your control of the data model.

A typical range import might look like the following:

{% highlight puppet %}
IMPORTRANGE("ID_OR_URL_OF_SOURCE_SHEET","Output Data!A:Z")
{% endhighlight %}{:class="formula"}

The user only needs access to the sheet containing the [importrange]({{ site.baseurl }}{% link _snippets/google_sheet_importrange.md %}) function, **not the sheet containing the source data**. Once you have been through the authorisation process to 'Allow Access' to the source sheet, this access is retained with the sheet.

### Enter Query

If you want to provide a pre-filtered view of the data, you can __wrap__ the import with a [query][3] function. This trick would allow you to have multiple tabs showing different 'parts' of your data from your master (source) sheet. By using '__1__' as the final parameter for the [query]({{ site.baseurl }}{% link _snippets/google_sheet_query.md %}) function, it will also import the first row of your data as a 'header' row. The '__*__' in your selection criteria means that you would like to import all columns, although you can restrict it if you prefer to by specifying the exact columns (e.g. SELECT Col1, Col2, Col5, Col6). Often it is easier to restrict the columns being imported rather than have to _hide_ them afterwards.

{% highlight puppet %}
QUERY(IMPORTRANGE("ID_OR_URL_OF_SOURCE_SHEET","Output Data!A:Z"), "SELECT * WHERE Col1 = 10 AND Col2 = 'A'", 1)
{% endhighlight %}{:class="formula"}

### Creating Drop-Downs

While the solution above is perfect for _fixed_ views, you can also create __dynamic__ views by leveraging [data validation][4] to create a drop-down list that then updates your query formula. To do this, you can either use a fixed list of options or generate a dynamic list from your source data. By way of an example, if you wanted to filter on the contents of Column 5 (E) in your source data, you will first need to build a list of the available values in that column (excluding the header column). The formula below shows this and wraps the query with a [sort][6] and [unique][5] function to create a list of possible values.

{% highlight puppet %}
=SORT(UNIQUE(QUERY(IMPORTRANGE("ID_OR_URL_OF_SOURCE_SHEET","Output Data!A2:Z", "SELECT Col5 WHERE (Col5 <> '' AND Col5 is not null)", 0)))
{% endhighlight %}{:class="formula"}

To generate a __drop-down__ for a cell with these possible options, sheets must reference an actual range in your spreadsheet (rather than taking the list from a custom formula). So you need to create a 'LISTS' tab in your sheet, or something similar, containing each list you want to use in the columns (e.g. use the formula above for each list/column). Then you can set the __criteria__ for your 'Data Validation' to 'List from a range' and the range to your column (e.g. 'LISTS'!A:A). This will then create a drop-down under your filtering criteria cell.

To help you keep track of these filtering cells, it's a good idea to make them prominent (e.g. large emboldened fonts and a yellow background). This helps users visually locate them, making using the sheet faster. You should also [name][7] them so you can directly reference them in your formulas. Names such as __FILTER_GROUP__ or __FILTER_NAME__ will help identify to which columns the filters apply.

### Dynamic Querying

Once you have added your filter selection cells, with their associated drop-down lists (dynamically populated from your source), you can then adapt your importing query to use these dynamic parameters. This is achieved by a simple conditional statement (using an [if][8] function) to test whether the filter cell has a length that is greater than zero (e.g. if a filter has been selected from the drop-down). If it does, then this value is used to filter that column, if not, a wildcard is filter is used to return all rows. If you would prefer to use an __or__ filter, just change the statement (or even use another dropdown to allow the user to select this). The wildcard filter means that the number of conditions in the query remains the same, regardless of how many filters are used, which makes writing the query statement a __lot easier__.

{% highlight puppet %}
QUERY(IMPORTRANGE("ID_OR_URL_OF_SOURCE_SHEET","Output Data!A:Z"), "SELECT * WHERE " & IF(LEN(FILTER_GROUP)>0, "Col5='"&FILTER_GROUP&"'", "Col5 like '%'") & " AND " & IF(LEN(FILTER_NAME)>0, "Col1='"&FILTER_NAME&"'", "Col1 like '%'"), 1)
{% endhighlight %}{:class="formula"}

[1]: https://support.google.com/docs/answer/3540681 "Sort and filter your data"
[2]: https://support.google.com/docs/answer/3093340 "How to use the IMPORTRANGE function"
[3]: https://support.google.com/docs/answer/3093343 "How to use the QUERY function"
[4]: https://support.google.com/docs/answer/186103 "Create an in-cell dropdown list"
[5]: https://support.google.com/docs/answer/3093198 "How to use the UNIQUE function"
[6]: https://support.google.com/docs/answer/3093150 "How to use the SORT function"
[7]: https://support.google.com/docs/answer/63175 "Name a range of cells"