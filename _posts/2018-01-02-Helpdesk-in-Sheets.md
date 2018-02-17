---
title: Running a Simple Helpdesk with Google Sheets
short_title: Helpdesk System in Sheets
layout: post
author:
  name: jd
category: coding
tags:
- sheet
- google
- example
published: true
lead: Create a simple __helpdesk__ and __request ticketing__ solution with just forms and sheets.
asset_prefix: sw23W
example: https://docs.google.com/spreadsheets/d/1hheJ4nIUyiGADCcYr6f0bBRw6R362QwmMB4a5EMZVEo/copy
---
{% include lead.md %}

Helpdesk management systems are common, but sometimes you just need something __simple__ and __easy__ to keep track of incoming issues and requests. The sheet below gives you this functionality within a __single spreadsheet__, out of the box. You can create your __own form__ for your users to submit their issues, and connect it up __straightaway__. __No__ formulas nor coding needed.

[![Example Helpdesk Sheet]({{ site.baseurl }}/assets/{{ page.asset_prefix }}_screen.png){:class="img-fluid"}]({{ page.example }}){:target="_blank" rel="noopener"}

## Configuration

The sheet above is provided with example data so that you can explore it straightaway. With some simple configuration (explained in the __CONFIG__ tab, you can link it up to your form responses). Remember to click the '__Allow Access__' buttons in the __TEST__ column of the __CONFIG__ tab once you entered in the URL of the sheet you want to link to (cell __B3__). This creates the [import range]({{ site.baseurl }}{% link _snippets/google_sheet_importrange.md %}) link that allows issues data to be imported dynamically.

You should include a field to indicate the __type__ of request/issue received. If you name this something other than __Type__, update the configuration in the _TYPE_FIELD_ row to ensure that everything works correctly.

## Mechanism

Spreadsheets are excellent for data analysis but are __harder__ to use for structured data input (forms) or management. In this tool, a sidebar is used to handle data selection and input. Click on the __Tracker__ menu, then __Show__ to display it.

Each issue is assigned a __code__ to help track it, and any log entries associated with it. This code is a __hash__ of the _submitting user_ and _submitting timestamp_. They _should_ be unique for our purposes.

## Usage

After displaying the __sidebar__, position your cursor on the issue row (on the __HELPDESK__ tab) that you wish to comment on or manage. Click the __Select__ button on the sidebar, which will then display the __code__ and __status__ of the selected issue. Fill in the form with the details you wish to log about the issue and click __Log__ to complete the process. The issue row will be updated, and your logged data will appear in the __LOG__ tab. If you mark the issue as __complete__, it will no longer be shown unless you set the __status filter__ to __ALL__.