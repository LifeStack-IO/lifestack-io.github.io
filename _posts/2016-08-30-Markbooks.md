---
title: Markbooks with Google Sheets
layout: post
author:
  name: jd
category: tutorial
tags:
- education
- google
- markbook
published: true
lead: A start of term chore, but also an opportunity to brush up on your spreadsheet & data-handling skills to make the rest of the year easier and more productive!
asset_prefix: erf54
---
{% include lead.md %}

## Why?

Taking a little time to set up a [sheets-based][1]{:target="_new"} markbook at the start of the year will pay dividends in terms of __productivity__, __organisation__ and __time-saving__ through the year (especially when it comes to reporting deadlines!). Few people would doubt the importance of using a markbook to track student progress, but a well structured and organised spreadsheet will just make this _traditional tool_ much more powerful and easier to keep updated.

## Setting it up

![Example Layout]({{ site.baseurl }}assets/{{ page.asset_prefix }}_layout.svg)

If you would like to keep things simple, you should probably opt for just a __single spreadsheet__[^spreadsheet] with a tab / individual sheet[^sheet] for each group that you teach during the year. If you have a lot of classes, need to share some class marks (but not all of them) with other teachers, or more complex needs (such as extra tabs for analysis etc.) then by all means use multiple spreadsheets. It doesn't make too much difference from a technological point of view, it simply comes down to what __suits you best__.

Don't worry too much about this at the moment, as it's fairly trivial to consolidate multiple spreadsheets into a single spreadsheet, or split a single spreadsheet into one for each class. For most people, a single spreadsheet to act as your markbook for the year should be more than sufficient.

### Creating the sheet

To kick off the process, you'll need to [create][2] a new spreadsheet in your Google Drive. As with all documents that you might end up sharing, you should name it appropriately. If you were to name it 'Markbook' or even 'My Markbook - Academic Year xxxx' then that will mean something to you (e.g. it's in your drive, and you know who __me__ is) but if you share it with others in your school / organisation then you're making life harder for them! They will end up with lots of spreadsheets shared with them, all called '__Markbook__'. This will force them to check the owner each time they want to find a particular group / teacher. Instead, make sure you include some contextual details (e.g. your name or teacher/staff 'code' if you use one). A good naming convention might be '__Markbook - Year xx-xx - CODE / NAME__'.

Once you have a named, blank markbook in front of you, create and name sheets / tabs for each class you'll be teaching during the year. If possible, [rename][3] these sheets to __match__ the class or group codes you use across your school. For example, using a name like 'My Year 11s' may mean something to you, it's likely not to be very helpful to others who don't necessarily know that whilst you are a Biology teacher, you also only teach Chemistry to Year 11. Using the standardised codes (such as 11Chem-1 or 11CH1) that everyone in your organisation would __recognise__ and __understand__ makes for happier colleagues and fewer mistakes! Furthermore, if you use the same codes that are used in your MIS or timetable it makes automated extraction or submission of data for reporting much quicker and easier for you as well.

### Adding the columns

You will need two types of columns in your markbook, the first are for information about the __students__ (e.g. name, identifier, email, previous attainment or 'working at' level etc.). The second are for __assignments__ or __assessments__ about which you wish to collect marks or grades. It is a good idea to use two or three rows for your column headers, as this gives you the opportunity to add extra 'meta' information about each assignment. This meta information might be the maximum mark for that piece of work, which is useful for calculation percentages automatically or the date due, which means you can easily highlight/color cells with missing marks once that date has passed.

###### Student information

For the student information, three columns should be considered the absolute minimum. You will need (normally your _first column_) a __unique identifier__ for the student to help facilitate submission or aggregation of marks in the future (students may share the same name). Different organisations may call this identifier by a different label (Student Id, Student Number, Enrolment or Admission Number etc.) but it should be widely recognisable and understood within the organisation.

