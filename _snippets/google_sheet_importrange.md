---
label: snippets
layout: post
title: The IMPORTRANGE Function
short_title: __IMPORTRANGE__ Function
author:
  name: jd
tags:
- google
- sheet
category: functions
lead: Use the IMPORTRANGE function in Google Sheets to aggregate and link information across spreadsheets.
published: true
---
{% include lead.md %}

### Introduction

Imagine being able to __link__ sheets together. Not by manually _copying_ and _pasting_ information, constantly checking to see if it needs to be updated, but actual __live__ linking. Imagine your data being __updated automatically__ whenever the source data changes. This is exactly what the [importrange][1] function does, it let's you import _real-time_ data from another sheet. Here is how to get the best out of it. 

### Method

###### Specifying the data source

[importrange][1] is all about _importing_, so the most important thing to do is to specify _where_ the data is coming from (the source spreadsheet). To do this, you will need to supply either the __spreadsheet id__ or the __spreadsheet url__. To get either, you'll need to jump onto your source spreadsheet and head up to the browser address bar. The url for the spreadsheet should begin with 'docs.google.com/spreadsheets'. The entire [string][2] is referred to as the __[URL][3]__ (it normally ends with 'edit' or 'view'). The __ID__ of the spreadsheet is the seemingly random long set of letters and numbers that you will find between the forward slashes (/) that delineate parts of the entire page address.

###### Writing the formula

Once you've copied *ctrl-c*{:.kb-shortcut} the id or whole address of the spreadsheet, you can create your formula in the sheet where you want the linked data to appear (the destination sheet). An example is shown below. Make sure that you quote your __URL__ or __ID__ using double-quote marks. As well as providing the source sheet address, you will also need to specify which data you want to import / link. This is supplied (quoted as well) in the same way you would reference cells in normal formulas, namely by providing the __sheet name__, following by an __exclamation mark__, and then the __range__.

{% highlight puppet %}
IMPORTRANGE("SPREADSHEET_ID OR SPREADSHEET_URL", "SHEET_NAME!A:A")
{% endhighlight %}{:class="formula"}

The first time in each destination sheet that you __run__ the formula (for a particular source sheet) you will be asked to _authorise_ access. This effectively __saves__ your access to the source sheet, meaning that if another user (who doesn't have access to the source sheet) does have access to destination sheet, will still be able to 'see' the data that you have imported. To authorise it, hover over the cell and click on the button that will pop up. Remember that this prompt won't happen if you have embedded the [importrange][1] function within a larger formula. So _good practice_ would be to run a test the import (importing a single cell, 'A1' for example) __first__, authorising the import __before__ writing any complex formulas.

###### Ranges

Understanding the language of the range is literally the __key__ to getting the __correct data__. Here are a few examples and explanations.

* __A:C__ will return all of the first _three_ columns
* __A1:C10__ will be the first _10_ rows of the first _three_ columns
* __A2:B__ will be the all of the first _two_ columns exluding the first row (useful if there are headers you don't need to import)
* __C1:Z1__ will return the _first_ row, from the _third_ column, _24_ columns wide
* __A1:1__ will return the entire _first_ row

### Furthermore

The standard output of this formula will be to __display__ the imported data in the destination sheet. However, you can also pass the imported data to other functions, such as [query][4], [vlookup][5], [match][6] or even [sparkline][7]. All of these formulas will allow you to further refine the data being displayed. For example, you might want to filter the data being imported for all the values larger than a defined number (greater than 100) or even by a value in your current sheet (greater than the value in cell A4). Notice how the formulas _wrap_ around each other. As is the case generally in mathematics, the innermost formula is _run_ first, working towards the outermost. So the output of the [importrange][1] function is passed ([piped][10]) as an input to the [query][4] function.

{% highlight puppet %}
QUERY(IMPORTRANGE("SPREADSHEET_ID OR SPREADSHEET_URL", "SHEET_NAME!A:D"), "select * where Col1 > 100")
{% endhighlight %}{:class="formula"}

{% highlight puppet %}
QUERY(IMPORTRANGE("SPREADSHEET_ID OR SPREADSHEET_URL", "SHEET_NAME!A:D"), CONCAT("select * where Col1 > ", A1)
{% endhighlight %}{:class="formula"}

You can use as many formulas as you wish, so you could first filter some data using [query][4] and then apply a [unique][8] function (to remove duplicate values) before finally a [sort][9], as shown here.

{% highlight puppet %}
UNIQUE(QUERY(IMPORTRANGE("SPREADSHEET_ID OR SPREADSHEET_URL", "SHEET_NAME!A:D"), CONCAT("select Col2 where Col1 > ", A1))
{% endhighlight %}{:class="formula"}

Whenever the underlying (source) data changes, the linked data will be updated to reflect this change. This means that you may end up with more or fewer rows. You should therefore be careful about implying a relationship with other data that shares the same row, as the __imported rows may change__! You can use [importrange][1] in conjunction with almost every other formula, and in almost any case where you can enter a range. The possibilities are almost __limitless__.

[1]: https://support.google.com/docs/answer/3093340 "How to use the IMPORTRANGE function"
[2]: https://en.wikipedia.org/wiki/String_(computer_science) "What is a 'string' in Computer Science - Wikipedia"
[3]: https://en.wikipedia.org/wiki/Uniform_Resource_Locator "What is a URL - Wikipedia"
[4]: https://support.google.com/docs/answer/3093343 "How to use the QUERY function"
[5]: https://support.google.com/docs/answer/3093318 "How to use the VLOOKUP function"
[6]: https://support.google.com/docs/answer/3093378 "How to use the MATCH function"
[7]: https://support.google.com/docs/answer/3093289 "How to use the SPARKLINE function"
[8]: https://support.google.com/docs/answer/3093198 "How to use the UNIQUE function"
[9]: https://support.google.com/docs/answer/3093150 "How to use the SORT function"
[10]: https://en.wikipedia.org/wiki/Pipeline_(computing) "What is a 'pipeline' in Computing - Wikipedia"