---
layout: default
---
Medietypen application/vnd.lokalebasen.location+json
----------------------------------------------------

Beskrivelse
-----------

Denne medietype beskriver de informationer Lokalebasen har om et enkelt
lokaler.

Elementer
---------

Rodelementet i et `application/vnd.lokalebasen.location+json` dokument
indeholder følgende elementer:

* self\_href: Kanonisk URL til det aktuelle lokale.
* kind: Typen af lokale, kan være `office`, `store` eller `warehouse`
* latitude: Breddegrad
* longitude: Længdegrad
* street\_name: Vejnavn
* house_number: Husnummer
* floor: Etage
* side: Side
* postal\_code: Postnummer
* area\_from: Arealintervallets minimumstørrelse
* area\_to: Arealintervallets maximumstørrelse, kan være null
* title: Titel
* description: Beskrivelse
* is_built: Er lejemålet opført, boolsk værdi
* yearly\_rent\_per\_m2\_from: Årlig leje i danske kroner, minimum
* yearly\_rent\_per\_m2\_to: Årlig leje i danske kroner, maximum, valgfri
* yearly\_operational\_cost\_per\_m2\_from: Årlige driftsomkostninger i danske kroner, minimum, valgfri
* yearly\_operational\_cost\_per\_m2\_to: Årlige driftsomkostninger i danske kroner, maximum, valgfri
* yearly\_heating\_cost\_per\_m2\_from: Årlig a conto varme i danske kroner, minimum, valgfri
* yearly\_heating\_cost\_per\_m2\_to: Årlig a conto varme i danske kroner, maximum, valgfri
* show\_as\_rented\_out\_until: Vis lejemålet som udlejet
* photos: Liste af billeder

Photos
------

Photos listen indeholder billeder i de 3 definerede størrelser, der bliver
brugt på Lokalebasen. Hvert element i listen har følgende attributer:

* full\_href: Adressen på billedet i fuld størrelse
* list\_href: Adressen på billedet i 80x60 pixels
* profie\_href: Adressen på billedet i 300x225 pixels

Eksempel
--------

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
      "yearly_heating_cost_per_m2_from": 70,
      "yearly_heating_cost_per_m2_to": null,
      "show_as_rented_out_until": null,
      "photos": [
        {
          "full_url": "http://some/url",
          "list_url": "http://some/url",
          "profile_url": "http://some/url"
        }
      ]
    }

Historik
--------

### 26. april 2012

Første udgave.
