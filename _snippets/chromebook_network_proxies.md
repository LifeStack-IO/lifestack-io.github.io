---
label: snippets
layout: post
title: Configure your Chromebook to connect via a Proxy Server
short_title: __Proxies__ and your Chromebook
author:
  name: jd
tags:
- chrome
- google
- networks
category: tutorial
lead: If you are using a Chromebook in a school environment, you may need to make a few small adjustments to your network settings to successfully connect via a proxy server.
published: true
date: 2017-09-01
---
{% include lead.md %}

### Introduction

A [proxy][1] is a server or device through which requests and responses for web pages and sites are routed. Think of it as a gatekeeper through which most, or all, Internet traffic is sent. They are commonly used to enforce __filtering policies__ (restricting access to inappropriate or harmful material), to __store__ (cache) parts of pages (e.g. videos or images) closer to your device so that they appear to load faster and also to __log__ Internet traffic for technical, legal or policy compliance.

Proxies can take a lot of different forms and are commonly found right the way through the networks which make up the [access][2] portion of the Internet. Mobile phone connections or any cellular data system (e.g. 4G Broadband) will typically send traffic through one or more [proxies][3]. These proxies are [transparent][4] and therefore require no extra configuration of your device to use them.

In smaller organisations, such as schools, a proxy __may not__ be transparent and thus may require a bit of configuration to get your Chromebook 'talking' to the outside world. It's a straightforward process, and very quick to do.

### Configuration

If you can connect to the network via an ethernet cable or wireless connection, but websites stubbornly refuse to load - you may be on a network that uses a proxy. The first thing to do is to ask if this is the case. Normally anyone who works with IT in the organisation will be able to tell you whether this is the case and give you the essential details you will need to successfully connect through the proxy.

While the exact wording, colour, shape, size and position of the Chrome OS Configuration pages changes a little with every software release, you can usually configure three 'flavours' of connection for __each__ wireless (or wired) network to which you connect. Just click on the network you are connected to (often the _name_ of the Wireless Network) from the __settings page__ (chrome://settings/), or the network connection icon at the end of your [shelf][5] (which is normally to be found at the bottom of the screen). From here, you should be able to locate the proxy settings, or a [proxy tab][6] (depending on your Chrome OS version). If you are not able to 'select' or 'configure' the proxy, you may need to switch on proxy settings for __shared networks__, which are connections (e.g. wireless networks) that 'are shared' between all users of your Chromebook.


The three (or occasionally four) connection flavours are:
  + __direct__ : No proxy (or a transparent proxy), which is a direct connection to the Internet and the default mode of operation.
  + __automatic configuration__ : You supply a web address where the full configuration details can be pulled from.
  + __manual__ : Where you will need to supply the address of the proxy server, a port and optional domain exceptions. These exceptions are used to specify content that is served locally from your network (e.g. an Intranet) that doesn't need to be fetched via the proxy.
  
Your __friendly__ IT contact will be able to tell you which of these to use, and give you the required details that you should enter. As these settings are pretty much standard across all device types and [browsers][7], __no extra__ or __specific__ Chromebook knowledge is needed.

Once you have added the correct settings and saved them, they will be active __just for that network__. This means when you head home, or to another wireless network at a different organisation, _you won't need to turn them off_. They will stay there, waiting for the next time you connected to the 'proxied' network - when they will become active and ensure your Internet traffic gets through!

  [1]: https://en.wikipedia.org/wiki/Proxy_server "What is a proxy server - Wikipedia"
  [2]: https://en.wikipedia.org/wiki/Internet_access "Internet Access - Wikipedia"
  [3]: http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.703.4245&rep=rep1&type=pdf "Investigating Transparent Web Proxies in Cellular Networks"
  [4]: https://www.maxcdn.com/one/visual-glossary/transparent-proxy/ "What is a Transparent Proxy?"
  [5]: https://support.google.com/chromebook/answer/3113576 "Customise your Chrome OS Desktop"
  [6]: https://www.schooltechnician.co.uk/configure-google-chromebook-proxy-server/ "Configure your Google Chromebook to use a Proxy Server"
  [7]: http://www.wikihow.com/Change-Proxy-Settings "How to Change Proxy Settings"