When choosing which identifier to use, you __should not use__ identifiers that are considered _privileged_ or _sensitive_ information (typically those that have a national meaning, such as a [UPN][4]{:target="_new"} in the UK) and make sure that identifier is one that has been generated and assigned by your organisation. Not only does this mean that unwelcome changes are unlikely, but also it will facilitate easier information movement around your systems.

Some people prefer to [concatenate][5] names into a single column (e.g. John Doe, or Doe, Jane) rather than having an individual columns for their family and given names. This comes down to __personal preference__, and whether you wish to be able to sort on individual 'parts' of the name. Remember that in sheets you can sort on any column you wish (and change it whenever you would like), so you can order your markbook by _name_, _attainment_ or even _seating position_.

Finally, you should also try to include a column for student __email address__ / google apps username. This will make integrating your markbook with [Google Classroom][6] and automatically sharing progress with students much easier. Depending on the environment in which you teach, you may wish to include columns for previous attainment, seating position, preferred nomenclature, or further information that you feel is useful. You should also try to [freeze][7] the columns referring to the student so that they remain __always visible__ whilst you are scrolling through the assignment columns.

If you appreciate a well-formatted and visually neat markbook, and you are using multiple rows for your headings (see below) you can [merge][8] the student column headings into a single cell. Then you can [vertically align][9] the cell text to the top, middle or bottom depending upon how you prefer it.

![Example Merge]({{ site.baseurl }}assets/{{ page.asset_prefix }}_merge.svg)

###### Assignment information

Depending upon how you choose to mark/grade assignments or tasks, you may need __one__ or __two__ columns for each piece of work for which you would like to record data. If possible, you should try to stick to a __single column__, although there are some cases (where you need to display a percentage from a raw mark) where you will need two.

In the top cell of your assignment, you should put the __title of the assignment__, followed by the date due (if required) and the maximum mark (if numerically graded) in the cells below this. If you would like to add further notes about the assignment (for yourself) you are best served adding a [note][10] to the cell, rather than an extra row. If you do this, and you can keep the title as short as possible (enabling text-wrapping within the cell should help too) you can minimise the width of the column. Narrower columns means it is easier to see more data (e.g. which helps_ contextualise information_ & _identify trends_ or concerns) on a single screen.

## Adding your data

At this point you're ready to add your class lists, which can be done in a number of ways.

If you have easy access to your MIS or school database, the most simple way to import your classes is to __copy__ and __paste__ from there. If you are able to access a webpage with the student list for your particular class, all you need to do is highlight the data, then copy it *ctrl-c*{:.kb-shortcut}. Then return to your sheet and paste it *ctrl-v*{:.kb-shortcut}. You can remove any unwanted formatting or borders using the format tools in the toolbar at the top of the sheet. Whilst this method is both quick and easy, the main drawback is that the imported data is static. When it changes in your MIS (names or attainment grades updated) these changes are not reflected in your markbook.

As an alternative, some organisations may provide a __master sheet__ with all the class or student data in an accessible format. If this is the case in your school, you can use a number of different [functions][13]{:target="_new"} to access and use this data. You will first need to ask for the _spreadsheet id_ and sheet name of the data spreadsheet in order to use it. Your support team or data manager should be able to supply this. The master spreadsheet is simply a normal spreadsheet that all your staff will have 'read' access to. A simplified version of this master data might look something like this:

|---
| Id | Given Name | Family Name | Class
|:-|:-|:-|:-
| 1000 | John | Doe | 11EN
| 1001 | Jane | Doe | 11EN
| 1002 | A | Person | 11EN
| 1003 | Another | Person | 11EN

You can then [import][14]{:target="_new"} the list of students for a particular class by entering the following formula. You will need to replace the __placeholders__ with your supplied ID and sheet name. The first time you use the [importrange][14]{:target="_new"} function you will need to authorise access to the sheet from which you are importing the data. You can do this by clicking on the button that will appear when you hover over the cell.

{% highlight puppet %}
QUERY(IMPORTRANGE("SPREADSHEET_ID", "SHEET_NAME!A:D"), "select * where Col4 = '11EN'")
{% endhighlight %}{:class="formula"}

