---
layout: default
---
Medietypen application/vnd.lokalebasen+json
-------------------------------------------

Beskrivelse
-----------

Denne medietype beskriver startpunktet for Lokalebasen.dk's API.

Elementer
---------

Rodelementet i et `application/vnd.lokalebasen+json` dokument indeholder
indtil videre kun følgende element:

* areas: Områder dækket af Lokalebasen.dk
* point\_searches\_href: URL, hvortil der kan POST'es punktsøgninger
* order\_href: URL, hvortil der kan POST'es ordrer

Areas
-----

Areas elementet er en liste over områder som Lokalebasen.dk dækker. Hvert
element i listen indeholder følgende attributer:

* href: adressen på det relevante `application/vnd.lokalebasen.area+json`
  dokument
* name: navnet for området

PointSearchesHREF
-----------------

Hertil kan der POST'es dokumenter af typen
`application/vnd.lokalebasen.point_search+json`. I `Location` headeren i responset vil stå URL'en til det oprettede dokument.

OrderHREF
---------

Hertil kan der POST'es dokumenter af typen
`application/vnd.lokalebasen.order+json`. I `Location` headeren i responset vil stå URL'en til det oprettede dokument.

Eksempel
--------

    {
      "areas": [
        {
          "href": "http://some/url",
          "name": "Sjælland"
        },
        {
          "href": "http://some/other/url",
          "name": "Fyn"
        }
      ],
      "point_searches_href": "http://some/url",
      "order_href": "http://some/url"
    }

Historik
--------

### 19. april 2012

Tilføjet info om PointSearchesHREF og OrderHREF

### 12. april 2012

Første udgave.
