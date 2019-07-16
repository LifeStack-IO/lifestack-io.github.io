---
label: snippets
layout: post
title: Denormalise & join tabular data into simple rows
short_title: __Creating__ expanded rows from data
author:
  name: jd
tags:
- google
- sheet
category: tutorial
lead: Like a database query join, how to __denormalise tabular data__ to create expanded rows, ideal for __mail-merges__ and __data imports__.
published: true
date: 2019-07-01
---
{% include lead.md %}

### Introduction

Before importing data into a system, or creating a mail-merge, you might need to [denormalise][1] your data. In simple terms, this means taking a more efficient data representation and expand it into a series of (often partially repeating) rows.

This is essential because whilst it is easy for you to read a compressed table of data, it isn't good fodder for feeding into a mail-merge routine or another system. For this, you will need a single row of data for each 'thing' you are representing - e.g. label you want to print.

### Source Data

Imagine we need to print book labels, with a single label for each book. Every individual will need one book for each subject, and each of these books will need a label. If we have 30 names, and 10 subjects, we will need 300 labels printed. To do this with a conventional mail-merge, we will need 300 rows in our source spreadsheet.

We might start with a simple table containing the names of each individual and a list of all the subjects (assuming everyone takes the same subjects).

|---
| Names [A] | Group [B] | Subjects [C]
|:-:|:-:|-:
| John Doe | 6A | Maths
| Jane Doe | 6A | English
| Jimmy Doe | 6B | Science
| | | History
| | | Geography
| | | ...

We now need to turn this into our de-normalised rows, __one row__ for each __name__ (Column A) and __subject__ (Column C). We can do this with a couple of clever little formulas.

### Denormalising

The first of these formulas will duplicate the names so that there are multiple rows (matching the number of subjects in column C) for each name. We start with the second row (A2:A) because the first row contains our column headings.

{% highlight puppet %}
ARRAYFORMULA(TRANSPOSE(SPLIT(CONCATENATE(ARRAYFORMULA(SPLIT(REPT(FILTER(A2:A, A2:A <> "")&"✏", COUNTIF(C2:C, "<>")),"✏"))&"✏"),"✏")))
{% endhighlight %}{:class="formula"}

To pull across the group codes for each name, we could use a similar formula, or we could fall back to using a simple [index/match]({{ site.baseurl }}{% link _snippets/google_sheet_index_match.md %}) approach (here we are assuming the output data begins on column E).

{% highlight puppet %}
IF(LEN(E2)>0,INDEX(B:B,MATCH(E2,A:A,0),1),)
{% endhighlight %}{:class="formula"}

Finally, we use a similar formula to above to create the list of subjects. But, instead of being the same value repeated a certain number of times, it is the entire list of subjects, repeated for each name.

{% highlight puppet %}
TRANSPOSE(ARRAYFORMULA(SPLIT(CONCATENATE(TRANSPOSE(ARRAYFORMULA(SPLIT(REPT(FILTER(C2:C, C2:C <> "")&"✏", COUNTIF(A2:A, "<>")),"✏")))&"✏"),"✏")))
{% endhighlight %}{:class="formula"}

### Output Rows

Using these formulas on our example data from above (3 names and 5 subjects), we will end up with 15 output rows that look something like this:

|---
| Names [D] | Group [E] | Subjects [F]
|:-:|:-:|:-:
| John Doe | 6A | Maths
| John Doe | 6A | English
| John Doe | 6A | Science
| John Doe | 6A | History
| John Doe | 6A | Geography
| Jane Doe | 6A | Maths
| Jane Doe | 6A | English
| Jane Doe | 6A | Science
| Jane Doe | 6A | History
| Jane Doe | 6A | Geography
| Jimmy Doe | 6B | Maths
| Jimmy Doe | 6B | English
| Jimmy Doe | 6B | Science
| Jimmy Doe | 6B | History
| Jimmy Doe | 6B | Geography

You can see the two patterns here, 5 (the number of subjects) rows for each of the names, and the 5 subjects repeated for each of the 3 names.

This data can then be used to create our label mailmerge. Best of all, if we need to add extra subjects or names to our source data; our output rows will __automatically update__ to reflect the new changes!

### Why the ✏?

No reason at all! You just need to use __any__ character or symbol that __will not appear__ in your values at all! The pencil unicode symbol is just a memorable one chosen to meet this requirement.

  [1]: https://en.wikipedia.org/wiki/Denormalization "Denormalization - Wikipedia"