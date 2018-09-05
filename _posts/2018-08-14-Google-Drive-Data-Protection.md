---
title: Protecting Data with Google Drive
short_title: Google Drive Data Protection
layout: post
author:
  name: jd
category: article
tags:
- education
- google
- storage
published: true
lead: How to best __protect__ and __secure__ confidential data using Google Drive and Google Apps / G-Suite
asset_prefix: lkp11k
---
{% include lead.md %}

## Introduction

[Perfect security][1]{:target="_blank" rel="noopener"} doesn't exist, but __better__ security does. Better data protection means [thinking pragmatically][2]{:target="_blank" rel="noopener"} about the [likely threats][28]{:target="_blank" rel="noopener"} that you face, and then doing something to mitigate the chances of them happening.

This is a __common sense guide__ to protecting data, with a particular focus on the challenges faced in education. It is structured around using [Google Drive][3]{:target="_blank" rel="noopener"} to protect your data, as part of the [G-Suite][4]{:target="_blank" rel="noopener"} for [Business][5]{:target="_blank" rel="noopener"} (Basic, Business or Enterprise), [Non-Profit][6]{:target="_blank" rel="noopener"} or [Education][7]{:target="_blank" rel="noopener"} plans.

While __Google Drive__ is likely going to be the most __secure option__ for most organisations, many of these principles will apply to other cloud storage systems too. Why is it __so secure__? Read on to find out ...

+ Google [encrypts][27]{:target="_blank" rel="noopener"} your data in when it is on the move (in transit) and when stored (at rest)
+ Supports 2-Factor authentication, which is essential to help protect your accounts
+ Wide device support and allows remote data/account removal on secure devices (e.g. tablets, phones, Chromebooks)
+ Allows simple sharing rather than relying on emailing files as attachments
+ Robust and straightforward auditing and logging, to see who has accessed data

## Security

We are taking information security to mean how __well protected__ your data is from __unauthorised access__ and __disclosure__. Typically the potential risks are your information storage system (servers, laptops, databases etc.) being broken into or your credentials being impersonated/stolen to gain access to your systems.

### Intrusion

Securing systems, which are repositories for information, has become a constant process of staying ahead of vulnerabilities. Any software and systems are designed and implemented __by people__ and by that very nature, is potentially insecure and flawed. Mistakes are __always made__, whether they are spotted or not. When these mistakes come to light (as they inevitably do), there is a vulnerability in your system. This could be from design, coding or configuration, but it will often open the door to your information. It is vital to keep on top of these vulnerability disclosures and ensure your any system upon which you store data is well-configured and stays patched against potential problems.

For organisations of any size, and __particularly schools__, this is an __onerous task__ and one that frequently is not done as diligently as we would like! A large number of security breaches and intrusions are caused by old system flaws that have not been patched. Hosting your data in the cloud isn't a solution to this problem, but you have to be pragmatic about this; who has more resources to ensure systems are kept patched, well-configured and secure? Is it you? Or is it a multi-national cloud provider, such as Google.

Of course, these larger providers are a __much more attractive__ target for people who want to break into information systems, but they also have much better defences and a __lot more__ money and time to throw into the fight. You might think that your organisation is too small for someone to spend the time targetting it, and you are probably right. But most attacks now are __automated__ and they are __indiscriminate__ and [destructive][9]. They don't assess the value of a target before trying to compromise it; they try to exploit known vulnerabilities. Organisations of all sizes are caught up in the [collatoral damanage][10]{:target="_blank" rel="noopener"}. [Security through obscurity][8]{:target="_blank" rel="noopener"} is really no security at all.

Putting your information into a well-respected cloud storage provider helps __minimise the likelhood__ of your information being exposed through an intrusive attack. The scale of these systems means that security monitoring is much more pro-active than you could ever hope to achieve, and draws upon a high-level of expertise that does not exist in most organisations.

### Credential Misuse

This is probably the __most common cause__ of unauthorised information access for most organisations. Security through passwords is a fundamentally [weak model][11]{:target="_blank" rel="noopener"}, not because passwords are themselves a security risk, but how we [manage them][12]{:target="_blank" rel="noopener"} is. There is a shocking rate of password re-use amongst most users, and this creates a __huge security problem__. Google spends millions on ensuring their systems are secure, but that doesn't matter at all if you have signed up to another __weaker__ site or app using the same username/password that you use for your Google account. All it takes is one intrusion into a less secure system, and your username/password is going to be available for all to see and misuse.

