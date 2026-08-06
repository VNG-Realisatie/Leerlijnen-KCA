---
title: "6.4 Koppelvlakspecificaties"
date: 2026-08-06
weight: 604
leerlijn: 6
paragraaf: "6.4"
parent: "StUF-standaard"
leerdoel: "Het kunnen lezen en beheren van een StUF koppelvlak standaard met alle documenten die daarbij horen."
---

## 6.4 Koppelvlakspecificaties

Kan StUF-koppelvlakspecificaties lezen en beheren.

### Wat zijn StUF koppelvlakspecificaties?

Een **StUF koppelvlakspecificatie** is een set van documenten die precies beschrijft hoe twee systemen met elkaar kunnen communiceren via StUF-berichten. Het definieert de berichten, scenario's en business-regels die nodig zijn voor succesvolle gegevensuitwisseling. een StUF koppelvlak specificeert hoe de gegevensuitwisseling tussen applicaties en voorzieningen eruit moet zien. Het legt concrete afspraken vast waarmee specifieke gegevens kunnen worden gecommuniceerd. Afspraken over specifieke berichten die tussen bepaalde referentiecomponenten uitgewisseld moeten en/of kunnen worden, afspraken over aanscherping van de berichten uit een StUF sectormodel en afspraken over de wijze waarop die berichten verstuurd moeten worden. In een StUF koppelvlakspecificatie is ook altijd aangegeven op welke referentiecomponenten de specificatie van toepassing is. Een StUF sectormodel is wat dat betreft minder restrictief en laat meer ruimte open voor eigen interpretatie.

Een aantal bekende StUF koppelvlakken zijn:
* Zaak- en Documentservices
* Documentcreatieservices
* en StUF Jeugdzorg

#### Componenten van een StUF koppelvlakspecificatie

De set van documenten van een StUF koppelvlakspecificatie bestaat minimaal uit een **functionele en technische specificatie** en een **berichtcatalogus**. In de eerste staat beschreven wat, waarom en hoe precies wordt uitgewisseld. Denk daarbij ook aan beveiliging en autorisatie. Over het algemeen is dit beschreven in een Word bestand dat wordt gepubliceerd m.b.v. een pdf. Het tweede bestaat uit een set van XML-Schema bestanden die soms gebaseerd zijn op een sectormodel en in dat geval een aanscherping op de berichten in het StUF sectormodel bevatten. Vaak ziet men dat in een koppelvlak ook vrije berichten worden gedefinieerd ten einde tegemoet te kunnen komen aan specifieke wensen m.b.t. de uit te wisselen gegevens.

Optioneel kan een StUF koppelvlakspecificatie ook nog **scenario beschrijvingen** bevatten. Workflows (zowel de happy als de unhappy) en use cases welke bijv. beschreven zijn m.b.v. een Excel spreadsheet. Tenslotte kunnen ook nog **implementatie-voorbeelden** van concrete berichten zijn toegevoegd.

Het opstellen van een koppelvlakspecificatie start altijd vanuit een specifieke behoefte van de business en vindt zijn basis in een informatiemodel, bijv. het RSGB, RGBZ, een ander, niet door VNG Realisatie beheerd, model of een specifiek voor het koppelvlak opgesteld model.

### Functionele en technische specificatie

Een functionele en technische specificatie bevat over het algemeen de volgende onderdelen:


Het opstellen en beheren van StUF-koppelvlakspecificaties vereist grondige kennis van zowel de technische als functionele aspecten van gegevensuitwisseling. Een goede specificatie is de basis voor succesvolle systeemintegratie en interoperabiliteit binnen de overheid.

**Resources:**
- [StUF Testplatform](https://www.stuftest.nl/)
- [GEMMA Koppelvlakspecificaties](https://www.gemmaonline.nl/)