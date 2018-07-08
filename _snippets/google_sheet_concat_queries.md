---
label: snippets
layout: post
title: How to concatenate columns in a query
short_title: __CONCATENATE__ in Queries
author:
  name: jd
tags:
- google
- sheet
category: functions
lead: How to __concatenate columns__ in a query and return the results.
published: true
date: 2018-07-05
---
{% include lead.md %}

### Introduction

If you want to produce aggregated columns in your query results (like concatenated columns), then you can do this without needing to add extra columns!

### Method

By using the [arrayformula][1] function in conjunction with [concatenate]({{ site.baseurl }}{% link _snippets/google_sheet_concatenate.md %}) you can supply concatenated columns into your [query]({{ site.baseurl }}{% link _snippets/google_sheet_concatenate.md %}) formulas.

{% highlight puppet %}
{ARRAYFORMULA(A2:A&", "&B2:B&" ("&C2:C&")"),K2:K}
{% endhighlight %}{:class="formula"}

The formula above creates a two-column list, with the first column being a concatenation of columns A, B and C. This is useful if you have names and a group/identifier in these columns. If column __A__ contains a surname (__Doe__), column __B__ a given name (__John__) and column __C__ a form group (__9A__) then then concatenated column will produce: "__Doe, John (9A)__". Column K in this example might be a status column or a value upon which you want to select, e.g. show all the people who are going on a trip.

{% highlight puppet %}
IFERROR(QUERY({ARRAYFORMULA(A2:A&", "&B2:B&" ("&C2:C&")"),K2:K}, "select Col1 where Col2 = TRUE or Col2 = 'TRUE'", 0),)
{% endhighlight %}{:class="formula"}

This data set can then be fed into a normal [query]({{ site.baseurl }}{% link _snippets/google_sheet_concatenate.md %}) function, to produce a filtered set of results, returning just the concatenated column! The outer [iferror][2] function is used to catch the condition where no rows are returned, showing a __blank__ rather than an __error__.

  [1]: https://support.google.com/docs/answer/3093275 "How to use the ARRAYFORMULA function"
  [2]: https://support.google.com/docs/answer/3093304 "How to use the IFERROR function"