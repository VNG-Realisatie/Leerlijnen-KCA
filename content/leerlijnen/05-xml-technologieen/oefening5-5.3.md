---
title: "Oefening 5 5.3"
date: 2026-03-17
weight: 3.1
leerlijn: 5
paragraaf: "5.3.2"
oefendoel: "Oefen het beperken van het waardetype van een element."
---

## Oefening 2: Beperken van waardetypes

In de voorgaande oefening hebben we de elementen `<voorletters>`, `<postcode>` en `<ordernummer>` gedefinieerd. In deze oefening gaan we het waardedomein daarvan beperken. Het element `<voorletters>` mag alleen maar bestaan uit een of meer combinaties van een hoofdletter en een pun (.). Het `<postcode>` element mag alleen waardes bevatten die starten met 4 cijfers direct gevold door 2 hoofdletters. En het `<ordernummer>` element mag niet langer dan 13 lang zijn.

**Opdracht**
* Open in 'Altova XMLSpy' een nieuw document via “File - New...” (of met Ctrl-N);
* Kies “xsd   XML Schema v1.0” en klik op “OK”;
* De editing modus staat nu op “Schema”, wijzig deze naar “Text”;
* Zoals je ziet is er een eerste `xs:element` aangemaakt met daarbinnen een `xs:annotation`. Die laatste kan gebruikt worden om de diverse XML-Schema onderdelen van documentatie te voorzien. Binnen deze cursus zullen we er verder geen aandacht aan besteden;
* Wijzig het `xs:element` zoals in de intro van deze oefening bij 'orderbon' staat aangegeven en voeg ook de twee andere `xs:element` elementen toe;
* Bewaar het bestand ergens als “Procesdocumentatie.xml”;
* Ga naar “DTD/Schema - Generate Sample XML/JSON/YAML File...”;
* Als alles goed is krijg je nu het menu “Generate sample XML file” met daarin in het veld “Please select root” de drie zojuist door je aangemaakte elementen. Selecteer er 1 en klik op “OK”. Er wordt vervolgens een XML-bestand gegenereerd dat voldoet aan het schema;
* Als je wil kan je dit voor alle drie de elementen doen. De gegenereerde bestanden hoeven niet bewaard te worden.

