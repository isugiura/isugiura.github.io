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


<!-- =========================
     BY YEAR
     ========================= -->

<div
  id="year-view"
  class="publication-view active"
>

  {% bibliography %}

</div>


<!-- =========================
     BY RESEARCH THEME
     ========================= -->

<div
  id="theme-view"
  class="publication-view"
>

  {% bibliography %}

</div>


<script>

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

</script>
