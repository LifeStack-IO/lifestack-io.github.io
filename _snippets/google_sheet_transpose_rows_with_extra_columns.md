---
label: snippets
layout: post
title: How to transpose values to column headers, including extra blank columns
short_title: __Making__ column headers from values
author:
  name: jd
tags:
- google
- sheet
category: tutorial
lead: How to __transpose values__ to become headers, adding extra blank columns in between the values as well.
published: true
date: 2018-02-15
---
{% include lead.md %}

### Introduction

When analysing data in a spreadsheet format, you will often need to __pivot__ a set of values (e.g. cells orientated in a single column) into a set of headings (cells orientated in a single row). This is normally very easy, but you might also want to do slightly more complicated things, such as add extra blank columns between each value to use sub-headings. Here is how.

### Basic Transposition

Imagine we were gathering information about fruit preferences (who likes which fruits) in a spreadsheet. We have a list of fruits (such as the one below) which we want to become our column headings (from the B column onwards). The first column will contain the name of each person for whom we are recording data.

|---
| Fruits
|:-
| Apricot
| Avocado
| Pomegranate
| Banana
| Blackberry
| Nectarine
| ...

The following formula, using the [transpose][1] function, will change the orientation of our values (assuming the values are in Column A, from rows 1 to 15 inclusive).

{% highlight puppet %}
TRANSPOSE(A1:A15)
{% endhighlight %}{:class="formula"}

We can also manipulate our list a little before we transpose it. In the following formula, we are applying a __sort__ to the values first, meaning our column headers will be __alphabetically sorted__.

{% highlight puppet %}
TRANSPOSE(SORT(A1:A15))
{% endhighlight %}{:class="formula"}

We could also take this further, using using [query]({{ site.baseurl }}{% link _snippets/google_sheet_query.md %}), [importrange]({{ site.baseurl }}{% link _snippets/google_sheet_importrange.md %}) or [filter][2] functions to refine the list of values we want in our headers.

### Adding Extra Columns

Occasionally, we may need to use __sub-headings__ to further record data. In this case, we might want to record a taste preference (likes, does not like) and an allergy notification for each fruit. We could combine this into a single cell ('Likes, Allergic') but this makes filtering much more difficult and is error-prone.

Instead, we can use the following formula to create our headers with __two columns__ per fruit (e.g. Apricot, _Blank Column_, Avocado, _Blank Column_, ...).

{% highlight puppet %}
SPLIT(ARRAYFORMULA(JOIN(REPT(" ✏", 2), SORT(A1:A15))), "✏")
{% endhighlight %}{:class="formula"}

Simply adjust the **2** value in the formula above to give the number columns you would like for each value. The key part of the formula is the blank space, as this will __become__ the blank column, so make sure you don't accidentally remove it when you use the formula above!

{% highlight puppet %}
SPLIT(REPT(JOIN("✏", {"Preference","Allergy"})&"✏", COUNTIF(A1:A15, "<>")),"✏")
{% endhighlight %}{:class="formula"}

To create our __sub-headings__ (a repeated set of 'Preference' and 'Allergy'), we can use the formula above. Using the [countif][3] function, it will create these column pairs the __same number of times__ as our fruits.

We will then end up with a set of headings that look something like this:

|---
| Name | Apple |  | Apricot | | ...
|  | Preference | Allergy | Preference | Allergy | ...
|:-
| John Doe | | | | |
| Jane Doe | | | | |
| ...

### Why the ✏?

No reason at all! You just need to use __any__ character or symbol that __will not appear__ in your values at all! The pencil unicode symbol is just a memorable one chosen to meet this requirement.

  [1]: https://support.google.com/docs/answer/3094262 "How to use the TRANSPOSE function"
  [2]: https://support.google.com/docs/answer/3093197 "How to use the FILTER function"
  [3]: https://support.google.com/docs/answer/3093480 "How to use the COUNTIF function"