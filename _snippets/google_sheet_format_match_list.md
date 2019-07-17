---
label: snippets
layout: post
title: Format values based on whether they appear in another column
short_title: __HIGHLIGHT__ List Matches
author:
  name: jd
tags:
- google
- sheet
category: functions
lead: How to use __conditional formatting__ to highlight cells that appear in another list.
published: true
date: 2018-07-05
---
{% include lead.md %}

### Introduction

You have a whole range of data (multiple columns and rows), and you wish to __highlight cells__ based on whether they __appear__ in __another list__ (such as absent students)? No problems, custom [conditional formatting][1] is here to help!

### Method

Let us assume that the list upon which you want to match is in __column A__ of your sheet, and the data you want to highlight (where a duplicate is found), is in __columns B-Z__.

Select this range (columns B onwards), and apply a conditional format (Format -> Conditional formatting...). Select __Custom Format__ from the 'Format cells if...' _dropdown_, and then enter the following formula (including the initial __=__ symbol).

{% highlight puppet %}
IF(MATCH(B1,$A$1:$A,0)>=0,TRUE,FALSE)
{% endhighlight %}{:class="formula"}

Then select the format you wish to apply to the cells, and those cells that match a value in your __A__ column will be highlighted.

Easy!

  [1]: https://support.google.com/docs/answer/78413 "How to use Conditional Formatting"