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


  /* =========================================================
     SOURCE PUBLICATIONS
     ========================================================= */

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


  /* =========================================================
     BUILD PUBLICATIONS FOR EACH RESEARCH THEME
     ========================================================= */

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


      /*
       * Only include publications associated
       * with the current research theme.
       */

      if (
        themeIds.includes(themeId)
      ) {


        /*
         * Clone the publication so that the
         * hidden source remains unchanged.
         */

        const clone =
          publication.cloneNode(true);


        /* ===================================================
           REMOVE CURRENT THEME
           ===================================================

           The theme being used as the section heading
           should not also appear under:

           "Other relevant theme(s):"
        */

        clone
          .querySelectorAll(
            ".publication-theme"
          )
          .forEach(function(themeElement) {


            if (
              themeElement.dataset.themeId === themeId
            ) {

              themeElement.remove();

            }

          });


        /* ===================================================
           REMOVE EMPTY THEME LABEL
           ===================================================

           If the publication had only the current theme,
           there are no "other" themes to display.

           Therefore remove the entire theme container.

           This prevents:

           Other relevant theme(s):

           from appearing by itself.
        */

        const themeContainer =
          clone.querySelector(
            ".publication-themes"
          );


        if (themeContainer) {


          const remainingThemes =
            themeContainer.querySelectorAll(
              ".publication-theme"
            );


          if (
            remainingThemes.length === 0
          ) {

            themeContainer.remove();

          }

        }


        /* ===================================================
           ADD PUBLICATION
           =================================================== */

        themeList.appendChild(
          clone
        );

      }

    });

  });

});

</script>
