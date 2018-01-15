---
layout: page
permalink: /snippets/
title: Snippets
lead: Code snippets, short examples & helpful explanations.
image: img/snippets.svg
image_fallback: img/snippets.png
---
{% include lead.md %}

{% assign categories = site.snippets | map: "category" | uniq %}
{% for category in categories %}
## {{ site.data.meta[category].name }}
{% if site.data.meta[category].description %}_{{ site.data.meta[category].description }}_{% endif %}
{% assign snippets_by_category = site.snippets | where: "category", category | sort: "title"  %}
{% for snippet in snippets_by_category  %}

###### [{% if snippet.short_title %}{{ snippet.short_title }}{% else %}{{ snippet.title }}{% endif %}]({{ snippet.url }})
{% if snippet.lead %}{{ snippet.lead }}{% else %}{{ snippet.content | strip_html | truncatewords: 30 , " ..." }}{% endif %}
&nbsp;[Read More ...]({{ snippet.url }})
{:.post-lead}
{% endfor %}

{% unless forloop.last %}
* * *
{% endunless %}

{% endfor %}