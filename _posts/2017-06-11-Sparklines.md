---
title: Sparklines with Google Sheets
layout: post
author:
  name: jd
category: tutorial
tags:
- sheet
- google
- training
published: true
lead: Simple, quick and useful. Sparklines let you visualise your spreadsheet data as small graphs, inside a single cell.
asset_prefix: qQv7K
---
{% include lead.md %}

## Sparklines?

A [sparkline][1]{:target="_blank"} is a small, spreadsheet cell-sized, graph. It is typically a line chart, but can also be a bar / column version. They are used to quickly visualise a series of data points (e.g. marks over time) in a way that allows fast comprehension of data patterns (e.g gradual improvement) at a glance. Most people find that graphical comprehension is much easier and faster than reading a row of numbers.

Sparklines are a native feature of Google Sheets, accessible via the [sparkline][1]{:target="_blank"} formula, which means they work seamlessly on the web and using mobile apps. Like other formulas, this will let you supply data in the form of a range of cells (e.g. a row, or column) or values from another function (this is useful if you have a non-contiguous dataset that you want to visualise). There are also a wide range of options you can also supply to format your sparkline in exactly the way that you want.

## A simple example

![Example Sparkline]({{ site.baseurl }}/assets/{{ page.asset_prefix }}_simple_animated.svg)

The easiest way to test out a simple sparkline is to use a row of data (6 columns wide in this example) and then the following formula.

{% highlight puppet %}
SPARKLINE(A1:G1)
{% endhighlight %}{:class="formula"}

This will draw a sparkline similar to the one above, namely a line chart illustrating the data series (from left to right, the same as our data). The vertical extents (the y-axis scale) are set automatically by sheets using the source data (the lower extent is the minimum value, and the upper the maximum). Typically, a line chart is best suited to a significant (non-trivial) number of data points and visualising broad data series (e.g. stock prices over time). Using a line in this way helps to visualise overall trends and patterns, which might not be obviously visible when looking at the data itself.

You can test this out by generating a larger series of 'pseudo-random' data (say 50-100 data points) in a single __column__ (Column A in this example) by using the following formula.

{% highlight puppet %}
RAND()+(ROW()*0.02)
{% endhighlight %}{:class="formula"}

The _0.02_ scalar ensures that the random sequence has an upward trend over a significant number of data points, but that the individual numbers themselves will jump around a little. Try plotting a sparkline using the following formula to confirm this. 

{% highlight puppet %}
SPARKLINE(A:A)
{% endhighlight %}{:class="formula"}

![Example Line Chart]({{ site.baseurl }}/assets/{{ page.asset_prefix }}_line_animated.svg)

As you can see from the above illustration, line charts work best for larger data series because the line is plotted continuously. In essence, it is a problem of resolution in such a small graphic. A line chart for a small number of points _implies_ that more data points exist than is actually the case (it 'looks' continuous). When using a higher number of points, this is _almost_ true (or at least a good approximation). For __smaller__ series of data (fewer points) you are much better using a simple columnar / bar chart sparkline.

### Customising the options

The second argument (which is optional) that you can supply to the sparkline function is _options_. Unusually for a spreadsheet, it takes the formation of a [JSON][3]{:target="_blank"}-style object that is a series of __name__ and __value__ pairs. The most important of which are in the table below.

|---
| Name | Values | Details
|:-|:-|:-
| charttype | _line_, _bar_, _column_ or _winloss_ | The visual style of the chart, for most uses this will be a choice between line and column.
| color | Name of the colour (red, green etc) or _RGB_ formatted string | This sets the colour for the lines / columns.
| ymin | Minimum value on the vertical / y-axis | This is normally set automatically, but can be very useful to scale charts.
| ymax | Maximum value on the vertical / y-axis | This is normally set automatically, but can be very useful to scale charts.
| lowcolor | Lowest value colour (red, green etc) or _RGB_ formatted string | This is only applicable for _column charts_.
| highcolor | Highest value colour (red, green etc) or _RGB_ formatted string | This is only applicable for _column charts_.
| negcolor | Negative value colour (red, green etc) or _RGB_ formatted string | This is only applicable for _column charts_.

All these options are supplied in double-quote marks (except numbers and booleans), and the "name" and the "value" are separated by a comma, which pairs being separated by a semi-colon. This leads to the general form being:

> {"name1" , "value" ; "name2" , true ; "name3" , 9 ... }
    
###### Chart Types

As discussed previously, the best type of chart for larger series of data is a _line_. This conveys overall trends very well. If you have a smaller data series and are looking to easily highlight __outliers__ (e.g. particular high or low values) then the _column_ chart is the best option. Depending on the size of your cells (height / width) a column chart with more than 10-20 data points will be very cluttered and difficult to read.

###### Colours

Using colours in a line chart is a useful way to make it stand out visually against the sea of black numbers / text that normally comprises a spreadsheet. Be wary of too __little contrast__ though (e.g. light colours like yellow) as this makes thin lines hard for most people to reliably see.

