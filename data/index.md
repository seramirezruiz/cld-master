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

This is an overview of the CLD's current coverage and other databases that it can be integrated with:

<table class="table-hover"> <thead>
          <tr>
            <th>Country</th>
            <th>Legislative sessions</th>
            <th>Politicians (unique)</th>
            <th>Integrated with</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>Austria (Nationalrat)</td>
            <td>all 27<br> (1920-2019)</td>
            <td>1,923</td>
            <td><a href="https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/L4OAKN" rel="nofollow">ParlSpeech V2</a> (Rauh/Schwalbach 2020)</td>
          </tr>
          <tr>
            <td>Canada (House of Commons)</td>
            <td>all 43<br> (1867-2019)</td>
            <td>4,515</td>
            <td></td>
          </tr>
          <tr>
            <td>Czech Republic (Poslanecka Snemovna)</td>
            <td>all 8<br> (1992-2017)</td>
            <td>1,020</td>
            <td><a href="https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/E4RSP9" rel="nofollow">ParlSpeech V1</a> (Rauh et al. 2017)</td>
          </tr>
          <tr>
            <td>France (Assemblée)</td>
            <td>all 15<br> (1958-2017)</td>
            <td>3,933</td>
            <td></td>
          </tr>
          <tr>
            <td>Germany (Bundestag)</td>
            <td>all 19<br> (1949-2017)</td>
            <td>4,075</td>
            <td><a href="https://dataverse.harvard.edu/dataverse/btvote" rel="nofollow">BTVote data</a> (Bergmann et al. 2018),<br> <a href="https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/E4RSP9" rel="nofollow">ParlSpeech V1</a> (Rauh et al. 2017),<br> <a href="https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/EBEDPI" rel="nofollow">Reelection Prospects data</a> (Stoffel/Sieberer 2017)</td>
          </tr>
          <tr>
            <td>Ireland (Dail)</td>
            <td>all 33<br> (1918-2020)</td>
            <td>1,408</td>
            <td><a href="https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/6MZN76" rel="nofollow">Database of Parliamentary Speeches in Ireland</a> (Herzog/Mikhaylov 2017)</td>
          </tr>
          <tr>
            <td>Scotland (Parliament)</td>
            <td>all 5<br> (1999-2016)</td>
            <td>305</td>
            <td><a href="https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/EQ9WBE" rel="nofollow">ParlScot</a> (Braby/Fraser 2021)</td>
          </tr>
          <tr>
            <td>Spain (Congreso de los Diputados)</td>
            <td>all 14<br> (1979-2019)</td>
            <td>2634</td>
            <td><a href="https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/L4OAKN" rel="nofollow">ParlSpeech V2</a> (Rauh/Schwalbach 2020)</td>
          </tr>
          <tr>
            <td>United Kingdom (House of Commons)</td>
            <td>all 58<br> (1801-2019)</td>
            <td>13,215</td>
            <td><a href="https://github.com/ArthurSpirling/EggersSpirlingDatabase">EggersSpirling data</a> (starting from <br> 38th session, Eggers/Spirling 2014),<br> <a href="https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/E4RSP9" rel="nofollow">ParlSpeech V1</a> (Rauh et al. 2017)</td>
          </tr>
          <tr>
            <td>United States (House and Senate)</td>
            <td>all 116<br> (1789-2019)</td>
            <td>12,512</td>
            <td><a href="https://voteview.com/data" rel="nofollow">Voteview data</a> (Lewis et al. 2019), <br> <a href="http://www.congressionalbills.org/" rel="nofollow">Congressional Bills Project data</a> (Adler/Wilkserson 2018)</td>
          </tr>
          <tr>
            <td><strong>10</strong></td>
            <td><strong>338</strong></td>
            <td><strong>45,540</strong></td>
            <td><strong>12</strong></td>
          </tr>
        </tbody>
      </table>
