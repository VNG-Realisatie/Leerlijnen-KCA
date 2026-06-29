---
title: "3.1 Informatiemodelleren bij VNG-realisatie"
date: 2026-06-29
weight: 31
leerlijn: 3
paragraaf: "3.1"
parent: "Informatiemodelleren bij VNG-Realisatie"
leerdoel: "Context van informatiemodelleren bij VNG-realisatie"
---



## 3.1 Informatiemodelleren bij VNG-realisatie

Informatiemodellen worden binnen VNG-Realisatie vanuit diverse perspectieven opgesteld. Kenniscentrum architectuur voert het beheer over twee informatiemodellen die gebruikt worden als referentie en ook gebruikt worden om uitwisselstandaarden op te baseren. 
Dat zijn het RSGB (Referentiemodel Stelsel van Gemeentelijke Basisgegevens) en het RGBZ (Referentiemodel Gemeentelijke Basisgegevens Zaken).

Deze modellen hebben model gestaan voor bijvoorbeel StUF-BG (RSGB) en StUF-Zaken (RGBZ). Later heeft het RGBZ ook een rol gespeeld bij de totstandkoming van de ZGW-API's (Zaakgericht Werken API's).

Naast deze basismodellen worden er ook infromatiemodellen uitgewerkt in projecten waarbij soms hergebruik gemaakt wordt van de reeds bestaande modellen, maar soms worden ook nieuwe concepten gemodelleerd. Een voorbeeld hiervan is het model voor Klantinteracties (alhoewel niet definitief afgerond en vastgesteld) en de modellen die binnen het programma Omnichannel worden opgeleverd. 

De informatiemodellen zijn ooit opgesteld als Semantische Informatiemodellen. In principe dus Conceptuele infromatiemodellen die met name de semantiek samenhang van de informatie beschrijven zonder dar implementatie-aspecten in door te laten werken. 

De informatiemodellen zijn UML-modellen die conform het MIM ([Metamodel InformatieModellen](./3-2-metamodel-informatie-modellering.md)) is opgesteld zijn. 

We onderhouen deze modellen met behulp van [Sparx Enterprise Architect](../08-modelleer-tooling/8-1-sparx-enterprise-architect.md) in combinatie met [Imvertor](../08-modelleer-tooling/8-3-imvertor.md).

## 3.1.1 UML

De informatiemodellen zijn opgesteld in UML (Unified Modeling Language). Dit is een standaardtaal om de structuur en het gedrag van software- en informatiesystemen visueel te beschrijven. Wij gebruiken bij het beschrijven van een informatiemodel een Klassendiagram met daarbinnen klassen, attributen en relsties die middel **Stereotypen** getypeerd worden. 

Deze Stereotypen zijn ondergebracht in een EA-profiel zodat gegarandeerd wordt dat deze eenduidig worden toegepast.  

Het MIM schrijft voor hoe UML-elementen moeten worden gebruikt en geïnterpreteerd, zodat informatiemodellen eenduidig zijn en automatisch kunnen worden omgezet naar andere representaties (zoals XML Schema, JSON Schema of RDF/Linked Data).

In [3.2 Metamodel Informatiemodellering](./3-2-metamodel-informatie-modellering.md) wordt verder uitgelegd hoe een UML informatiemodel wordt opgebouwd. 
