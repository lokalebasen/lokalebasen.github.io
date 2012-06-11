---
layout: default
---
API til Lokalebasen.dk
======================

Lokalebasens API er et REST API.

URL
---

API'et kan findes på adressen:

    http://www.lokalebasen.dk/api

Medietyper
----------

API'et er baseret på en række medietyper. Den første medietype man møder er
`application/vnd.lokalebasen` og findes på nuværende tidspunkt kun som JSON,
dvs. med typen `application/vnd.lokalebasen+json`. Derudover findes en række
mere specifikke medietyper, f.eks. 
`application/vnd.lokalebasen.location+json`.

Bemærk
------

Det anbefales, at klienten ikke lagrer andre URL'er end ovenstående URL, men
derimod benytter API'ets indbyggede links til at navigere API'et. Der gives
ikke garanti for at URL'er i API'et er stabile, så de kan ændre sig
løbende.
