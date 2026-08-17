<!-- =========================================================
     EDUCATION
     ========================================================= -->

{% if site.data.site_info.cv.education %}

<h2>Education</h2>

{% for item in site.data.site_info.cv.education %}

<div class="cv-entry">

  <strong>{{ item.degree }}</strong>

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
