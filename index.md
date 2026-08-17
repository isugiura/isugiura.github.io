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

<div class="cv-entry">

  <strong>
    {{ item.degree }}
  </strong>

  <div>
    {{ item.institution }}
  </div>

  {% if item.years %}
  <div>
    {{ item.years }}
  </div>
  {% endif %}

  {% if item.details %}
  <p>
    {{ item.details }}
  </p>
  {% endif %}

</div>

{% endfor %}

{% endif %}
