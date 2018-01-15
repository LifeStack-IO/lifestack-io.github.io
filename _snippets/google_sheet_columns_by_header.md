---
label: snippets
layout: post
title: Address columns by their header name rather than letter position
short_title: Columns by __header__ name
author:
  name: jd
tags:
- google
- sheet
category: tutorial
lead: Columns can move, and when using complex formulas (such as importrange), this can lead to problems. Here is how to __address__ a column by its header value, rather than it's position.
asset_prefix: fg4FF
published: true
date: 2018-01-15
example: https://docs.google.com/spreadsheets/d/1PJhH9mTLZUPnFDAQ3nhdpTe02c80Txzg4A5dzZ4Mt6Y/copy
---
{% include lead.md %}

[![Example Sheet]({{ site.baseurl }}/assets/{{ page.asset_prefix }}_screen.png){:class="img-fluid"}](https://docs.google.com/spreadsheets/d/1PJhH9mTLZUPnFDAQ3nhdpTe02c80Txzg4A5dzZ4Mt6Y/copy){:target="_new"}

The example google sheet above (populated with __random__ [generated test data](https://www.generatedata.com/){:target="_new"}) is also a generic [template](https://docs.google.com/spreadsheets/d/https://docs.google.com/spreadsheets/d/1PJhH9mTLZUPnFDAQ3nhdpTe02c80Txzg4A5dzZ4Mt6Y/edit?usp=sharing/copy){:target="_new"} that you can use right now to analyse __your own data__.

### Introduction

Writing _easy to use_, _robust_ and _customisable_ spreadsheets is a challenge, particularly if the people using your spreadsheets are not confident in writing their own custom formulas. You might be [importing]({{ site.baseurl }}{% link _snippets/google_sheet_importrange.md %}) data from a Google form responses sheet, or providing a summary analysis of a detailed dataset - both of which rely on being able to successfully address the correct columns. What happens if those columns move around? Or you want to be able to just type in the column header and generate data analysis for that column, without having to worry about column letters?

### Addressing a Range

Referencing, or addressing, a range normally requires simply selecting the relevant number of cells, be they a small group or entire row/column. When cells move around (rows/columns are inserted or removed), the reference is normally updated without you needing to do anything.

When using the [importrange][1] function to bring in data from another sheet, this doesn't happen automatically, particularly if you are using a static cell reference (e.g. just importing a couple of columns). You might also want to give the option of providing data analysis for a particular row or column, based upon the selection made by a user (e.g. for a particular data point or data subject).

In these more complex cases, you can use an alternate approach by __matching__ the column (or row) header and then return the data for that particular range.

### Indirect & R1C1 Notation

[Indirect][2] is a vital function when you need to resolve some more complicated range addressing problems. It allows you to build your range address dynamically using the [concatenate]({{ site.baseurl }}{% link _snippets/google_sheet_concatenate.md %}) function, and also to use the alternate __R1C1__ style of cell notation.

    What is R1C1?

_R1C1_ is an alternate way of addressing spreadsheet cells. Instead of using the traditional letters to indicate which column you are referring to (A-ZZ) you use a number. The __R__ specifies that the number that follows it refers to the row you are addressing (starting at 1) and the __C__ indicates that the number refers to a column (again, starting at 1). So, _R1C1_ refers to the same cell as _A1_. The notation is more verbose (which is why it isn't used as standard), but it is incredibly useful because numbers are a lot easier to handle in formulas.

    Using R1C1

While _Excel_ allows you to switch to __R1C1__ notation globally, _Sheets_ does not have that functionality. Instead, you can use this notation with the [Indirect][2] function by passing _false_ as the second parameter.

{% highlight puppet %}
INDIRECT("R1C1", false)
{% endhighlight %}{:class="formula"}

The formula _above_ with give you the value in cell A1 (first row and first column), and the table _below_ gives some equivalent range addresses in both __A1__ and __R1C1__ notation.

|---
| A1 Notation | R1C1 Notation | Description
|:-:|:-:|:-
| A1 | R1C1 | Cell in the __first__ row and __first__ column (A)
| B2 | R2C2 | Cell in the __second__ row and __second__ column (B)
| C:C | R1C3:C3 | All the cells in the __third__ column (C)
| 4:4 | R4C1:R4 | All the cells in the __fourth__ row
| 4:4 | R4C1:R4 | All the cells in the __fourth__ row
| B4:4 | R4C2:R4 | All the cells in the __fourth__ row starting from the __second__ column (B)
| E3:F | R3C5:C6 | All the cells in the __fifth__ and __sixth__ columm (E & F) starting from the __third__ row

### Finding a column

This is actually fairly easy using [match]({{ site.baseurl }}{% link _snippets/google_sheet_index_match.md %}). All we need to do is find our column name (which could be a cell value, like __A2__ in the example below, or an actual string) in the range of possible column name headings (the first row in this example).

{% highlight puppet %}
MATCH($A2, $1:$1, 0)
{% endhighlight %}{:class="formula"}

{% highlight puppet %}
MATCH("End of Year Test", $1:$1, 0)
{% endhighlight %}{:class="formula"}

In these [match][3] formulas, we supply __0__ as the third parameter to indicate that we want an exact match. The function itself will either return the position where the header name was found (the __column number__) or an error if the column wasn't found.

### Using INDIRECT

To reference the entire column, we need to concatenate the column number into an __R1C1__ formula for [indirect][2], shown below.

{% highlight puppet %}
INDIRECT("Data!R1C"&MATCH($A2,$1:$1,0)&":C"&MATCH($A2,$1:$1,0), false)
{% endhighlight %}{:class="formula"}

This formula will return the contents of the entire column, matching the header specified in cell __A2__.

### Putting it all together

Instead of just displaying the values from a particular column, we can pass all that range data into another aggregating function, such as [average][4].

{% highlight puppet %}
IFERROR(IF(LEN($A2)>0,AVERAGE(INDIRECT("R1C"&MATCH($A2,$1:$1,0)&":C"&MATCH($A2,$1:$1,0), false)),),)
{% endhighlight %}{:class="formula"}

We can also add in a length check using [len][5] (to make sure there is a value in cell __A2__) and wrap the whole formula in an [error handler][6] in case the column name is mistyped. This makes a __robust formula__ to address a column, regardless of its position, just by supplying the header name (or form field, in the case of Google Forms).

  [1]: https://support.google.com/docs/answer/3093340 "How to use the IMPORTRANGE function"
  [2]: https://support.google.com/docs/answer/3093377  "How to use the INDIRECT function"
  [3]: https://support.google.com/docs/answer/3093378 "How to use the MATCH function"
  [4]: https://support.google.com/docs/answer/3093615 "How to use the AVERAGE function"
  [5]: https://support.google.com/docs/answer/3094081 "How to use the LEN function"
  [6]: https://support.google.com/docs/answer/3093304 "How to use the IFERROR function"