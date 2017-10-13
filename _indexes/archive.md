---
layout: page
title: Archive
permalink: /all/
lead: Delve into the archive. Every post, every thought, article, tutorial and coding example right here, at your fingertips.
image: img/archive.svg
image_fallback: img/archive.png
---
{% include lead.md %}

{% assign _all = "" | split: "" %}{% for _snippet in site.snippets %}{% assign _all = _all | push: _snippet %}{% endfor %}{% for _post in site.posts %}{% assign _all = _all | push: _post %}{% endfor %}{% for _link in site.links %}{% assign _all = _all | push: _link %}{% endfor %}{% assign _all = _all | sort: 'date' | reverse %}{% for post in _all %}
{% unless post.next %}
#### {{ post.date | date: "%B, %Y" }}
{% else %}
{% capture year %}{{ post.date | date: '%Y %b' }}{% endcapture %}
{% capture nyear %}{{ post.next.date | date: '%Y %b' }}{% endcapture %}
{% if year != nyear %}
#### {{ post.date | date: "%B, %Y" }}
{% endif %}
{% endunless %}
{% assign d = post.date | date: "%-d" %}
* [ {{ post.title }} ]({{ root_url }}{{ post.url }})
{% if post.lead %} -- {{ post.lead }}{% endif %}
{% unless forloop.last %}
* * *
{% endunless %}
{% endfor %}