The formula above consists of __two__ individual functions combined together (the result of the first function is fed, or piped, into the second). The first (inner) function _imports_ the data from the master sheet. The second (outer) function _filters_ it using a query to extract only the relevant rows. The [query][16] function allows you to filter the imported data using various conditions. In this case, we are looking for all the rows where Column 4 (Class) matches 11EN. You can also sort the imported data directly by including an [order by][15] clause. The formula below will sort first by Column 3 (Family Name) then by Column 2 (Given Name) if more that one student shares the same value in the primary sort column.

{% highlight puppet %}
QUERY(IMPORTRANGE("SPREADSHEET_ID", "SHEET_NAME!A:D"),
  "select * where Col4 = '11EN' order by Col3, Col2")
{% endhighlight %}{:class="formula"}

Whilst this method is _great_ because you don't need to worry about keeping your markbook current with changes in names and classes (this is all done in the master sheet), there is an important word of __warning__ if you are using this method. Whilst the formula name includes the word __import__, what is really means is __link__. If the source data changes, then you markbook will change too. This isn't a problem if new data is only added to the end of the master sheet, or informal names change slightly, but if it is appended in the middle (e.g. when a new student joins your class mid-way through the year), then you will end up with a extra row too. This will mean that marks assigned to that student (e.g. that row) will now appear to belong to someone else. The same problem can occur when a student leaves a class and their row is deleted from the master sheet. Down this particular road, terrible data-handling mistakes lurk!

![Example Mismatch]({{ site.baseurl }}assets/{{ page.asset_prefix }}_mismatch.svg)

This is a common problem in spreadsheet markbooks, and often happens when data is carelessly sorted or filtered (one column is re-ordered but _not_ all the others!). Of course, Google Sheets helps us by normally expanding our [sorts][17] to include all columns, and by providing the ability to [roll-back][18] to a previous version of the sheet if we get into a jumble - but mistakes do still happen and, even worse, __remain unnoticed__.

You can avoid this problem in different ways. Firstly, you could ask for _joined_ and _left_ columns to be added to the master spreadsheet. This would be used to track when a student joined or left a particular class, and would mean the data looks something like this:

|---
| Id | Given Name | Family Name | Class | Joined | Left
|:-|:-|:-|:-
| 1000 | John | Doe | 11EN | 05/09/2016
| 1001 | Jane | Doe | 11EN | 05/09/2016 | 09/09/2016
| 1002 | A | Person | 11EN | 07/09/2016
| 1003 | Another | Person | 11EN | 05/09/2016

Then, if you sorted by the joining date (Column 5) in your query function, new students will always __appear at the end__ of your list (rather than in the middle, which causes the re-ordering problem). If student rows are not deleted from the master sheet, but merely have a leaving date appended, they won't disappear from your markbook either. You can use the presence of a leaving date to trigger a conditional format in order to 'grey' out the row in your markbook. This will preserve the data for you, but minimise its presence as it is no longer as important. Your formula and resulting data would look something like:

{% highlight puppet %}
QUERY(IMPORTRANGE("SPREADSHEET_ID", "SHEET_NAME!A:F"),
  "select Col1, Col2, Col3, Col6 where Col4 = '11EN' order by Col5, Col3, Col2")
{% endhighlight %}{:class="formula"}

|---
| Id | Given Name | Family Name | Left
|:-|:-|:-|:-
| 1001 | Jane | Doe | 09/09/2016
| 1000 | John | Doe
| 1003 | Another | Person
| 1002 | A | Person

Alternatively, if adding the requisite columns __isn't possible__ or desirable, you could join the _static importing_ and _dynamic linking_ model together by pasting a list of student identifiers into your markbook and using sheets to do the heavy lifting, by looking up their details from a master sheet. Firstly, get a list of student identifiers using either of the methods above. If you are grabbing them from a master spreadsheet, import them into a temporary sheet, then _copy_ just the identifiers and _paste values_ *ctrl+shift+v*{:.kb-shortcut} into your markbook. Then you can use the following formula in the next column to the identifier to grab the matching student details from the master sheet. This formula assumes that your starting row number for your student identifiers is '4', if it isn't you will need to adjust the final part of the formula (A4) accordingly.

