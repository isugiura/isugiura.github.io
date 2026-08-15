---
layout: default
title: Research Interests
permalink: /research-interests/
---

<h1>Research Interests</h1>


<!-- =========================================================
     HIDDEN PUBLICATION SOURCE
     ========================================================= -->

<div
  id="research-publication-source"
  style="display: none;"
>
  {% bibliography %}
</div>


<!-- =========================================================
     RESEARCH THEMES
     ========================================================= -->

{% for theme_pair in site.data.themes %}

  {% assign theme_id = theme_pair[0] %}
  {% assign theme = theme_pair[1] %}


  <section
    class="research-interest"
    id="research-theme-{{ theme_id }}"
  >

    <h2>
      {{ theme.theme-name }}
    </h2>


    <p>
      {{ theme.description }}
    </p>


    <details class="research-publications">

      <summary>
        Publications
      </summary>


      <div
        class="research-publications-list"
        data-theme-id="{{ theme_id }}"
      >
      </div>

    </details>

  </section>

{% endfor %}


<!-- =========================================================
     JAVASCRIPT
     ========================================================= -->

<script>

document.addEventListener("DOMContentLoaded", function() {


  const source =
    document.getElementById(
      "research-publication-source"
    );


  const publications =
    source.querySelectorAll(
      ".publication"
    );


  const themeLists =
    document.querySelectorAll(
      ".research-publications-list"
    );


  themeLists.forEach(function(themeList) {


    const themeId =
      themeList.dataset.themeId;


    publications.forEach(function(publication) {


      const themeIds =
        (
          publication.dataset.themeIds || ""
        )
        .split(",")
        .map(function(theme) {

          return theme.trim();

        });


      if (themeIds.includes(themeId)) {


        themeList.appendChild(
          publication.cloneNode(true)
        );

      }

    });

  });

});

</script>
