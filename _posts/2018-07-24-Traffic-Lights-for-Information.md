---
title: Dealing with confidential information in schools
short_title: Categorising Confidential Information 
layout: post
author:
  name: jd
category: article
tags:
- education
- google
- storage
published: true
lead: Using a simple __traffic light__ system for categorising types of information __commonly__ found in schools and the classroom.
asset_prefix: fdg45z
---
{% include lead.md %}

## Introduction

This isn't intended to be an exhaustive list but is a good overview of the types of information found in schools and how they should be best handled to ensure data protection and confidentiality.

## Red

__High__{:.badge .high} confidentiality data (such as that listed below) should only be stored on a [secure system]({{ site.baseurl }}{% link _posts/2018-08-14-Google-Drive-Data-Protection.md %}), __encrypted__ both in transit and at rest. Access to this data should be secured by __two-factor logons__ and should only be given to __authorised users__ within your organisation, and to outside contractors/individuals only when necessary.

External users should also adhere to equivalent security practices (e.g. restricted access and two-factor logins). This type of data should not be removed from your systems and duplicated, unless under exceptional circumstances.

Most of the data below would typically be held within an __MIS system__, but there may be other sources, such as a __SEN Register__ or spreadsheet that would also be considered to contain highly confidential data.

+ __Personal__ Data (Staff, students, parents, contacts etc)
  + __Medical__ or __health__ information
  + __Dates of Birth__ and personal information (such as religious beliefs)
+ __Student__ Data
  + Sensitive __personal__ information, such as family/home situation
  + __SEND__ information
  + Pupil __UPNs__
  + __Passport__ or ID information
  + __In-Care__ details
  + __FSM__ details
  + __Telephone__ numbers or __personal email__ addresses
+ Parental Data
  + __Sensitive__ information, such as legal or financial data
+ __Web logs__ or Browsing Histories
  + Retention of these forms of data should only be undertaken for [specific purposes]({{ site.baseurl }}{% link _posts/2018-07-24-Traffic-Lights-for-Information.md %}), with details about this process clearly communicated to all users
{:.condensed}

## Amber

__Medium__{:.badge .medium} confidentiality data should only be stored on a __organisation__ system or device, __encrypted__ both in transit and at rest. Access to this data should be secured by __two-factor logons__.

This sort of data may be shared with third-party contractors, organisations and individuals where required for the fulfilment of services (e.g. trips and visits) but only where people have been informed (generally via data processing or consent forms).

Typically, medium confidentiality data may reside under __the control of individuals__ within the organisations (e.g. teacher markbooks in their Google Drive) rather than fully centralised systems.

+ __Personal__ Data (Staff, students, parents, contacts etc)
    + Trip contact forms and details
  + Emergency allergy or conditions that need to be widely known to ensure safety (e.g. peanut allergy, asthma, heart arrhythmia)
    + __Names__ and __addresses__
  + Emergency contact details, such as __Telephone__ numbers or __email__ addresses
+ Teacher __Markbooks__
    + Admission numbers / Student Identifiers (__except sensitive identifiers__ such as UPNs)
  + Names
  + Groups or Sets
  + Grades
  + Comments about academic progress
  + Brief markers about handling medical or SEND conditions (such as 'sit near front of class' or 'may need to leave the classroom urgently')
  + __Not__ details about actual SEND (brief non-specific markers) conditions or medical information
+ __Registers__ and Attendance Data
  + Names
  + Absence Codes
  + Parental letters containing sensitive, medical or personal information should be __treated as highly confidential__ information
{:.condensed}

## Green

__Low__{:.badge .low} confidentiality information should not contain any personal data at all. This means they can be stored on any device, and do not need any special handling or logons.

They can be __widely shared__ with other colleagues both inside and outside your organisation. __Continuity of access__ is more critical with this type of information (e.g. ensuring lesson plans are not lost when staff leave).

+ __Lesson Plans__ Data (Staff, students, parents, contacts etc)
  + Should __never refer to individuals__, if specific instructions are required for particular students, then this should be phrased generically (e.g. students with attention issues should be checked at frequent intervals to make sure they understand the task in hand)
+ __Teaching__ Materials
    + Handouts
  + Worksheets
  + Slides
  + Model answers for exams (with any personally identifying information redacted)
+ Departmental __Resources__
  + Workbooks
  + Equipment Lists
  + Experiment details
  + Safety and material handling procedures
{:.condensed}

## Applying

__Overlaying__ this information onto your documents is an __excellent way__ to ensure everyone knows what sort of information they are dealing with! You can use Google metadata and [this handy][1]{:target="_blank" rel="noopener"} Chrome Extension to do just that. Simply [install][2]{:target="_blank" rel="noopener"} it and __sign in__ with your Google Account. Then you can add tags to your documents to indicate __how confidential__ the information is with them.

  [1]: https://educ.io/extensions/tag-a-doc "Tag-A-Doc Chrome Extension"
  [2]: https://chrome.google.com/webstore/detail/tagadoc/ekniapbebejhamindielmdgpceijdpff "Install Tag-A-Doc"