---
title: Simple Bulk Emailing from Google Sheets
layout: post
author:
  name: jd
category: coding
tags:
- google
- sheet
- coding
- javascript
published: true
lead: Send __better looking__ emails to a bulk set of email addresses, straight from Google Sheets.
asset_prefix: WQ0kj
example: https://docs.google.com/spreadsheets/d/19N_cW5WROWyQCO3qYpWoEq-MsFBnzqUCWXsxXqVBjos/copy
---
{% include lead.md %}

[![Example Emailer]({{ site.baseurl }}/assets/{{ page.asset_prefix }}_screen.png){:class="img-fluid"}]({{ page.example }}){:target="_blank" rel="noopener"}

If you need to send __small batches__[^small] of 'bulk' emails, then this spreadsheet provides __all the code you need__ to make it happen! The email address list is stored in the sheet, and you can customise the email itself by writing simple [Markdown][1]. You can even send __tabular data__ straight from your sheet, which will be re-formatted as HTML.

## Caveats

Designed as a __learning exercise__, this __shouldn't__ be considered as a _production ready_ system. It is simple, and easy to tweak for your own needs, but you should probably only jump into it if you are __comfortable__ with concepts such as HTML and scripting. It __won't__ send bulk emails by default until you _tweak the configuration_ to put it into __live mode__. Any bulk-mailing code should be __considered dangerous__ to play around with unless you know what you are doing!

There are also [limits][2] on the __quantity of emails__ you can send from your Gmail account, so you should have a look at these first to ensure you're not likely to exceed them.

## Credits

 - This builds upon the excellent [Cerberus][3] responsive email patterns to create a simple HTML email template for sending. If you want to refine the design of the template, have a look at the project site first to see what is possible.
 - The code behing this spreadsheet (__Tools__ -> __Script Editor ...__) includes the versatile [showdown][4] parser. This converts [Markdown][1] to HTML, and is freely available under an [open-source license](https://github.com/showdownjs/showdown/blob/master/license.txt){:target="_blank" rel="noopener"}. The code itself is __copyright__ (c) 2007, [John Fraser](http://www.attacklab.net){:target="_blank" rel="noopener"} and all rights have been reserved.
 - If you wish to know more about some of the __techniques__ used in this script, you can read about how to create [menus]({{ site.baseurl }}{% link _snippets/apps_script_menus.md %}) and use [configuration]({{ site.baseurl }}{% link _snippets/apps_script_config.md %}).

## Instructions

### Testing

Firstly, you need to __author__ your email. A straightforward example has been provided, but you can alter this straightaway. The content of the message can be found in the __MESSAGE__ tab. The tabular data comes from __TABLE__. If you delete all the cell values, the table will disappear from your output email. If you need a larger table, adjust the size of the __TABLE__ [named range][5]. The message content can be authored in plain text, or [Markdown][1] if you would prefer more precise control over how will look to your recipients.

Once you have authored your message, you can use the __Email__ menu to send yourself a test message by clicking __Send Test Email__. If it is the first time you have run the script, you'll be prompted to authorise the script to access your email account (required to send the emails). It's good security practice to have a look at the script first, to make sure you're happy with what it will be doing. The critical parts are in the __Code.gs__ file, and any command that interacts with your email will be prefixed with __GmailApp__. This allows you to quickly find the important lines and review their intended actions.

Having sent yourself a test email, you can __review how it looks__ and make any [customisations](#customise) to the details, colours and fonts.

### Emailing

The email list will initially contain randomly [generated test data](https://www.generatedata.com/){:target="_blank" rel="noopener"}). The list of email address to send to is column __F__ in the __LIST__ tab. This is referenced as a [named range][5] called __EMAILS__ for easier reference. A simple parser is also included to help generate an email list from a __TO__ or __BCC__ string containing many email addresses. You don't have to use this; it's just there to help you to migrate from a standard __BCC__ emailing without having to re-type all the addresses in again. If you have a string containing all your addresses in this format, paste them in cell __E2__ on the parser sheet to extract the email addresses from them (there is an example in there to help you).

When you are happy with your email, and your list, you can set the various configuration options explained in the __CONFIG__ tab. Remember to send a final email to yourself before switching the __LIVE__ configuration value to __TRUE__. Without doing this, the script will not send any emails other than the test one.

Having sent emails, they will appear in your sent items, so you can verify that they have been correctly sent. Any bounces or replies will come straight to you.

### Customise

If you would like to change fonts or colours, you can do so on the __CONFIG__ tab. You can also add __logo images__ and an __email signature__. If you wish to alter the layout or perform more advanced customisation to the email template itself, edit the __Email.html__ file in the script editor. Make sure you test it properly before sending out any live emails (you may wish to change the __LIVE__ config mode back to __FALSE__ while you do this, just in case).

*[HTML]: Hypertext Markup Language

[^small]: Typically __below__ a few hundred at a time.

  [1]: https://daringfireball.net/projects/markdown/syntax "Markdown Syntax"
  [2]: https://support.google.com/a/answer/166852 "Gmail sending limits in G Suite"
  [3]: https://github.com/TedGoas/Cerberus "Cerberus Responsive Email Patterns"
  [4]: http://showdownjs.com/ "A Markdown to HTML converter written in Javascript"
  [5]: https://support.google.com/docs/answer/63175 "Name a range of cells"