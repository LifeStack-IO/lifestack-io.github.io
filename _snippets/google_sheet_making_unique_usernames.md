---
label: snippets
layout: post
title: Generate Unique Usernames using Spreadsheet Functions
short_title: Generating __Unique__ Usernames
author:
  name: jd
tags:
- google
- sheet
category: functions
lead: How to create a list of _unique_ __usernames__ from a list of given names and surnames.
published: true
date: 2017-10-24
---
{% include lead.md %}

### Introduction

If you work with technology, you will often find you need to generate a list of unique __usernames__ for importing into a system. You might only have a simple set of names to start from, and not fancy the job of manually checking all of them for duplicates (easy for __tens__, possible for __hundreds__, painful for __thousands__!). Here is how to do this automatically with just spreadsheet functions.

### Concatenating a Username

Firstly, you need to know how you are going to be generating your usernames. In fact, these can be any strings you need to be unique, but we'll stick to calling them usernames here. Imagine you have the following source data.

|---
| Given Name | Surname
|:- |:-
| John | Doe
| Peter | Doe
| Jane | Doe
| Joseph | Doe

From this example list, we want to generate usernames. A typical format might be first letter of the given name, followed by the surname (all set as lowercase). The formula, using a [concatenation]({{ site.baseurl }}{% link _snippets/google_sheet_concatenate.md %}), for this would be as follows:

{% highlight puppet %}
LOWER(CONCAT(Left(A2,1),B2))
{% endhighlight %}{:class="formula"}

We use the [lower][1] function to wrap our concatenation, which ensures that all the usernames are __lowercase__ (regardless of how our source data is formatted). If you are dealing with a long, or variable length list, and you want to just copy your username formula right down to the bottom of the sheet, you can wrap the entire formula in an [if][2] statement to check that the row has values before attempting the concatenation. If your source data is poorly formatted and has erroneous whitespace (e.g. spaces) before or after the values, you can also use [trim][3] to clean up the source values before you operate on them.

{% highlight puppet %}
IF(AND(LEN(A2)>0,LEN(B2)>0), LOWER(CONCAT(Left(TRIM(A2),1),TRIM(B2))), "")
{% endhighlight %}{:class="formula"}

### Avoiding Duplicates

|---
| Given Name | Surname | Username
|:- |:- | :-:
| John | Doe | jdoe
| Peter | Doe | pdoe
| Jane | Doe | jdoe
| Joseph | Doe | jdoe

After you have run the concatenation, you will end up with a table of data similar to the __one above__. This is great, apart from the _duplicates_. We __need unique usernames__. Ideally, we want our concatenation to step up, be a little more clever, and deal with these duplicates for us by appending a number to the end of each duplicate (to give us jdoe1, jdoe2 etc.).

To do this, we are going to need to break down the problem into a few steps. The first of these is looking for usernames that are duplicates of our current username. This requires us to add another column to the right of our username, to eventually contain our new __unique__ username. Initially, though, we will use [countif][4] to work out how many duplicates of our username exist __before__ our current row in the list.

{% highlight puppet %}
COUNTIF(INDIRECT("C1:C"&(ROW()-1)),C2)
{% endhighlight %}{:class="formula"}

|---
| Given Name | Surname | Username | Duplicates
|:- |:- | :-: | :-:
| John | Doe | jdoe | 0
| Peter | Doe | pdoe | 0
| Jane | Doe | jdoe | 1
| Joseph | Doe | jdoe | 2

The complex part here is the use of [indirect][5]. It is used to build a __dynamic range__ of all cells in the C column, before the current one, which then allows us to compare the values in previous rows to our one.

{% highlight puppet %}
INDIRECT("C1:C"&(ROW()-1))
{% endhighlight %}{:class="formula"}

Once we have done that, we can concatenate together the __duplicate count__ with our username to give a truly unique one.

{% highlight puppet %}
CONCAT(C2,COUNTIF(INDIRECT("C1:C"&(ROW()-1)),C2))
{% endhighlight %}{:class="formula"}

|---
| Given Name | Surname | Username | Unique Username
|:- |:- | :-: | :-:
| John | Doe | jdoe | jdoe0
| Peter | Doe | pdoe | pdoe0
| Jane | Doe | jdoe | jdoe1
| Joseph | Doe | jdoe | jdoe2

This satisfies our requirement, but the __zeros__ at the end of the usernames are rather ugly. Duplicates aren't that common, so we should really just append the number if it's more than zero. We can do this in two ways, the first using a simple [if][2] statement and the second using a more elegant [regexreplace][6].

    A simple IF
        
{% highlight puppet %}
CONCAT(C2,IF(COUNTIF(INDIRECT("C1:C"&(ROW()-1)),C2)>0, COUNTIF(INDIRECT("C1:C"&(ROW()-1)),C2), ""))
{% endhighlight %}{:class="formula"}

    An elegant REGEXREPLACE
        
