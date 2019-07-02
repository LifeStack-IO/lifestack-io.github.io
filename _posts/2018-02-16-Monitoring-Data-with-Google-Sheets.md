---
title: Monitoring Data with Google Sheets
short_title: Monitoring Data
layout: post
author:
  name: jd
category: tutorial
tags:
- sheet
- google
- example
published: true
lead: Easily monitor data collected weekly, with formatting to highlight __missing__ & __notable__ values.
asset_prefix: ki8Up
example: https://docs.google.com/spreadsheets/d/1aGo37Si2_YHmQntj4Q3fzFUtReQli-zNkjdPFICjFcg/copy
---
{% include lead.md %}

If you collect data __regularly__ (from a Google form, or perhaps another system) then being able to monitor that data quickly is an indispensable tool to make your task a __little easier__. The sheet linked below is an __ideal__ place to start, and you can customise it to meet your needs.

[![Example Monitoring Sheet]({{ site.baseurl }}/assets/{{ page.asset_prefix }}_screen.png){:class="img-fluid"}]({{ page.example }}){:target="_blank" rel="noopener"}

## Structure

The example sheet itself is split into three tabs. The '__DATA__' tab contains randomly [generated test data](https://www.generatedata.com/){:target="_blank" rel="noopener"}), but you can replace this with your own data (or have your form store response data here). The '__Monitoring__' tab contains information derived completely from the other tab. Finally, the '__CONFIG__' tab allows you to customise the monitoring sheet without having to update any formulas.

## Features

### Auto-Populating Headers

The names on the left-hand-side are __automatically pulled__ from the data tab itself. Likewise, the week numbers (and associated start & end dates for these weeks) are also __drawn dynamically __ from the data. This saves you the __hassle__ of having to pre-populate these column headers. You can re-use these monitoring sheets every year, and the dates will stay current. Week numbers starting from the first date in your dataset (e.g. the first week of a school term) are particularly useful for __keeping track__ as the year progresses.

### Summary Counts

Each column (__week__) and row (__person__) has a summary count, which is also __conditionally formatted__ using a simple scale to give you low (red) and high (green) numbers. These are calculated slightly differently to help you. Imagine you ask each person to fill in their reflections from each week. Most people will do this per-week, but sometimes they might forget, or circumstances may force them to write two in the same week (even though they are reflecting on different weeks). The values in the cells will reflect this (this is a count of how many rows contain their name and fall within the week specified). The __row__ count (to the right of the name) counts the total number of rows for that person (so you can monitor that each person is submitting the correct number of times). The __column__ count counts the number of people who have rows that fall within that week. This should equal a maximum of the total number of people in your data. The count allows you to __quickly check__ that you are receiving the __correct number__ of responses _per week_. It is not the total responses for the week, as this may be misleadingly high if individuals submitted more that one response/row.

### Discriminator Values

The monitoring values also include suffixed discriminators (by default a '+' sign) to indicate that at least one of the values in that week meets the conditions specified in the discriminator query. By default (and by example) this is that the value in the __C__ column of the data must be __TRUE__ and the value in the __D__ column greater than __8__. Conditional formatting will pick up this value and highlight it in bold.

## Customising

You can easily customise the way in which the monitoring works by editing the values in the __CONFIG__ tab. If your data has the date in column __D__ (rather than the __B__ column in the example data) then just update the '_Date Column_' value to reflect this. If you would like to __update__ (or remove) the highlighted discriminator values, then you can change this here as well. All the details of each configuration option are provided in this tab.

__Happy Monitoring!__