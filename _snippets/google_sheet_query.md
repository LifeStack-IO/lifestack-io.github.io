---
label: snippets
layout: post
title: The QUERY Function
author:
  name: jd
tags:
- google
- sheet
category: tutorial
lead: Transform, filter and aggregate sets of data using the QUERY function.
published: true
---
{% include lead.md %}

### Introduction

[query][1] does exactly what it says on the tin. More powerful and sophisticated than the [filter][2] function, [query][1] allows you to execute [complex queries][3] to help answer specific questions about your data.

### Method

Let us look briefly at the simplified table of data below. It is trival to use the [average][4] function to find the arithmetic mean of all the numeric values in column F, as illustrated below. The same outcome could also be achieved using the [query][1] function too, albeit with a little more complexity.

{% highlight puppet %}
AVERAGE(F:F)
{% endhighlight %}{:class="formula"}

{% highlight puppet %}
INDEX(QUERY(F1:F5, "select avg(F)", 1), 2, 1)
{% endhighlight %}{:class="formula"}

|---
| Id | Given Name | Family Name | Display Name | Class | Mark
|:-|:-|:-|:-|:-|:-
| 1000 | John | Doe | John Doe | 11EN | 30
| 1001 | Jane | Doe | Jane Doe | 11EN | 35
| 1002 | A | Person | A Person | 11EN | 45
| 1003 | Another | Person | Another Person | 11EN | 23

Using query we can also select all the students from the table above who beat the class average, outputting them as a new list.

{% highlight puppet %}
QUERY(A1:F5, CONCATENATE("select D, F where F > ", INDEX(QUERY(F1:F5, "select avg(F)", 1), 2, 1)), 1)
{% endhighlight %}{:class="formula"}

Most __powerfully__, we can use use a variety of complex query constructs, such as _group by_, _max_, _min_, _limit_ and _pivot_. It is also fairly trivial to use the function to operate on data sets imported using the [importrange][5] function. When using [query][1] function on data that is in the same spreadsheet, you have to address the columns using __column letters__ (as shown above). These need to refer to the actual column letters, rather than letters that are relative to the range you are using, e.g. if you are querying range C:F, use the letters C, D, E & F - rather than A-D. When using it on remote / imported sources of data, you need to use the nomenclature of __Col1__, __Col2__ etc. These numbers __are__ relative to the range you are importing (as the function won't have any context of where the source data is positioned within a sheet).

[1]: https://support.google.com/docs/answer/3093343 "How to use the QUERY function"
[2]: https://support.google.com/docs/answer/3093197 "How to use the FILTER function"
[3]: https://developers.google.com/chart/interactive/docs/querylanguage "Query Language Reference"
[4]: https://support.google.com/docs/answer/3093615 "How to use the AVERAGE function"
[5]: https://support.google.com/docs/answer/3093340 "How to use the IMPORTRANGE function"