{% highlight puppet %}
CONCAT(C2,REGEXREPLACE(TEXT(COUNTIF(INDIRECT("C1:C"&(ROW()-1)),C2),"0"),"^0", ""))
{% endhighlight %}{:class="formula"}

The elegant solution uses a [regular expression][7] to check for a zero at the start of the count (__^0__) and replace it with an empty string if it is found. We can't just replace __all zeros__ because that would mean numbers like 10 and 100 would be reduced to 1, causing us new duplicate problems! Using either of these formulas, you will end up with nicely formatted unique usernames, like the ones in the table below.

|---
| Given Name | Surname | Username | Unique Username
|:- |:- | :-: | :-:
| John | Doe | jdoe | jdoe
| Peter | Doe | pdoe | pdoe
| Jane | Doe | jdoe | jdoe1
| Joseph | Doe | jdoe | jdoe2

### Using a single column

The only annoying part of our solution above is that it requires __two columns__, and therefore __two steps__, to get a unique list. Firstly we have to generate all the _normal_ usernames; then we have to use these usernames to check for duplicates and create a unique list. This is quite easy to follow (making it a _simple_ solution), but it is quite convoluted (making it an _inelegant_ solution). Can we take this further and do everything in a simple column/formula?

The answer is __yes__, and the _secret_ is to use a combination of [query]({{ site.baseurl }}{% link _snippets/google_sheet_query.md %}) and [arrayformula][8] functions to generate a dynamic list of all the previous usernames. The [arrayformula][8] function runs the username concatenation for each row, and the query returns only the usernames previous to the current one, by using the __limit__ instruction and our [ROW()][9]-1 statement in the same way as our earlier [indirect][5] call.

{% highlight puppet %}
QUERY(ARRAYFORMULA(LOWER(CONCAT(Left(A$2:A,1),B$2:B))), "select Col1 limit "&(Row()-1), 0)
{% endhighlight %}{:class="formula"}

Once we have that list, it's straightforward to use another query to return only the duplicates of our current username. Remember that because we are using a __query on a query__, and a __query on the output of [arrayformula][8]__, we need to use _Col1_, rather than the _column heading letter_, in our query.

{% highlight puppet %}
QUERY(QUERY(ARRAYFORMULA(LOWER(CONCAT(Left(A$2:A,1),B$2:B))), "select Col1 limit "&(Row()-1), 0), "select Col1 where Col1='"&LOWER(CONCAT(Left(A2,1),B2))&"'", 0)
{% endhighlight %}{:class="formula"}

As our data starts on __row 2__, we end up counting our current row too, so we have to adjust for that by taking one away from the result of our [countif][4] function. This gives us our duplicate count, as shown in the table below (without the need for the extra column).

{% highlight puppet %}
COUNTIF(QUERY(QUERY(ARRAYFORMULA(LOWER(CONCAT(Left(A$2:A,1),B$2:B))), "select Col1 limit "&(Row()-1), 0), "select Col1 where Col1='"&LOWER(CONCAT(Left(A2,1),B2))&"'", 0), "<>") - 1
{% endhighlight %}{:class="formula"}

|---
| Given Name | Surname | Duplicates
|:- |:- | :-: | :-:
| John | Doe |  0
| Peter | Doe | 0
| Jane | Doe | 1
| Joseph | Doe | 2

Finally, we can wrap it all up with the same value checks, lowercase formatting and regex replacement that we have described earlier, giving us a single formula that __does everything__.

{% highlight puppet %}
IF(AND(LEN(A2)>0,LEN(B2)>0), LOWER(CONCATENATE(Left(A2,1),B2,REGEXREPLACE(TEXT(COUNTIF(QUERY(QUERY(ARRAYFORMULA(LOWER(CONCAT(Left(A$2:A,1),B$2:B))), "select Col1 limit "&(Row()-1), 0), "select Col1 where Col1='"&LOWER(CONCAT(Left(A2,1),B2))&"'", 0), "<>")-1,"0"), "^0", ""))),"")
{% endhighlight %}{:class="formula"}

|---
| Given Name | Surname | Unique Username
|:- |:- | :-: | :-:
| John | Doe | jdoe
| Peter | Doe | pdoe
| Jane | Doe | jdoe1
| Joseph | Doe | jdoe2

__Success__! Take a bow and enjoy the applause.

[1]: https://support.google.com/docs/answer/3094083 "How to use the LOWER function"
[2]: https://support.google.com/docs/answer/3093364 "How to use the IF function"
[3]: https://support.google.com/docs/answer/3094140 "How to use the TRIM function"
[4]: https://support.google.com/docs/answer/3093480 "How to use the COUNTIF function"
[5]: https://support.google.com/docs/answer/3093377 "How to use the INDIRECT function"
[6]: https://support.google.com/docs/answer/3098245 "How to use the REGEXREPLACE function"
[7]: https://en.wikipedia.org/wiki/Regular_expression "Regular Expressions - Wikipedia"
[8]: https://support.google.com/docs/answer/3093275 "How to use the ARRAYFORMULA function"
[9]: https://support.google.com/docs/answer/3093316 "How to use the ROW function"