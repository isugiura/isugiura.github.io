---
layout: default
title: Research
permalink: /research/
---

<h1>Research</h1>


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
     RESEARCH TOPICS
     ========================================================= -->

{% for topic_pair in site.data.research-topics %}

  {% assign topic_id = topic_pair[0] %}
  {% assign topic = topic_pair[1] %}


  <section
    class="research-interest"
    id="research-topic-{{ topic_id }}"
  >

    <h2>
      {{ topic.topic-name }}
    </h2>


    <p>
      {{ topic.description }}
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
        data-topic-id="{{ topic_id }}"
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


  const topicLists =
    document.querySelectorAll(
      ".research-publications-list"
    );


  /* =========================================================
     BUILD PUBLICATIONS FOR EACH RESEARCH TOPIC
     ========================================================= */

  topicLists.forEach(function(topicList) {


    const topicId =
      topicList.dataset.topicId;


    publications.forEach(function(publication) {


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


      /*
       * Only include publications associated
       * with the current research topic.
       */

      if (
        !topicIds.includes(topicId)
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
         REMOVE CURRENT TOPIC
         =====================================================

         The topic being used as the section heading
         should not also appear as an "other" topic.
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


      /* =====================================================
         HANDLE OTHER RELEVANT TOPICS
         =====================================================

         If other topics remain, change the label to:

         Other relevant topic(s):

         If no other topics remain, remove the entire
         topic container, including the label.
      */

      const topicContainer =
        clone.querySelector(
          ".publication-topics"
        );


      if (topicContainer) {


        const remainingTopics =
          topicContainer.querySelectorAll(
            ".publication-topic"
          );


        if (
          remainingTopics.length === 0
        ) {


          /*
           * Publication has only the current topic.
           *
           * Remove the entire topic container so
           * "Other relevant topic(s):" does not appear.
           */

          topicContainer.remove();


        } else {


          /*
           * Publication has additional topics.
           *
           * Change the label to:
           *
           * Other relevant topic(s):
           */

          const topicLabel =
            topicContainer.querySelector(
              ".publication-topic-label"
            );


          if (topicLabel) {

            topicLabel.textContent =
              "Other relevant topic(s):";

          }

        }

      }


      /* =====================================================
         ADD PUBLICATION
         ===================================================== */

      topicList.appendChild(
        clone
      );

    });

  });

});

</script>
