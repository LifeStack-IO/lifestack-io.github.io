---
label: snippets
layout: post
title: How to aggregate rows and columns in sheets
short_title: __Aggregating__ data
author:
  name: jd
tags:
- google
- sheet
category: tutorial
lead: How to aggregate data from different rows and columns for further processing
published: true
---
{% include lead.md %}

### Introduction

There are many ways in which aggregated data can be used. You might need to grab an array of data from different rows or produce a sorted and unique list of items from some columns. Commonly these aggregations are often used as inputs for other functions and are known as [arrays][1] in the Google Sheets product documentation.

### Basic Arrays

Arrays are built using the curly brace syntax ({**LIST OF RANGES**}). Ranges of cells are addressed in the normal way (e.g. A1, A:A, A2:C etc.) but are delineated by either a comma (,) or a semicolon (;). The delineating character essentially sets the direction (comma = horizontal, semicolon = vertical) of the output array.

|---
| Fruit 1 | Fruit 2 | Fruit 3
|:-|:-|:-
| Apple | Guava | Satsuma
| Apricot | Melon | Tamarind
| Avocado | Mango | Yuzu
| Banana | Mulberry | Pomegranate
| Blackberry | Nectarine | Pear
| Bilberry | Orange | Plum
| Blackcurrant | Elderberry | Strawberry
| Blueberry | Gooseberry | Pineapple
| Currant | Grape | Avocado
| Boysenberry | Grapefruit | Damson
| Cherry | Tangerine | Date

If you wished to pull these three columns together into a single column/array, you could use the following formula.

{% highlight puppet %}
{A1:A11;B1:B11;C1:C11}
{% endhighlight %}{:class="formula"}

If you wanted a single row containing all these fruits, then you could do this.

{% highlight puppet %}
{A1:C1,A2:C2,A3:C3,A4:C4,A5:C5,A6:C6,A7:C7,A8:C8,A9:C9,A10:C10,A11:C11}
{% endhighlight %}{:class="formula"}

### Arrays within Functions

That was inelegant and tiresome to type, but you get the idea. The easiest way to swap the orientation would be to wrap our array in a [transpose][2] function.

{% highlight puppet %}
TRANSPOSE({A1:A11;B1:B11;C1:C11})
{% endhighlight %}{:class="formula"}

This is much more useful, as we are using the array as an input to another function. It is particularly helpful when we want to sort our array or output **unique** values.

{% highlight puppet %}
SORT(UNIQUE(({A1:A11;B1:B11;C1:C11})))
{% endhighlight %}{:class="formula"}
{% highlight puppet %}
QUERY(UNIQUE({A:A;B:B;C:C}), "select Col1 where Col1 <> '' order by Col1")
{% endhighlight %}{:class="formula"}

In the second example above, we are using a [query]({{ site.baseurl }}{% link _snippets/google_sheet_query.md %}) function to remove any blank entries from our output list (by way of a 'where' condition). This is particularly useful as it allows us the aggregate the entire columns and not have to change our formula every time we add more data. Similar to using query with [importrange]({{ site.baseurl }}{% link _snippets/google_sheet_importrange.md %}), when using an array as a data source for a query, you can't address the columns by their letter headings anymore. Instead, you have to use the _Col1, Col2, Col3_ naming unless you specify a heading row.

We can also use our array as an input into a [query]({{ site.baseurl }}{% link _snippets/google_sheet_query.md %}) or [sparkline]({{ site.baseurl }}{% link _posts/2017-06-11-Sparklines.md %}) function. The latter is particularly useful as it allows the selective use of data from a single row as the source for a sparkline. So, instead of having to use a contiguous set of cells in your sparkline, you can pick and choose.

{% highlight puppet %}
SPARKLINE({C1:E1,M1:O1,Q1:R1})
{% endhighlight %}{:class="formula"}

Any function that accepts a range can also normally accept an array, just make sure that you get the orientation correct!

  [1]: https://support.google.com/docs/answer/6208276 "Using arrays in Google Sheets"
  [2]: https://support.google.com/docs/answer/3094262  "How to use the TRANSPOSE function"