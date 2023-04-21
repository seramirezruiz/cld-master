---
layout: page
title: Data
---

The Comparative Legislators Database (CLD) is a one-stop shop for rich, diverse and integrated individual-level data on national political representatives. The database contains information for over 67,000 contemporary and historical legislators from 16 countries. In our project, we unite collaborative micro-data collection efforts. We bring these together through the use of Wikipedia and Wikidata.

---

<h2 class="legislator-blue">Data access</h2>

<p>There are multiple ways to access the data depending your use-case. You can download the files for individual legislatures or use the <span style = "color:#cc0065">legislatoR</span> package for the software environment R.</p>

<ul>
<li> Download the files from the Dataverse: <a href="https://doi.org/10.7910/DVN/Z2V8DD" target="_blank">.csv</a> |  <a href="https://doi.org/10.7910/DVN/LB9BMN" target="_blank">.rds</a> | <a href="https://doi.org/10.7910/DVN/HCVCBA" target="_blank">.sqlite</a></li>
<li> Learn to use the <a href="{{ site.baseurl }}/data/legislator/">legislatoR package</a></li>
</ul>

---

<h2 class="legislator-blue">Database structure</h2>

The CLD is a relational database. This means that all data can be joined with the Core table via one of two keys - the <span style="color:#cc0065">Wikipedia page ID</span> or the <span style="color:#cc0065">Wikidata ID</span>.

Learn more about the <a href="{{ site.baseurl }}/data/structure/">database structure</a>.

---

<h2 class="legislator-blue">Data coverage</h2>

In its current version, the CLD covers the following legislatures:

<div class="table-wrapper" markdown="block">

| Country                              | Legislative sessions        | Politicians (unique*) | Integrated with    |
| ------------------------------------ | --------------------------- | -------------------- | ------------------ |
| Austria (Nationalrat)                | all 27<br /> (1920-2019)        | 1,923                | [ParlSpeech V2](https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/L4OAKN) (Rauh/Schwalbach 2020)      |
| Brazil (Câmara dos Deputados)        | 38-57<br /> (1947-2022)     | 3,474                |                    |
| Canada (House of Commons)            | all 44<br /> (1867-2021)        | 4,567                |                    |
| Czech Republic (Poslanecka Snemovna) | all 9<br /> (1992-2021)         | 1,124                | [ParlSpeech V1](https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/E4RSP9) (Rauh et al. 2017)          |
| France (Assemblée)                   | all 16<br /> (1958-2022)        | 4,263                |                    |
| Germany (Bundestag)                  | all 20<br /> (1949-2021)        | 4,371                | [BTVote data](https://dataverse.harvard.edu/dataverse/btvote) (Bergmann et al. 2018),<br /> [ParlSpeech V1](https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/E4RSP9) (Rauh et al. 2017),<br /> [Reelection Prospects data](https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/EBEDPI) (Stoffel/Sieberer 2017)   |
| Ireland (Dail)                       | all 33<br /> (1918-2020)        | 1,408                |	[Database of Parliamentary Speeches in Ireland](https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/6MZN76) (Herzog/Mikhaylov 2017)	|
| Israel (Knesset)                     | all 25<br /> (1949-2022)        | 1,022                |                 |
| Italy (Camera dei deputati and Senato della Repubblica) | all 19<br /> (1948-2022)  | 5,149   |                 |
| Japan (Shūgiin)                      | all 49<br /> (1890-2021)          | 6,581                |               |
| Netherlands (Tweede Kamer)           | all 65<br /> (1815-2021)          | 1,887                |               |
| Scotland (Parliament)                | all 6<br /> (1999-2021)           | 348                  | [ParlScot](https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/EQ9WBE) (Braby/Fraser 2021)      			 |
| Spain (Congreso de los Diputados)    | all 14<br /> (1979-2019)          | 2,616           | [ParlSpeech V2](https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/L4OAKN) (Rauh/Schwalbach 2020)      |        
| Turkey (Büyük Millet Meclisi)        | all 27<br /> (1920-2018)          | 5,298                |              |
| United Kingdom (House of Commons)    | all 58<br /> (1801-2019)          | 11,321               | [EggersSpirling data](https://github.com/ArthurSpirling/EggersSpirlingDatabase) (starting from <br /> 38th session, Eggers/Spirling 2014),<br /> [ParlSpeech V1](https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/E4RSP9) (Rauh et al. 2017) |
| United States (House and Senate)     | all 117<br /> (1789-2021)         | 12,593               | [Voteview data](https://voteview.com/data) (Lewis et al. 2019), <br /> [Congressional Bills Project data](http://www.congressionalbills.org/) (Adler/Wilkerson 2018) |
| **16**                                | **529**                     | **67,945**           | **12** 		       |

\* We only count legislators with a unique Wikipedia page or Wikidata ID. Sometimes legislators do not have either. Such cases are indicated by the string "miss" in the wikidataid or pageid.
</div>
