* Table of Contents
{:toc}

{% if page.lead %}{{ page.lead | markdownify }}{% endif %}
{% if page.image %}<img class="lead_image" src="{{ site.baseurl }}{{page.image}}"{% if page.image_fallback %} onerror="this.src='{{ site.baseurl }}{{ page.image_fallback }}'; this.onerror=null;"{% endif %} alt="{% if page.image_alt %}{{page.image_alt}}{% else %}Page Lead Image{% endif %}">{% endif %}