---
label: snippets
layout: post
title: Finding Duplicates Using Sheets
short_title: Finding __Duplicates__
author:
  name: jd
tags:
- google
- sheet
category: tutorial
lead: How to identify duplicate values or rows in Google Sheets
published: true
---
{% include lead.md %}

### Introduction

Highlighting duplicates in Google Sheets is quite straightforward if you use [custom conditional formatting][1]. You can check for duplicates based on a single value, or an entire row.

### Method

To check for duplicates, select the column you wish to de-duplicate (we're assuming it's column A in this example) and click 'Format -> Conditional formatting...'. Then select 'Custom formula' from the drop-down menu and type the following formula (including the equals sign).

{% highlight puppet %}
COUNTIF(A:A,A1)>1
{% endhighlight %}{:class="formula"}

Then select how you want to highlight duplicates (e.g. red background) and click 'Done'. You can also highlight duplicate rows by using the [concatenate]({{ site.baseurl }}{% link _snippets/google_sheet_concatenate.md %}) function to generate a 'key' for each row, using a formula such as this (assuming your row is three columns wide). The key will be unique for each combination of cells, so if the key matches another key, you have a duplicate row.

{% highlight puppet %}
CONCATENATE(A1:C1)
{% endhighlight %}{:class="formula"}

This can be used on data such as the following table, then perform the conditional format on the __key__ column to identify duplicate rows.

|---
| Given Name | Middle Name | Family Name | Key
|:-|:-|:-|:-
| John | | Doe | JohnDoe
| Jane | Louise | Doe | JaneLouiseDoe

###### Case Sensitivity

To handle case-insensitive row duplicate matching, convert all your keys to __UPPERCASE__, using the [upper][2] function. The formula looks like this.

{% highlight puppet %}
UPPER(CONCATENATE(A1:C1))
{% endhighlight %}{:class="formula"}

[1]: https://support.google.com/docs/answer/78413 "Use conditional formatting rules in Google Sheets"
[2]: https://support.google.com/docs/answer/3094219 "How to use the UPPER function"