Colours in column charts can easily be used to highlight the highest (green) and lowest (red) values in a data set. This is helpful for quickly scanning a lot of data looking for patterns (e.g. the third value in easy data series tends to be the lowest). You may need to use one of the examples below, or carefully set your y-min value though if you use a colour to highlight the lowest value, as this is often represented by a very short column (e.g. a line) and is therefore difficult to see.

## Advanced examples

### Non-Contiguous Ranges

Typically, a sparkline will expect a contiguous (e.g. next to each other) set of data (e.g. columns A:G). You can't normally 'skip' columns by using a _comma_ or a _semi-colon_ in your range statement. This can be difficult if you tend to cluster contextual columns together (e.g. column 1 is the raw value, column 2 the percentage, column 3 the rank etc.). If the unwanted columns contain non-numerical data, you can use the sparkline options to exclude / ignore these values when plotting the chart. If they have numerical values, then we have to find a different way.

In order to pull in non-contiguous data sets, you can combine the sparkline with [query][4] function. Imagine you had a row of data with 12 columns, and you wanted to extract the 1st (__A__), 4th (__D__), 7th (__G__) and 10th (__J__) columns then you can embed the following query statement as the source for our sparkline:

{% highlight puppet %}
QUERY(A1:L1, "select A,D,G,J")
{% endhighlight %}{:class="formula"}

Combining this with the sparkline function would give the following formula.

{% highlight puppet %}
SPARKLINE(QUERY(A1:L1, "select A,D,G,J"))
{% endhighlight %}{:class="formula"}

If you want to take this further, you can use the power of the [query]({{ site.baseurl }}{% link _snippets/google_sheet_query.md %}) function to transform your source data without the need for 'extra' columns to hold temporary data.

### Dynamic Ranges & Averages

{% highlight puppet %}
SPARKLINE(A1:G1, {"charttype","column"; "lowcolor", "red"; "highcolor", "green"})
{% endhighlight %}{:class="formula"}

If you consider the formula above applied to a simple set of values: _1.56, 1.4, 1.38, 1.92, 1.41, 1.85, 1.63_. With this formula you will get a chart that has a range / y-axis scale of about 1.38 (lowest value) to 1.92 (highest value). This is useful as it makes the best use of the available cell space, and gives a good indication of the differences between the individual values. It is misleading, however, when you compare it to a sparkline of a different data set (e.g. _1.96, 1.80, 1.78, 1.98, 1.89, 2.02, 2.98_). Ths second data series will result in a sparkline that _looks_ like it contains a lot of smaller values (e.g. smaller columns) when in fact almost all the varies in the second series are __higher__ than the first. This is because the range (difference between the highest and lowest value) is great in the second series, which 'stretches' the sparkline.

{% highlight puppet %}
SPARKLINE(A1:G1, {"charttype","column"; "lowcolor", "red"; "highcolor", "green"; "ymin", 0; "ymax", 4})
{% endhighlight %}{:class="formula"}

If you are using sparklines to compare different series of data, it is important to use a consistent vertical scale, such as the formula above. Or you may choose to use a custom formula (using __MAX__ and __MIN__) to set the ranges according the the minimum and maximum values of your whole set of data values (rather than each series) as set out below.

{% highlight puppet %}
SPARKLINE(A1:G1, {"charttype", "column"; "axis", true; "lowcolor", "red"; "highcolor", "green"; "ymin", MIN($A$1:$G); "ymax", MAX($A$1:$G)})
{% endhighlight %}{:class="formula"}

If you combine this with an [arrayformula function][5] you can use the sparkline to plot the deviation of each value in your series from the overall average by making use of these dynamic ranges. The following formula assumes that you have numeric data in the first seven columns of your sheet (_A:G_) but is easily tweaked to suit the shape of your data.

{% highlight puppet %}
SPARKLINE(ARRAYFORMULA(A1:G1-AVERAGE(A:G)), {"charttype", "column"; "axis", true; "negcolor", "red"; "color", "green"; "ymin", MIN(ARRAYFORMULA($A:$G-AVERAGE($A:$G))); "ymax", MAX(ARRAYFORMULA($A:$G-AVERAGE($A:$G)))})
{% endhighlight %}{:class="formula"}

Sparklines can therefore be used to _communicate_ important information through visualisation. You can use them in the traditional way to show changes in a data series over time (e.g. marks over a term) but also to show attainment over time in combination with performance against a wider metric (targets, other data series etc). This gives an incredibly powerful tool to gain insights into the data in a spreadsheet in a quick and succinct manner.

*[RGB]: #Red-Green-Blue notation in hexadecimal, e.g. #FF0000 for bright red.

  [1]: https://en.wikipedia.org/wiki/Sparkline "All about Sparklines - Wikipedia"
  [2]: https://support.google.com/docs/answer/3093289 "How to use the SPARKLINE function"
  [3]: https://en.wikipedia.org/wiki/JSON "All about JSON - Wikipedia"
  [4]: https://support.google.com/docs/answer/3093343 "How to use the QUERY function"
  [5]: https://support.google.com/docs/answer/3093275 "How to use the ARRAYFORMULA function"