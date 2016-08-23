---
layout: page
title: Tags
permalink: /tags/
lead: An indexed collection of everything, arranged by tag to make it a little easier to find serendipity.
image: images/tags_header.svg
---
{% include lead.md %}

{% assign last_category = "" %}
{% assign sorted_links = site.links | sort: 'title' %}

{% for tag in site.data.meta %}

<!-- Get all the information about the Tag from the Meta file -->
{% assign tag_name = tag[0] %}
{% assign tag_title = tag[1].name %}
{% assign tag_desc = tag[1].description %}

<!-- This gets all the posts tagged with this tag -->
{% assign posts_by_tag = site.tags[tag_name] %}
{% assign posts_by_tag_size = posts_by_tag | size %}
{% if posts_by_tag and posts_by_tag_size > 0 %}{% assign has_posts = true %}{% else %}{% assign has_posts = false %}{% endif %}

<!-- This checks if any links are tagged with this tag -->
{% assign has_links = false %}
{% for link in site.links %}{% if link.tags contains tag_name %}{% assign has_links = true %}{% endif %}{% endfor %}

{% if has_posts or has_links %}

<!-- Add Tag Title Header (and ID) -->

### {{ tag_title }}
{: #{{ tag_name }}}

<!-- Add Tag Description -->
{% if tag_desc %}_{{tag_desc}}_{% endif %} 

{% if has_posts %}

{% assign posts_by_tag = posts_by_tag | sort: 'category' %}
{% assign posts_by_category = posts_by_tag | group_by:"category" %}
{% for category in posts_by_category %}

{% if site.data.meta[category.name].name != last_category%}
###### {{ site.data.meta[category.name].name }}
{% assign last_category = site.data.meta[category.name].name %}
{% endif %}

{% for post in category.items | sort: 'title' %}
[ {{ post.title }} ]({{ root_url }}{{ post.url }}){% if post.lead %} -- {{ post.lead }}{% endif %} ({{ post.date | date: "%b, %Y" }})
{% endfor %}

{% endfor %}
{% endif %}

{% if has_links %}

{% if "Links" != last_category%}
###### [Links](../links)
{% assign last_category = "Links" %}
{% endif %}

{% for link in sorted_links %}

{% if link.tags contains tag_name %}
[{{ link.title }}]({{ link.link }}){:target="_new"} - {{ link.content | strip_html | truncatewords: 10 , "" }}&nbsp;[...]({{ link.url }})
{% endif %}

{% endfor %}

{% endif %}

* * *  

{% endif %}

{% endfor %}