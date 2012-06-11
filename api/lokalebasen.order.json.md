---
layout: default
---
Medietypen application/vnd.lokalebasen.order+json
-------------------------------------------------

Beskrivelse
-----------

Denne medietype beskriver en ordre vedrørende et eller flere lejemål.

Elementer
---------

Rodelementet i et `application/vnd.lokalebasen.order+json` dokument indeholder
følgende elementer:

* person\_name: Navn på kunde
* company\_name: Navn på virksomhed
* email: Kundens email
* phone\_number: Kundens tlf. nummer
* comment: Evt. kommentar til ordren
* locations:
  * href: URL'er til lokale, der ønskes information om
  * provider\_name: Udbyders firmanavn \*
  * contact\_name: Navn på kontaktperson \*
  * provider\_phone: Udbyders telefonnummer \*
  * contact\_email: Kontaktpersons e-mailadresse \*

_\* Det er ikke tanken at klienten skal POST'e oplysninger om udbyder. Klienten skal blot angive "href"._

Locations
---------

Eksempel
--------

    {
      "person_name": "Kasper Jørgensen",
      "company_name": "Lokalebasen",
      "email": "kj@lokalebasen.dk",
      "phone_number": "70200814",
      "comment": "",
      "locations": [
        {
          "href": "http://url/to/other_location",
          "provider_name": "Company",
          "contact_name": "John Doe",
          "provider_phone": "43214321",
          "contact_email": "john@example.com"
        },
        {
        "href": "http://url/to/other_location",
          "provider_name": "Company",
          "contact_name": "John Doe",
          "provider_phone": "43214321",
          "contact_email": "john@example.com"
        }
      ]
    }

Historik
--------

### 11. juni 2012

Tilføjelse af felter til "locations".

### 23. april 2012

Første udgave.
