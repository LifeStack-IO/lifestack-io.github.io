---
label: snippets
layout: post
title: Showing Menus in Container-Bound Google App Scripts
short_title: __Menus__ in App Scripts
author:
  name: jd
tags:
- google
- sheet
- javascript
category: coding
lead: How to show __menus__ and __sidebars__ configuration to write _more flexible_ App Scripts.
published: true
date: 2017-10-13
---
{% include lead.md %}

### Introduction

The __easiest__ way to interact with your [container-bound][1] apps script is through a custom menu. This gives you the ability to map menu items (and sub-menu items) to individual functions in your script.

### Custom Menus

It's a good idea to keep this code in its own script file, I prefer to name it __entry.gs__ to make it clear that it is the generic entry point for the script. Then, you simply need to take the app container, in this case, `SpreadsheetApp` (as the script is hosted within a Google Sheet), and append the newly created menu. The __major limitation__ is that you must supply the name of the function to be called as a string, rather than a Javascript function itself. This means, for _common_ or _shortcut_ methods, you will need to create __facade-style functions__ to call generic methods. In the example below, `processUpdateThisWeek` and `processUpdateNextWeek` functions both call a more generic `processUpdate` method by passing a start date (for the week) as a parameter, but both methods need to exist because this parameterised call cannot be made directly from the menu.
    
{% highlight javascript %}

/**
 * Creates a custom menu in Google Sheets when the spreadsheet installs/opens.
 */
function onInstall(e) {
  onOpen(e);
}

function onOpen() {
  
  PropertiesService.getScriptProperties().setProperty("ID", SpreadsheetApp.getActive().getId());
  
  var ui = SpreadsheetApp.getUi();
  
  ui.createMenu(NAME_APPLICATION)
    .addItem("Enter Absence", "processStaffAbsence")
    .addItem("Unwell Today", "processStaffUnwellToday")
    .addItem("Arrange Cover", "processArrangeCover")
    .addSubMenu(ui.createMenu("Absence")
      .addItem("Approve", "processApproveAbsence")
      .addItem("Reject", "processRejectAbsence")
    )
    .addSubMenu(ui.createMenu("Update")
      .addItem("This Week", "processUpdateThisWeek")
      .addItem("Next Week", "processUpdateNextWeek")
      .addItem("Week after Next", "processUpdateNextPlusWeek")
      .addItem("Future Week", "processUpdateFutureWeek")
      .addItem("Currently Open", "processUpdateCurrentlyOpen")
      .addItem("All Open", "processUpdateAllOpen")
    )
    .addSubMenu(ui.createMenu("Export")
      .addItem("Today's Cover", "processExportToday")
      .addItem("Next Day's Cover", "processExportNextDay")
      .addItem("Future Cover", "processExportFuture")
    )
    .addSubMenu(ui.createMenu("Cover")
      .addItem("Arrange", "processArrangeCover")
      .addItem("Update", "processUpdateCover")
      .addItem("Cancel", "processCancelCover")
      .addItem("Notify", "processNotifyCover")
    )
    .addSubMenu(ui.createMenu("Import")
      .addItem("From CPD System", "processImportCPD")
      .addItem("From Cover Requests", "processImportCoverRequests")
    )
    .addSubMenu(ui.createMenu("Extras")
      .addItem("Generate ID/GUID to Cell/s", "processGenerateGUID")
      .addItem("Generate Code for Absence", "processGenerateAbsenceCode")
      .addItem("Pre-Cache", "preCache")
      .addItem("Apply Default Sorts", "applyDefaultSorts")
      .addItem("Send Pending Notifications", "processNotifications")
    )
    .addItem("Archive", "processArchive")
    .addItem("Suspensions", "processSuspensions")
    .addItem("Configure", "processConfigure")
  .addToUi();
  
  preCache();
};
{% endhighlight %}{:class="code"}

### Launch Sidebar

If you need a more complex user interface for your script application, you might prefer to use an HTML sidebar. This gives you a large area on the right-hand-side of the screen to present your UI. You can even have the sidebar open automatically when the sheet itself opens, with the code below. If you are interacting with any API, data or service which requires _OAuth permission_ to be __granted__ by the user (most scripts will need this), then you can't trigger that authentication from the sidebar itself. To deal with this case, the code below sets a script property when the menu item is first clicked (as this will trigger the OAuth process). Then, if that property is found to be set in subsequent sheet open events, the sidebar is automatically shown. This will prevent a potentially confusing error to be shown to the user, and the menu item will also provide a mechanism to re-open the sidebar if it closed.

{% highlight javascript %}
/**
 * Creates a custom menu in Google Sheets when the spreadsheet opens.
 */
function onInstall(e) {

  onOpen(e);

}

function onOpen() {

  var ui = SpreadsheetApp.getUi();
  ui.createMenu("Example Script")
      .addSeparator()
      .addItem("Show", "showSidebar")
      .addToUi();
  
  if (PropertiesService.getScriptProperties().getProperty("STARTED") == true) showSidebar();
  
};

function menuShowSidebar() {
  PropertiesService.getScriptProperties().setProperty("STARTED", true);
  showSidebar();
}

function showSidebar() {

  var html = HtmlService.createHtmlOutputFromFile("Sidebar").setTitle("Example Sidebar").setWidth(300);
  SpreadsheetApp.getUi().showSidebar(html);
  
}
{% endhighlight %}{:class="code"}

  [1]: https://developers.google.com/apps-script/guides/bound "Container-bound App Scripts"
  [2]: https://developers.google.com/apps-script/guides/dialogs#custom_sidebars "Dialogs and Sidebars in G Suite Documents"
  [3]: https://developers.google.com/apps-script/guides/properties "Properties Service"