{% highlight puppet %}
QUERY(IMPORTRANGE("SPREADSHEET_ID", "SHEET_NAME!A:F"),
  CONCAT("select Col2, Col3, Col6 where Col1=", A4))
{% endhighlight %}{:class="formula"}

Once you have added this formula to your first row of the student data, and it is working as expected, you can use a [drag-down fill][19] to replicate it to each row. The keyboard shortcut for doing this is to select the whole range you want to fill (every cell in the column next to your identifier) and press *ctrl-d*{:.kb-shortcut} (fill down). Using this _hybrid_ method you can ensure your student details stay accurate but also control when you add / remove students from your markbook. _Surely the __best__ of the both worlds_?

### Privacy Considerations

Whilst not a __public__ document, a markbook will typically be used in a virtually public environments; the classroom, in front of parents/guardians, a departmental or moderation meeting. In all these settings, many eyes will see the information it contains. You should therefore be careful about what [personal][11] or [sensitive personal][12] data you retain in your markbook.

Any data that you choose to include and store about a student should be relevant, useful and help you in the classroom on a day-to-day basis. Medical histories and extensive lists of special education needs should not be included, although you might choose to include a hyperlink to a __secure__ page (password / credential protected) on your MIS / Intranet where that information can be found. Data that changes without your knowledge (such as contact details) should also not be included, as you may be relying on out-of-date information.

If you choose to include information about a student that could be deemed sensitive (such as particular educational needs or medical conditions) it is better done in terms of _strategies_, such as: _may need to sit close to the front of the room_. This ensures you are __aware__ but without going into any specifics about the _why_. Always consider whether you would be professionally comfortable for a student or parent reading this information over your shoulder before including it.

## Using it

If you are a [Google Classroom][25]__ devotee__, then you will likely be creating, managing and marking assignments with Classroom. Classroom gives you two mechanisms to extract the marks / grades you enter. For the technologically confident, you can use the [Classroom API][26] and a little bit of [Google Apps Script][27] to import the most current results straight into your markbook every time you open it (see the [snippets](/snippets) section of this site for further information). Alternatively, you can [export][28] all the current data from a class into a google sheet using the _Student Work_ section of the class page (the same page where you return work from).

Currently, every time you export to Google sheets, it will create a new spreadsheet. This means you'll need to copy and paste all the data from this sheet into your markbook. The __easiest way__ to do this at the moment is to create a new sheet in your markbook for each class you have in your markbook, and also have in Classroom. From our earlier example, if you are creating a markbook for a class called '11CH', and are also using Classroom to mark assignments, you should create a new sheet in your markbook called '11CH Classroom' or something similar.

When you have done this, and every time you export your grades, make sure you have highlighted a cell inside your Classroom export sheet (just click anywhere) and select everything *ctrl-a*{:.kb-shortcut}. Then copy this selected data *ctrl-c*{:.kb-shortcut} and return to your newly created 'xxx Classroom' sheet. Here, select the top left cell (A1) and paste the current data *ctrl-v*{:.kb-shortcut}. This will take a moment or two to import, but then you will have all the current data in your markbook. Unfortunately it is not yet in your __main__ markbook for that class. For this you will need to use the _wizardry_ of the formula below, copied into each cell where you would like the mark to magically appear.

{% highlight puppet %}
IFERROR(INDIRECT(ADDRESS(MATCH(INDIRECT(ADDRESS(ROW(), 5)), 'xxxxx Classroom'!$C:$C, 0),
  MATCH(INDIRECT(ADDRESS(1, COLUMN())), 'xxxxx Classroom'!$2:$2, 0),,, "xxxxx Classroom")), "")
{% endhighlight %}{:class="formula"}

