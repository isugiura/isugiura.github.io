---
layout: default
title: Home
---

<h1>About Me</h1>


<!-- =========================================================
     BIO
     ========================================================= -->

{% if site.data.site_info.profile.bio %}

  {% for paragraph in site.data.site_info.profile.bio %}

    <p>
      {{ paragraph }}
    </p>

  {% endfor %}

{% endif %}


<!-- =========================================================
     RESEARCH INTERESTS
     ========================================================= -->

{% if site.data.site_info.profile.research_interests %}

  <h2>Research Interests</h2>

  <ul>

    {% for interest in site.data.site_info.profile.research_interests %}

      <li>
        {{ interest }}
      </li>

    {% endfor %}

  </ul>

{% endif %}


<!-- =========================================================
     EDUCATION
     ========================================================= -->

{% if site.data.site_info.cv.education %}

  <h2>Education</h2>

  {% for item in site.data.site_info.cv.education %}

    <div class="cv-entry">

      <strong>
        {{ item.degree }}
      </strong>

      <div>
        {{ item.institution }}

        {% if item.location %}
          · {{ item.location }}
        {% endif %}
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
