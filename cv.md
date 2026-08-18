---
layout: default
title: CV
permalink: /cv/
---------------

<h1>Curriculum Vitae</h1>

<!-- =========================================================
     DOWNLOAD CV
     ========================================================= -->

{% if site.data.site_info.cv.document %}

<p>
  View
  <a
    href="{{ site.data.site_info.cv.document | relative_url }}"
    target="_blank"
    rel="noopener"
  >
    my full CV
  </a>
  <span class="cv-last-updated">
    (last updated: {{ site.data.site_info.cv.last_updated }})
  </span>
</p>

{% endif %}

<!-- =========================================================
     EDUCATION
     ========================================================= -->

{% if site.data.site_info.cv.education %}

<h2 class="cv-section-heading">
  Education
</h2>

{% for item in site.data.site_info.cv.education %}

<div class="cv-entry">

  <strong>
    {{ item.degree }}
  </strong>

  <div>
    <em>{{ item.institution }}</em>

```
{% if item.year %}
  <span class="cv-separator">·</span>
  {{ item.year }}
{% endif %}
```

  </div>

{% if item.location %}

  <div>
    {{ item.location }}
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

<!-- =========================================================
     RESEARCH EXPERIENCE
     ========================================================= -->

{% if site.data.site_info.cv.research_experience %}

<h2 class="cv-section-heading">
  Research Experience
</h2>

{% for item in site.data.site_info.cv.research_experience %}

<div class="cv-entry">

  <strong>
    {{ item.position }}
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

  <ul>

```
{% for detail in item.details %}

<li>
  {{ detail }}
</li>

{% endfor %}
```

  </ul>

{% endif %}

</div>

{% endfor %}

{% endif %}

<!-- =========================================================
     TEACHING
     ========================================================= -->

{% if site.data.site_info.cv.teaching %}

<h2 class="cv-section-heading">
  Teaching
</h2>

{% for item in site.data.site_info.cv.teaching %}

<div class="cv-entry">

  <strong>
    {{ item.position }}
  </strong>

{% if item.course %}

  <div>
    {{ item.course }}
  </div>
  {% endif %}

  <div>
    {{ item.institution }}
    {% if item.years %}
      · {{ item.years }}
    {% endif %}
  </div>

{% if item.details %}

  <ul>

```
{% for detail in item.details %}

<li>
  {{ detail }}
</li>

{% endfor %}
```

  </ul>

{% endif %}

</div>

{% endfor %}

{% endif %}

<!-- =========================================================
     AWARDS AND HONORS
     ========================================================= -->

{% if site.data.site_info.cv.awards %}

<h2 class="cv-section-heading">
  Awards and Honors
</h2>

{% for item in site.data.site_info.cv.awards %}

<div class="cv-entry">

  <strong>
    {{ item.name }}
  </strong>

{% if item.institution or item.year %}

  <div>

```
{% if item.institution %}
  <em>{{ item.institution }}</em>
{% endif %}

{% if item.institution and item.year %}
  <span class="cv-separator">·</span>
{% endif %}

{% if item.year %}
  {{ item.year }}
{% endif %}
```

  </div>
  {% endif %}

</div>

{% endfor %}

{% endif %}

<!-- =========================================================
     GRANTS
     ========================================================= -->

{% if site.data.site_info.cv.grants %}

<h2 class="cv-section-heading">
  Grants
</h2>

{% for item in site.data.site_info.cv.grants %}

<div class="cv-entry">

  <strong>
    {{ item.title }}
  </strong>

{% if item.agency %}

  <div>
    {{ item.agency }}
  </div>
  {% endif %}

{% if item.role %}

  <div>
    {{ item.role }}
  </div>
  {% endif %}

{% if item.amount %}

  <div>
    {{ item.amount }}
  </div>
  {% endif %}

{% if item.years %}

  <div>
    {{ item.years }}
  </div>
  {% endif %}

{% if item.details %}

  <ul>

```
{% for detail in item.details %}

<li>
  {{ detail }}
</li>

{% endfor %}
```

  </ul>

{% endif %}

</div>

{% endfor %}

{% endif %}

<!-- =========================================================
     PRESENTATIONS
     ========================================================= -->

{% if site.data.site_info.cv.presentations %}

<h2 class="cv-section-heading">
  Presentations
</h2>

{% for item in site.data.site_info.cv.presentations %}

<div class="cv-entry">

  <strong>
    {{ item.title }}
  </strong>

{% if item.venue %}

  <div>
    {{ item.venue }}
  </div>
  {% endif %}

{% if item.location %}

  <div>
    {{ item.location }}
  </div>
  {% endif %}

{% if item.year %}

  <div>
    {{ item.year }}
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

<!-- =========================================================
     PROFESSIONAL MEMBERSHIPS
     ========================================================= -->

{% if site.data.site_info.cv.professional_memberships %}

<h2 class="cv-section-heading">
  Professional Memberships
</h2>

{% for item in site.data.site_info.cv.professional_memberships %}

<div class="cv-entry">

  <strong>
    {{ item.organization }}
  </strong>

{% if item.role %}

  <div>
    {{ item.role }}
  </div>
  {% endif %}

{% if item.years %}

  <div>
    {{ item.years }}
  </div>
  {% endif %}

</div>

{% endfor %}

{% endif %}

<!-- =========================================================
     SERVICE
     ========================================================= -->

{% if site.data.site_info.cv.service %}

<h2 class="cv-section-heading">
  Service
</h2>

{% for item in site.data.site_info.cv.service %}

<div class="cv-entry">

  <strong>
    {{ item.role }}
  </strong>

{% if item.organization %}

  <div>
    {{ item.organization }}
    {% if item.years %}
      · {{ item.years }}
    {% endif %}
  </div>
  {% endif %}

{% if item.details %}

  <ul>

```
{% for detail in item.details %}

<li>
  {{ detail }}
</li>

{% endfor %}
```

  </ul>

{% endif %}

</div>

{% endfor %}

{% endif %}

<!-- =========================================================
     OUTREACH
     ========================================================= -->

{% if site.data.site_info.cv.outreach %}

<h2 class="cv-section-heading">
  Outreach
</h2>

{% for item in site.data.site_info.cv.outreach %}

<div class="cv-entry">

  <strong>
    {{ item.activity }}
  </strong>

{% if item.organization %}

  <div>
    {{ item.organization }}
    {% if item.years %}
      · {{ item.years }}
    {% endif %}
  </div>
  {% endif %}

{% if item.location %}

  <div>
    {{ item.location }}
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
