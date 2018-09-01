---
title: Google Calendars on the Web
layout: post
author:
  name: jd
category: article
tags:
- google
- coding
- javascript
published: true
lead: Displaying Google Calendar events on the web, a __simple diary banner__ for your site.
asset_prefix: hn89a
---
{% include lead.md %}

## Introduction

You have a website, you have a [Google calendar][1]{:target="_blank" rel="noopener"} which you have [shared publically][2]{:target="_blank" rel="noopener"}. Now you would like to have some of the events from your calendar display as a banner on your website, highlighting the most important events for the world to see.

## Instructions

The easiest way to do this is to make a [client-side][3]{:target="_blank" rel="noopener"} request for your calendar events and render them directly on your web-page. This approach will work on any site and is also easily embeddable if you are using a templated site (like Wordpress).

### An API Key

To ensure your website can make a valid request to get your calendar events, you will need an API key from Google. This is a [quick process][4]{:target="_blank" rel="noopener"} and will result in a long string of letters and numbers that looks like a randomly generated password (which is pretty much what it is). To get a key, follow the instructions in the article linked above, or log onto the [Google Developers Console][5]{:target="_blank" rel="noopener"}, create a project and enable the Calendar API.

Once you have created your project, and the API key, you can __further secure__ the usage of that key (to make sure that it can only be used from your website) by setting '_Application Restrictions_' from the '_Key Restrictions_' section of the API key page (click on the key name, or edit icon). Here you can list your website address/es (e.g. www.example.com/*) in the '_HTTP referrers (websites)_' section. This will restrict the key, so it only works from your site.

### Calendar ID

Before you make a request for calendar data, you need to know which calendar you wish to access. This is done by supplying your calendar ID, which can be found in the settings page of the calendar, under 'Integrate calendar' and 'Calendar ID'. It will look like an email address, and much be quite long in the case of a shared or secondary public calendar. Your calendar uses your email address as it's ID.

### Your Web Page

If you are looking to embed this calendar banner on an existing page, you can skip over this section. The banner embed code assumes you already have [JQuery][6]{:target="_blank" rel="noopener"} linked into your page, and assumes we are using the [Roboto][7]{:target="_blank" rel="noopener"} font family.

If you want to embed the banner in a new HTML page, you can use the following as a good starting point for that page. It links the relevant JQuery library and the Roboto font family, as well as providing a __full width__ body element (without any padding or margins) so that the __banner stretches__ right __across the page__.

{% highlight html %}
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
      <title>My Public Calendar Banner</title>
      <meta name="viewport"
      content="width=device-width, initial-scale=1, minimum-scale=1, maximum-scale=1">
    <link href="https://fonts.googleapis.com/css?family=Roboto:700%2C400%2C500"
      rel="stylesheet" property="stylesheet" type="text/css" media="all">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.3.1/jquery.min.js" 
      integrity="sha256-FgpCb/KJQlLNfOu91ta32o/NMZxltwRo8QtmkMRdAu8="
      crossorigin="anonymous"></script>
    <style id="page-inline-css" type="text/css">
      html, body {
          position: relative;
          height: 100%;
        }
        body {
          background: #eee;
          font-family: Roboto, Helvetica Neue, Helvetica, Arial, sans-serif;
          font-size: 14px;
          color:#000;
          margin: 0;
          padding: 0;
        }
    </style>
  </head>
  <body></body>
</html>
{% endhighlight %}{:class="html"}

### Embedding a banner

Using the excellent [Swiper][8]{:target="_blank" rel="noopener"} library to provide touch control and animated transitions, the code below can be __dropped into your page__. Insert your __API Key__ and __Calendar ID__ in into the relevant spots, and you are good to go! If you don't see anything on the screen when you test the page, remember to check the developer console in your browser for any errors. Pay particular attention to checking you have enabled the calendar API in your developer console project, as this often gets forgotten!

{% highlight html %}
<!DOCTYPE html>
<div class="swiper-container">
    <link rel="stylesheet"
      href="https://cdnjs.cloudflare.com/ajax/libs/Swiper/4.3.5/css/swiper.css"
      integrity="sha256-I23rKKBc0+Qh38KLk0F8kfmLoQQ9F4dS0f8064Jfu8I="
      crossorigin="anonymous" />
    <script src="https://cdnjs.cloudflare.com/ajax/libs/native-promise-only/0.8.1/npo.js"
      integrity="sha256-o/UXdF4sFrbgV5UCIWF5ca7VMLDdplhzA4knJ4nFsc0="
      crossorigin="anonymous"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/fetch/2.0.4/fetch.min.js"
      integrity="sha256-eOUokb/RjDw7kS+vDwbatNrLN8BIvvEhlLM5yogcDIo="
      crossorigin="anonymous"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.22.2/moment.min.js"
      integrity="sha256-CutOzxCRucUsn6C6TcEYsauvvYilEniTXldPa6/wu0k="
      crossorigin="anonymous"></script>
    <style id="div-inline-css" type="text/css">
        .swiper-container {
            width: 100%;
            height: 350px;
            background: #000;
        }
        
        .swiper-slide {
            text-align: center;
            font-size: 18px;
            background: #000;
            color: #fff;
            display: -webkit-box;
            display: -ms-flexbox;
            display: -webkit-flex;
            display: flex;
            -webkit-box-pack: center;
            -ms-flex-pack: center;
            -webkit-justify-content: center;
            justify-content: center;
            -webkit-box-align: center;
            -ms-flex-align: center;
            -webkit-align-items: center;
            align-items: center;
        }
        
        .swiper-button {}
        
        .swiper-pagination-bullet {
            opacity: .5;
            background: #ccc;
        }
        
        .swiper-pagination-bullet-active {
            background: #fff;
        }
        
        .swiper-content {
            position: relative;
            display: block;
            overflow: hidden;
            z-index: 5;
            font-weight: 400;
            letter-spacing: 0px;
            font-family: Roboto;
            opacity: 1;
            padding: 10px 40px 20px 40px;
        }
        
        .swiper-content strong {
            font-weight: 600;
        }
        
        .swiper-content-header {
            font-size: 42px;
            line-height: 48px;
            text-align: left;
            border-width: 0px;
            margin: 0px;
            padding: 0 0 10px 0;
        }
        
        .swiper-content-button {
            float: left;
            white-space: nowrap;
            min-width: 229px;
            max-width: 229px;
            font-size: 16px;
            line-height: 17px;
            font-weight: 500;
            border-color: #fff;
            border-style: solid;
            border-width: 3px;
            border-radius: 30px;
            outline: none;
            box-shadow: rgb(153, 153, 153) 0px 0px 0px 0px;
            box-sizing: border-box;
            cursor: pointer;
            margin: 0 10px 5px 0;
            padding: 12px 35px;
            min-height: 0px;
            max-height: none;
        }
        
        a.swiper-content-button,
        .swiper-content-button a {
            text-decoration: none;
            color: inherit;
        }
        
        .swiper-content-button:hover {
            background-color: #fff !important;
            color: #000 !important;
        }
        
        .waiting {
            font-size: 42px;
        }
        
        .waiting:after {
            overflow: hidden;
            display: inline-block;
            vertical-align: bottom;
            -webkit-animation: ellipsis steps(6, end) 1.5s infinite 400ms;
            -moz-animation: ellipsis steps(6, end) 1.5s infinite 400ms;
            animation: ellipsis steps(6, end) 1.5s infinite 400ms;
            content: "\2026";
            width: 0px;
        }
        
        @keyframes ellipsis {
            to {
                width: 1.25em;
            }
        }
        
        @-webkit-keyframes ellipsis {
            to {
                width: 1.25em;
            }
        }
        
        @media only screen and (max-width: 600px) {
            .swiper-container {
                height: 450px;
            }
            .swiper-content-header {
                font-size: 32px;
                line-height: 38px;
            }
        }
        
        #diary-slides .swiper-button-prev,
        #diary-slides .swiper-button-next {
            position: absolute !important;
            top: 50% !important;
            width: 27px !important;
            height: 44px !important;
            margin-top: -22px !important;
            z-index: 10 !important;
            cursor: pointer !important;
            background-size: 27px 44px !important;
            background-position: center !important;
            background-repeat: no-repeat !important;
        }
    </style>

    <!-- Additional required wrapper -->
    <div id="diary-slides" class="swiper-wrapper">
        <div class="swiper-slide">
            <div class="waiting"></div>
        </div>
    </div>

    <!-- If we need pagination -->
    <div class="swiper-pagination swiper-button-white"></div>

    <!-- If we need navigation buttons -->
    <div class="swiper-button swiper-button-prev swiper-button-white"></div>
    <div class="swiper-button swiper-button-next swiper-button-white"></div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/Swiper/4.3.5/js/swiper.js"
      integrity="sha256-o7yDjDHWk2mV1DlZ+RGyve6aaUOYwV2Rkp6I9M2GMzI="
      crossorigin="anonymous"></script>
    <script id="diary">
        var _loadDiary = function() {

            var API_KEY = "<< YOUR API KEY HERE>>";
            var CALENDAR_ID = window.location.hash && 
              window.location.hash.indexOf("@") > 0 ? 
                window.location.hash.replace("#", "") : "";
            var FILTERED = false;
            var BY = "Highlight=TRUE";
            
            var START = moment().subtract(2, "days").startOf("day").toDate().toISOString();
            var LIMIT = "5";

            var URL = "https://content.googleapis.com/calendar/v3/calendars/" + 
              encodeURIComponent(CALENDAR_ID) + "/events?maxResults=" + LIMIT + 
              "&orderBy=startTime&" + 
              (FILTERED ? "sharedExtendedProperty=" + encodeURIComponent(BY) + "&" : "") + 
              "showDeleted=false&singleEvents=true&timeMin=" + encodeURIComponent(START) + 
              "&key=" + API_KEY;

            fetch(URL, {
                method: "GET",
                headers: {
                    "Content-Type": "application/json",
                },
                redirect: "follow",
            }).then(function(response) {
                if (response.ok && response.status >= 200 && response.status < 300) {
                    return response.json();
                }
                else {
                    var error = new Error(response.statusText);
                    error.response = response;
                    throw error;
                }
            }).then(function(data) {

                console.log("Diary Data:", data);

                var _formatDate = function(dt) {
                        return moment(dt).format("dddd MMMM Do YYYY");
                    },
                    _formatTime = function(dt) {
                        return moment(dt).format("ha");
                    };

                var _wrapper = jQuery("#diary-slides").empty();

                if (data.items && data.items.length > 0) {

                    for (var i = 0; i < data.items.length; i++) {
                        var _item = data.items[i];
                        var _slide = jQuery("<div />", {
                            class: "swiper-slide"
                        });
                        var _content = jQuery("<div />", {
                            class: "swiper-content"
                        }).appendTo(_slide);

                        if (_item.summary) {

                            var _header = jQuery("<div />", {
                                class: "swiper-content-header"
                            }).appendTo(_content);
                            _header.append(jQuery("<strong />", {
                                text: _item.summary
                            }));
                            _header.append(jQuery("<br />"));

                            if (_item.start.date) {
                                _header.append(_formatDate(_item.start.date));
                            }
                            else if (_item.start.dateTime) {
                                var _time = _formatTime(_item.start.dateTime);
                                if (_item.end.dateTime) {
                                    _time += " - ";
                                    _time += _formatTime(_item.end.dateTime);
                                }
                                _header.append(_time);
                                _header.append(", " + _formatDate(_item.start.dateTime));
                            }

                            _wrapper.append(_slide);

                        }
                        if (_item.description) {
                            var _description = jQuery.parseHTML(_item.description);
                            console.log("Description:", _description);
                            for (var j = 0; j < _description.length; j++) {
                                if (_description[j].nodeName == "A") {
                                    jQuery(_description[j]).attr("target", "_blank")
                                      .addClass("swiper-content-button")
                                      .appendTo(_content);
                                }
                            }
                        }
                    }
                }
                return true;
            }).then(function() {
                var mySwiper = new Swiper(".swiper-container", {
                    loop: true,
                    autoplay: {
                        delay: 9000,
                    },
                    pagination: {
                        el: ".swiper-pagination",
                        dynamicBullets: true,
                    },
                    navigation: {
                        nextEl: ".swiper-button-next",
                        prevEl: ".swiper-button-prev",
                    },
                });
            });
        };

        if (window.attachEvent) {
            window.attachEvent("onload", _loadDiary);
        }
        else {
            if (window.onload) {
                var curronload = window.onload;
                var newonload = function(evt) {
                    curronload(evt);
                    _loadDiary(evt);
                };
                window.onload = newonload;
            }
            else {
                window.onload = _loadDiary;
            }
        }
    </script>
</div>
{% endhighlight %}{:class="html"}

### Filtering your Events

The code above will display the next five events, starting from a couple of days before __now__. You can alter this behaviour by adjusting the __LIMIT__ and __START__ variables. You can also choose to filter the events using [extended properties][9]{:target="_blank" rel="noopener"}. These data fields are baked into the Google Calendar system, but there is __no standard Google UI__ available for editing them. Instead, you can choose to write your code to add these properties to your events (e.g. using Apps Script) or install a [third-party tool][10]{:target="_blank" rel="noopener"} to do it for you!

If you use the [Tag-A-Doc][11]{:target="_blank" rel="noopener"} chrome extension and associated [web app][12]{:target="_blank" rel="noopener"}, add the __Highlight__ tag to your events. Then change the value of the __FILTERED__ variable in the code above to true. This will request only those events that have the __Highlight__ tag applied, using the filter: "Highlight=TRUE". You need not stop there; you can add your own tags and filters to display just the events you would like to show!

  [1]: https://support.google.com/calendar/answer/37095 "Create a new calendar"
  [2]: https://support.google.com/calendar/answer/37083 "Create & manage a public Google calendar"
  [3]: https://www.codeconquest.com/website/client-side-vs-server-side/ "Client Side vs. Server Side"
  [4]: https://docs.simplecalendar.io/google-api-key/ "Creating a Google API Key"
  [5]: https://console.developers.google.com/ "Google Developers Console"
  [6]: https://www.w3schools.com/jquery/jquery_get_started.asp "JQuery Get Started"
  [7]: https://fonts.google.com/specimen/Roboto "Roboto - Google Fonts"
  [8]: http://idangero.us/swiper/ "Swiper - Most Modern Mobile Touch Slider"
  [9]: https://developers.google.com/calendar/extended-properties "Google Calendar - Extended Properties"
  [10]: https://chrome.google.com/webstore/detail/tag-a-doc/ekniapbebejhamindielmdgpceijdpff "Chrome Extension to show Google Apps Document/Event Tags"
  [11]: https://educ.io/extensions/tag-a-doc "Chrome Extension to show Google Apps Document/Event Tags"
  [12]: https://educ.io/events/ "Tag and filter your Google Calendar Events"