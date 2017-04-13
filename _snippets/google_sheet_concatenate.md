---
label: snippets
layout: post
title: The CONCATENATE Function
author:
  name: jd
tags:
- google
- sheet
category: functions
lead: How to 'add' or 'combine' text or cells in Google Sheets
published: true
---
{% include lead.md %}

### Introduction

Combining text (or '[strings][3]' in programming parlance) is more useful than you might _initially_ imagine. It can typically be used to combine names (e.g. Given name & Family name) into a display name or salutation. It can also be used to help [identify duplicates entries]({{ site.baseurl }}{% link _snippets/google_sheet_duplicates.md %}) within a list of rows (e.g. duplicate customers, records or products) by create a unique single value for each __row__.

You can do this by using the [concatenate][1] function, or it's more basic [concat][2] form.
### Method

###### Inputs & Outputs

Like many other functions, [concatenate][1] can take either a string or a range as an argument. An _argument_ is the word we use (commonly also referred to as a parameter) to describe the data that we provide to a function, in other words, the __input__. What we get back (the __output__) will be displayed in the cell. In the short example below, we could use the formula to add two numbers together (our inputs) to get the answer (our output).

{% highlight puppet %}
2+2
{% endhighlight %}{:class="formula"}

This formula could be rewritten using the [add][4] function, with our numbers being provided as arguments.

{% highlight puppet %}
ADD(2, 2)
{% endhighlight %}{:class="formula"}

We can also provide the address of a cell containing our values, rather than the explicit values themselves. Imagine we had these numbers in cells __A1__ and __A2__. Then our formula would read as follows.

{% highlight puppet %}
ADD(A1, A2)
{% endhighlight %}{:class="formula"}

Sheets understands that __A1__ is the address of a cell (a _reference_ to the value within that cell) because it is __not__ a number. References can either be to an individual cell (e.g. A1) or to a range of cells (e.g. A1:A2). A range is an inclusive _list_ of cells, in that it will include the first cell specified, the last cell specified, and all the cells in between. The range __A1__:__A3__ would, therefore, include __A1__, __A2__ and __A3__. __A1__:__B3__ would include __A1__, __A2__, __A3__, __B1__, __B2__ and __B3__.

Most formulas (e.g. [sum][5] and [concatenate][1]) allow you to use cells ranges as inputs (e.g. add all the numbers in this range of cells) but some, simple versions, of formulas (e.g. [add][4] and [concat][2]) will only allow you to use references to individual cells. Functions with a fixed number of arguments (both [add][4] and [concat][2] will only accept two inputs) tend to only allow single cell references, whereas those that accept _n_ arguments ([sum][5] and [concatenate][1] will take as many inputs as you provide) will normally accept ranges. If in doubt, try it!

###### Using the formula

[Concatenate][1] combines the arguments you supply, even if they are numbers. The formula below will output the string __John Doe__, but the one below that will output __22__ (remember, combine rather than add). All the inputs will be treated as text, regardless or whether they are numbers or not.

{% highlight puppet %}
CONCATENATE("John", " ", "Doe")
{% endhighlight %}{:class="formula"}

{% highlight puppet %}
CONCATENATE(2, 2)
{% endhighlight %}{:class="formula"}

If you have a sheet with some data on people, laid out below, then you can use this to generate display names (e.g. __Mr John Doe__) in a single cell, which is useful for mailings & merges. To do this, we need to concatenate the constituent name parts with spaces (" ").

|---
| Title | Given Name | Family Name
|:-|:-|:-|:-
| Mr | John | Doe
| Ms | Jane | Doe

{% highlight puppet %}
CONCATENATE(A2, " ", B2, " ", C2)
{% endhighlight %}{:class="formula"}

If you are importing data into sheets, you can also do the opposite ('decomposing' or splitting a display name into given name, family name etc) by using the [split]({{ site.baseurl }}{% link _snippets/google_sheet_split.md %}) function.

###### Shorthand Version

In the same way that '+' is a shorthand operator for the [add][4] function (or perhaps the function is a longhand version of the operator), you can also use '&' as a shorthand operator for [concat][2]. The example below will give the same output as the previous formula but in a more compact form. This is particularly useful when embedding in a longer formula to avoid too many confusing nested brackets.

{% highlight puppet %}
A2&" "&B2&" "&C2
{% endhighlight %}{:class="formula"}

###### Mixing Strings, Cell References and Functions

Remember that you can 'mix and match' between text and references (as we did above with spacing characters), so you can use the function to append or prepend a specific string to your cell values. This is helpful if you can to include a conditional or optionally append an initial to a display name. Consider the following sheet of data, now with an optional middle name.

|---
| Title | Given Name | Family Name | Middle Name
|:-|:-|:-|:-
| Mr | John | Doe | Peter
| Ms | Jane | Doe |

We can include the first letter of the middle name (using the [left][7] function) into our concatenation as follows.

{% highlight puppet %}
CONCATENATE(A2, " ", B2, " ", LEFT(D2, 1), " " C2)
{% endhighlight %}{:class="formula"}

This will work perfectly when the middle name is present, giving us __Mr John P Doe__ for our first record. However, when we use the same formula on our second record, we get an awkward visual double space because no middle name is present, e.g. __Ms Jane&nbsp;&nbsp;Doe__. To avoid this, we can insert a conditional [if][8] to test the length of the middle name cell, and only output the initial (and space) if the length is greater than zero.D2

{% highlight puppet %}
CONCATENATE(A2, " ", B2, " ", IF(LEN(D2)>0, CONCAT(LEFT(D2, 1), " "), ""), C2)
{% endhighlight %}{:class="formula"}

### Advanced Cell Referencing with INDIRECT

Concatenation can also be used with the [indirect][6] function to produce cell references. Whilst this is not common, it can be very helpful if you are programmatically populating cell references and are therefore unable to take advantage of [autofill][8] referencing (when references automatically increment when you 'drag fill').

{% highlight puppet %}
INDIRECT(CONCAT("A", ROW()))
{% endhighlight %}{:class="formula"}

The formula above concatenates a known column reference (e.g. 'A') with the current row number (e.g. 1) to produce a cell reference string ('A1'). This is then used by [indirect][6] to give you the value of that cell.

[1]: https://support.google.com/docs/answer/3094123 "How to use the CONCATENATE function"
[2]: https://support.google.com/docs/answer/3093592 "How to use the CONCAT function"
[3]: https://en.wikipedia.org/wiki/String_(computer_science) "What is a 'string' in Computer Science - Wikipedia"
[4]: https://support.google.com/docs/answer/3093590 "How to use the ADD function"
[5]: https://support.google.com/docs/answer/3093669 "How to use the SUM function"
[6]: https://support.google.com/docs/answer/3093377 "How to use the INDIRECT function"
[7]: https://support.google.com/docs/answer/3094079 "How to use the LEFT function"
[8]: https://support.google.com/docs/answer/75509 "Automatically create a series or list"
[8]: https://support.google.com/docs/answer/3093364 "How to use the IF function"