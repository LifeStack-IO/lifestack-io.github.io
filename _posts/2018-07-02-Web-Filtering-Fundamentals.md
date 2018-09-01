---
title: Fundamentals of Web Filtering & Logging
short_title: Understand Web Filtering
layout: post
author:
  name: jd
category: article
tags:
- education
- network
published: true
lead: With ever more intrusive, and ever __more expensive__, web filtering options available - here is a fundamental review of the technology to help __you decide__ what approach suits you best!
asset_prefix: io7Ds
---
{% include lead.md %}

## Introduction

We should begin with what __should__ be obvious, but is often 'clouded' by marketing claims and sales tactics:

> There is __no such thing__ as a perfect web filter.

Expanding this statement even further, web filters __aren't really that much better__ than each other (despite what their makers may say!). What they may be, though, is __better suited__ to your particular needs and environment. By understanding the fundamentals of how this technology works, and the balance of trade-offs each type of filter requires, you can make an informed choice.

With __yearly filtering costs__ ranging (for a typically sized organisation, like a secondary school) from about £/$/€ 1,000 to __tens of thousands__ (and growing!), your choice needs to help deliver both a suitable service and value for money.

### Education

In UK schools, the statuatory requirement for 'Online Safety' is found in __Annex C__  of '[Keeping children safe in education: for schools and colleges](https://www.gov.uk/government/publications/keeping-children-safe-in-education--2){:target="_blank" rel="noopener"}' and the __IT Policies__ section of '[The Prevent Duty](https://www.gov.uk/government/publications/protecting-children-from-radicalisation-the-prevent-duty){:target="_blank" rel="noopener"}'. Both sections are very brief, and generalised, and neither stipulates a particular technological approach nor level of appropriate filtering.

> Whilst filtering and monitoring are an important part of the online safety picture for schools and colleges to consider, it is only __one part__. [Department of Education, 2018: _emphasis added_]

Instead, they both encourage schools to think beyond filtering as a '__solution__' and into the wider area of online safety. They caution against '__overblocking__' and highlight the importance of staff training and pupil education, alongside appropriate technological measures.

> Whilst considering their responsibility to safeguard and promote the welfare of children, and provide them with a safe environment in which to learn, governing bodies and proprietors should consider the age range of their pupils, the number of pupils, how often they access the IT system and the proportionality of __costs vs risks__. [Department of Education, 2018: _emphasis added_]

Communication networks are an abundant resource in the modern world, and a school's IT system is just one, __small part__ of a myriad of ways that pupils can connect with the broader Internet. It cannot protect everywhere, so __education__, rather than just __prohibition__, will have a far __greater impact__ on actually safeguarding children.

### Trade-Offs

There are three main areas which a filtering system will need to balance. These traits tend to be __mutually exclusive__, so if you want to improve/increase performance in one area, that will cause a corresponding drop in the other areas. As with so much in technology, this is pretty much an inviolable rule - however much we may wish it weren't.

#### Inspection and Logging Depth

The __complexity__ of the modern web has __increased manifoldly__ over recent years, as has the number of apps and services which use it for communication. Getting __inside__ that traffic, so it can be logged and checked for inappropriate content, is a challenging process because it flies in the face of our concerted efforts to __improve web security__. If you can see right into web traffic, then others could too ...