This formula, whilst it looks complex, is in fact quite simple to use. All you need to do is name the assignment in your markbook exactly the same as the name of it in Classroom (case-sensitive). Then replace the three instances of 'xxxxx Classroom' with the name of your Classroom sheet in your markbook and also change the '5' to match the column number where you have your student email address (it will need these to match the ones in Classroom). In this case these are in the 5th column of the markbook (Column E). Also change the '1' to match the row where you have put your assignment titles in your markbook (for most people this will be the first row, so you can leave it as one). You can copy and paste this formula, or _drag-fill_ it across rows or down columns. It'll __work__ every time. When you paste in new data from Classroom, everything will update neatly, even if you've remarked an existing assignment.

### Formulae

Percentages can be __easily calculated__ by adding a column to the right of your assignment column (the easiest way to do this is by clicking on the small downward pointing arrow in the column letter header, then selecting 'Insert 1 right'). You can then add a formula to calculate the percentage by dividing the mark awarded by the maximum mark in the assignment column header. You should use the '__$__' [notation][31] in your formula to _lock_ the maximum mark reference (e.g. =E4/E$2). By doing this, when you fill or move the formula it will continue to divide by the maximum mark.

### Analysis

Once you have collected a non-trivial amount of data into your markbook, you can start to use it for analytical purposes. These will often take the form of questions, such as:

* What is the __attainment__ of each student and how has it __changed__ over time?
* How does the attainment of each student __compare__ to a __predicted__ value ([value added][23])?
* Which students are above, or below, the [__arithmetic mean__][22](commonly known as the _average_) of the class?
* Who are the __outliers__? Those students whose attainment falls above or below _two [standard deviations][24]_ from the mean.

Many of the tools available in a spreadsheet can help you visualise and summarise data in order to answer these questions. None of the tools have much value __unless__ you have a question you are looking to answer. The collection and interpretation of data is useless unless it is put into the service of answering specific questions. 

###### Conditional Formatting 

You are able to add another dimension of data display by highlighting individual cells (marks), rows (students) or columns (assignments) in your markbook using conditional formatting rules. These rules allow you to mark selections according to pre-programmed rules or write your own selection formulas. Ranges that match those criteria can then be formatted by changing background or text colours to draw attention to them. This will then give you an instant visual _clue_ to help answer the types of questions posed above, an information _dashboard_ formed from your class assessment data.

A sophisticated use of this might be to highlight missing marks (where there is no cell value), or those marks which are particularly high or particularly low. You can even set colours to band attainment (low, medium, high). Using highlighting colour in your markbook is an excellent way to convey further information about the values you see. It should __never__, __ever__ be used as a way of 'storing' information, such as colouring a cell yellow to indicate that a student was absent for that assignment. It is much better to insert the word 'absent' and use conditional formatting to highlight all cells displaying that value in yellow. Why? Words are much less ambiguous that colours and meaning is therefore rarely lost or misinterpreted.

###### Sparklines

First codified by [Edward Tufte][20], [sparklines][21] provide an excellent and compact mechanism to visualise a series of complex data points in the space of a single cell. A simple example is provided below (Example 1), showing all data from the second row of a sheet, from columns 5 to 9 (E2:I2).

{% highlight puppet %}
SPARKLINE(E2:I2, {"charttype","column";"max",100})
{% endhighlight %}{:class="formula"}

You can also use the built-in [sparkline command][29] to create more complex sparklines for a range / set of data (e.g. marks for a student over time). For example, you might wish to use a columnar sparkline to visualise this data, with the highest / lowest marks highlighted in particular colours (such as red & green).

![Example Sparklines]({{ site.baseurl }}assets/{{ page.asset_prefix }}_sparklines.svg)

The formula below (Example 2) is for the same range of data, but includes highlight colours and also dynamically sets the minimum and maximum extents of the y-axis (the vertical, value axis) to the min / max mark in your markbook for this class. This helps keep all the axis for each sparkline the same, allowing for a simple visual comparison __between__ students. If you are more concerned with the performance of an individual over time then you can let the formula choose axis extents for you, to give the greatest level of detail.

