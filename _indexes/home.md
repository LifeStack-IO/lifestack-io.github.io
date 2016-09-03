---
layout: page
title: Home
permalink: /
---

_{{ site.description }}_

The most __recent posts__ are below, but you can find everything in the [archive](/archive). All the content is [tagged](/tags) but you can also browse [links](/links) and [snippets](/snippets) too.

{% assign categories = site.posts | map: "category" | uniq %}
{% for category in categories %}
{% assign posts_by_categories = site.posts | where: "category", category %}

###### [{{ site.data.meta[category].name }}]({{ site.baseurl }}all/{{ category }})

{% for post in posts_by_categories limit:2 %}
{% if forloop.first %}
## [ {{ post.title }} ]({{ post.url }})
{% else %}
### [ {{ post.title }} ]({{ post.url }})
{% endif %}
{% if post.lead %}
  {{ post.lead | strip_html }}
{% elsif post.content contains '<!--more-->' %}
  {{ post.content | split:'<!--more-->' | first | strip_html }}
{% elsif post == site.posts.first %}
  {{ post.content | strip_html | truncatewords: 40 , "  .." }}
{% else %}
  {{ post.content | strip_html | truncatewords: 16 , "  .." }}
{% endif %}

__{{ post.date | date_to_string }}__ ► {% for tag in post.tags %}[{{tag | capitalize}}]({{ site.baseurl }}tags/#{{ tag|slugize }}){% unless forloop.last %}, {% endunless %}{% endfor %}
{:.finally}

{% endfor %}

{% if site.data.meta[category].lead_image %}<img src="{{ site.baseurl }}{{ site.data.meta[category].lead_image }}"{% if site.data.meta[category].image_fallback %} onerror="this.src='{{ site.baseurl }}{{ site.data.meta[category].image_fallback }}'; this.onerror=null;"{% endif %} alt="{{ site.data.meta[category].name }}">{% endif %}

{% unless forloop.last %}
* * *
{% endunless %}
{% endfor %}

###### &copy; {% capture year %}{{ site.time | date: '%Y' }}{% endcapture %}{% if year != site.launched %}{{ site.launched }}-{% endif%}{{ year }} [{{site.author.name}}]({{site.baseurl}}about/#copyright--licensing)