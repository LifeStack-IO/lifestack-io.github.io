---
label: snippets
layout: post
title: How to use dates in the QUERY function
short_title: __Query__ using dates
author:
  name: jd
tags:
- google
- sheet
category: tutorial
lead: Use the QUERY function to return results before, on or after a certain date
published: true
---
{% include lead.md %}

### Introduction

In Google Sheets you use the [query][1] function in a number of [very powerful ways]({{ site.baseurl }}{% link _snippets/google_sheet_query.md %}), including selecting and aggegating data for use in other functions (such as [sparkline][2]).

Occasionally you might want to select rows or data from a sheet based on a relative date (e.g. before today or in the future). This can be useful for show future orders, exams due to being sat in the next few days, or new employees starting in the next few weeks who need to be provisioned and trained.

### Method

A typical query function might look like this:

    Static Query
{% highlight puppet %}
QUERY(MY_DATA!1:1000, "select B, D, E, F, G, Y where (Y is null OR Y >= 3)")
{% endhighlight %}{:class="formula"}

This will return six columns from your *MY_DATA* sheet tab, where the value in column Y is either missing or greater than or equal to 3. This is a static query, as it is fixed until you change it. If you wanted to be more flexible with the values that you select, you may wish to move the *3* value into a cell and just reference that. That's pretty each using the [concatenate]({{ site.baseurl }}{% link _snippets/google_sheet_concatenate.md %}) operator, like this (assuming the selection criteria value of 3 gets put into cell A1).

    Dynamic Query
{% highlight puppet %}
QUERY(MY_DATA!1:1000, "select B, D, E, F, G, Y where (Y is null OR Y >= "&A1&")")
{% endhighlight %}{:class="formula"}

This builds a query dynamically, e.g. whenever the value of cell A1 changes, the results returned from the query will be updated. We can use this same technique to build dynamic queries based on dates. Normally, the format for dates used as [criteria][3] in the where clause of a query is *yyyy-mm-dd* (e.g. 2017-09-01). Helpfully, we can use the [text][4] function to provide this date formatting for us.

    Dynamic Dates
{% highlight puppet %}
QUERY(MY_DATA!1:1000, "select B, D, E, F, G, Y where G >= '"&TEXT(NOW(),"yyyy-mm-dd"))
{% endhighlight %}{:class="formula"}

The formula above uses the [now][5] function to generate a dynamic query that returns results where the date value in column G is in the future (relative to midnight on the current date). We supply the format to the [text][4] function to ensure [query][1] can understand our date. You will also need to make sure that your source data is correctly interprete as a 'date' by using the _Format -> Number -> Date_ menu command. You can also use this same style to reference a cell containing a date (e.g. A1, rather than NOW()). Or you can perform a calculation using the current date:

    Date Ranges
{% highlight puppet %}
QUERY(MY_DATA!1:1000, "select B, D, E, F, G, Y where (G >= '"&TEXT(NOW()-14,"yyyy-mm-dd")&"' and G <= '"&TEXT(NOW()+14,"yyyy-mm-dd")&"')")
{% endhighlight %}{:class="formula"}

This example will return all rows where the date in column G is on or after 14 days ago and on or before 14 days in the future, e.g. within four weeks centred on today. This can be very useful for selecting 'current' or relevant rows of data from a larger set.

  [1]: https://support.google.com/docs/answer/3093343 "How to use the QUERY function"
  [2]: https://support.google.com/docs/answer/3093289 "How to use the SPARKLINE function"
  [3]: https://developers.google.com/chart/interactive/docs/querylanguage?csw=1#where "The where clause in Query Language"
  [4]: https://support.google.com/docs/answer/3094139 "How to use the TEXT function"
  [5]: https://support.google.com/docs/answer/3092981 "How to use the NOW function"