We have come to rely on HTTPS[^HTTPS] / TLS[^TLS] / SSL[^SSL] to secure almost everything we do on the web. Recent [browser changes](https://security.googleblog.com/2016/09/moving-towards-more-secure-web.html){:target="_blank" rel="noopener"} have moved it from the exception, to the norm. No competent application developer would even consider launching a service that didn't encrypt its communications using this standard protocol.

Modern web-security __encrypts communication__ between the client device (laptop, Chromebook, iPad, mobile phone etc.) and the server. This renders both the content of the communication and the destination address (the URL in the web-browser) unreadable to all the systems that exist between the client and server (e.g. ISP, network providers etc.). This is right, and precisely what __users want__. We want our banking/shopping to __be secure__ and our messaging and email to be only visible to intended recipients. Filtering is in natural tension and conflict with this drive towards security, for to filter content, we want to inspect it - so it has to be readable to the network provider (e.g. your IT department).

Less intrusive inspection (e.g. filtering by site requested, rather than by the content of that request/response) can be achieved without the need to read (or decrypt) the content of all communications, but this gives less depth of control.

#### Reliability

The web has thrived because it has emerged as a __highly resilient__ technology. We __expect__ it to work, and except for some high-profile site failures, it broadly does. This reliability is founded on diversity and duplication. There are often multiple, or 'cloud-based', servers at the other end of each request, numerous paths to any destination on the web and local caches which can serve up content faster. This reliability is hard won, and the introduction of a __intercepting web filter__ can create a single point of failure in your network, as all the traffic needs to run through it.

As many organisations transition to entirely cloud provided systems, this sort of reliability concern can __seriously impact operations__ if the filtering device fails or is misconfigured. More complex configuration work may be required (together with potentially expensive load balancing equipment) to provide any fault tolerance in an intercepting or on-site proxy filtering device.

#### Usability and Ease of Deployment

Ideally, a web filtering solution should be __entirely transparent__ to users. They should merely browse the web, safe in the knowledge that viewing inappropriate content is prevented. Deployment should also, ideally, be similarly simple for technical support teams, with just a little bit of configuration and/or hardware installation.

The more complex the functionality offered, concerning interception and HTTPS decryption, the more complex the user experience is probably going to be. They may need to go through the process of __installing__ a __wildcard intercepting certificate__, or a __proxy configuration__ file, on their device __before__ they can access the internet. More sophisticated logging or policy requirements may require __captive portal__ authentication/identification for BYOD devices at the start of each day's browsing session. In some environments (particularly schools), these usability speedbumps may lead a __significant proportion__ of users to use their __own mobile data__ services, rather than rely on the organisation provided WiFi. Perversely, this may mean a __lower overall filtering effectiveness__ by reducing the number of users that connect via the filtered system. There is no point in delivering an incredibly complex and hardened filtering service if no-one uses it.

## Technologies

Now that we know the broad concerns we are seeking to address, and the sort of competing areas we wish to balance, we can look at the specific technologies and solutions available.

### Identity

To provide any logging or customised filtering (allow sites/ content through for some users, but not others) one needs to know _who_ the user is. In traditional IT systems, with rooms full of identical grey PC hardware, this was quite straightforward. A user would log onto the device, using their Windows / Active Directory username and password. Each computer was configured to send all of its web requests to a simple onsite web proxy. Their username was passed through as part of this request, and dependent on who they were, their request was then logged and filtered appropriately.

Now, most organisations will run on a __multiplicity of platforms__. There will be PCs, Macs, Chromebooks, iPads, Android tablets and Chromebooks. Some of these will belong to the organisation and be tightly managed, others will be supplied by the organisation but configured wholely by the users, others may be brought in by users themselves (BYOD[^BYOD]).

Gathering of identity information from there devices is __challenging__, so most systems tend to default to a [captive portal](https://en.wikipedia.org/wiki/Captive_portal){:target="_blank" rel="noopener"} style of authentication (think hotel or venue wifi). The user is redirected to a __login page__ when they try to access the Internet for the first time in a session (where a session is typically, but not always, a day). This login page verifies user credentials against a centralised store, such as Microsoft Active Directory or Google G-Suite. The limitations here are that apps that use web connections for operating (such as native Google drive apps on iPads, tablets and phones) will __not trigger the redirection__ to a captive portal, nor will requests to __secure websites__ (e.g. Google drive in a web browser - which, we have noted above, are increasingly common!). These requests __will fail__, leading to confused and frustrated users, and an increase in associated technical support queries.

Other solutions may integrate with an existing network level authentication system, such as [RADIUS](https://en.wikipedia.org/wiki/RADIUS){:target="_blank" rel="noopener"} to gather the authentication information that a user supplied to access the network. This is done via a procedure called __accounting__, and needs to be supported by __both__ the __filtering solution__, and the specific __network infrastructure__ that you have in place. This type of authentication is done by the device when it connects to the network, and therefore requires no user input or intervention beyond the initial set-up (and absolutely no user input if RADIUS is already in place). Wireless networks that are secured with a single password (often referred to as PSK or Pre-Shared Key networks) won't be able to supply this sort of information, as they are not 'user aware'.

Finally, agent-style apps, software or extensions may be required on devices to help gather identity data - but this needs considerable work to deploy or install, particularly on BYOD devices or devices that are not under centralised administrative control.

Establishing identity is __not essential__ for filtering, but it is required for differentiated filtering, and for logging and monitoring. It is entirely possible to provide __simple__ and __safe filtering__ at different levels by using a BYOD scheme that puts users into different network segments, without the need to individually identify them. These source segments can then be checked when a request is made to the filter, and the appropriate filtering policy applied depending upon your configuration. Again, one has to think about the __best balance__ in any approach. Is the increased visibility of __who__ is making a request actually required, and if it is, does it justify the extra work of installation and support if your network doesn't provide that sort of information already? Does the pain of having to authenticate through an imperfect captive portal mean that users will avoid using your filtered connection entirely?

### Interception

An __intercepting__ web-filter is one where all 'protected' web traffic must pass through the web-filter itself. In essence, it is a 'man-in-the-middle' device, which sits in the path of the traffic flows from your network to the wider Internet.

#### HTTPS Decryption

As discussed in an earlier section, an [increasing amount](https://transparencyreport.google.com/https/overview){:target="_blank" rel="noopener"} (as much as __84%__ for Chrome OS users at time of writing) of web traffic is now encrypted. This means that a rapidly shrinking proportion (likely __less than a quarter__) of traffic actually 'filterable' without full TLS decryption. More modern combinations of browsers and web filters can do some basic level of HTTPS 'decoding', which essentially means using [Server Name Indication](https://en.wikipedia.org/wiki/Server_Name_Indication){:target="_blank" rel="noopener"} to help understand which actual domain was requested by the client, but this support isn't completely universal.

To filter and log the __actual contents__ of the web traffic (e.g. block, log and alert when users search for particular terms on a Search Engine), this traffic has to be [decrypted](https://blog.heckel.xyz/2013/07/01/how-to-use-mitmproxy-to-read-and-modify-https-traffic-of-your-phone/) by the web filter. This is achieved by way of a Man-In-The-Middle attack (MITM). The intercepting filter 'pretends' to be the website, and the client connects securely to this. Then it sets up another encrypted connection to the final endpoint (e.g. Google). This means that the traffic is decrypted and examined/logged at the filter.

How can it __do this__? Isn't HTTPS __secure__, and this sort of eavesdropping __should be impossible__? Yes - for decryption to occur, each client devices has to essentially authorise it. This is done by way of a wildcard CA certificate, which has to be __trusted__ and __installed__ on each device. HTTPS security is achieved with public key certificates. When HTTPS is enabled for a domain (e.g. www.google.com) the administrator for that domain applies for a certificate (free or paid) and there is some sort of validation process (such as email, domain name checking, DNS record etc) to prove that person has full control of whatever server/service sits at the domain.

That certificate (the private part of it anyway) is then used to secure communications to anyone who wants to visit the website. The browser checks the certificate against the domain name and provided they match, it says the site is secure and everything works (non-secure sites get a __huge warning__ and a pile of steps to go through to get to them - which is enforced by the browser/client). Decrypting web-filters produce their own certification, which then claims to be valid for every site on the internet. Of course, it isn't, unless each client device is explicitly told that it is!

This certificate deployment can be done automatically for Active Directory controlled PCs and Google Admin Managed Chromebooks. But not for non-managed, BYOD / personal devices, which need manual intervention to do this. Without the certificate being installed, you effectively can't really browse the web via those filters - as everything is listed as insecure! As for whether this is a good idea? The jury is very much out, as it fundamentally [breaks](https://www.us-cert.gov/ncas/alerts/TA17-075A){:target="_blank" rel="noopener"} the trust network upon which the secure web is based. There is an advantage to being able to [decrypt](https://www.secureworks.com/research/transitive-trust){:target="_blank" rel="noopener"} web searches in __some cases__ but also huge privacy and [security](https://jhalderm.com/pub/papers/interception-ndss17.pdf){:target="_blank" rel="noopener"} implications regarding this for __all your users__ (colleagues and pupils). With this capability, who really knows whether banking or financial information is verifiably secure? Users may need extra training to understand the risks, and to ensure the systems they use can be properly audited to ensure security. It can also risk introducing unintended [security problems](https://insights.sei.cmu.edu/cert/2015/03/the-risks-of-ssl-inspection.html){:target="_blank" rel="noopener"} onto the network. Using decryption in this way undermines a lot of the work that network and security professionals do to help make the web a secure environment for us all.

#### Connections & Content

A traditional interception device will receive __all web traffic__ (that is, traffic destined for [ports](https://en.wikipedia.org/wiki/Port_(computer_networking)){:target="_blank" rel="noopener"} 80 or 443). This can be inefficient as once a filtering decision has been made (e.g. this url, or site, is allowed), is is not often changed during the lifetime of the conversation. This means that all traffic has to go through a (sometimes unnecessary) __extra stop__ on it's journey to/from its final destination. As the [perception of speed](https://en.wikipedia.org/wiki/Latency_(engineering)#Packet-switched_networks){:target="_blank" rel="noopener"} is normally down to the __latency__ of a connection (e.g. the round trip time for a request).

The alternative approach is to filter the __initial connection__, rather than the whole conversation. Typically this is done via a [DNS filtering](https://en.wikipedia.org/wiki/Content-control_software#Types_of_filtering){:target="_blank" rel="noopener"}, which uses the [Domain Name System](https://en.wikipedia.org/wiki/Domain_Name_System){:target="_blank" rel="noopener"} to provide filtered responses to requests for a particular website. This has drawbacks, as only the domain (e.g. www.google.com) is passed to the filter, rather than the precise URL. So, filtering can only be done at the domain, rather than the page, level. Yet for most scenarios, this is more than good enough, and the __advantages__ are that filtered DNS lookups are __much faster__ than interception and need only be done once for each user/domain/day (meaning only the initial connection request needs to be filtered, rather than all the traffic).

Typically, the infrastructure needed to deliver DNS filtering is much more __simple__ and __reliable__ too, meaning lower total cost. There is no need to rely on technologies like 'Server Name Indication', which can be bypassed, to filter HTTPS connections - so, in many ways, a DNS filtering solution is actually better than an intercepting filter for HTTPS traffic if you have no need or desire to fully decrypt the traffic. Like all web filtering systems, logging and identity can be challenging, and is dependent on __where__ filters are located in your network (or in the cloud).

## Solutions

### Approach

In the end, the choice of approach is going to come down to four basic questions, which echo our balancing act:

1. #### How much logging & filter differentiation is really required?
   If this feature is needed, you are going to need to look at __onsite/internal filters__, or sophisticated external filters with either a complex technology that you need to manage yourself or a disruptive installation and/or identity requirements.  
    
2. #### Does HTTPS __need__ to be decrypted?
   If so, an __intercepting__, rather than DNS-based filtering solution is the only choice, and there needs to be robust and available technical support to help users with problems.  
   
3. #### How transparent should the experience for users to be?
   DNS filters or inline transparent web filters (without SSL decryption and captive portal authentication) are the only __really transparent__ options.  
   
4. #### How important is reliability & robustness of connectivity?
   Single points of failure need to be avoided here, so cloud-based solutions will be best - or those deployed in a hybrid solution - with the ideal being a logging __DNS filter__.  

### Location

Web filtering is typically implemented __inside__ (e.g. onsite) the firewall, or __outside__ (hosted, or in the cloud). Both of these deployment locations have their own set of __benefits__ and __drawbacks__. Some filtering systems (such as DNS-based approaches) offer a __hybrid model__, with onsite data collection and cloud filtering.

#### Internal

The _good_ ...
+ Logging is __much easier__, as the web filter will be able to __see__ all your individual clients when they connect to it.
+ Easier to set __targetted policies__ for individual users or groups.
+ Single pathway to the Firewall/Internet means you can use the __same__ web filtering solution on __multiple__ outgoing lines.
+ Can be used __inline__, requiring no proxy configuration on client devices.

... and the _bad_
+ Needs on-site installation, configuration and management.
+ __Single point of failure__ for your connectivity, even with multiple diverse lines.
+ Extra hardware means __much higher initial cost__, and ongoing service/warranty costs.

#### External

The _up_ side ...
+ Provided as a hosted, or cloud-delivered solution, which means no onsite hardware.
+ Normally __less costly__ to install and maintain.
+ For cloud, or load-balanced offerings, much more __resilient__ and __reliable__.

... and the _down_
+ Has no visibility into the local network, so needs further logging device onsite or complex/brittle captive portal authentication.
+ Can only be used inline/transparently with firewall support ([WCCP](https://en.wikipedia.org/wiki/Web_Cache_Communication_Protocol){:target="_blank" rel="noopener"}) or ISP integration (meaning one filtering solution per line).
+ More likely to require proxy configuration for client devices unless transparency is supported.
+ Can increase latencies for web usage, depending on capacity and architecture.

## Restrictions

### Legal

Whilst the legal 'right' to enforce Internet filtering for students in schools is clear, it is not so for employees or staff. Nor is it clear whether organisations have the right to retain web-traffic logs and if they can, for how long? [Opinion 2/2017](http://ec.europa.eu/newsroom/document.cfm?doc_id=45631){:target="_blank" rel="noopener"}, authored and published by the European Commission Article 29 Data Protection Working Party is entitled '__On data processing at work__'. This working party, the predeccesor to the [European Data Protection Board](https://edpb.europa.eu/){:target="_blank" rel="noopener"} (EDPB) and was [set up](https://en.wikipedia.org/wiki/Article_29_Data_Protection_Working_Party){:target="_blank" rel="noopener"} to 'promote consistent application of the Data Protection Directive' and to provide 'expert advice'.

As such, organisations (such as schools) would likely claim that the __processing__ and __storage__ of personal data (such as web access logs and/or content) was __legally justified__ under article 7b (the performance of a contract) or article 7f (legitimate interest) for employees, and article 7c (legal obligations) for students. The working party document details an example (page 13 onwards) where HTTPS decryption is proposed at an organisation, with specific recommendations being to respect the fundamental rights of employee privacy over the desire to log and monitor encrypted communications:

> Irrespective of the technology concerned or the capabilities it possesses, the legal basis of Article 7(f) is only available if the processing meets certain conditions. Firstly, employers utilising these products and applications must consider the proportionality of the measures they are implementing. [EC Article 29 Data Protection Working Party, 2017]

- - -

> The appliance should be configured in a way to prevent permanent logging of employee activity. [EC Article 29 Data Protection Working Party, 2017]

- - -

> If some general logging would nonetheless be deemed strictly necessary, the appliance may also be configured not to store log data unless the appliance signals the occurrence of an
incident, with a minimization of the information collected.  [EC Article 29 Data Protection Working Party, 2017]

- - -

> Employers should consider certain types of traffic whose interception endangers the proper balance between their legitimate interests and employee’s privacy—such as the use of private webmail, visits to online banking and health websites—with the aim to appropriately configure the appliance so as not to proceed with interception of communications in circumstances that are not compliant with proportionality. Information on the type of communications that the appliance is monitoring should be specified to the employees.  [EC Article 29 Data Protection Working Party, 2017]

#### Why Monitor?

Monitoring, and storage of web logs, or even decrypted data from secure HTTPS connections are all __personal data__, and much of it (financial information, health, beliefs, private communication) is __highly sensitive__. Some monitoring __may be required__ to ensure (and demonstrate) that filtering is at least partly __effective__. However, any storage and monitoring must be undertaken in a way that is communicated to users and for strictly __defined purposes__.

The GDPR is very clear that data processing by organisations is only legally justified in cases where there is a __clearly stated__ and __clearly communicated purpose__, and that in the cases of employees (and students too, one would assume) consent to these operations __cannot reasonably be freely given__. If that purpose is to ensure the proper operation of a system, then logs should only be retained for a __very short period__ of time, and should never be used in other ways (such as to try to evidence under-performance by an employee). To do this would be a clear breach of duties under this legislation and could open up the organisation to a potentially __serious legal challenge__.

It is absolutely vital that if any web filtering technology is being used which stores this data, users should be properly informed about __what__ data is being held, __why__, __who can access it__ and for __how long__.

### Pragmatic

Technology is rarely the answer to 'people problems', and online safety is clearly an example of that. More time and money should go into educating users about safely using the Internet (particularly children) than goes into prohibition. Filtering is simply one tool, and a small one at that, in ensuring online safety. It covers users for only a proportion of their time online, and probably an ever-shrinking proportion at that. There will always be restrictions to its effectiveness and there will always be ways to circumvent even the most tightly controlled systems. Spending vast sums of money and associated time to chase an unobtainable perfection is rarely a wise plan!

## Suggestions

An imperfect technological solution that is __lightweight__, requires __little management__, just __occasional maintainence__ and does __not impede access__ to the Internet from any device is likely going to be __more successful__ at filtering harmful content than a __complex__ and __heavyweight__ one. Simply because users are more likely to continue to use it. A lightly filtered wireless connection is always better than an unfiltered mobile data or VPN one. If the aim is truly to improve online safety, this much should be very clear. An inexpensive solution means more resources are available for actual online safety education, and that is never a bad thing. So, think carefully about the best solution - because best often means __most workable__ and most able to integrate with the __wider goals__!

[^HTTPS]: The secure version of the protocol used to serve up web-content and pages to client devices, see [this page](https://en.wikipedia.org/wiki/HTTPS){:target="_blank" rel="noopener"} for more details.
[^TLS]: A cryptographic protocol which enables communication security, see [this page](https://en.wikipedia.org/wiki/Transport_Layer_Security){:target="_blank" rel="noopener"} for a more indepth look.
[^SSL]: The predecessor to TLS, now infrequently used. See [this video](https://vimeo.com/135666049){:target="_blank" rel="noopener"} for further explanation.
[^BYOD]: Bring your own device, the increasing trend to seperate out services provided by an organisation (e.g. email, storage, applications) from the device required to access them, typically owned by the user themselves. See [this page](https://en.wikipedia.org/wiki/Bring_your_own_device){:target="_blank" rel="noopener"} for a more comprehensive description.