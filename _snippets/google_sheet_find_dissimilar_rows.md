---
label: snippets
layout: post
title: How to identify dissimilar duplicate rows in sheets
short_title: __Identifying__ dissimilar duplicates
author:
  name: jd
tags:
- google
- sheet
- markbook
category: tutorial
lead: How to __identify__ duplicate rows in a sheet that have dissimilar values, such as multiple grades for the same student in the same subject from different teachers.
published: true
date: 2018-02-15
---
{% include lead.md %}

### Introduction

You might encounter a situation where you have duplicate data rows that you need to identify and deal with. This commonly occurs during __data collection cycles__, where multiple people might erroneously enter data about the same 'thing'. Grades for students in a particular subject is a classic example.

Having realised that you have these __pseudo-duplicates__, where the majority of the row is the same but just one column/cell might be different, how do you use formulas to show you which duplicate rows need your attention automatically?

### Sorting to the rescue

It's not as difficult as it might initially seem. Consider the rows below, which is a simplified version of what you might face.

|---
| Student | Name | Subject | Skill | Grade
|:-|:-|:-|:-|:-
| 1001 | Ann Q. Pace | English | Reading | B
| 1001 | Ann Q. Pace | Maths | Numeracy | B
| 1001 | Ann Q. Pace | English | Reading | A
| 1002 | Bernard A. Hanson | English | Reading | C
| 1003 | Adrienne Erickson | English | Reading | A+
| 1002 | Bernard A. Hanson | Maths | Numeracy | B
| 1004 | Hakeem Faulkner | Maths | Numeracy | E
| 1004 | Hakeem Faulkner | English | Reading | C
| 1004 | Hakeem Faulkner | English | Reading | C-
| 1003 | Adrienne Erickson | Maths | Numeracy | D

Of course, with such a __small number of rows__, it's easy to identify the two pairs of pseudo-duplicate entries (Rows 1 & 3, 8 & 9). But imagine if this dataset was for 200 students, with ten subjects and four skills in each subject. That's __8,000 rows__ already, which is __too many__ to scan manually and accurately.

The first task is to ensure our data is sorted suitably. We need to order the data by __student__, then __subject__ and finally __skill__ (in that precedence). The data in the above it _almost_ sorted, with just a few minor adjustments needed.

|---
| Student | Name | Subject | Skill | Grade
|:-|:-|:-|:-|:-
| 1001 | Ann Q. Pace | English | Reading | B
| 1001 | Ann Q. Pace | English | Reading | A
| 1001 | Ann Q. Pace | Maths | Numeracy | B
| 1002 | Bernard A. Hanson | English | Reading | C
| 1002 | Bernard A. Hanson | Maths | Numeracy | B
| 1003 | Adrienne Erickson | English | Reading | A+
| 1003 | Adrienne Erickson | Maths | Numeracy | D
| 1004 | Hakeem Faulkner | English | Reading | C
| 1004 | Hakeem Faulkner | English | Reading | C-
| 1004 | Hakeem Faulkner | Maths | Numeracy | E

Once the data has sorted correctly, we can use two comparison formulas to identify which rows are about the same student/subject/skill, and which have dissimilar grades.

### Concatenating Keys

To compare our rows, we need to reduce them to two [keys]({{ site.baseurl }}{% link _snippets/google_sheet_duplicates.md %}). The first needs to concatenate the student, subject and skill, and the second adds the grade to this mix.

{% highlight puppet %}
CONCATENATE(A2,"_",C2,"_",D2)
{% endhighlight %}{:class="formula"}

{% highlight puppet %}
CONCATENATE(A2,"_",C2,"_",D2,"_",E2)
{% endhighlight %}{:class="formula"}

To work out whether the current row is similar (same student, subject and skill) to the previous one, we need to compare the first of these keys. To work out if it has a different grade, we need to compare the second key to the previous row.

{% highlight puppet %}
IF(CONCATENATE(A2,"_",C2,"_",D2)=CONCATENATE(A3,"_",C3,"_",D3),TRUE,FALSE)
{% endhighlight %}{:class="formula"}

{% highlight puppet %}
IF(CONCATENATE(A2,"_",C2,"_",D2,"_",E2)=CONCATENATE(A3,"_",C3,"_",D3,"_",E3),TRUE,FALSE)
{% endhighlight %}{:class="formula"}

A duplicate row would have a **true** value for the first comparison (it is similar to the row before) and a **false** value for the second (the grade is not the same).

### Single Formula Solution

We can build a conditional statement to test this, which will show **true** if the row is a pseudo-duplicate (different grade) of the previous one. The formula can be simplified by just comparing the grade as the second part of the conditional test.

{% highlight puppet %}
IF(AND(IF(CONCATENATE(A2,"_",C2,"_",D2)=CONCATENATE(A3,"_",C3,"_",D3),TRUE,FALSE)=TRUE, IF(E2=E3,TRUE,FALSE)=FALSE), TRUE,)
{% endhighlight %}{:class="formula"}

This outputs the following, correctly identifying the rows which are similar to the previous ones (apart from the grade). The sorts we implemented ensures that all the duplicates will be found.

|---
| Student | Name | Subject | Skill | Grade | Duplicate
|:-|:-|:-|:-|:-
| 1001 | Ann Q. Pace | English | Reading | B |
| 1001 | Ann Q. Pace | English | Reading | A | TRUE
| 1001 | Ann Q. Pace | Maths | Numeracy | B |
| 1002 | Bernard A. Hanson | English | Reading | C |
| 1002 | Bernard A. Hanson | Maths | Numeracy | B |
| 1003 | Adrienne Erickson | English | Reading | A+ |
| 1003 | Adrienne Erickson | Maths | Numeracy | D |
| 1004 | Hakeem Faulkner | English | Reading | C |
| 1004 | Hakeem Faulkner | English | Reading | C- | TRUE
| 1004 | Hakeem Faulkner | Maths | Numeracy | E |