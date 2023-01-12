---
layout: page
title: Collecting the data
---

Once you have created our collector function, you have to follow a series of steps to gather all the data. Things from here will be straightforward. You just need to create a data frame containing the names of the files, the legislative session, and the years. After that, it will be an exercise of replacing strings to match the new legislature. This tutorial will follow-through with the Camera dei Deputati. Still, to make things easier, you can use the <code>code/02-collection-sample</code> script that has clear instructions on which strings to replace to collect the data.

---

<h3 class="legislature-blue">Building the legislature index</h3>

At this stage, the HTML files of the legislature should be downloaded locally to the <code>data/italy_chamber/html/</code> folder.

```r
#### PREPARATIONS =======================================================================

source("code/packages.R")
source("code/functions.R")


#### DOWNLOAD INDEX PAGES =========


leg_ses <- c("1948", "1953", "1958", "1963", "1968", "1972", "1976",
             "1979", "1983", "1987", "1992", "1994", "1996", "2001",
             "2006", "2008", "2013", "2018") # 1st to 18th sessions

url_list <- glue::glue("https://it.wikipedia.org/wiki/Eletti_alla_Camera_dei_deputati_nelle_elezioni_politiche_italiane_del_{leg_ses}")

file_names <- glue::glue("{leg_ses}_chamber_session_ITA.html")

# download pages
folder <- "data/italy_chamber/html/"
dir.create(folder)
for (i in 1:length(url_list)) {
  if (!file.exists(paste0(folder, file_names[i]))) {
    download.file(url_list[i], destfile = paste0(folder, file_names[i])) # , method = "libcurl" might be needed on windows machine
    Sys.sleep(runif(1, 0, 1))
  }
}
```

An index to guide the handling of exceptions from the <code>collectorItalyChamber()</code> can be built around these files. You can build the table manually and load it into the environment, or create within <code>R</code>. The <code>path_source</code> table should contain the following elements:

+ files contains the local path to each HTML file which contains the data you intend to scrape.
+ session contains the session numbers that the collector function will use for exception handling.
+ year contains the start year of the legislative session.

```r
#### DATA COLLECTION ====================================================================

# path to local html files --------------------------------------------------------------
source <- "data/italy_chamber/html" # local html location

# session-specific xpaths ---------------------------------------------------------------
path_source <- tibble(files = mixedsort(list.files(source, full.names = TRUE), decreasing = TRUE),
    session = seq(18,1,-1),
    year = as.numeric(stringr::str_extract(files, stringr::regex("\\d+"))))

path_source

## A tibble: 18 × 3
## files                                                     session year
## <chr>                                                       <dbl> <dbl>
## 1  data/italy_chamber/html/2018_chamber_session_ITA.html       18  2018
## 2  data/italy_chamber/html/2013_chamber_session_ITA.html       17  2013
## 3  data/italy_chamber/html/2008_chamber_session_ITA.html       16  2008
## 4  data/italy_chamber/html/2006_chamber_session_ITA.html       15  2006
## 5  data/italy_chamber/html/2001_chamber_session_ITA.html       14  2001
## 6  data/italy_chamber/html/1996_chamber_session_ITA.html       13  1996
## 7  data/italy_chamber/html/1994_chamber_session_ITA.html       12  1994
## 8  data/italy_chamber/html/1992_chamber_session_ITA.html       11  1992
## 9  data/italy_chamber/html/1987_chamber_session_ITA.html       10  1987
## 10 data/italy_chamber/html/1983_chamber_session_ITA.html       9  1983
## 11 data/italy_chamber/html/1979_chamber_session_ITA.html       8  1979
## 12 data/italy_chamber/html/1976_chamber_session_ITA.html       7  1976
## 13 data/italy_chamber/html/1972_chamber_session_ITA.html       6  1972
## 14 data/italy_chamber/html/1968_chamber_session_ITA.html       5  1968
## 15 data/italy_chamber/html/1963_chamber_session_ITA.html       4  1963
## 16 data/italy_chamber/html/1958_chamber_session_ITA.html       3  1958
## 17 data/italy_chamber/html/1953_chamber_session_ITA.html       2  1953
## 18 data/italy_chamber/html/1948_chamber_session_ITA.html       1  1948
```

---

<h3 class="legislator-blue">Using the <code>collectorItalyChamber()</code> function</h3>

In the previous section, you built the collector function. You leveraged the patterns in the different legislative index pages to create the instructions to parse the entities. The code will iterate across pages with a similar structure based on the legislative session, while handling differences between them.