If you are responsible for managing confidential or personal information (and almost everyone who works in education is), then you must ensure you have secured your accounts with __2-factor authentication__. If you don't, __you are being negligent__. Two-factor authentication, often abbreviated as [2FA][13]{:target="_blank" rel="noopener"}, requires the use of two tokens when you log on. A password is something that you know; the second token is from something you have. Typically this takes the form of a numerical code generated by an authenticator app (on your phone or tablet), a code delivered by SMS to your phone or (even better) a [USB security key][15]{:target="_blank" rel="noopener"}. On the Google platform, this form of authentication is __free to use__ and takes just a __few seconds to setup__. If you are not using, __stop reading__ right now and [go do it][14]{:target="_blank" rel="noopener"}.

Using 2FA to secure your account helps to __instantly minimise__ the chance that your credentials will be misused. By requiring another piece of information, generated from something that you have, an attacker cannot gain access to your account and data with just your username and password. By doing this, you __massively increase the security__ of your information in a single act.

### Device Loss

Lost USB keys, laptops left on trains, hard drives not wiped before computers are sold. These are all __horror stories__ of data loss, and they are worryingly familiar. We all lose things, expensive electronics are always an attractive target for theft, so what can we do about this to improve our information security?

Like credential security, you can make significant improvements very simply:

1. __Don't use portable media__ devices, such as __external hard-drives__ or __USB keys__ for personal or confidential information.

   There is no need in the modern connected world to rely on these sort of tools. Stick your files on Google Drive, and access them on all your devices, wherever you are. Ensure you have a secure password/PIN on your phone and tablet, and a strong password on your computer.
   
   The convenience of this sort of access will help __stop you copying essential files__ to insecure portable devices, and this will increase security. If you are not sure what type of educational information is personal or confidential, have a look at our [handy guide]({{ site.baseurl }}{% link _posts/2018-07-24-Traffic-Lights-for-Information.md %}).

2. __Only use devices which natively encrypt__ your data.

   You cannot get away from the fact that even with the best cloud service, data is going to be __stored__ and __cached__ on your local device. Encryption at rest is essential. This means that if you lose physical control of your device, your data is still encrypted, generally with a key that is derived from your account credentials.
   
   Without this encryption, it is trivial to access any data on a device, including confidential information! If you use __windows servers__ or __laptops__, you need to ensure they have been encrypted properly using a full-disk encryption system such as [Bitlocker][18]{:target="_blank" rel="noopener"}.

If you use [Chromebooks][16]{:target="_blank" rel="noopener"} to access your [data offline][19]{:target="_blank" rel="noopener"} then you will be __benefiting__ from their native (and default) __encryption__, making them an __extremely secure device__ to access your data from, without requiring any extra management or technical configuration time. Other tablet/phone devices, such as those running [Android 7.0][20]{:target="_blank" rel="noopener"}/[IOS 4][21]{:target="_blank" rel="noopener"} (or later) also natively encrypt data - protecting them in case they are lost. Leaving confidential data in an unencrypted state is just inviting trouble.

Should you discover you have lost your mobile device, you can __remove these devices__ from accessing your Google account from your [recently used devices][26]{:target="_blank" rel="noopener"} page. Then tell your organisations Google administrator (usually a senior official or IT Support team) that you have lost a device. They should be able to __remotely clear__ any cached email or cloud files from the device too.

## Privacy

Now you have dealt with the most critical security issues by __uploading your data__ to a secure cloud provider, __secured your accounts__ with 2FA, and ensured that any device you use to access or store data __is encrypted__. Then you can turn your attention to ensuring that only the __correct__ people have access to your protected information.

One of the unique features of modern cloud storage platforms is that they allow users to take control of data sharing in ways they haven't done in the past. This empowers them to work more collaboratively, but this __power and responsibility__ means they may need __time and guidance__ to become comfortable exercising it. It is essential that all your users know __what information__ is __personal__ or __confidential__, and with whom they can share it with. They must be confident in being able to check who has access to data, and how to restrict access if need be.

### Sharing

An __emailed file__ is a __lost file__. Once a file has been attached to an email and sent, you lose any control over it. Confidential, personal or even important data __should never__ be sent as an __email attachment__. The recipient of the email can forward it to any third party, or they can start to make changes to the file that won't be shared back with you. Granting others access to your file is a far better way to communicate information. Ideally, you should [share][25]{:target="_blank" rel="noopener"} with a named account (e.g. an email address), but you can also use link sharing if you need to you. __Anything is better__ than attaching! Remember that if you make a mistake with sharing, and include someone who actually shouldn't have access, you can always rescind a share but recalling an email with an attachment is almost always impossible.

### Auditing

