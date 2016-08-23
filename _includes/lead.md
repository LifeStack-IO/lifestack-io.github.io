* Table of Contents
{:toc}

{% if page.lead %}{{ page.lead | markdownify }}{% endif %}
{% if page.image %}<img class="lead_image" src="{{page.image}}" alt="{% if page.image_alt %}{{page.image_alt}}{% else %}Page Lead Image{% endif %}" />{% endif %}