---
layout: page
title: Database structure
---

The Comparative Legislators Database (CLD) comes as a relational database. This means that all tables can be joined with the Core table via one of two keys - the <span style="color:#cc0065">Wikipedia page ID</span> or the <span style="color:#cc0065">Wikidata ID</span>. These keys uniquely identify individual politicians.

For each legislature, the CLD holds nine tables:

* <em class="legislator-blue">Core</em> (sociodemographic data)
* <em class="legislator-blue">Political</em> (political data)
* <em class="legislator-blue">History</em> (full revision records of individual Wikipedia biographies)
* <em class="legislator-blue">Traffic</em> (daily user traffic on individual Wikipedia biographies starting from July 2007)
* <em class="legislator-blue">Social</em> (social media handles and personal website URLs)
* <em class="legislator-blue">Portraits</em> (URLs to portraits)
* <em class="legislator-blue">Offices</em> (public offices)
* <em class="legislator-blue">Professions</em> (professions)
* <em class="legislator-blue">IDs</em> (identifiers linking politicians to other files, databases, or websites)

The figure below illustrates this structure and the CLD's content.

---

<object data="../../img/data-structure.svg" style="display:block;margin-left:auto;margin-right:auto;height:auto;width:75%;"> </object>