A [traffic light system]({{ site.baseurl }}{% link _posts/2018-07-24-Traffic-Lights-for-Information.md %}) to classify information security is a useful tool to help guide users in making these decisions. You can even overlay these [traffic-light tags][22]{:target="_blank" rel="noopener"} onto your Google Docs, Sheets and Slides to help ensure everyone knows that sort of data they are dealing with. You can also [audit sharing permissions][23]{:target="_blank" rel="noopener"} or (as an administrator) [view audit logs][24]{:target="_blank" rel="noopener"} to check __exactly who__ has access to your data, as well as who has opened and edited it.

## Continuity

Ensuring access to valuable data is __vital__. If you are keeping your files on a single server, even with a __reliable backup solution__, then you are putting the continuity of access at risk. To recover those files you may need to purchase a new server, wait for it to be delivered, build it, configure it and then restore the backup. If your financial system or critical supplier information was on that server, then the job is even harder. All this __takes time__.

Well-designed cloud services will likely have significantly less downtime that this, even in the worst case scenario. On any secure client platform, you can cache files for offline access. This technique can be used to ensure you have access to critical information, such as essential __medical__, __contact__ or __technical__ data.

## Advice

+ Store your files in a __secure__ and well-respected __cloud service__
+ Enable __2-Factor Authentication__ on your Google Account (any every other account you can too!)
+ __Don't use__ portable media devices to store files
+ To access your files, use a __Chromebook__, modern Android tablet, iPad, iPhone or Windows device __with BitLocker enabled__
+ __Never email files__ as attachments
+ Take the time to __learn__ how to confidently __share files__, how to check who files are shared with and the best ways to audit sharing

- - -

  [1]: https://www.forbes.com/sites/forbestechcouncil/2018/03/27/the-illusion-of-perfect-cybersecurity/ "The Illusion Of Perfect Cybersecurity"
  [2]: https://www.ncsc.gov.uk/blog-post/not-perfect-better-improving-security-one-step-time "Not perfect, but better: improving security one step at a time"
  [3]: https://en.wikipedia.org/wiki/Google_Drive "Google Drive"
  [4]: https://gsuite.google.com/ "Get Gmail, Docs, Drive, and Calendar for business"
  [5]: https://en.wikipedia.org/wiki/Google_Drive "Compare G Suite Editions"
  [6]: https://www.google.com/nonprofits/products/ "Google for Non-Profits"
  [7]: https://edu.google.com "Google for Education"
  [8]: https://en.wikipedia.org/wiki/Security_through_obscurity "Security through Obscurity"
  [9]: https://www.wired.com/story/notpetya-cyberattack-ukraine-russia-code-crashed-the-world/ "The Untold Story of NotPetya"
  [10]: https://en.wikipedia.org/wiki/WannaCry_ransomware_attack "WannaCry Ransomware Attach"
  [11]: https://www.securitymagazine.com/articles/88804-beyond-passwords-how-security-can-improve-identity-in-2018 "Beyond Passwords"
  [12]: https://www.rit.edu/security/content/benefits-using-password-manager "Benefits of using a Password Manager"
  [13]: https://en.wikipedia.org/wiki/Multi-factor_authentication "Multi-factor authentication"
  [14]: https://www.google.com/landing/2step/ "Stronger security for your Google Account"
  [15]: https://www.yubico.com/ "Yubikey - Strong 2nd Token Authentication"
  [16]: https://support.google.com/chromebook/answer/3438631 "Chromebook security"
  [17]: https://www.cnet.com/news/how-google-chromebooks-became-the-go-to-laptop-for-security-experts/ "https://www.cnet.com/news/how-google-chromebooks-became-the-go-to-laptop-for-security-experts/"
  [18]: https://en.wikipedia.org/wiki/BitLocker "BitLocker"
  [19]: https://support.google.com/chromebook/answer/2809731 "Work on Google Drive files offline on your Chromebook"
  [20]: https://source.android.com/security/encryption/#file-based "Android Encryption"
  [21]: https://ssd.eff.org/en/module/how-encrypt-your-iphone "How to: Encrypt Your iPhone"
  [22]: https://educ.io/extensions/tag-a-doc "Tag-A-Doc Chrome Extension"
  [23]: https://educ.io/tutorials/folders/audit-permissions "Auditing Sharing Permissions in Google Drive"
  [24]: https://support.google.com/a/answer/4579696 "Drive audit log"
  [25]: https://support.google.com/drive/answer/2494822 "Share files from Google Drive"
  [26]: https://myaccount.google.com/device-activity "Recently Used Devices"
  [27]: https://support.google.com/googlecloud/answer/6056693 "Does Google encrypt my data?"
  [28]: https://www.theregister.co.uk/2018/09/04/cckup_over_conspiracy_tops_selfreported_data_breaches/ "Cock-ups, rather than conspiracies, top self-reported data breaches"