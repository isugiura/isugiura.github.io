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


    <!-- =====================================================
         RELEVANT PUBLICATIONS TOGGLE
         ===================================================== -->

    <details class="research-publications">

      <summary>
        Relevant publications
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

        })
        .filter(function(theme) {

          return theme !== "";

        });


      /*
       * Only include publications associated
       * with the current research theme.
       */

      if (
        !themeIds.includes(themeId)
      ) {

        return;

      }


      /* =====================================================
         CLONE PUBLICATION
         =====================================================

         Keep the hidden bibliography source unchanged.
      */

      const clone =
        publication.cloneNode(true);


      /* =====================================================
         REMOVE CURRENT THEME
         =====================================================

         The theme being used as the section heading
         should not also appear as an "other" theme.
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


      /* =====================================================
         HANDLE OTHER RELEVANT THEMES
         =====================================================

         If other themes remain, change the label to:

         Other relevant theme(s):

         If no other themes remain, remove the entire
         theme container, including the label.
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


          /*
           * Publication has only the current theme.
           *
           * Remove the entire theme container so
           * "Other relevant theme(s):" does not appear.
           */

          themeContainer.remove();


        } else {


          /*
           * Publication has additional themes.
           *
           * Change the label from:
           *
           * Relevant research theme(s):
           *
           * to:
           *
           * Other relevant theme(s):
           */

          const themeLabel =
            themeContainer.querySelector(
              ".publication-theme-label"
            );


          if (themeLabel) {

            themeLabel.textContent =
              "Other relevant theme(s):";

          }

        }

      }


      /* =====================================================
         ADD PUBLICATION
         ===================================================== */

      themeList.appendChild(
        clone
      );

    });

  });

});

</script>
