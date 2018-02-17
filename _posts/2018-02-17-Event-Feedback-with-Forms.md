---
title: Analysing Event Feedback with Forms & Sheets
short_title: Event Feedback with Forms
layout: post
author:
  name: jd
category: tutorial
tags:
- sheet
- google
- example
published: true
lead: __Dynamically__ and __professionally__ handle your event feedback, gathered with a google form, analysed with sheets.
asset_prefix: ca1VD
example: https://docs.google.com/spreadsheets/d/1aUj-4ahcHzaTAiZLq9Mhlt4JbeOvSv8ZnrfclHpZjV8/copy
---
{% include lead.md %}

Forms are an __excellent__ way to gather feedback from regular events or training sessions. If you can structure your response form to be __generic__, you can re-use the same form each week and __analyse the data quickly__ using the sheet below. This __avoids the tiresome job__ of generating, managing, tracking and evaluation form after form after form!

[![Example Analysis Sheet]({{ site.baseurl }}/assets/{{ page.asset_prefix }}_screen.png){:class="img-fluid"}]({{ page.example }}){:target="_blank" rel="noopener"}

## Form

A generic form is an excellent way to collect feedback. Structure it to ask questions that are __relevant to all sessions__, so that they produce __comparable data__. Questions about the quality of materials, delivery and content as a good way to go. If you need to gather more qualitative feedback, include specific questions inviting comments at the end of the form.

Make sure you also include a question relating to the session/event about which you are gathering data. We'll use this field, when sending out the form to your [users][1] (perhaps using our simple [bulk email tool]({{ site.baseurl }}{% link _posts/2017-12-14-Bulk-Emailing-from-Google-Sheets.md %})?) with a [pre-filled question][2].

## Configuration

The sheet above is provided with example data so that you can explore it straightaway. With some simple configuration (explained in the __CONFIG__ tab, you can link it up to your form responses). Remember to click the '__Allow Access__' buttons in the __TEST__ column of the __CONFIG__ tab once you entered in the URL of the sheet you want to link to (cell __B3__). This creates the [import range]({{ site.baseurl }}{% link _snippets/google_sheet_importrange.md %}) link that allows data to be analysed dynamically.

To ensure your users evaluate the correct sessions, you should send out pre-filled URLs. Follow [instructions][2] from the web to extract the __ID__ of the field you want to pre-fill (it will be different for each form) and enter it into the configuration section too, together with the URL of your form too.

## Analysis

Even if your form questions are different to the example data, you __don't need to write any formulas__ to start analysing your data. Once your configuration has been entered, all the analysis will happen automatically. All you need to do is __select the session__ you wish to analyse on the __ANALYSIS__ tab, and the formulas will work their magic. If you need to provide this analysis to third-parties, you can copy and paste the output tables into a separate spreadsheet, or even an email.

  [1]: https://support.google.com/docs/answer/2839588 "Send your form to people"
  [2]: https://trevorfox.com/2015/06/dynamically-pre-fill-google-forms-with-mailchimp-merge-tags/ "Dynamically Pre-fill Google Forms with URL Parameters"