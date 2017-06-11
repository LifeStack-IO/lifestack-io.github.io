---
label: snippets
layout: post
title: Finding a character from a list in a sheets cell
short_title: __Find__ from a list
author:
  name: jd
tags:
- google
- sheet
category: tutorial
lead: How to use the find function with an array of values to search for
published: true
---
{% include lead.md %}

### Introduction

In Google Sheets you use the [arrayformula][1] function in conjunction with [find][2] to find the first instance of __any__ value from an array in a single cell.

### Method

Imagine you wanted to remove the numbers at the end of a cell value, but you didn't know in advance which numbers they would be, or how long they would be?

You can use the following formula to get the position of the first instance of a number in a cell value (Cell _A1_ in this example).

{% highlight puppet %}
INDEX(SORT(ArrayFormula(FIND({0;1;2;3;4;5;6;7;8;9},A1))),1,1)
{% endhighlight %}{:class="formula"}

If this formula was applied to the string __Fred123__ it will return _5_ as '1' is the 5th character in the string. It works by sorting the response array from the __find__ function and returning the first element (using __index__).

To return only the part of the string _before_ the number, we can combine it with the [mid][3] function, like this:

{% highlight puppet %}
IFERROR(MID(A1,1,INDEX(SORT(ArrayFormula(FIND({0;1;2;3;4;5;6;7;8;9},A1))),1,1)-1),"")
{% endhighlight %}{:class="formula"}

Or, to return just the number, simply change around the parameter order a litte:

{% highlight puppet %}
=IFERROR(MID(A1,INDEX(SORT(ArrayFormula(FIND({0;1;2;3;4;5;6;7;8;9},A1))),1,1), 1000),"")
{% endhighlight %}{:class="formula"}

The [iferror][4] function is used to catch the scenario where there are no numbers in the string, and just return nothing (although you could also adapt this to return the whole string if preferred).

You can supply any list you want, including words, so you could also adapt the formula to return a _true_ or _false_ value if any character / word in a list occurs in a cell, like:

{% highlight puppet %}
IF(IFERROR(INDEX(SORT(ArrayFormula(FIND({0;1;2;3;4;5;6;7;8;9},A1))),1,1), -1)>=0,true,false)
{% endhighlight %}{:class="formula"}

{% highlight puppet %}
IF(IFERROR(INDEX(SORT(ArrayFormula(FIND({"and";"the";"or";"to"},A1))),1,1), -1)>=0,true,false)
{% endhighlight %}{:class="formula"}

Remember that __find__ is case-sensitive, so you may want to adjust your 'search' list to accomodate this.

  [1]: https://support.google.com/docs/answer/3093275 "How to use the ARRAYFORMULA function"
  [2]: https://support.google.com/docs/answer/3094126 "How to use the FIND function"
  [3]: https://support.google.com/docs/answer/3094129 "How to use the MID function"
  [4]: https://support.google.com/docs/answer/3093304 "How to use the IFERROR function"