---
title: Caveats when deleting G-Suite Accounts
layout: post
author:
  name: jd
category: article
tags:
- google
- sheet
published: true
lead: If you are using Google Sheets or Google Apps Script in your domain, here are a few _caveats_ you __need to be aware of__ when deleting a G-Suite User Account.
---
{% include lead.md %}

## Introduction

If your organisation or team are making extensive use of the G-Suite platform, the chances are you have begun to use __Apps Script__ or __Sheets__ in relatively sophisticated ways. This might be using the [importrange]({{ site.baseurl }}{% link _snippets/google_sheet_importrange.md %}) function to pull data together from different sheets, or a website/web app served by Apps Script, or even just some sheet helper functions coded using Apps Script, like [form response notifications]({{ site.baseurl }}{% link _snippets/google_form_response_notifications.md %}). Deleting a user account can __impact the continued usability__ of all of these features, __unless__ you do a few _simple things_ first.

## ImportRange

When you first use the [importrange][1] function in a sheet, you will be asked to __Allow Access__ to the source sheet (e.g. the one specified by the _url_ or _id_ in the formula). You will only be asked for this the __first__ time you try to connect to a particular source sheet. All subsequent uses of the function to import cell ranges from that source sheet with use the same 'authorisation' behind the scenes and work straightaway (without further prompting). This authorisation process stores a _token_ behind the sheet (in which you are using the formula) that grants access to the source sheet in the context of __your__ user account (e.g. __as you__).

This neat bit of technological trickery means any other users with whom you have shared your sheet (the one with the formula in it, __not the source one__) will be able to see the results of the [importrange][1] function. This works even if they __don't__ have access to the source sheet because the import is running __as you__. This is great __until__ the user who originally pressed the __Allow Access__ button moves on, and their account is subsequently deleted from the G-Suite / Google Apps domain. At this point, the _token_ is no longer valid and the [importrange][1] function will fail.

Unfortunately, there is currently no way to _audit_ or even _view_ which __user provided that initial authorisation__, nor is there a way for an administrator to see which authorisations a user may have provided before they are deleted. The best solution is either to ask the user themselves (and they may, or may not, remember) or to re-authorise the [importrange][1] functions _as_ and _when_ they fail. This is a quick and easy process if you know what to look for, as Google Sheets will re-prompt you to authorise the function when you hover your mouse cursor over the offending cell. The only issue with this is that if the [importrange][1] function is wrapped by another function (as part of a larger formula) the __Allow Access__ button will not be shown. The best was to design sheets which make use of [importrange][1] is to provide a simple function in a _configuration_ or _extra_ tab that just imports a single cell from each source sheet you intend to use. These formulas (as shown below) can then be quickly checked and re-authorised as required.

{% highlight puppet %}
IMPORTRANGE("SPREADSHEET_ID OR SPREADSHEET_URL", "A1")
{% endhighlight %}{:class="formula"}

The key here is user awareness. If and when you need to delete a user from your domain, send an email round to their colleagues to let them know that there might be issues, and what they should look out for, and what they should do to fix it. It's frustrating to see a working sheet begin to fail, but very quick to resolve if you are fore-armed with this info. Send them a link to this article if you think it will help!

## Apps Scripts

When you start to work with apps scripts, you will quickly find there are __two__ main types that you will be dealing with.

#### Standalone Scripts

