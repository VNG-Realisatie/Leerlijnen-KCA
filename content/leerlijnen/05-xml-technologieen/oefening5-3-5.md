---
title: "Oefening 5-3-5"
date: 2026-03-30
weight: 3.1
leerlijn: 5
paragraaf: "5.3.5"
oefendoel: "Krijg gevoel voor kardinaliteit."
---

## Oefening 5.3.5: Kardinaliteiten

In deze oefening gaan we er voor zorgen dat in het schema “Procesdocumentatie5.xsd”
* enkele elementen meerdere keren voor mogen komen
* enkele elementen optioneel worden
* en dat het attribuut `betaald` binnen het element `<betaalbevestiging>` verplicht wordt.

Bewaar zelf regelmatig het bestand.


**Opdracht**
* Ga naar het XML-Schema 'Procesdocumentatie5.xsd' dat je in de voorgaande oefening hebt vervaardigd of open het opnieuw in 'Altova XMLSpy';
* Wijzig zo nodig de editing modus naar “Text”;
* Pas het schema zo aan dat de volgende elementen optioneel worden:
  - `<tussenvoegsel>`;
  - `<huisnummer-toevoeging>`;
  - `<omschrijving>`.
* Zorg er voor dat het element `<artikel>` op beide plaatsen waar het voorkomt meerdere keren voor mag komen;
* Maak het attribuut `betaald` tenslotte verplicht;
* Bewaar het bestand, bewaar het ook meteen als “Procesdocumentatie6.xsd” en bekijk de root elementen weer in Schema view.
