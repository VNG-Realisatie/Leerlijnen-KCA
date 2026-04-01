---
title: "Oefening 5-3-2"
date: 2026-03-17
weight: 3.1
leerlijn: 5
paragraaf: "5.3.2"
oefendoel: "Oefen het beperken van het waardetype van een element."
---

## Oefening 5.3.2: Beperken van waardetypes

In de voorgaande oefening hebben we de elementen `<voorletters>`, `<postcode>` en `<ordernummer>` gedefinieerd. In deze oefening gaan we het waardedomein daarvan beperken. Het element `<voorletters>` mag alleen maar bestaan uit een of meer combinaties van een hoofdletter en een punt (.). Het `<postcode>` element mag alleen waardes bevatten die starten met 4 cijfers direct gevolgd door 2 hoofdletters. En het `<ordernummer>` element mag niet langer dan 13 lang zijn.

**Opdracht**
* Ga naar het XML-Schema 'procesdocument2.xsd' dat je in de voorgaande oefening hebt vervaardigd of open het opnieuw in 'Altova XMLSpy';
* Wijzig zo nodig de editing modus naar “Text”;
* In de definitie van element `<voorletters>` moet een restriction op basis van `xs:string` worden gedefinieerd waarin de regular expression "([A-Z]{1}\.)+" wordt gebruikt.
* Hetzelfde geldt voor de definitie van het element `<postcode>` alleen gebruiken we daar de regular expression "[0-9]{4}[A-Z]{2}".
* Tenslotte moet ook in de definitie van element `<ordernummer>` een restriction worden gedefinieerd. Daarin beperken we echter de lengte tot 13.
* Bewaar het bestand en bewaar het daarna ook meteen als “Procesdocumentatie3.xsd”;
* Ga naar “DTD/Schema - Generate Sample XML/JSON/YAML File...”;
* Kies in het menu “Generate sample XML file” een van de drie zojuist aangepaste elementen en klik op “OK”. Check het resultaat en speel wat met de waardes;
* Doe dit ook voor andere twee aangepaste elementen. De gegenereerde bestanden hoeven niet bewaard te worden.

