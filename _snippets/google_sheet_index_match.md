---
label: snippets
layout: post
title: The INDEX & MATCH Functions
short_title: __INDEX__ & __MATCH__ Functions
author:
  name: jd
tags:
- google
- sheet
category: functions
lead: How to link data from one part of a Google Sheet to another (or even between different sheets) using the __INDEX__ and __MATCH__ functions.
published: true
date: 2017-04-01
---
{% include lead.md %}

### Introduction

The ability to [lookup][1] data from another part of a spreadsheet is tremendously important to building really useful solutions using sheets. It gives us the power to maintain a [list][2] that we can effectively __choose__ from, then other cells can be populated with further details based upon the choice we have made. Not only does this __save time__ (reducing the amount of typing we have to do) but it also ensures __consistency__ and __accuracy__ by _reducing_ / _highlighting_ erroneous data.

### Method

When constructing lookups, most people would normally turn to the two dedicated functions, [vlookup][3] and [hlookup][4]. However, there are a number of reasons why you might want to use [index][5] and [match][6] [instead][7].

[index][5] / [match][6] is more powerful than [vlookup][3], frequently faster for larger data sets and 
it _isn't_ really harder to use at all. Using this combination gets round the most common issue with _normal_ lookups, namely you cannot lookup (return) values that are __left__ of the value you are matching. This commonly means that your lookup table has to be arranged so that the key values are in the first few columns, or you end up having to put __extra__ columns in to replicate data that originally appears on the wrong side of your _key_ column.

|---
| Id | Given Name | Family Name | Class
|:-|:-|:-|:-
| 1000 | John | Doe | 11EN
| 1001 | Jane | Doe | 11EN
| 1002 | A | Person | 11EN
| 1003 | Another | Person | 11EN

Using the table of data above, to __find__ a particular value using the [match][6] function we might use the following formula. This will return the row number of the first row where the value 'Person' occurs in the __C__ (third) column. The result will be __four__ (counting the header column as one). If we wanted to exclude the header column from the match, we could specify the range as __C2:C__.

{% highlight puppet %}
MATCH("Person", C:C, 0)
{% endhighlight %}{:class="formula"}

Now, with a traditional lookup, we would only be able to return values from the __D__ (fourth) column. So if we wanted to return the _given name_ of the first individual with a _family name_ of 'Person', we'd be a bit stuffed.

###### Enter Index

{% highlight puppet %}
INDEX(B:B, MATCH("Person", C:C, 0), 1)
{% endhighlight %}{:class="formula"}

By passing our returned value (4) to the [index][5] function as the row number, we can precisely specify the cell value we would like to retrieve. In this case, we want the value at __column 1__, __row 4__ in the range __B:B__. If we had opted to exclude the header rows then we would also need to do the same in our [index][5] function, otherwise we'd would return the value for the cell _above_ (-1) the one we wanted. We could also widen our indexing range to __A2:D__ and return the second column (this would do exactly the same thing).

{% highlight puppet %}
INDEX(A2:D, MATCH("Person", C2:C, 0), 2)
{% endhighlight %}{:class="formula"}

Using [index][5] gives extra flexibility, because you can use a further [match][6] condition to return the column number. This is __especially useful__ when you need to pull a value from a different sheet that matches a row header and column header (e.g. student id & assignment title) in your sheet.

[1]: https://en.wikipedia.org/wiki/Lookup_table "What is a lookup table - Wikipedia"
[2]: https://support.google.com/docs/answer/186103 "How to create a drop-down list"
[3]: https://support.google.com/docs/answer/3093318 "How to use the VLOOKUP function"
[4]: https://support.google.com/docs/answer/3093375 "How to use the HLOOKUP function"
[5]: https://support.google.com/docs/answer/3098242 "How to use the INDEX function"
[6]: https://support.google.com/docs/answer/3093378 "How to use the MATCH function"
[7]: http://trumpexcel.com/2014/11/vlookup-vs-index-match-debate-ends/ "Why INDEX / MATCH is better than VLOOKUP"