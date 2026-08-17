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
    data-view="topic-view"
  >
    By Research Topic
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
     BY RESEARCH TOPIC
     ========================================================= -->

<div
  id="topic-view"
  class="publication-view"
>

  <!-- Hidden source bibliography -->

  <div
    id="topic-publication-source"
    style="display: none;"
  >

    {% bibliography %}

  </div>


  <div id="topic-publication-lists">


    {% for topic_pair in site.data.research-topics %}

      {% assign topic_id = topic_pair[0] %}
      {% assign topic = topic_pair[1] %}


      <section
        class="publication-topic-section"
        id="publication-topic-{{ topic_id }}"
      >

        <h2 class="publication-topic-heading">
          {{ topic.topic-name }}
        </h2>


        <div
          class="publication-list"
          data-topic-id="{{ topic_id }}"
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


          /*
           * Keep all research topics in the
           * By Year view.
           */

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


          /*
           * Keep all research topics in the
           * status sections.
           */

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
     BY RESEARCH TOPIC
     ========================================================= */

  const topicSource =
    document.getElementById(
      "topic-publication-source"
    );


  const topicPublications =
    topicSource.querySelectorAll(
      ".publication"
    );


  const topicLists =
    document.querySelectorAll(
      ".publication-list[data-topic-id]"
    );


  topicLists.forEach(function(topicList) {


    const topicId =
      topicList.dataset.topicId;


    topicPublications.forEach(
      function(publication) {


        /*
         * bib.html exposes the BibTeX
         * "topics" field as data-topic-ids.
         */

        const topicIds =
          (
            publication.dataset.topicIds || ""
          )
          .split(",")
          .map(function(topic) {

            return topic.trim();

          })
          .filter(function(topic) {

            return topic !== "";

          });


        if (
          topicIds.includes(topicId)
        ) {


          /*
           * Clone the publication so that the
           * hidden source remains unchanged.
           */

          const clone =
            publication.cloneNode(true);


          /* -------------------------------------------------
             REMOVE CURRENT TOPIC
             -------------------------------------------------

             The topic being used as the section
             heading should not also appear as an
             "Other relevant topic."
          */

          clone
            .querySelectorAll(
              ".publication-topic"
            )
            .forEach(function(topicElement) {


              if (
                topicElement.dataset.topicId === topicId
              ) {

                topicElement.remove();

              }

            });


          /* -------------------------------------------------
             CHECK FOR OTHER TOPICS
             -------------------------------------------------

             If there are remaining topics, keep:

             Other relevant topic(s):

             If there are no remaining topics,
             remove the entire topic container.
          */

          const topicsContainer =
            clone.querySelector(
              ".publication-topics"
            );


          const remainingTopics =
            clone.querySelectorAll(
              ".publication-topic"
            );


          if (
            remainingTopics.length > 0
          ) {


            const topicLabel =
              clone.querySelector(
                ".publication-topic-label"
              );


            if (topicLabel) {

              topicLabel.textContent =
                "Other relevant topic(s):";

            }

          } else {


            /*
             * No other topics remain.
             *
             * Remove the entire container so
             * that no empty label is displayed.
             */

            if (topicsContainer) {

              topicsContainer.remove();

            }

          }


          /*
           * Add the modified publication to
           * this research-topic section.
           */

          topicList.appendChild(
            clone
          );

        }

      }
    );


    /* -------------------------------------------------------
       HIDE EMPTY RESEARCH-TOPIC SECTIONS
       ------------------------------------------------------- */

    if (
      topicList.children.length === 0
    ) {

      topicList
        .closest(
          ".publication-topic-section"
        )
        .style.display = "none";

    }

  });


});

</script>
