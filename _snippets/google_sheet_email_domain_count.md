---
label: snippets
layout: post
title: Counting Email Address Domains using the QUERY Function
short_title: __Email Address Domain__ Count
author:
  name: jd
tags:
- google
- sheet
category: functions
lead: How to create a summary list of unique email domains from a list of email addresses, and count how many times they appear in that list.
published: true
---
{% include lead.md %}

### Introduction

It's a __common requirement__. Perhaps you have a list of respondent email addresses from a [Google Form]({{ site.baseurl }}{% link _snippets/google_form_response_notifications.md %}) or for bulk emailing you are sending. You want to see how many __unique email domains__ (the part of the address after the '@' sign, e.g. gmail.com) are in your list, and how many email addresses are at those domains.

### Email Domains

|---
| Email
|:-
| john.doe@example.com
| jane.doe@example.com
| a.person@testing_some_more.com
| another.person@example.com
| penultimate.example@testing.example.com
| final.example@testing_some_more.com

Consider a list that looks something like the example one above. Email addresses in a single column, starting at row number 2 on your sheet with a simple header. Firstly, we need to get a unique list of all the email domains. We can use the [query]({{ site.baseurl }}{% link _snippets/google_sheet_query.md %}) function to solve this problem, combined with [arrayformula][1] here, as follows.

{% highlight puppet %}
IFERROR(SORT(UNIQUE(QUERY(ARRAYFORMULA(SPLIT(A2:A,"@")), "select Col2"))),"")
{% endhighlight %}{:class="formula"}

In this example, we're assuming our email address list in the first column of the spreadsheet (Column A). If yours is elsewhere, simple update the cell references (A2:A) within the split function, and it will produce a result like this.

|---
| Domain
|:-
| example.com
| testing_some_more.com
| testing.example.com

    How does it work?

As with all 'embedded' formulas (where functions _wrap_ other functions), we have to read from the inside of the formula out. So, let's break it down, beginning with the innermost function (split).

{% highlight puppet %}
SPLIT(A2:A,"@")
{% endhighlight %}{:class="formula"}

The [split][2] function is used to divide the email address into two parts, the first part is the 'username' portion of the address, and the second is the 'domain'. Normally we would use split on a single value/cell, but here we are passing it our whole column of values. If we run __just__ this part of our formula, we will just get a single row in return. To get __every__ row in our source, we need too wrap the [split][2] function with a call to [arrayformula][1].

{% highlight puppet %}
ARRAYFORMULA(SPLIT(A2:A,"@"))
{% endhighlight %}{:class="formula"}

In simple terms, this coerces the [split][2] function to run for __each__ of the values in our supplied range (our column of email addresses) and return an array of results. Running this formula would give an output similar to the one below.

|---
| Username | Domain
|:- |:-
| john.doe | example.com
| jane.doe | example.com
| a.person | testing_some_more.com
| another.person | example.com
| penultimate.example | testing.example.com
| final.example | testing_some_more.com

You will also, likely, get a lot of '#VALUE!' errors as well. This is because the [split][2] is running on __every__ cell in our column. You could constrain it be explicitly specifying an end to your email address range by changing __A2:A__ to something like __A2:A7__ (in our six email address example, plus 1 for the header). In our case, we're not going to worry as we'll clean that up later in the formula! The next challenge is to __just__ get the domain (the second column in our results). The easiest way to do this is to use [query][3] to return this column only, using _select Col2_.
    
{% highlight puppet %}
QUERY(ARRAYFORMULA(SPLIT(A2:A,"@")), "select Col2")
{% endhighlight %}{:class="formula"}

Using query has the bonus of removing those error messages too, leaving us with a nice list of email domains (one for each entry in our email list).

|---
| Domain
|:- |:-
| example.com
| example.com
| testing_some_more.com
| example.com
| testing.example.com
| testing_some_more.com

We're getting close to our final list here, but now we need a [sorted][4] list of [unique][5] domains. This is straightforward, with two further wrapping functions to first produce a unique set from our list, and then sort them into alphabetical order. Finally, we wrap the whole formula using [iferror][7] to handle the situation where our list is empty. In our example, we are outputting an __empty string__ ("") in this case, but you could always change it to something more meaningful, like below.

{% highlight puppet %}
IFERROR(SORT(UNIQUE(QUERY(ARRAYFORMULA(SPLIT(A2:A,"@")), "select Col2"))),"NO DATA IN COLUMN A!")
{% endhighlight %}{:class="formula"}

### Email Address Counts

To count the email addresses that are in each domain, we can't simply use a [countif][6] function, as the comparator/criterion part of that function is not sophisticated enough to deal with a partial match (e.g. just the domain). Instead, we can fall back to the ever flexible [query][3] to provide our count, using the formula below.

{% highlight puppet %}
IF(LEN(C2)>0, QUERY(A$2:A, "select count(A) where A contains '"&C2&"' label count(A) ''"),"")
{% endhighlight %}{:class="formula"}

The assumption here is that the data is in column A (as above) and your generated list of domains is in column C (starting in row 2 again). This formula needs to be placed in another column and __copied down__ for all the unique domains in your list. You can copy it right the way down to the bottom of the column, to anticipate any __growth/shrinkage__ in your email list (and consequently your unique domain list). The [if][8] function takes care of this by checking that the domain column cell value has something in it (e.g. it's length is greater than zero) and only runs the counting formula if this is the case. This saves remembering to expand or contract a formula list when the source data changes.

[1]: https://support.google.com/docs/answer/3093275 "How to use the ARRAYFORMULA function"
[2]: https://support.google.com/docs/answer/3094136 "How to use the SPLIT function"
[3]: https://support.google.com/docs/answer/3093343 "How to use the QUERY function"
[4]: https://support.google.com/docs/answer/3093150 "How to use the SORT function"
[5]: https://support.google.com/docs/answer/3093198 "How to use the UNIQUE function"
[6]: https://support.google.com/docs/answer/3093480 "How to use the COUNTIF function"
[7]: https://support.google.com/docs/answer/3093304 "How to use the IFERROR function"
[8]: https://support.google.com/docs/answer/3093364 "How to use the IF function"