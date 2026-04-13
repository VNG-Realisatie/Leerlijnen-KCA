---
title: "Oefening 5-3-6"
date: 2026-03-23
weight: 3.1
leerlijn: 5
paragraaf: "5.3.6"
oefendoel: "Oefen het werken met extensions en restrictions."
---

## Oefening 5.3.6: Extensions en restrictions

Men wil een aantal wijzigingen aanbrengen in de procesdocumenten.

Orderbon
* hierop mag het adres alleen nog maar bij de leveringsgegevens worden vermeld;
* Het element `<omschrijving>` binnen `<artikel>` mag nog maar 30 lang zijn.

betaalbevestiging
* het type klant (Goud, Zilver of Normaal) hoeft hierop niet meer op getoond te worden;
* het adres in `<klantgegevens>` hoeft alleen nog maar de elementen `<straatnaam>`, `<huisnummer>` en `<postcode>` te bevatten. De elementen `<huisnummer-toevoeging>`en `<woonplaats>` komen hierop te vervallen;
* aan het `<artikel>` moet het element `<`stuksprijs>` worden toegevoegd.

Binnen factuur blijft alles zoals het was.

Bewaar gedurende de onderstaande oefeining wederom zelf regelmatig het bestand.

### Onderstaande nog aanpassen!!!


**Opdracht**
1. Ga naar het XML-Schema 'Procesdocumentatie6.xsd' dat je in de voorgaande oefening hebt vervaardigd of open het opnieuw in 'Altova XMLSpy';
2. Om zonodig deze opdracht opnieuw te kunnen doen is het wellicht verstandig het bestand nog even onder een andere naam te bewaren;
3. Wijzig zo nodig de editing modus naar “Text”;
4. We willen een XML-Schema realiseren waarin we zoveel mogelijk hergebruik maken van `xs:complexType` constructies. Maak voor jezelf een overzicht waarin duidelijk wordt welke `xs:complexType` constructies als basis kunnen dienen voor `xs:extension` of `xs:restriction` constructs in andere `xs:complexTypes`.<br/>**Tip** Een `xs:complexType` hoeft niet persé gebruikt te worden in het XML-Schema, het mag ook alleen dienen als basis voor een ander `xs:complexType`. Zo'n `xs:complexType` mag je zelfs abstract maken door er het attribuut `abstract` op te definiëren met de waarde 'true';
5. Breng op basis van het overzicht wijzigingen aan in het XML-Schema;
6. Ga naar “DTD/Schema - Generate Sample XML/JSON/YAML File...”;
7. Kies in het menu “Generate sample XML file” het element `<orderbon>` en klik op “OK”;
8. Check of je de bovenaan deze opdracht beschreven wijzigingen inderdaad hebt weten te realiseren en check ook of er niet tegelijkertijd ongewenste neveneffecten zijn opgetreden. Corrigeer zonodig het XML-Schema waar nodig en check dat vervolgens ook weer. Het gegenereerde bestand hoeft niet bewaard te worden;
9. Herhaal de stappen 6 t/m 8 voor de andere documenten ('betaalbevestiging' en 'factuur').


