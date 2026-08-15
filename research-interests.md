---
layout: default
title: Research Interests
permalink: /research-interests/
---

<h1>Research Interests</h1>


<!-- =========================================================
     CLIMATE VARIABILITY
     ========================================================= -->

<section class="research-interest">

  <h2 id="climate-variability">
    Climate Variability
  </h2>

  <p>
    My research examines variability in the climate system across
    different spatial and temporal scales, with a particular focus on
    understanding the mechanisms driving regional and global changes.
  </p>

  <details class="research-publications">

    <summary>
      Publications
    </summary>

    <div class="research-publications-list">

      {% assign theme_publications = site.bibliography
        | where_exp: "entry", "entry.theme contains 'climate variability'"
      %}

      {% assign years = theme_publications
        | map: "year"
        | uniq
        | sort
        | reverse
      %}

      {% for year in years %}

        <h3 class="publication-year">
          {{ year }}
        </h3>

        {% for entry in theme_publications %}

          {% if entry.year == year %}

            {% include bib.html %}

          {% endif %}

        {% endfor %}

      {% endfor %}

    </div>

  </details>

</section>


<!-- =========================================================
     VOLCANIC FORCING
     ========================================================= -->

<section class="research-interest">

  <h2 id="volcanic-forcing">
    Volcanic Forcing
  </h2>

  <p>
    My research investigates the climatic impacts of volcanic eruptions,
    including the spatial and temporal evolution of post-eruption
    temperature and precipitation responses.
  </p>

  <details class="research-publications">

    <summary>
      Publications
    </summary>

    <div class="research-publications-list">

      {% assign theme_publications = site.bibliography
        | where_exp: "entry", "entry.theme contains 'volcanic forcing'"
      %}

      {% assign years = theme_publications
        | map: "year"
        | uniq
        | sort
        | reverse
      %}

      {% for year in years %}

        <h3 class="publication-year">
          {{ year }}
        </h3>

        {% for entry in theme_publications %}

          {% if entry.year == year %}

            {% include bib.html %}

          {% endif %}

        {% endfor %}

      {% endfor %}

    </div>

  </details>

</section>


<!-- =========================================================
     CLIMATE DYNAMICS
     ========================================================= -->

<section class="research-interest">

  <h2 id="climate-dynamics">
    Climate Dynamics
  </h2>

  <p>
    I study interactions among different components of the climate
    system and how large-scale modes of climate variability influence
    regional climate.
  </p>

  <details class="research-publications">

    <summary>
      Publications
    </summary>

    <div class="research-publications-list">

      {% assign theme_publications = site.bibliography
        | where_exp: "entry", "entry.theme contains 'climate dynamics'"
      %}

      {% assign years = theme_publications
        | map: "year"
        | uniq
        | sort
        | reverse
      %}

      {% for year in years %}

        <h3 class="publication-year">
          {{ year }}
        </h3>

        {% for entry in theme_publications %}

          {% if entry.year == year %}

            {% include bib.html %}

          {% endif %}

        {% endfor %}

      {% endfor %}

    </div>

  </details>

</section>
