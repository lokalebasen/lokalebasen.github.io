---
layout: default
---
Medietypen application/vnd.lokalebasen.point_search+json
--------------------------------------------------------

Beskrivelse
-----------

Denne medietype beskriver et dokument, der indeholder information om en
søgning efter lokaler i nærheden af et geografisk punkt.

Elementer
---------

Rodelementet i et `application/vnd.lokalebasen.point_search+json` dokument
indeholder følgende elementer:

* latitude: Breddegrad
* longitude: Længegrad
* kind: Typen af lokale, kan være `office`, `store` eller `warehouse`
* locations: (Valgfri) Liste af emner. Se dokumentationen for
  [lokalebasen.locations+json.md](lokalebasen.locations.json.html).

Det er ikke meningen at klienter skal angive `locations` når de sender
dokumenter af denne type.

Eksempel
--------

    {
      "kind": "warehouse",
      "latitude": 56.1816043,
      "longitude": 9.535053,
      "locations": [
        {
          "self_href": "http://url/to/self",
          "kind": "warehouse",
          "latitude": 56.1816043,
          "longitude": 9.535053,
          "street_name": "Højbovej",
          "house_number": "1 D",
          "floor": "kld.",
          "side": "",
          "postal_code": 4140,
          "postal_district_id": 891057622,
          "area_from": 100.0,
          "area_to": null,
          "title": "Udelukkende lokaler til opbevaring/arkiv i kælderplan",
          "description": "Der er mulighed for at leje 100 m² til opbevaring i kælderen i ejendommen.
      
          Der er i samme ejendom mulighed for at leje op til 716 m² kontor.
      
          Drift er ikke inkl i lejen.",
          "is_built": true,
          "yearly_rent_per_m2_from": 900,
          "yearly_rent_per_m2_to": null,
          "yearly_operational_cost_per_m2_from": 100,
          "yearly_operational_cost_per_m2_to": null,
          "show_as_rented_out_until": null,
          "photos": [
            {
              "full_url": "http://some/url",
              "list_url": "http://some/url",
              "profile_url": "http://some/url"
            }
          ]
        }
      ]
    }

Historik
--------
### 13. juni 2012

Fjernet `radius` rodelement.

### 11. juni 2012

Fjernet `result_href` rodelement. Tilføjet `locations` rodelement.

### 7. maj 2012

Tilføjelse af "radius".

### 19. april 2012

Første udgave.
