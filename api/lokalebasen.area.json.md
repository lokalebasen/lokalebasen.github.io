---
layout: default
---
Medietypen application/vnd.lokalebasen.area+json
-------------------------------------------

Beskrivelse
-----------

Denne medietype beskriver de informationer Lokalebasen har om et geografisk
område.

Elementer
---------

Rodelementet i et `application/vnd.lokalebasen.area+json` dokument indeholder
følgende elementer:

* name: Navn på området
* postal\_districts: Liste over postdistrikter

Postal Districts
----------------

Postal Districts elementet er en liste over de postdistrikter, der ligger i det aktuelle område. Hvert element i listen indeholder følgende attributer:

* name: navn på distriktet
* office\_count: antallet af ledige kontorlokaler i distriktet
* office\_href: adressen på det relevante
  `application/vnd.lokalebasen.locations+json` dokument indeholdende
  kontorlokaler i distriktet
* store\_count: antallet af ledige butikslokaler i distriktet
* store\_href: adressen på det relevante
  `application/vnd.lokalebasen.locations+json` dokument indeholdende
  butikslokaler i distriktet
* warehouse\_count: antallet af ledige produktions/lagerlokaler i distriktet
* warehouse\_href: adressen på det relevante
  `application/vnd.lokalebasen.locations+json` dokument indeholdende
  produktions/lagerlokaler i distriktet

Eksempel
--------

    {
      "name": "København,"
      "postal_districts": [
        {
          "name": "København K",
          "office_count": 132,
          "office_href": "http://some/url",
          "store_count": 14,
          "store_href": "http://some/url",
          "warehouse_count": 6,
          "warehouse_href": "http://some/url"          
        },
        {
          "name": "Hellerup",
          "office_count": 13,
          "office_href": "http://some/url",
          "store_count": 4,
          "store_href": "http://some/url",
          "warehouse_count": 0,
          "warehouse_href": "http://some/url"          
        }
      ]
    }

Historik
--------

### 12. april 2012

Første udgave.
