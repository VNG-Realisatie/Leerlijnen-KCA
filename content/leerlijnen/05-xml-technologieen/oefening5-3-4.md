---
title: "Oefening 5-3-3"
date: 2026-03-17
weight: 3.1
leerlijn: 5
paragraaf: "5.3.3"
oefendoel: "Oefen het beperken van het waardetype van een element."
---

## Oefening 5.3.3: Definiëren van complexere structuren

In deze oefening gaan de elementen `<orderbon>`, `<factuur>` en `<betaalbevestiging>` flink op de schop. De elementen `<voorletters>`, `<postcode>` en `<ordernummer>` zullen onderdeel gaan uitmaken van de nieuwe structuur.
Hieronder zie je het informatiemodel dat als basis dient voor deze nieuwe structuur.

<img width="932" alt="IM Procesdocumenten" src="/Leerlijnen-KCA/bestanden/oefeningen-5-3/Procesdocumenten.jpg" />

Je ziet dat in deze grafische weergave van het model de objecttypes 'Factuur', 'Orderbon' en 'Betaalbevestiging' anders zijn vormgegeven evenals de relaties die van daaruit naar 'Order' lopen.
Dit komt omdat we al hebben onderkent dat deze objecttypes geen rol spelen in enige database of berichtuitwisseling. De structuur in de documenten zal zoals je zal zien ook niet helemaal overeenkomen met die in dit informatiemodel.

Bewaar gedurende de onderstaande oefeining zelf regelmatig het bestand.


**Opdracht**
* Ga naar het XML-Schema 'Procesdocumentatie3.xsd' dat je in de voorgaande oefening hebt vervaardigd of open het opnieuw in 'Altova XMLSpy';
* Wijzig zo nodig de editing modus naar “Text”;

***Orderbon***
* We starten met de orderbon. Verwijder het `type` attribuut in deze elementdefinitie en creëer een structuur waarin je in een sequence de elementdefinities voor de elementen `<klantgegevens>`, `<ordergegevens>` en `<leveringsgegevens>` plaatst;
* Binnen `<klantgegevens>` doe je hetzelfde t.b.v. de elementen `<naam>` en `<adres>`;
* Binnen `<naam>` doe je wederom hetzelfde. Het element `<voorletters>` dat nu nog direct onder het element `<xs:schema>` staat moet je naar hier verplaatsen. Daarachter definieer je de elementdefinities voor de elementen `<tussenvoegsel>` en `<achternaam>`. De beide laatste elementen mag je als datatype 'xs:string' geven;
* Binnen `<adres>` doe je hetzelfde. Daar doe je hetzelfde met `<postcode>` wat je in `<naam>` met `<voorletters>` hebt gedaan;
* In `<ordergegevens>` plaats je in een sequence de al in het schema voorkomende elementdefinitie van elementen `<ordernummer>` en creëer je een elementdefinitie voor het element `<artikel>`.;
* In artikel creëer je wederom in een sequence de elementdefinities voor `<artikelnummer>`, `<productnaam>`, `<omschrijving>` en `<aantal>`. Deze krijgen allen het datatype 'xs:string' behalve de laatste, die krijgt het datatype 'xs:positiveInteger';
* Tenslotte `<leveringsgegevens>`. Maak daarin een sequence met de elementdefinities voor `<leverdatum>` en `<adres>`. De eerste krijgt als datatype 'xs:date'. Kopieer voor de tweede de structuur zoals je die eerder binnen de elementdefinitie van `<klantgegevens>' hebt gecreëerd. In een van de volgende oefeningen gaan we dit efficienter modelleren;
* Ga naar “DTD/Schema - Generate Sample XML/JSON/YAML File...”;
* Kies in het menu “Generate sample XML file” het element `<orderbon>` en klik op “OK”. Check het resultaat en speel wat met de structuur. Het gegenereerde bestand hoeft niet bewaard te worden;

***Factuur***
* Verwijder het `type` attribuut in de elementdefinitie van `<factuur>` en creëer een structuur waarin je in een sequence de elementdefinities voor de elementen `<klantgegevens>`, `<ordergegevens>` plaatst;
* Binnen de elementdefinitie voor `<klantgegevens>` kopieer je de structuur die je in `<orderbon>` ook hebt gecreëerd voor `<klantgegevens>`;
* In de elementdefinitie `<ordergegevens>` kopieer je de structuur die je in `<orderbon>` ook hebt gecreëerd voor `<ordergegevens>`;
* Breidt de structuur binnen de elementdefinitie voor `<artikel>` vervolgens uit met `<stuksprijs>`. Deze krijgt als datatype 'xs:decimal';
* Ga naar “DTD/Schema - Generate Sample XML/JSON/YAML File...”;
* Kies in het menu “Generate sample XML file” het element `<factuur>` en klik op “OK”. Check het resultaat en speel wat met de structuur. Het gegenereerde bestand hoeft niet bewaard te worden;


***Betaalbevestiging***
* Verwijder het `type` attribuut in de elementdefinitie van `<betaalbevestiging>` en creëer een structuur waarin je in een sequence de elementdefinities voor de elementen `<klantgegevens>`, `<ordergegevens>` plaatst;
* Binnen de elementdefinitie voor `<klantgegevens>` kopieer je de structuur die je in `<orderbon>` en `<factuur>` ook hebt gecreëerd voor `<klantgegevens>`;
* In de elementdefinitie `<ordergegevens>` kopieer je de structuur die je in `<factuur>` ook hebt gecreëerd voor `<ordergegevens>`;
* Voorzie de structuur van de elementdefinitie van `<betaalbevestiging>` van het attribuut `betaald` en geef dat het datatype 'xs:boolean';
* Ga naar “DTD/Schema - Generate Sample XML/JSON/YAML File...”;
* Kies in het menu “Generate sample XML file” het element `<betaalbevestiging>` en klik op “OK”. Check het resultaat en speel wat met de structuur. Het gegenereerde bestand hoeft niet bewaard te worden;


* Bewaar het bestand en bewaar het daarna ook meteen als “Procesdocumentatie4.xsd”.
