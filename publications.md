---
layout: default
title: Publications
permalink: /publications/
---

<h1>Publications</h1>


<div class="publication-tabs">

  <button
    class="publication-tab active"
    data-view="year-view"
  >
    By Year
  </button>

  <button
    class="publication-tab"
    data-view="theme-view"
  >
    By Research Theme
  </button>

</div>


<!-- =========================================================
     BY YEAR
     ========================================================= -->

<div
  id="year-view"
  class="publication-view active"
>

  <!-- Hidden source bibliography -->

  <div
    id="year-publication-source"
    style="display: none;"
  >

    {% bibliography %}

  </div>


  <div id="year-publication-lists">

    <!-- SUBMITTED -->

    <section class="publication-status-section">

      <h2 class="publication-year">
        Submitted
      </h2>

      <div
        class="publication-status-list"
        data-status="submitted"
      >
      </div>

    </section>


    <!-- IN PREPARATION -->

    <section class="publication-status-section">

      <h2 class="publication-year">
        In Preparation
      </h2>

      <div
        class="publication-status-list"
        data-status="in-preparation"
      >
      </div>

    </section>


    <!-- PUBLISHED YEARS -->

    <div id="year-sections"></div>

  </div>

</div>

<!-- =========================================================
     BY RESEARCH THEME
     ========================================================= -->

<div
  id="theme-view"
  class="publication-view"
>

  <!-- Hidden source bibliography -->

  <div
    id="theme-publication-source"
    style="display: none;"
  >

    {% bibliography %}

  </div>


  <!-- Theme publications will be inserted here -->

  <div id="theme-publication-lists">

    {% for theme_pair in site.data.themes %}

      {% assign theme_id = theme_pair[0] %}
      {% assign theme = theme_pair[1] %}

      <section
        class="publication-theme-section"
        id="publication-theme-{{ theme_id }}"
      >

        <h2 class="publication-theme-heading">
          {{ theme.name }}
        </h2>

        <div
          class="publication-theme-list"
          data-theme-id="{{ theme_id }}"
        >
        </div>

      </section>

    {% endfor %}

  </div>

</div>


<script>

/* =========================================================
   PUBLICATION VIEW SWITCHER
   ========================================================= */

document
  .querySelectorAll(".publication-tab")
  .forEach(function(button) {

    button.addEventListener("click", function() {

      document
        .querySelectorAll(".publication-tab")
        .forEach(function(tab) {
          tab.classList.remove("active");
        });

      document
        .querySelectorAll(".publication-view")
        .forEach(function(view) {
          view.classList.remove("active");
        });

      button.classList.add("active");

      document
        .getElementById(button.dataset.view)
        .classList.add("active");

    });

  });


/* =========================================================
   ORGANIZE PUBLICATIONS BY RESEARCH THEME
   ========================================================= */

document.addEventListener("DOMContentLoaded", function() {

  const source = document.getElementById(
    "theme-publication-source"
  );

  const publications = source.querySelectorAll(
    ".publication"
  );

  const themeLists = document.querySelectorAll(
    ".publication-theme-list"
  );


  themeLists.forEach(function(themeList) {

    const themeId = themeList.dataset.themeId;


    publications.forEach(function(publication) {

      const themeIds = publication
        .dataset
        .themeIds
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
