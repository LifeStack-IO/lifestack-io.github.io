---
layout: page
title: Home
permalink: /
---

Welcome to __LifeStack__{:.brand} We write _clear_, _helpful_ and _informative_ content to help you get the very best from technology. Below are our most __recent posts__, including [articles]({{ site.baseurl }}all/article), [tutorials]({{ site.baseurl }}all/tutorial), [snippets]({{ site.baseurl }}snippets) & [links]({{ site.baseurl }}links). Looking for something else? You can find __everything__ in the [archive](/all), or by clicking on any [tags](/tags). Or take a moment to [read more]({{ site.baseurl }}about) about our vision, approach and philosophy!
{:.lead}

{% assign _recent = "" | split: "" %}{% assign _recent_snippets = site.snippets | sort: 'date' | reverse | limit:10 %}{% assign _recent_posts = site.posts | sort: 'date' | reverse | limit:10 %}{% assign _recent_links = site.links | sort: 'date' | reverse | limit:10 %}{% for _snippet in _recent_snippets %}{% assign _recent = _recent | push: _snippet %}{% endfor %}{% for _post in _recent_posts %}{% assign _recent = _recent | push: _post %}{% endfor %}{% for _link in _recent_links %}{% assign _recent = _recent | push: _link %}{% endfor %}{% assign _recent = _recent | sort: 'date' | reverse | limit:10 %}{% assign categories = _recent | map: "category" | uniq %}{% for category in categories %}
{% assign posts_by_categories = _recent | where: "category", category %}

###### [{{ site.data.meta[category].name }}]({{ site.baseurl }}all/{{ category }})

{% for post in posts_by_categories limit:3 %}
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

__{{ post.date | date_to_string }}__ ► {% for tag in post.tags %}[{{tag | capitalize}}]({{ site.baseurl }}/tags/#{{ tag|slugize }}){% unless forloop.last %}, {% endunless %}{% endfor %}
{:.finally}

{% endfor %}

{% if site.data.meta[category].lead_image %}<img src="{{ site.baseurl }}/{{ site.data.meta[category].lead_image }}"{% if site.data.meta[category].image_fallback %} onerror="this.src='{{ site.baseurl }}/{{ site.data.meta[category].image_fallback }}'; this.onerror=null;"{% endif %} alt="{{ site.data.meta[category].name }}">{% endif %}

{% unless forloop.last %}
* * *
{% endunless %}
{% endfor %}

###### &copy; {% capture year %}{{ site.time | date: '%Y' }}{% endcapture %}{% if year != site.launched %}{{ site.launched }}-{% endif%}{{ year }} [{{site.author.name}}]({{site.baseurl}}about/#copyright--licensing)