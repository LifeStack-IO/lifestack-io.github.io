---
label: snippets
layout: post
title: The SPLIT Function
author:
  name: jd
tags:
- google
- sheet
category: functions
lead: Splitting text values into constituent parts
published: true
---
{% include lead.md %}

### Introduction

Google Sheets now has the built-in ability to [split data][2] in an existing spreadsheet, or even when you paste *ctrl-v*{:.kb-shortcut} in new data. If you have more complex or specific requirements, you can also achieve a similar outcome by using the [split][1] function.

### Method

Imagine that you have a set of names, like the following, that you want to split (decompose) into their constituent parts (e.g. _given_ name and _family_ name).

|---
| Full Name
|:-
| John Doe
| Jane Louise Doe

###### Using SPLIT

The easiest way to accomplish this (mirroring the functionality offered within Google Sheets itself) is to use the [split][1] function to expand the text into an array of values split by the space character.

{% highlight puppet %}
SPLIT(A2, " ", TRUE)
{% endhighlight %}{:class="formula"}

This will output all the constituent parts of the name into _adjacent horizontal_ cells. If any of the destination cells have existing content, you will get an error until you clear them. The output will take the form of a '[jagged array][9]', such as the one below.

|---
| Full Name | | |
|:-|:-|:-|:-
| John Doe | John | Doe |
| Jane Louise Doe | Jane | Louise | Doe

If you would like to transform the direction of these cells (e.g. have the names split out to a vertical, rather than horizontal, list) then you can use the [transpose][8] function to achieve this (as below).

{% highlight puppet %}
TRANSPOSE(SPLIT(A2, " ", TRUE))
{% endhighlight %}{:class="formula"}

###### Using FIND

The [split][1] function works well for simple names (e.g. John Doe), but with names that include middle names, it will create a list that will need further processing because the second column may sometimes contain family names, and sometimes middle names. You can improve on this in a number of ways. Firstly by using a combination of the [left][3], [find][7], [len][5] and [mid][4] functions to 'find' the first space and output the text before it (the first formula) and also after it (the second formula). The table below illustrates the output.

{% highlight puppet %}
LEFT(A2, FIND(" ", A2, 1) - 1)
{% endhighlight %}{:class="formula"}

{% highlight puppet %}
MID(A2, FIND(" ", A2, 1) + 1, LEN(A2) - FIND(" ", A2, 1))
{% endhighlight %}{:class="formula"}

|---
| Full Name | Given Name | Rest of Name
|:-|:-|:-
| John Doe | John | Doe
| Jane Louise Doe | Jane | Louise Doe

###### Using SPLIT and INDEX

The solution above is useful, but if you only want the 'first' and the 'last' part of the name, then [split][1] can be used in conjunction with [index][6] as part of an array formula to do just that. In the examples below, the first outputs the __first element__ of the split array (1) and the second outputs the __last element__ (using [counta][10] to determine the length). The braces are used to convert the output of the [split][1] function so it can be properly understood by the [index][6] function (an array formula). The table that follows the formula shows the results, which gives the first and last names in their correct columns, irrespective of the number of middle names in the source data.

{% highlight puppet %}
INDEX({SPLIT(A2, " ", FALSE)},1)
{% endhighlight %}{:class="formula"}

{% highlight puppet %}
INDEX({SPLIT(A2, " ", FALSE)}, COUNTA(SPLIT(A2, " ")))
{% endhighlight %}{:class="formula"}

|---
| Full Name | Given Name | Family Name
|:-|:-|:-
| John Doe | John | Doe
| Jane Louise Doe | Jane | Doe

[1]: https://support.google.com/docs/answer/3094136 "How to use the SPLIT function"
[2]: https://support.google.com/docs/answer/6325535 "Split Text into Columns"
[3]: https://support.google.com/docs/answer/3094079 "How to use the LEFT function"
[4]: https://support.google.com/docs/answer/3094129 "How to use the MID function"
[5]: https://support.google.com/docs/answer/3094081 "How to use the LEN function"
[6]: https://support.google.com/docs/answer/3098242 "How to use the INDEX function"
[7]: https://support.google.com/docs/answer/3094126 "How to use the FIND function"
[8]: https://support.google.com/docs/answer/3094262 "How to use the TRANSPOSE function"
[9]: https://en.wikipedia.org/wiki/Jagged_array "Jagged Array - Wikipedia"
[10]: https://support.google.com/docs/answer/3093991 "How to use the COUNTA function"