The <code>collectorItalyChamber()</code> function expects a single argument paths, the **legislature index** (i.e., paths_source), which will provide the HTML source to extract the nodes and gather the expected output for all the 18 legislative terms of the *Camera dei Deputati*. The function renders a set of nested lists containing the tables with the constituency, political party, name, and Wikipedia URL of each legislator for each session.

```r
# retrieve basic data from Wikipedia tables ---------------------------------------------
italy_chamber_core <- collectorItalyChamber(paths = path_source) %>%
  purrr::map(magrittr::set_colnames, c("constituency", "party", "name", "url", "session"))

italy_chamber_core

## [[1]]
## A tibble: 704 × 5
##    constituency party              name                        url                                     session
##    <chr>        <chr>              <chr>                       <chr>                                   <dbl>
##  1 Piemonte 1   Centrosinistra     Andrea Giorgis              /wiki/Andrea_Giorgis                    18
##  2 Piemonte 1   Centrodestra       Roberto Rosso               /wiki/Roberto_Rosso_(politico_196…      18
##  3 Piemonte 1   Centrodestra       Augusta Montaruli           /wiki/Augusta_Montaruli                 18
##  4 Piemonte 1   Centrosinistra     Stefano Lepri               /wiki/Stefano_Lepri_(politico)          18
##  5 Piemonte 1   Movimento 5 Stelle Celeste D'Arrando           /wiki/Celeste_D%27Arrando               18
##  6 Piemonte 1   Centrodestra       Alessandro Manuel Benvenuto /wiki/Alessandro_Manuel_Benvenuto       18
##  7 Piemonte 1   Centrodestra       Carluccio Giacometto        /wiki/Carluccio_Giacometto              18
##  8 Piemonte 1   Centrodestra       Claudia Porchietto          /wiki/Claudia_Porchietto                18
##  9 Piemonte 1   Centrodestra       Claudia Porchietto          /wiki/Claudia_Porchietto                18
## 10 Piemonte 1   Centrodestra       Daniela Ruffino             /wiki/Daniela_Ruffino                   18
### … with 694 more rows
### ℹ Use `print(n = ...)` to see more rows
##
## [[2]]
### A tibble: 635 × 5
##    constituency party                  name              url                           session
##    <chr>        <chr>                  <chr>             <chr>                          <dbl>
##  1 Piemonte 1   Partito Democratico    Cesare Damiano    /wiki/Cesare_Damiano           17
##  2 Piemonte 1   Partito Democratico    Paola Bragantini  /wiki/Paola_Bragantini         17
##  3 Piemonte 1   Partito Democratico    Giacomo Portas    /wiki/Giacomo_Portas           17
##  4 Piemonte 1   Partito Democratico    Francesca Bonomo  /wiki/Francesca_Bonomo         17
##  5 Piemonte 1   Partito Democratico    Edoardo Patriarca /wiki/Edoardo_Patriarca        17
##  6 Piemonte 1   Partito Democratico    Anna Rossomando   /wiki/Anna_Rossomando          17
##  7 Piemonte 1   Partito Democratico    Andrea Giorgis    /wiki/Andrea_Giorgis           17
##  8 Piemonte 1   Partito Democratico    Antonio Boccuzzi  /wiki/Antonio_Boccuzzi         17
##  9 Piemonte 1   Partito Democratico    Silvia Fregolent  /wiki/Silvia_Fregolent         17
## 10 Piemonte 1   Partito Democratico    Umberto D'Ottavio /wiki/Umberto_D%27Ottavio      17
##  # … with 625 more rows
##  # ℹ Use `print(n = ...)` to see more rows
##
##  [[3]]
##  # A tibble: 749 × 5
##     constituency   party                name                   url                               session
##     <chr>          <chr>                <chr>                  <chr>                             <dbl>
##  1  Piemonte 1     Partito Democratico  Piero Fassino          /wiki/Piero_Fassino               16
##  2  Piemonte 1     Partito Democratico  Antonio Boccuzzi       /wiki/Antonio_Boccuzzi            16
##  3  Piemonte 1     Partito Democratico  Anna Rossomando        /wiki/Anna_Rossomando             16
##  4  Piemonte 1     Partito Democratico  Giorgio Merlo          /wiki/Giorgio_Merlo               16
##  5  Piemonte 1     Partito Democratico  Marco Calgaro          /wiki/Marco_Calgaro               16
##  6  Piemonte 1     Partito Democratico  Gianni Vernetti        /wiki/Gianni_Vernetti             16
##  7  Piemonte 1     Partito Democratico  Stefano Esposito       /wiki/Stefano_Esposito            16
##  8  Piemonte 1     Partito Democratico  Giacomo Antonio Portas /wiki/Giacomo_Antonio_Portas      16
##  9  Piemonte 1     Partito Democratico  Mimmo Lucà             /wiki/Mimmo_Luc%C3%A0             16
##  10 Piemonte 1     Popolo della Libertà Guido Crosetto         /wiki/Guido_Crosetto              16
##  # … with 739 more rows
##  # ℹ Use `print(n = ...)` to see more rows
##  …
```

