---
layout: page
title: Data collection
---

The data collection framework for the Comparative Legislators Database (CLD) relies on the open-collaboration platforms <span style="color:#cc0065">Wikipedia</span> and <span style="color:#cc0065">Wikidata</span>.

The data collection is divided into four steps:

+ <span style="color:#cc0065">Entity identification</span>
+ <span style="color:#cc0065">Data collection</span>
+ <span style="color:#cc0065">Cleaning and verification</span>
+ <span style="color:#cc0065">Database integration</span>

---

<img src="../../img/data-collection.png" style="display:block;margin-left:auto;margin-right:auto;height:auto;width:100%">

---

<div class="row">
  <div class="col-sm-12 col-md-6">
    <h4 class="legislator-blue">1. Entity identification</h4>
    <p>The process starts from legislatures' Wikipedia index pages. During the first step of the data collection, you need to identify and scrape parliamentary members from the index sites to extract the member-specific Wikipedia and Wikidata IDs.</p>
    <hr>
  </div>
  <div class="col-sm-12 col-md-6">
    <h4 class="legislator-blue">2. Data collection</h4>
    <p>With the Wikipedia identifiers, you can collect most of the information about the individual legislators from the properties in their Wikidata entry. In some instances, you can tackle incomplete data by integrating external data sources.</p>
    <hr>
  </div>
</div>


<div class="row">
  <div class="col-sm-12 col-md-6">
    <h4 class="legislator-blue">3. Cleaning and verification</h4>
    <p>During the third step, you will clean and verify our data. This normally means removing noise in values, harmonizing variables within and across legislatures, and performing checks against alternative data sources.</p>
    <hr>
  </div>
  <div class="col-sm-12 col-md-6">
    <h4 class="legislator-blue">4. Database integration</h4>
    <p>The final step of the data collection process entails integrating the newly compiled data with the database interface. The database is built around the Wikipedia and Wikidata IDs and provide access via the <code>legislatoR</code> package in R.</p>
    <hr>
    </div>
</div>

<a type="button" class="btn btn-lg btn-block" style="background-color:#0A3b76;color:#fff;" href="{{ site.baseurl }}/tutorial/getting-the-files/">Start the tutorial</a>
