---
label: snippets
layout: post
title: Using Configuration Data in Google App Scripts
short_title: __Configurable__ App Scripts
author:
  name: jd
tags:
- google
- sheet
- javascript
category: coding
lead: Combining __user__ and __general__ configuration to write _more flexible_ App Scripts.
published: true
date: 2017-10-12
---
{% include lead.md %}

### Introduction

It's tempting to [hard code](https://en.wikipedia.org/wiki/Hard_coding) configurable data into your apps script. It's _easy_ and _quick_, but also makes maintaining that script a lot __harder__ in the future. A configurable script is more __robust__[^fragility] and therefore more reliable. It adapts to change better, and will require less of your time in the future to keep it working!

### Configuration Types

Typically there are __two__ types of configurable values you might use in a script.

    System Config

The first is set by the developer and stored within the source code/script itself. The most __important aspects__ of these values is that they are declared [only once](https://en.wikipedia.org/wiki/Single_source_of_truth) and in one commonly known place (e.g. a single file or object). Following these rules ensures it is __trivial__ for a developer to find and update a single value, instead of having to search through source-code to find and _replace all instances_ of that configuration value.

    User Config

The second type of configuration data is that which comes from the __users themselves__. On a complex script project, you would like want to build a [custom dialog](https://developers.google.com/apps-script/guides/dialogs#custom_dialogs) UI to prompt for (and store) configuration data. This could include a [picker](https://developers.google.com/picker/) to select content from Google Drive, and validation logic to ensure the configuration data is acceptable (using HTML5 inputs or custom code). For a smaller project, an easier way to achieve similar functionality is to use the spreadsheet UI itself, by created a configuration tab.

### A CONFIG Tab

|---
| KEY | VALUE | TYPE | DESCRIPTION
|:-|:-|:-|:-
| FROM | john.doe@example.com | String | This is the name that will appear in the 'from' part of the email (before your email address)
| BATCH_SIZE | 20 | Integer | If you leave this blank, or use a value of 1 or lower, an email will be sent to each address in the EMAILS tab. If you set this to 2 or higher, emails will be sent in BCC batches of that number.
| SOURCE | Emails | String | The name of the sheet to take the email list from.
| DATA_ROW | 4 | Integer | The row at which data starts in your source sheet
| LIVE | TRUE | Boolean | Whether the script is 'live' and sending emails, or in a testing / debug mode.
| CC | jane.doe@example.com; archive@example.com | Array | List of addresses to CC every email to (for archive / information).

The table above is a good example of how to create a __config__ tab in a spreadsheet. Even a [standalone script][1] can use this technique, provided you supply the id of the sheet holding your configuration. If you are using a sheet to [host your][2] apps script, it makes sense to keep the configuration in the same place as the user interacts with your system (to save future confusion!).

The __type__ column helps the configuration parser to _understand_ the syntax of the value it is given. This means a string, delineated with semi-columns, can be parsed into an array as well as booleans being correctly handled as native boolean values (rather than being [coerced](https://javascriptweblog.wordpress.com/2011/02/07/truth-equality-and-javascript/)). The __description__ column helps your users understand the usage and impact of the configurable value, added essential documentation to your system.

### Configuration Code

    System Config
    
{% highlight javascript %}
var config = {
  prompts : {
    to : {
      title : "Send Example / Test Email",
      desc : "Send Email to ..."
    },
    confirm : {
      title : "Please confirm",
      desc : "Do you want to send emails to %s addresses, in %s batch/es?"
    },
  },
  alerts : {
    missing_value : "Please ensure you have filled in a '%s' cell for the email",
    missing_emails : "Can't find a sheet entitled %s",
    sent : "Sent emails to %s address/es, in %s batch/es"
  }
}
{% endhighlight %}{:class="code"}

A simple [javascript object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects) can act as the _container_ for all the __system__ configuration values. Logical organisation of values around a hierarchy makes for easier usage (e.g. `config.alerts.sent`). If this object is stored in a dedicated script file within your project it makes it easy to locate and update (e.g. config.gs or .config.gs if you would like at alphabetically sorted to the top of your script file list).

    User Config

{% highlight javascript %}
function loadConfig(id) {
  
  var _configSheet = id ? SpreadsheetApp.openById(id).getSheetByName("CONFIG") : SpreadsheetApp.getActive().getSheetByName("CONFIG");
  
  if (_configSheet) {
     var _data = _configSheet.getDataRange().getValues();
     for (var i = 1; i < _data.length; i++) {
       if (_data[i][0] && _data[i][1]) {
         if (_data[i][2] && _data[i][2] == "Array") {
           if (!_data[i][1] || _data[i][1] == "") {
             config[_data[i][0]] = false;
           } else {
             config[_data[i][0]] = _data[i][1].split(";");
           }
           
         } else if (_data[i][2] && _data[i][2] == "Boolean") {
           config[_data[i][0]] = (_data[i][1] === true || (_data[i][1] && _data[i][1].toLowerCase() == "true"));
         } else {
           config[_data[i][0]] = _data[i][1];
         }
       }
     }
  }
   
}
{% endhighlight %}{:class="code"}

The function above will dynamically load the configuration values from your sheet into your config object. If your configuration resides in a sheet to which the code is not container-bound (e.g. a standalone script), then you will need to supply the ID of that sheet so the code can find it! The function above means you can access the values in your code as if you had declared then in the config object itself making a single, and simple, source for all the configuration across your script.

{% highlight javascript %}
function doSomething() {
  
  loadConfig();
  if (config.LIVE) {
    // Proceed to send emails
  }

}
{% endhighlight %}{:class="code"}

Remember that object properties/keys in javascript are case-sensitive, so stick with a casing scheme in your configuration sheet (ALL CAPS is a sensible option).

[^fragility]: __Fragility__ or __robustness__ (in this case) refers to the ability of the code to tolerate change, or be susceptible to bugs caused by [inconsistent/repetitive statements](http://mhjongerius.tumblr.com/post/61853273412/the-seven-design-smells-of-rotting-software) or configuration values.

  [1]: https://developers.google.com/apps-script/guides/standalone "Standalone App Scripts"
  [2]: https://developers.google.com/apps-script/guides/bound "Container-bound App Scripts"