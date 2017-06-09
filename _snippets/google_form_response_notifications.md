---
label: snippets
layout: post
title: Google Form Response Notifications
short_title: __Form Response__ Notifications
author:
  name: jd
tags:
- google
- sheets
category: coding
lead: Use Google Apps Script to send notifications to different recipients based on a form value (e.g. organisation)
published: true
---
{% include lead.md %}

### Aim

It is fairly straightforward to set up a form for information collection in Google Apps, but often the ensuing proliferation means that important responses may get overlooked and missed. It is easy to set up an email notification for new responses, but these only go to the form owner. For more complex implementations, you may wish to be able to 'route' these notifications to different email addresses based on a particular form value.

Imagine you set up a generic booking form, with a drop-down question that allowed the respondent to select which event they were booking. In your organisation, different people are responsible for different events, so you want different individuals to be notified when a booking is submitted for their event. This code does just that.

### Method

###### Set-Up your Form and Response Sheet

Either create a new form, or use an existing one. You'll need to store your form responses in a Google Sheet. You will also need to decide which question on your form acts as the 'discriminator' in deciding who receives the notification email (e.g. Organisation or Event).

On this sheet, you'll need to create a new tab/sheet called 'Notifications' (if you'd like to name it something else, that's fine, just update the code below). In this sheet, you'll need a simple table that looks something like this:

|---
| [Field Name] | Email
|:-|:-
| Organisation A | a.person@example.com
| Organisation B | b.person@example.com
| Organisation C | c.person@example.com
| Organisation D | d.person@example.com

Simply entitle the first column ([Field Name]) with the name of the 'discriminator' question that you have chosen. Then fill in possible values (normally the field will be a drop-down box on your form, so this list should match that one). For each option, fill in a destination email address too.

###### Add the Code

You'll need to open the [Script Editor](https://developers.google.com/apps-script/guides/bound){:target="_new"} from __Tools__ -> __Script Editor__ in your Google Sheet. Then you can paste the two sections of code in from below. Explanatory comments are provided within the code, to make it easier to understand and change within the script editor itself.

{% highlight javascript %}
// Change this variable value to match the name of the 'extra' sheet/tab holding the notification table.
var notification_sheet = "Notifications";

function get_Notification_Routing() {
  
  // Firstly, we need to get the sheet with the notification information in.
  // This uses 'method chaining', which means we can call one function after another.
  var sheet = SpreadsheetApp.getActive().getSheetByName(notification_sheet);
  
  // Once we have the sheet, we can find out what the last column and last row used (e.g. the extent of the data range).
  var last_col = sheet.getLastColumn(), last_row = sheet.getLastRow();
  
  // Using this, and with another method chain, we can get data from this range (this will include headers too)
  var routing_Data = sheet.getRange(1, 1, last_row, last_col).getValues();
  
  // This declares an 'object' that will hold our names/values and email addresses.
  var routing = {field : routing_Data[0][0], routes : {}};
  
  // This loops through all the data (starting at 1, because we are ignoring the headers)
  for (var i = 1; i < routing_Data.length; i++) {
    
    // The first column (0 as we start from zero) is the name/value
    var name = routing_Data[i][0];
    
    // The second column is the email address
    var email = routing_Data[i][1];
    
    // Here we set the email address
    routing.routes[name] = email;
    
  }
  
  // The return statement means we give this data back to the code from which this function was called.
  return routing;
}
{% endhighlight %}

{% highlight javascript %}
// This is the catch-all address (e.g. if there isn't an email for a particular value). In this case, notifications will be sent here.
// If it is set to nothing (e.g. var default_email;) then notifications will only be sent when a match is found.
var default_email = "email@example.com";

function handle_onSubmit(e) {
  
  /* 
    This function is set up as a 'handler' for a specific event. It is done through 'Resources' -> 'Current Project's Triggers'.
    In practice, it means that this function will be run whenever that event occurs. In this case, we will use the 'On Form Submit' event.
    This should be fired every time a form response is submitted (either originally, or when it has been edited.
    The 'e' parameter holds all the information that has been submitted as part of the response.
    The code will run 'as' the user who created the trigger, so emails etc will come from them, not from the response submitting user.
  */
  
  // First we 'get' the route for the email we want to send.
  var routing = get_Notification_Routing();
  
  // We then can get the user, value and the email that we need to send to.
  var user_submitting_form = e.namedValues["Username"][0];
  var value_to_send_to = e.namedValues[routing.field][0];
  var email_to_send_to = routing.routes[value_to_send_to] ? routing.routes[value_to_send_to] : default_email;
  
  // Here we are 'building' the body content of the email by outputting each field name/value from the form.
  var email_Body = "";
  for (field in e.namedValues) {
    email_Body = email_Body + field + ": " + e.namedValues[field][0] + "\n";
  }
    
  // This checks to see if we have an email to send to!
  if (email_to_send_to) {
  
    // Send the email. The function call is formatted slightly differently (over multiple lines) to make it more 'readable'
    MailApp.sendEmail(
      email_to_send_to,
      user_submitting_form ? "New Form Request from: " + user_submitting_form : "New Form Request",
      email_Body
    );
  
  }
  
}
{% endhighlight %}

###### Set Up the Trigger

Once your code has been pasted in and saved, you now need to create a [trigger](https://developers.google.com/apps-script/guides/triggers/events){:target="_new"} to run the code every time a form response is submitted. You can do this in the script editor by selecting __Resources__ -> __Current project's triggers__. Then select _handle_onSubmit_ to run when the form is submitted. Email notifications will be sent from the account you are using to do this, so at this point you'll be asked to authorise the code to send email on your behalf.

### Finally

__Test__, __test__ & __test__! Use some familiar email accounts to check that it is working in the way you want it to, then put in the 'real' routing and watch those emails fly around. You'll also be able to see them in your 'sent email' label.