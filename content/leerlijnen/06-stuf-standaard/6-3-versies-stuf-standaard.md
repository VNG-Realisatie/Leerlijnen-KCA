---
title: "6.3 Versies van de StUF-standaard"
date: 2026-05-13
weight: 603
leerlijn: 6
paragraaf: "6.3"
parent: "StUF-standaard"
leerdoel: "Leerdoel nog toe te voegen"
---

## 6.3 Versies van de StUF-standaard

Kent de twee door VNG Realisatie ondersteunde versies van de StUF-standaard en hun onderlinge verschillen.

### Versie 2.04


!!!!!!!!!!!!!!!!!!!!!! Hieronder kijken of ik kan voorzien in illustraties !!!!!!!!!!!!!!!!!!!!!!!!

Versie 2.04 van de StUF standaar is tezamen met het sectormodel StUF-BG 2.04 in 2004 gepubliceerd. Deze versie van de StUF onderlaag en sectormodel wordt ook nu nog ondersteund. T.o.v. StUF-BG 3.10 is het arsenaal aan berichtsoorten van StUF-BG 2.04 veel beperkter. In StUF-BG 2.04 kennen we alleen de vraag- en antwoordberichten (La01, La02, Lv01 en Lv02), kennisgevingberichten (Lk01), een bevestigingsbericht (Bv01) en een foutbericht (Fo01).

Van synchronisatie(verzoek)berichten en vrije berichten is in StUF 2.04 dus geen sprake.

Waar in StUF 3.01 voor elk berichttype/entiteit combinatie een specifiek bericht is gecreëerd hanteert StUF 2.04 een veel generieker berichtconcept. Zo kent StUF-BG 2.04 slechts één kennisgevingsbericht, één vraagBericht, één synchroonAntwoordBericht en één asynchroonAntwoordBericht. De inhoud van het `<BG:body>` element in deze berichten bestaat uit een keuze van de in XML-Schema gedefinieerde structuren van de diverse in het GFO (de voorloper van het RSGB) onderkende entiteiten. Waar nodig is echter wel voorzien in aparte structuren voor kennisgeving-, vraag- en antwoordberichten. Bij het opstellen van een bericht moet dus steeds uit een van deze structuren worden gekozen. Voor veel entiteiten zijn deze structuren echter niet anders voor kennisgeving- dan voor vraag- of antwoordbericht.

Ook de structuur voor de `<StUF:stuurgegevens>` is in StUF-BG 2.04 generieker van opzet. Voor alle berichten wordt dezelfde structuur gehanteerd. De `<StUF:stuurgegevens>` structuur bevat echter wel specifieke elementen die alleen van toepassing zijn bij specifieke berichttypes. Bij het opstellen van een bericht bepaald de software welke elementen nodig zijn maar kan deze het gerealiseerde bericht slechts beperkt valideren. Wat dat betreft is de 3.10 versie van StUF-BG strakker gedefinieerd al is die definitie wel veel groter.

Dit alles geeft natuurlijk een veel grotere kans op fouten.

### Integratie versie 2.04 met versie 3.01

Voor zowel versie 2.04 als 3.01 is het sectormodel (zie verderop voor een uitleg) StUF-BG gepubliceerd (2.04 resp. 3.10). Voor de transformatie in de keten van StUF-BG 2.04 naar StUF-BG 3.10 en vice versa zijn mapping tabellen gepubliceerd.


### Resources
- [StUF Standaard Versiehistorie](https://www.gemmaonline.nl/index.php/StUF)
- [VNG Realisatie StUF-documentatie](https://vng-realisatie.github.io/StUF-Standaarden/)