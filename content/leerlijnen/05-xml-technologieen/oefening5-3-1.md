---
title: "Oefening 5-3-1"
date: 2026-03-17
weight: 3.1
leerlijn: 5
paragraaf: "5.3.1"
oefendoel: "Oefen het vervaardigen van een XML-Schema met 3 root elementen."
---

## Oefening 5.3.1: Een eenvoudig XML-SChema

We gaan in het onderliggende cursusonderdeel toewerken naar een XML-Schema dat geschikt is voor drie verschillende typen documenten, een orderbon, een betaalbevestiging en een factuur.

Maak daarvoor in een XML-Schema de volgende elementen aan met daarachter tussen haakjes het datatype.
* orderbon (string);
* betaalbevestiging (boolean);
* factuur (integer);
* voorletters (string);
* postcode (string).
* ordernummer (string);

**Opdracht**
* Open in 'Altova XMLSpy' een nieuw document via “File - New...” (of met Ctrl-N);
* Kies “xsd   XML Schema v1.0” en klik op “OK”;
* Wijzig zo nodig de editing modus naar “Text”;
* Zoals je ziet is er direct onder het element `xs:schema` (root niveau) een eerste `xs:element` aangemaakt met daarbinnen een `xs:annotation`. Die laatste kan gebruikt worden om de diverse XML-Schema onderdelen van documentatie te voorzien. Binnen deze cursus zullen we er verder geen aandacht aan besteden;
* Wijzig het `xs:element` zoals in de intro van deze oefening bij 'orderbon' staat aangegeven en voeg ook de vijf andere `xs:element` elementen toe;
* Bewaar het bestand ergens als “Procesdocumentatie1.xml” en meteen ook als “Procesdocumentatie2.xml”;
* Ga naar “DTD/Schema - Generate Sample XML/JSON/YAML File...”;
* Als alles goed is krijg je nu het menu “Generate sample XML file” met daarin in het veld “Please select root” de zes zojuist door je aangemaakte elementen. Selecteer er 1 en klik op “OK”. Er wordt vervolgens een XML-bestand gegenereerd dat voldoet aan het schema;
* Als je wil kan je dit voor alle zes de elementen doen. De gegenereerde bestanden hoeven niet bewaard te worden.

