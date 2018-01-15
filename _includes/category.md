{% assign page_title = site.data.meta[page.category].name %}
{% if site.data.meta[page.category].description %}{{ site.data.meta[page.category].description }}{% endif %}

{% if site.data.meta[page.category].image %}<img src="{{ site.baseurl }}/{{ site.data.meta[page.category].image }}"{% if site.data.meta[page.category].image_fallback %} onerror="this.src='{{ site.baseurl }}/{{ site.data.meta[page.category].image_fallback }}'; this.onerror=null;"{% endif %} alt="{{ site.data.meta[page.category].name }}">{% endif %}

{% for post in site.categories[page.category] %}

{::options parse_block_html="true" /}

<div class="post-lead">

  {% if forloop.first %}
## [ {{ post.title }} ]({{ post.url }})
  {% else %}
### [ {{ post.title }} ]({{ post.url }})
  {% endif %}
  {% if post.lead %}
{{ post.lead }}
  {% elsif post.content contains '<!--more-->' %}
{{ post.content | split:'<!--more-->' | first | strip_html }}
  {% elsif post == site.posts.first %}
{{ post.content | strip_html | truncatewords: 40 , "  .." }}
  {% else %}
{{ post.content | strip_html | truncatewords: 16 , "  .." }}
  {% endif %}
  
__{{ post.date | date_to_string }}__ ► {% for tag in post.tags %}[{{tag | capitalize}}]({{ site.baseurl }}/tags/#{{ tag|slugize }}){% unless forloop.last %}, {% endunless %}{% endfor %}
{:.finally}

</div>

{% endfor %}

{% assign snippets_by_category = site.snippets | where: "category", page.category | sort: "title"  %}
{% for snippet in snippets_by_category  %}

###### [{% if snippet.short_title %}{{ snippet.short_title }}{% else %}{{ snippet.title }}{% endif %}]({{ snippet.url }})
{% if snippet.lead %}{{ snippet.lead }}{% else %}{{ snippet.content | strip_html | truncatewords: 30 , " ..." }}{% endif %}
&nbsp;[Read More ...]({{ snippet.url }})
{:.post-lead}

{% endfor %}