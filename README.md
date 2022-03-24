# person-creator

* Vue.js app for finding probable nationalities, age and probable gender based of a persons name
* App includes API calls to the following APIs:
  * [agify.io](https://agify.io/)
  * [genderize.io](https://genderize.io/)
  * [nationalize.io](https://nationalize.io/)

## Information

* Mateo Borina
* 0303088140
* Web aplikacije (Web apps)
* Faculty of informatics in Pula
* Juraj Dobrila University of Pula

## Task / Description

### General description

Zadatak je poslati zahtjev u obliku imena na sva tri endpointa (API-ja) i na temelju tog zahtjeva prikazati sve podatke u jednoj tablici.

### Specific tesk

Prvo treba definirati jedan v-text-field od Vuetifyja u koji se unosi ime. To ime će se iskoristiti kao parametar u slanju get requesta (link + upitnik i jedna "varijabla" -> pr. https://api.nationalize.io?name= + var ). Kada stignu odgovori tih API-ja, prikazati ih u v-datatable od Vuetifyja na način da se prikažu stupci: Ime; Države i Vjerojatnosti; Godine; Spol i Vjerojatnost.
