---
layout: page
title: Data
---

The Comparative Legislators Database (CLD) is a one-stop shop for rich, diverse and integrated individual-level data on national political representatives. The database contains information for over 45,000 contemporary and historical legislators from 14 countries and the European Parliament. In our project, we unite collaborative micro-data collection efforts. We bring these together through the use of Wikipedia and Wikidata.

---

<h2 class="legislator-blue">Data access</h2>

<p>There are multiple ways to access the data depending your use-case. You can download individual <span style = "color:#cc0065">.csv </span>files for individual legislatures, generate <span style = "color:#cc0065">SQL queries</span> to gather specific information from the database, and finally use the <span style = "color:#cc0065">legislatoR</span> package for the software environment R.</p>

<ul>
<li> Download <a href="{{ site.baseurl }}/data/csv/">.csv</a> files <i class="fa fa-download"></i></li>
<li> Sample <a href="{{ site.baseurl }}/data/sql/">SQL queries</a> <i class="fa fa-database"></i></li>
<li> Learn to use the <a href="{{ site.baseurl }}/data/legislator/">legislatoR package</a> <i class="fa fa-code"></i></li>
</ul>

---

<h2 class="legislator-blue">Database structure</h2>

The CLD is a relational database. This means that all data can be joined with the Core table via one of two keys - the <span style="color:#cc0065">Wikipedia page ID</span> or the <span style="color:#cc0065">Wikidata ID</span>.

Learn more about the <a href="{{ site.baseurl }}/data/structure/">database structure</a>.

---

<h2 class="legislator-blue">Data coverage</h2>

In its current version, the CLD covers the following legislatures:

<div class="table-wrapper" markdown="block">

| Legislature               | Country        | Years     | Legislative sessions | Politicians (unique) | Integrated with                                                                                                       |
|---------------------------|----------------|-----------|----------------------|----------------------|-----------------------------------------------------------------------------------------------------------------------|
| Nationalrat               | Austria        | 1920-2019 | all 27               | 1,923                | [ParlSpeech V2](https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/L4OAKN) (Rauh/Schwalbach 2020)                                                                                  |
| House of Commons          | Canada         | 1867-2019 | all 43               | 4,515                |                                                                                                                       |
| Poslanecka Snemovna       | Czech Republic | 1992-2017 | all 8                | 1,020                | [ParlSpeech V1](https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/E4RSP9) (Rauh et al. 2017)                                                                                      |
| Assemblée                | France         | 1958-2017 | all 15               | 3,933                |                                                                                                                       |
| Bundestag                 | Germany        | 1949-2017 | all 19               | 4,075                | [BTVote data](https://dataverse.harvard.edu/dataverse/btvote) (Bergmann et al. 2018),<br /> [ParlSpeech V1](https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/E4RSP9) (Rauh et al. 2017),<br /> [Reelection Prospects data](https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/EBEDPI) (Stoffel/Sieberer 2017) |
| Dail                      | Ireland        | 1918-2020 | all 33               | 1,408                | [Database of Parliamentary Speeches in Ireland](https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/6MZN76) (Herzog/Jankin Mikhaylov 2017)                                                 |
| Parliament                | Scotland       | 1999-2016 | all 5                | 305                  | [ParlScot](https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/EQ9WBE) (Braby/Fraser 2021)                                                                                          |
| Congreso de los Diputados | Spain          | 1979-2019 | all 14               | 2634                 | [ParlSpeech V2](https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/L4OAKN) (Rauh/Schwalbach 2020)                                                                                  |
| House of Commons          | United Kingdom | 1801-2019 | all 58               | 13,215               | [EggersSpirling data](https://github.com/ArthurSpirling/EggersSpirlingDatabase) (starting from <br /> 38th session, Eggers/Spirling 2014),<br /> [ParlSpeech V1](https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/E4RSP9) (Rauh et al. 2017)              |
| House of Representatives       | United States  | 1789-2019 | all 116              | 12,512               | [Voteview data](https://voteview.com/data) (Lewis et al. 2019), <br /> [Congressional Bills Project data](http://www.congressionalbills.org/) (Adler/Wilkserson 2018)                           |
| Senate          | United States  | 1789-2019 | all 116              | 12,512               | [Voteview data](https://voteview.com/data) (Lewis et al. 2019), <br /> [Congressional Bills Project data](http://www.congressionalbills.org/) (Adler/Wilkserson 2018)                           |
|   **XX**                      | **10**             |         | **338**                  | **45,540**               |                                                                                                                |

</div>
