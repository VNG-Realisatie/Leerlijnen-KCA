---
title: "Oefening 5-3-4"
date: 2026-03-23
weight: 3.1
leerlijn: 5
paragraaf: "5.3.4"
oefendoel: "Oefen het creëren en gebruiken van globale types."
---

## Oefening 5.3.4: Het creëren en gebruiken van globale types

In deze oefening gaan we het schema “Procesdocumentatie4.xsd”, dat je in de voorgaande oefening hebt bewaard zo aanpassen dat we geen redundant definities meer in het schema hebben staan.

Bewaar gedurende de onderstaande oefeining wedrom zelf regelmatig het bestand.


**Opdracht**
* Ga naar het XML-Schema 'Procesdocumentatie4.xsd' dat je in de voorgaande oefening hebt vervaardigd of open het opnieuw in 'Altova XMLSpy';
* Wijzig zo nodig de editing modus naar “Text”;

***Klantgegevens***
* We hebben in het XML-Schema op 3 locaties het element `<klantgegevens>` gedefinieerd. Knip het element `<xs:complexType>` dat direct in de elementdefinitie van `<klantgegevens>` binnen de structuur voor `<orderbon>` staat en plak deze onderaan het schema direct binnen het element `<xs:schema>`;
* Definieer op het element `<xs:complexType>` dat we zojuist geplaatst hebben een `name` attribuut en geef dat de waarde `Klant`;
* Maak van het element `<klantgegevens>` waaruit we zojuist het element `<xs:complexType>` hebben geknipt een leeg element en plaats er het attribuut `type` met de waarde 'Klant' op;
* Doe met de twee andere `<klantgegevens>` elementen hetzelfde. Daarvoor moet je daar het `<xs:complexType>` verwijderen;
* Bewaar het bestand;
* Wijzig de editing modus naar “Schema” en klik op 'orderbon';
* Je ziet nu het schema in een grafische structuur waarin je de verschillende XML-Schema componenten open en dicht kunt klikken door op de plusjes of minnetjes achter de elementnamen te klikken. Klik 'klantgegevens' open;
* Je ziet nu een geel vlak met linksbovenin de naam 'Klant'. Dit gele vlak vertegenwoordigd de 'complexType' op het hoogste niveau dat we zojuist hebben vervaardigd;
* Via de knop <img width="24" style="display: block; margin-top: 0; margin-bottom: 0;" alt="ToRootView" src="/Leerlijnen-KCA/bestanden/oefeningen-5-3/Root-schemaview.jpg"/> linksboven kun je weer terug naar de vorige view. Bekijk ook even de grafische structuur voor 'factuur' en 'betaalbevestiging';
* Wijzig de editing modus weer naar “Text”. 

***Extension***
* Kijk nu of je dezelfde techniek los kunt laten op de elementen `<naam>`, `<adres>`, `<ordergegevens>`, `<artikel>` en `<leveringsgegevens>` maar vervang de inhoud van de elementen `<ordergegevens>` en `<artikel>` binnen `<factuur>` nog niet. 
Dat laatste element ziet er daar nl. iets anders uit dan op de andere plaatsen. Het bevat daar nl. ook het element `<stuksprijs>`.
* Pas dezelfde techniek toe op het element `<ordergegevens>` binnen `<factuur>` maar noem die complexType 'FactuurOrder';
* Pas ook weer dezelfde techniek toe op het element `<artikel>` binnen de complexType 'FactuurOrder' en noem dat complexType 'ArtikelMetPrijs';
* We gaan er nu voor zorgen dat we de complexType 'Artikel' gaan hergebruiken binnen de complexType 'ArtikelMetPrijs'. Plaats daartoe direct binnen het element `<xs:complexType>` met het `name` attribuut met de waarde 'ArtikelMetPrijs' een `<xs:complexContent>` element;
* Plaats daarbinnen weer een `<xs:extension>` element met als `base` attribuutwaarde 'Artikel';
* Knip nu het `<xs:sequence>` element uit het complexType 'ArtikelMetPrijs' en plaats dat binnen het zojuist vervaardigde '<xs:extension>` element;
* Verwijder tenslotte de elementdefinities van de elementen `<artikelnummer>`, `<productnaam>` en `<omschrijving>`;
* Bewaar het bestand en bekijk de root elementen weer in Schema view.

***SimpleType***
* Op `<xs:simpleType>` elementen kun je dezelfde techniek toepassen. Doe dat op de elementen `<voorletters>`, `<postcode>`, `<ordernummer>` en het attribuut `afleverstatus`;
* Bewaar het bestand, bewaar het ook meteen als “Procesdocumentatie6.xsd” en bekijk de root elementen weer in Schema view.
