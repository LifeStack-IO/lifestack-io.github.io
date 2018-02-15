---
title: Analysing Data with Custom Conditional Formatting
layout: post
author:
  name: jd
category: article
tags:
- sheet
- google
- training
- education
- markbook
published: true
lead: How to use _conditional formatting_ to __visually analyse data__, including non-numeric data such as grades, levels and categories.
asset_prefix: tx3bR
example: https://docs.google.com/spreadsheets/d/1c-sX-3PqRXBwYbavNIOjNeQL3JlWLDVl_k0PmoCZTDo/copy
---
{% include lead.md %}

_Visual data analysis_ is a potent tool for quickly understanding __patterns__, __trends__ and areas for __action__. In an educational context, this can be used to track __performance over time__, or as a __comparative__ tool to highlight achievement in different areas (e.g. subjects or skills).

[![Example Layout]({{ site.baseurl }}/assets/{{ page.asset_prefix }}_screen.png){:class="img-fluid"}]({{ page.example }}){:target="_new"}

The example google sheet above (populated with __random__ [generated test data](https://www.generatedata.com/){:target="_new"}) is also a generic [template]({{ page.example }}){:target="_new"} that you can use right now to analyse __your own data__.

## Populating with Data

While you might be lucky enough to have purely numerical (continuous) data to analyse, frequently it may be fully discrete (such __levels__, __categories__ or __grades__) or a mixture of both types. Building upon the techniques explored in our tutorial on handling [grades]({{ site.baseurl }}{% link _posts/2017-09-15-Grades.md %}), this template sheet can __handle all data types__ (discrete, textual and numerical).

### Conversion Magic!

Sadly not, but __close__! If you are analysing non-numerical data like __UK 1-9 GCSE Grades__ or standard __A-E__ grading scales, you need to tell the sheet a little about the type of data you are using. This is done by creating a _scale_ of all possible values in the column, delineated by '__&#124;__' characters.

U|G|F|E|D|C|B|A|A*||
{:class="center"}

This is done by putting these scales in a [hidden row](https://gsuitetips.com/tips/sheets/hide-rows-and-columns-in-a-google-spreadsheet/) at the top of the _template sheet_. Any column __without__ a scale at the top will be interpreted as a column containing numerical data. If you have data in a column with a scale, the scale __must contain__ all the potential values in the column, otherwise the calculations will fail (e.g. if you are using the grade scale above, don't include a value such as 'Z' that isn't included in your scale).

You can use the example scales (in the __config__ tab of the _template spreadsheet_) or customise your own. In order for the scale to work reliably, make sure it __ends with__ a '__&#124;__' character but doesn't start with one (e.g. D&#124;C&#124;B&#124;A&#124;). You may also choose to use __words__ / __phrases__ in your scale too, which will work perfectly as well.

Needs Improvement|Meets|Exceeds|Outstanding||
{:class="center"}

The various formulas in the _template sheet_ will convert the cell values into numbers before performing calculations on them (such as [average][1], [median][2] and [stdevp][3]), without you needing to do anything else!

### Paste Your Data

There are five main areas of the _template sheet_, which are listed below. To 'clear' the _template sheet_ for first use, select all the cells under the __grey__ and __black__ headed columns, and press delete on your keyboard. All the data will be removed, and calculations will be __reset to blanks__. 

When you paste your own data into the sheet, you should make sure you only paste values (not formats) by using the 'Paste special -> Paste values only' menu command, or press *ctrl-shift-v*{:.kb-shortcut}. By doing this, you won't override any of the existing formats or conditional formats.

- The __section at the top__ (above the coloured row) gives summary information about the data in the columns below. You don't need to touch any of this, apart from the first hidden row, where you should put your scales.
- The columns with __grey headers__ contain __metadata__ about each row, such as the name of person/student and any associated IDs. You don't __have__ to use all of these columns, but you should __paste your class/group list__ in here!
- __Green headers__ are for columns that are blank for your __custom data__ (such as important scores for each individual, or specific academic information such as learning difficulties). Most of these columns are hidden by default, but feel free to unhide them if you need them or hide them all if you don't.
- Calculated columns (__dark red headers__) shouldn't need to be touched at all. All the formulas in here will spring into life when they see some data to process!
- Data columns have __black headers__ and are where you should paste your __results / performance data__ (such as marks, predictions, exam scores etc.). You can rename the headings to whatever you would like (such as 'English', 'Maths', 'January Exam' etc.).

## What else does it do?

Once you have finished pasting your data in the _template sheet_ (into the columns with __black__, __grey__ or __green__ headers), it will generate summary figures for all your data. At the top of each column will be the aggregated statistics for each column, including:

- __Normalised Average__: This is the numerical average (mean) of the column, but normalised by the 'size' of the scale for each column. This means that this value in each column is comparable with the other columns (regardless of how 'large' the scale is for each column). These values are colour coded between red (lowest) and green (highest).
- __Normalised Standard Deviation__: This is a measure of how _varied_ the data is in the column. It is also normalised according to the size of the scale, so should be used to _compare_ different columns of data. A _wide variance_ of data values (e.g. a spread of values from A-E if you are using grades) will show a _higher number_ here, and a _narrow spread_ (e.g. mostly from A-C) will show a _smaller number_. Most people would regard a tighter spread (consistent performance) to be a desirable trait, so larger numbers are coloured red here.
- __Grade__: This is the numerical average _converted_ back into a value from the accompanying column scale. If there is no scale for the column, nothing will be displayed here.

Each row (person) will also have a set of summary figures in the columns with __dark red__ headers. This will include similar an __average__ and __standard deviation__, which are both _normalised_ and coloured in the same way as the column summaries above. There are also:

- __Count__: This is the number of values in each row, which is useful for checking that you have the same amount of data points for each individual.
- __Total__: The numerical total of the values in the row, useful for troubleshooting any unexpected results!
- __Median__: This is the _middle_ value in the data row. It is helpful because it helps describe the 'shape' of the data. If the average is above the median, then the data is skewed towards the higher values (e.g. with a long tail) with the opposite being true if the average is below the median. An average and median that are very similar indicates that the data is __normally distributed__ (e.g. there is approximately the same number of values above and below the median).
- __Rank__: A measure of where each individual falls within the group/cohort based on their average (a lower number means a high performer).
- __Sparkine__: The compact line graph for each row is a visual representation of the data. In the case of subject comparisons, it helps show how 'varied' the data is (like the standard deviation). If you are analysing data over time, then the sparkline will help show progression over this period and it a straightforward way to identify individuals making expected, higher or lower __rates of improvement__.

### Conditional Formatting

The ability to __change the appearance of cells__ according to __rules__ is a powerful tool for quick data analysis. It is important to use it properly though. Simply colouring cells according to their values is often not the best way to proceed (you'll end up with a sea of green or red!). The key is to use format to communicate something that __isn't__ already conveyed by the value.

In the case of our _template sheet_, indicating whether a value is high or low with colour (over the whole cohort) __isn't much use__, as it will merely highlight lower-performing individuals (which is already done by the average column and the rank). It is duplicate information and a waste of our precious bandwidth!

We need something we can __visualise__ and then __action__, so the _template sheet_ highlights (in red/green) especially low or high values __for each row__. Our approach immediately shows skills or subjects need attention for __each individual__.

The template achieves this by comparing the value in each cell to the average for each individual and highlighting it if it is a certain number of standard deviations away from that average. By default, any value that is more than __1.4__ standard deviations from the average will be highlighted (although this can be altered as required).

## Customising

The _template sheet_ will work straight away, for a large number of rows and columns, so you shouldn't need to do any further customisation work! If you need to add additional rows, you will need to copy down the formulas in the __dark red__ columns. Add extra columns to the right of the last data column (e.g. before the blank end column). Conditional formats should _automatically_ adjust to include the extra cells.

### Rounding Precision

By default, the output summary values are rounded to two decimal places of precision. This can easily be adjusted on the 'config' tab, although it is worth considering how precise your source data is before setting this too high.

### Trigger Levels

These are set in the last hidden row at the top of the _template sheet_ and labelled __high__ (this is for green) and __low__ (this is for red). If you find you have too many value cells (in the __black headed__ columns) being formatted in a particular colour, slightly increase the appropriate value here. If the opposite is true (too few cells being highlighted) then gradually reduce it until the right number are coloured! The '__right number__' is up to you, and specific to what you want to achieve. Most people will only want to have a few cells highlighted in each row so that they can target the most important weaknesses or celebrate the clearest strengths. It's not an absolute; it's just an indicator of where best to target your efforts, in other words, it is the product of __analysis__.

  [1]: https://support.google.com/docs/answer/3093615 "How to use the AVERAGE function"
  [2]: https://support.google.com/docs/answer/3094025 "How to use the MEDIAN function"
  [3]: https://support.google.com/docs/answer/3094105 "How to use the STDEV function"