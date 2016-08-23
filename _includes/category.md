{% assign page_title = site.data.meta[page.category].name %}
{% if site.data.meta[page.category].description %}{{ site.data.meta[page.category].description }}{% endif %}
{% if site.data.meta[page.category].image %}{% assign image = site.data.meta[page.category].image %}{% include {{image}} %}{% endif %}
{% for post in site.categories[page.category] %}
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
{{ post.date | date_to_string }} ► {% for tag in post.tags %}[{{tag | capitalize}}]({{ site.baseurl }}tags/#{{ tag|slugize }}){% unless forloop.last %}, {% endunless %}{% endfor %}
{% endfor %}