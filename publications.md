---
layout: default
title: Publications
permalink: /publications/
---

<h1>Publications</h1>


<style>
.publication-themes::before {
  content: "Keywords:";
  color: var(--text-main);
  font-size: 0.75rem;
  font-weight: 400;
  margin-right: 4px;
}
</style>


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


    <!-- =====================================================
         SUBMITTED
         ===================================================== -->

    <section class="publication-status-section">

      <h2 class="publication-year">
        Submitted
      </h2>

      <div
        class="publication-status-list publication-list"
        data-status="submitted"
      >
      </div>

    </section>


    <!-- =====================================================
         IN PREPARATION
         ===================================================== -->

    <section class="publication-status-section">

      <h2 class="publication-year">
        In Preparation
      </h2>

      <div
        class="publication-status-list publication-list"
        data-status="in-preparation"
      >
      </div>

    </section>


    <!-- =====================================================
         PUBLISHED BY YEAR
         ===================================================== -->

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


  <div id="theme-publication-lists">


    {% for theme_pair in site.data.themes %}

      {% assign theme_id = theme_pair[0] %}
      {% assign theme = theme_pair[1] %}


      <section
        class="publication-theme-section"
        id="publication-theme-{{ theme_id }}"
      >

        <h2 class="publication-theme-heading">
          {{ theme.theme-name }}
        </h2>


        <div
          class="publication-list"
          data-theme-id="{{ theme_id }}"
        >
        </div>

      </section>

    {% endfor %}


  </div>

</div>


<!-- =========================================================
     JAVASCRIPT
     ========================================================= -->

<script>

document.addEventListener("DOMContentLoaded", function() {


  /* =========================================================
     VIEW SWITCHER
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
     SOURCE PUBLICATIONS
     ========================================================= */

  const yearSource =
    document.getElementById(
      "year-publication-source"
    );


  const yearPublications =
    yearSource.querySelectorAll(
      ".publication"
    );


  /* =========================================================
     BY YEAR
     ========================================================= */

  const yearSections =
    document.getElementById(
      "year-sections"
    );


  const publicationsByYear = {};


  yearPublications.forEach(function(publication) {


    const journalElement =
      publication.querySelector(
        ".publication-journal"
      );


    if (!journalElement) {
      return;
    }


    const yearMatch =
      journalElement.textContent.match(
        /\((\d{4})\)/
      );


    if (!yearMatch) {
      return;
    }


    const year = yearMatch[1];


    if (!publicationsByYear[year]) {

      publicationsByYear[year] = [];

    }


    publicationsByYear[year].push(
      publication
    );

  });


  Object
    .keys(publicationsByYear)
    .sort(function(a, b) {

      return b - a;

    })
    .forEach(function(year) {


      const section =
        document.createElement(
          "section"
        );


      section.className =
        "publication-year-section";


      const heading =
        document.createElement(
          "h2"
        );


      heading.className =
        "publication-year";


      heading.textContent =
        year;


      const list =
        document.createElement(
          "div"
        );


      list.className =
        "publication-list";


      publicationsByYear[year].forEach(
        function(publication) {


          list.appendChild(
            publication.cloneNode(true)
          );

        }
      );


      section.appendChild(
        heading
      );


      section.appendChild(
        list
      );


      yearSections.appendChild(
        section
      );

    });


  /* =========================================================
     SUBMITTED / IN PREPARATION
     ========================================================= */

  const statusLists =
    document.querySelectorAll(
      ".publication-status-list"
    );


  statusLists.forEach(function(statusList) {


    const status =
      statusList.dataset.status;


    let count = 0;


    yearPublications.forEach(
      function(publication) {


        const publicationStatus =
          (
            publication.dataset.status || ""
          )
          .trim()
          .toLowerCase();


        if (
          publicationStatus === status
        ) {


          statusList.appendChild(
            publication.cloneNode(true)
          );


          count++;

        }

      }
    );


    /* Hide empty sections */

    if (count === 0) {


      statusList
        .closest(
          ".publication-status-section"
        )
        .style.display = "none";

    }

  });


  /* =========================================================
     BY RESEARCH THEME
     ========================================================= */

  const themeSource =
    document.getElementById(
      "theme-publication-source"
    );


  const themePublications =
    themeSource.querySelectorAll(
      ".publication"
    );


  const themeLists =
    document.querySelectorAll(
      ".publication-list[data-theme-id]"
    );


  themeLists.forEach(function(themeList) {


    const themeId =
      themeList.dataset.themeId;


    themePublications.forEach(
      function(publication) {


        const themeIds =
          (
            publication.dataset.themeIds || ""
          )
          .split(",")
          .map(function(theme) {

            return theme.trim();

          });


        if (
          themeIds.includes(themeId)
        ) {


          themeList.appendChild(
            publication.cloneNode(true)
          );

        }

      }
    );

  });


});

</script>