---

<h3 class="legislator-blue">Extracting and saving the data</h3>

Once the <code>italy_chamber_core</code> object has been created. Things are very straightforward. You just need to use a set of provided functions that make the API calls to render the respective output for each of the tables in the database. If you are working with a different legislature, the only changes you will need to perform are:

+ replace all strings matching "<code>italy_chamber</code>" to the respective legislature name.
+ replace all "<code>it.wikipedia</code>" strings to match the project containing the legislature.

Finally, the function to retrieve the portraits of the legislators makes a call to the Face++ API. It does so to ensure that the photographs are indeed portraits. You will need to provide an API key; however, if cannot set this up, the CLD team can take care of it.

```r
# retrieve basic data from Wikipedia tables ---------------------------------------------
italy_chamber_core <- collectorItalyChamber(paths = path_source) %>%
  purrr::map(magrittr::set_colnames, c("constituency", "party", "name", "url", "session"))

# retrieve wikipedia page and wikidata ids ----------------------------------------------
italy_chamber_ids <- italy_chamber_core %>%
  purrr::map(mutate, url = paste0("https://it.wikipedia.org", url)) %>%
  purrr::map(wikiIDs, .x$url)

# bind ids to core data and collapse ----------------------------------------------------
italy_chamber <- italy_chamber_ids %>%
  purrr::map2_dfr(bind_cols, .y = italy_chamber_core)
saveRDS(italy_chamber, "data/italy_chamber/italy_chamber")

# retrieve wikipedia revision histories -------------------------------------------------
italy_chamber_history <- italy_chamber %>%
  magrittr::use_series(pageid) %>%
  unique %>%
  purrr::map_dfr(wikiHist, project = "it.wikipedia")
saveRDS(italy_chamber_history, "data/italy_chamber/italy_chamber_history")

# retrieve undirected wikipedia urls/titles ---------------------------------------------
italy_chamber_title <- italy_chamber %>%
  magrittr::use_series(pageid) %>%
  unique %>%
  undirectedTitle(project = "it.wikipedia")
saveRDS(italy_chamber_title, "data/italy_chamber/italy_chamber_title")

# retrieve wikipedia user traffic -------------------------------------------------------
italy_chamber_traffic <- italy_chamber_title %>%
  wikiTrafficNew(project = rep("it", dim(italy_chamber_title)[1]))
saveRDS(italy_chamber_traffic, "data/italy_chamber/italy_chamber_traffic")

# retrieve Wikidata entities ------------------------------------------------------------
italy_chamber_entities <- italy_chamber %>%
  magrittr::use_series(wikidataid) %>%
  unique %>%
  WikidataR::get_item()
saveRDS(italy_chamber_entities, "data/italy_chamber/italy_chamber_entities")

# retrieve legislator's sex -------------------------------------------------------------
italy_chamber_sex <- italy_chamber %>%
  magrittr::use_series(wikidataid) %>%
  unique %>%
  wikiData(entity = italy_chamber_entities,
           property = "P21") %>%
  dplyr::mutate(sex = dplyr::case_when(
    male == TRUE ~ "male",
    female == TRUE ~ "female"
  )) %>%
  dplyr::select(-c(2,3))
saveRDS(italy_chamber_sex, "data/italy_chamber/italy_chamber_sex")

# retrieve legislator's religion --------------------------------------------------------
italy_chamber_religion <- italy_chamber %>%
  magrittr::use_series(wikidataid) %>%
  unique %>%
  wikiData(entity = italy_chamber_entities,
           property = "P140")
saveRDS(italy_chamber_religion, "data/italy_chamber/italy_chamber_religion")

# retrieve and format birth dates -------------------------------------------------------
italy_chamber_birth <-  italy_chamber %>%
  magrittr::use_series(wikidataid) %>%
  unique %>%
  wikiData(entity = italy_chamber_entities, date = TRUE,
           property = "P569") %>%
  mutate(date = stringr::str_replace_all(date, "\\+|T.+", "")) %>%
  mutate(date = stringr::str_replace_all(date, "-00", "-01")) %>%
  mutate(date = as.POSIXct(date, tz = "UTC"))
saveRDS(italy_chamber_birth, "data/italy_chamber/italy_chamber_birth")

# retrieve and format death dates -------------------------------------------------------
italy_chamber_death <-  italy_chamber %>%
  magrittr::use_series(wikidataid) %>%
  unique %>%
  wikiData(entity = italy_chamber_entities, date = TRUE,
           property = "P570") %>%
  mutate(date = stringr::str_replace_all(date, "\\+|T.+", "")) %>%
  mutate(date = stringr::str_replace_all(date, "-00", "-01")) %>%
  mutate(date = as.POSIXct(date, tz = "UTC"))
saveRDS(italy_chamber_death, "data/italy_chamber/italy_chamber_death")

# retrieve and format birth places ------------------------------------------------------
italy_chamber_birthplace <- italy_chamber %>%
  magrittr::use_series(wikidataid) %>%
  unique %>%
  wikiData(entity = italy_chamber_entities, location = TRUE,
           property = "P19") %>%
  mutate(lat = round(lat, digit = 5),
         lon = round(lon, digit = 5)) %>%
  mutate(birthplace = stringr::str_c(lat, ",", lon)) %>%
  dplyr::select(wikidataid, birthplace)
saveRDS(italy_chamber_birthplace, "data/italy_chamber/italy_chamber_birthplace")

# retrieve and format death places ------------------------------------------------------
italy_chamber_deathplace <- italy_chamber %>%
  magrittr::use_series(wikidataid) %>%
  unique %>%
  wikiData(entity = italy_chamber_entities, location = TRUE,
           property = "P20") %>%
  mutate(lat = round(lat, digit = 5),
         lon = round(lon, digit = 5)) %>%
  mutate(deathplace = stringr::str_c(lat, ",", lon)) %>%
  dplyr::select(wikidataid, deathplace)
saveRDS(italy_chamber_deathplace, "data/italy_chamber/italy_chamber_deathplace")

# retrieve and format social media data -------------------------------------------------
italy_chamber_twitter <- italy_chamber %>%
  magrittr::use_series(wikidataid) %>%
  unique %>%
  wikiData(entity = italy_chamber_entities, serial = TRUE,
           property = "P2002")
italy_chamber_instagram <- italy_chamber %>%
  magrittr::use_series(wikidataid) %>%
  unique %>%
  wikiData(entity = italy_chamber_entities, serial = TRUE,
           property = "P2003")
italy_chamber_facebook <- italy_chamber %>%
  magrittr::use_series(wikidataid) %>%
  unique %>%
  wikiData(entity = italy_chamber_entities, serial = TRUE,
           property = "P2013")
italy_chamber_youtube <- italy_chamber %>%
  magrittr::use_series(wikidataid) %>%
  unique %>%
  wikiData(entity = italy_chamber_entities, serial = TRUE,
           property = "P2397")
italy_chamber_linkedin <- italy_chamber %>%
  magrittr::use_series(wikidataid) %>%
  unique %>%
  wikiData(entity = italy_chamber_entities, serial = TRUE,
           property = "P6634")
italy_chamber_website <- italy_chamber %>%
  magrittr::use_series(wikidataid) %>%
  unique %>%
  wikiData(entity = italy_chamber_entities, serial = TRUE,
           property = "P856")
italy_chamber_social <- list(italy_chamber_twitter, italy_chamber_facebook, italy_chamber_youtube, italy_chamber_instagram,
                             italy_chamber_linkedin, italy_chamber_website) %>%
  purrr::reduce(full_join, by = "wikidataid") %>%
  purrr::set_names("wikidataid", "twitter", "facebook", "youtube",
                   "linkedin", "instagram", "website")
saveRDS(italy_chamber_social, "data/italy_chamber/italy_chamber_social")

# retrieve and format portrait data -----------------------------------------------------
italy_chamber_images <- italy_chamber %>%
  magrittr::use_series(pageid) %>%
  unique %>%
  imageUrl(project = "it.wikipedia") %>%
  faceDetection(api_key = api_key,
                api_secret = api_secret) %>%
  tidyr::drop_na()
saveRDS(italy_chamber_images, "data/italy_chamber/italy_chamber_images")

# retrieve and format ids ---------------------------------------------------------------
italy_chamber_parlid <- italy_chamber %>%
  magrittr::use_series(wikidataid) %>%
  unique %>%
  wikiData(entity = italy_chamber_entities, serial = TRUE,
           property = "P1341") #italian
italy_chamber_gndid <- italy_chamber %>%
  magrittr::use_series(wikidataid) %>%
  unique %>%
  wikiData(entity = italy_chamber_entities, serial = TRUE,
           property = "P227")
italy_chamber_libcon <- italy_chamber %>%
  magrittr::use_series(wikidataid) %>%
  unique %>%
  wikiData(entity = italy_chamber_entities, serial = TRUE,
           property = "P244")
italy_chamber_bnfid <- italy_chamber %>%
  magrittr::use_series(wikidataid) %>%
  unique %>%
  wikiData(entity = italy_chamber_entities, serial = TRUE,
           property = "P268")
italy_chamber_freebase <- italy_chamber %>%
  magrittr::use_series(wikidataid) %>%
  unique %>%
  wikiData(entity = italy_chamber_entities, serial = TRUE,
           property = "P646")
italy_chamber_munzinger <- italy_chamber %>%
  magrittr::use_series(wikidataid) %>%
  unique %>%
  wikiData(entity = italy_chamber_entities, serial = TRUE,
           property = "P1284")
italy_chamber_nndb <- italy_chamber %>%
  magrittr::use_series(wikidataid) %>%
  unique %>%
  wikiData(entity = italy_chamber_entities, serial = TRUE,
           property = "P1263")
italy_chamber_imdb <- italy_chamber %>%
  magrittr::use_series(wikidataid) %>%
  unique %>%
  wikiData(entity = italy_chamber_entities, serial = TRUE,
           property = "P345")
italy_chamber_brittanica <- italy_chamber %>%
  magrittr::use_series(wikidataid) %>%
  unique %>%
  wikiData(entity = italy_chamber_entities, serial = TRUE,
           property = "P1417")
italy_chamber_quora <- italy_chamber %>%
  magrittr::use_series(wikidataid) %>%
  unique %>%
  wikiData(entity = italy_chamber_entities, serial = TRUE,
           property = "P3417")
italy_chamber_google_knowledge_graph <- italy_chamber %>%
  magrittr::use_series(wikidataid) %>%
  unique %>%
  wikiData(entity = italy_chamber_entities, serial = TRUE,
           property = "P2671")
italy_chamber_ids <- list(italy_chamber_parlid, italy_chamber_gndid, italy_chamber_libcon, italy_chamber_bnfid,
                          italy_chamber_freebase, italy_chamber_munzinger, italy_chamber_nndb, italy_chamber_imdb,
                          italy_chamber_brittanica, italy_chamber_quora, italy_chamber_google_knowledge_graph) %>%
  purrr::reduce(full_join, by = "wikidataid") %>%
  purrr::set_names("wikidataid", "parlid", "gndif", "libcon", "bnfid",
                   "freebase", "munzinger", "nndb", "imdb",
                   "brittanica", "quora", "google_knowledge_graph")
saveRDS(italy_chamber_ids, "data/italy_chamber/italy_chamber_ids")

# retrieve and format positions ---------------------------------------------------------
italy_chamber_positions <- italy_chamber %>%
  magrittr::use_series(wikidataid) %>%
  unique %>%
  wikiData(entity = italy_chamber_entities, unique = TRUE,
           property = "P39") %>%
  dplyr::select(-unknown) %>%
  data.table::setcolorder(order(names(.))) %>%
  dplyr::select(wikidataid, everything())
saveRDS(italy_chamber_positions, "data/italy_chamber/italy_chamber_positions")

# retrieve and format occupation --------------------------------------------------------
italy_chamber_occupation <- italy_chamber %>%
  magrittr::use_series(wikidataid) %>%
  unique %>%
  wikiData(entity = italy_chamber_entities, unique = TRUE,
           property = "P106") %>%
  dplyr::select(-unknown) %>%
  data.table::setcolorder(order(names(.))) %>%
  dplyr::select(wikidataid, everything())
saveRDS(italy_chamber_occupation, "data/italy_chamber/italy_chamber_occupation")
```

---

<a type="button" class="btn btn-lg btn-block" style="background-color:#0A3b76;color:#fff;" href="#">Go back to the top.</a>