{% highlight puppet %}
SPARKLINE(E2:I2, {"charttype", "column"; "axis", true; "lowcolor", "red"; "highcolor", "green"; "ymin", MIN($E$2:$I); "ymax", MAX($E$2:$I)})
{% endhighlight %}{:class="formula"}

Taking this particular sparkline further, we can combine it with an [arrayformula function][30] to plot deviation of marks from a class average over time (anything green above the horizontal axis has beaten the average, anything red is below the average) as show below (Example 3).

{% highlight puppet %}
SPARKLINE(ARRAYFORMULA(E2:I2-AVERAGE(E:I)), {"charttype", "column"; "axis", true; "negcolor", "red"; "color", "green"; "ymin", MIN(ARRAYFORMULA($E:$I-AVERAGE($E:$I))); "ymax", MAX(ARRAYFORMULA($E:$I-AVERAGE($E:$I)))})
{% endhighlight %}{:class="formula"}

To use these examples, simply adjust the ranges to encompass the data you with to visualise.

*[MIS]: Management Information System (or school database)
*[ID]: Identifier, normally unique

[^spreadsheet]: This refers to the entire Google Spreadsheet (e.g. the 'file' in your Google Drive). This is the equivalent of a '_workbook_' in Excel parlance.
[^sheet]: A spreadsheet can contain multiple sheets arranged as tabs at the bottom. It's easy to reference data in each of these sheets using formulas or add-ons. In Excel, you would call this a '_worksheet_'

  [1]: https://www.google.co.uk/sheets/about/
  [2]: https://support.google.com/docs/answer/49114?hl=en
  [3]: https://support.google.com/docs/answer/180897?hl=en
  [4]: https://nationalpupildatabase.wikispaces.com/IDs#toc1
  [5]: https://en.wikipedia.org/wiki/Concatenation
  [6]: https://support.google.com/edu/classroom/answer/6020294
  [7]: https://support.google.com/docs/answer/54813?hl=en
  [8]: https://support.google.com/docs/answer/141104?hl=en
  [9]: http://www.gcflearnfree.org/googlespreadsheets/formatting-cells/2/
  [10]: https://www.shorttutorials.com/google-docs-spreadsheet/insert-note.html
  [11]: https://en.wikipedia.org/wiki/Personally_identifiable_information
  [12]: https://ico.org.uk/for-organisations/guide-to-data-protection/key-definitions/
  [13]: https://support.google.com/docs/table/25273?hl=en
  [14]: https://support.google.com/docs/answer/3093340
  [15]: https://developers.google.com/chart/interactive/docs/querylanguage#Order_By
  [16]: https://support.google.com/docs/answer/3093343
  [17]: https://www.youtube.com/watch?v=3OcDd55JJXQ
  [18]: https://support.google.com/docs/answer/190843?hl=en
  [19]: http://www.howtogeek.com/howto/15799/how-to-use-autofill-on-a-google-docs-spreadsheet-quick-tips/
  [20]: http://www.edwardtufte.com/bboard/q-and-a-fetch-msg?msg_id=0001OR
  [21]: https://en.wikipedia.org/wiki/Sparkline
  [22]: https://en.wikipedia.org/wiki/Average#Arithmetic_mean
  [23]: http://www.education.gov.uk/schools/performance/archive/schools_04/sec3b.shtml
  [24]: https://en.wikipedia.org/wiki/Standard_deviation
  [25]: https://classroom.google.com
  [26]: https://developers.google.com/classroom/
  [27]: https://developers.google.com/apps-script/
  [28]: https://support.google.com/edu/classroom/answer/6020294
  [29]: https://support.google.com/docs/answer/3093289
  [30]: https://support.google.com/docs/answer/3093275
  [31]: http://web.pdx.edu/~stipakb/CellRefs.htm