Apps scripts which you can _see_ in Google Drive are called [standalone][2] scripts. They are normally created via the Google Drive Web App and appear in the same way as _normal_ docs and sheets. You can edit them, share them and transfer ownership as you would do for any other file. These scripts are much easier to handle if you delete a user, as an admin can choose to transfer ownership of them when deleting a user (in an identical way to the rest of that user's Google Drive content), or the user themselves can transfer ownership to a colleague before they leave.

The caveat here is to watch out for [triggers][4], as these will not be smoothly transferred to another user without some manual intervention. __Triggers__ are commonly used in standalone scripts to run _processes_ on a particular schedule (e.g. once an hour, or three times a day etc.). As these triggers run in the __context of the user who created them__, they should ideally be:

1. Removed by the original user (as part of a handover process).
2. Then re-created by a new user (who has access to the same sheet and will be taking responsibility for that process).
3. Tested to check that the trigger continues to work as expected.

#### Container-Bound Scripts

A [container-bound script][3] is one that sits behind an existing Google doc, sheet or set of slides. These are created when you open the __Script Editor__ from within an existing doc. They don't appear within Google drive on their own (as they are bound to an existing file) and they are not accessible via the Google API. This makes them harder to deal with, but they are still handy as they allow you to easily add extra functionality in the Google Apps user interface, through [custom menus][5] for example. This functionality makes them a popular choice, and are common across large G-Suite domains.

The __major drawback__ of these scripts is that they __do not__ follow the ownership of their containing document. What this means in practice is that the script may not be _owned_ by the __same user__ as the document, and ownership of the script is not transferred when the ownership of the containing document is transferred. Even worse, it is currently __not actually possible__ to transfer ownership of one of these scripts (e.g. they live, and die, with the user who first created them).

As with [importrange][1] above, there is no way ~~(at time of writing)~~ to completely audit the scope of this problem in a domain (e.g. list all container-bound scripts owned by a user). It is also not possible to see who currently owns a container-bound script. If an administrator deletes a user from the domain and transfers ownership of their drive files to another user, container-bound scripts are not transferred and could be lost forever. The only way to ensure that this does not happen is some careful management before the user has been deleted! There is now an __excellent__ user-accessible [tool][8] that will allow individual users to check who __owns__ the various script projects (including container-bound scripts) they have access to.

The way to handle these scripts is for a new user (whoever is taking over the responsibility for this code) to __make a copy__ of the [script project][6] via the script editor itself. This can currently be done by selecting '__Make a copy...__' under the '__File__' menu. This creates a duplicate copy of the script project, owned by the new user, bound to the same document. Once this has been done, it can be tested and the old 'project' deleted by the original owning user (the user who is being deleted).

This can result in a lot of work if there are a lot of scripts, so you may choose to rename and retain the original user instead of deleting them (normally viable in an education context, but might be costly on a paid per-user domain). If there are _triggers_ or _API projects_ associated to the script, you may also need to re-create and test them appropriately.

If an orderly handover process is not feasible, or a user has already been deleted (and the scripts owned by them has therefore disappeared), all is not lost. They can often be [restored][7] via the Google Admin site, together with their files. You can then reset the password for the account, and then log on as that user to help run through the steps detailed above.

## Published Web Apps

Published web-apps are [standalone][2] scripts that can act as web-apps, serving up (or even receiving) HTML, JSON or text content. Like triggers, the 'server' process is often authorised by (and therefore __run as__) an individual user. If this user is subsequently deleted, the web-app itself will no longer be successfully published and will fail to work. Again, the best solution here is to identify these scripts in advance of a user leaving the organisation and ask them to de-publish the app, and then transfer ownership to another colleague who can then re-publish. If the user has already left (or been deleted), you should be able to use a similar technique (restoration or the user/password changing to take control of the account) to ensure a successful _de-publish_ then _publish_ again procedure.

  [1]: https://support.google.com/docs/answer/3093340 "How to use the IMPORTRANGE function"
  [2]: https://developers.google.com/apps-script/guides/standalone "Standalone App Scripts"
  [3]: https://developers.google.com/apps-script/guides/bound "Container-bound App Scripts"
  [4]: https://developers.google.com/apps-script/guides/triggers/ "Simple Triggers"
  [5]: https://developers.google.com/apps-script/guides/menus "Custom Menus in G Suite"
  [6]: https://developers.google.com/apps-script/guides/bound#access_to_bound_scripts "Access to Container-bound App Scripts"
  [7]: https://support.google.com/a/answer/1397578 "How to restore a recently deleted user"
  [8]: https://script.google.com/home "Manage your Apps Scripts"