---
layout: default
title: Home
---

# About Me

{% if site.data.site_info.profile.bio %}

{% for paragraph in site.data.site_info.profile.bio %}

{{ paragraph }}

{% endfor %}

{% endif %}


## Research Interests

{% if site.data.site_info.profile.research_interests %}

{% for interest in site.data.site_info.profile.research_interests %}
- {{ interest }}
{% endfor %}

{% endif %}


## Education

{% if site.data.site_info.cv.education %}

{% for item in site.data.site_info.cv.education %}

**{{ item.degree }}**

{{ item.institution }}{% if item.location %} · {{ item.location }}{% endif %}

{% if item.years %}
{{ item.years }}
{% endif %}

{% if item.details %}
{{ item.details }}
{% endif %}

{% endfor %}

{% endif %}
