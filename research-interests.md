---
layout: default
title: Research Interests
permalink: /research-interests/
---

<h1>Research Interests</h1>

{% for theme_pair in site.data.themes %}

  {% assign theme_id = theme_pair[0] %}
  {% assign theme = theme_pair[1] %}

  <section
    class="research-interest"
    id="{{ theme_id }}"
  >

    <h2>
      {{ theme.name }}
    </h2>

    <p>
      {{ theme.description }}
    </p>

    <details class="research-publications">

      <summary>
        Publications
      </summary>

      <div class="research-publications-list">

        {% bibliography --query "@*[theme_id~=climate-variability]" %}
      
      </div>

    </details>

  </section>

{% endfor %}
