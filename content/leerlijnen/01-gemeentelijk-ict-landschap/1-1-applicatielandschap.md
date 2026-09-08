---
title: "1.1 Het gemeentelijk applicatielandschap en de rol van KCA"
date: 2026-05-28
weight: 101
leerlijn: 1
paragraaf: "1.1"
leerdoel: "Hoe is het gemeentelijk applicatielandschap in de praktijk opgebouwd:  werken met pakketten, de rol van gegevensmagazijnen en servicebussen, en wat dit betekent voor de informatie-analist."
---

## 1.1 Het gemeentelijk applicatielandschap

Gemeenten voeren honderden wettelijke taken uit — van het bijhouden van persoonsgegevens tot het verlenen van omgevingsvergunningen. Voor al die taken worden applicaties ingezet.

Het gemeentelijk applicatie-landschap is daarom complex. Daarnaast is het applicatielandschap in vrijwel elke gemeenten anders. Dit wordt veroorzaakt door het feit dat gemeenten hiervoor zelf verantwoordelijk zijn. 
Die verschillen ontstaan o.a. door: 
-  verschillen in omvang
-  de beschikbaarheid van ICT- en Architectuur-kennis binnen een gemeente
-  de ambitie om zaken zelf te ontwikkelen danwel van software van leveranciers gebruik te maken
-  werk dat (veelal kleinere) gemeenten uitbesteden aan andere gemeenten of andersoortige organisaties

Dat leidt op hoofdlijnen tot de volgende indeling, die natuurlijk niet absoluut is: 
-  Grote gemeenten, met name de G4-gemeenten (Utrecht, Rotterdam Den Haag en Amsterdam), zullen veelal onder eigen regie zelf hun applicaties bouwen en beheren. Daarbij is ook vaak sprake van maatwerk
-  Middelgrote gemeenten hebben vaak een hybride landschap van standaardsoftware met daarnaast beperkt zelfbouw of maatwerk van leveranciers
-  Kleine gemeentes maken over het algemeen gebruik van geïntegreerde suites van leveranciers en zijn ook voor de kennis op ICT-gebied vaak afhankelijk van deze leveranciers

In leerlijn 2 gaan we dieper in op die complexiteit middels de GEMMA (GEMeentelijke Model Architectuur)

### Middelgrote en kleine gemeenten werken veel met pakketten

Anders dan grote commerciële organisaties die veel maatwerk-software laten bouwen, kopen gemeenten over het algemeen **standaardpakketten** van gespecialiseerde leveranciers. Dat heeft een aantal praktische redenen:

- Gemeenten hebben zelf geen ICT-capaciteit nodig om eigen systemen te bouwen en te onderhouden.
- Gemeentelijke taken zijn **grotendeels gelijk**: dezelfde wetgeving (BRP, WOZ, Wabo, Wmo) geldt voor alle 342 gemeenten, dus een pakket van één leverancier werkt voor tientallen afnemers waarbij middels configuratie vaak de "gemeente-eigen" aspecten kunnen worden ingeregeld. 
- Leveranciers leveren ook **updates bij wetswijzigingen**, zodat de gemeente zelf niet hoeft te programmeren.

In Nederland is er een relatief kleine groep leveranciers die het merendeel van de gemeentelijke markt bedient.

#### Bekende leveranciers en hun pakketten

| Domein | Leverancier | Pakket(ten) |
|---|---|---|
| **Burgerzaken (BRP)** | Centric | GovUnite, Key2Burgerzaken |
| **Burgerzaken (BRP)** | PinkRoccade Local Government | iBurgerzaken |
| **Belastingen** | Centric | Key2Belastingen |
| **Belastingen** | GBLT / Heffen | diverse belastingsystemen |
| **Zaakgericht werken** | Rx Mission | Rx.Mission |
| **Zaakgericht werken** | Decos | JOIN |
| **Vergunningen (VTH)** | Centric | Squit XO |
| **Vergunningen (VTH)** | Rx Mission | Rx.Mission |
| **Sociaal domein** | Centric | Suite voor Sociaal Domein (SSD) |
| **Sociaal domein** | Stipter | GWS4all |
| **Financiën** | Unit4 | Unit4 ERPx |
| **Financiën** | Centric | Key2Financiën |
| **Openbare ruimte** | Antea Group | Obsurv |
| **Openbare ruimte** | Gobar | GBI |
| **GIS / Geo** | Esri | ArcGIS |
| **GIS / Geo** | PDOK | diverse basiskaartdiensten |
| **Documentbeheer (DMS)** | Decos | Decos ONE |
| **Documentbeheer (DMS)** | Rx Mission | Rx.Mission DMS |
| **Integratie / ESB** | PinkRoccade | MSB Gemeente |
| **Integratie / ESB** | MuleSoft | Anypoint Platform |

> **Tip:** Je ziet Centric en PinkRoccade Local Government terug in veel domeinen. Dit zijn de twee grootste leveranciers voor de Nederlandse gemeentemarkt. Kennis van hun producten en werkwijze is waardevol.

---

### De samenhang: hoe praten die pakketten met elkaar?

Al die losse pakketten moeten gegevens uitwisselen. Een verhuizing, verwerkt in het BRP-systeem, moet ook in het belastingsysteem, het sociaal domein-systeem en het zaaksysteem terechtkomen. Pakketten van verschillende leveranciers spreken bij het uitwisselen van gegevens echter niet automatisch dezelfde taal.

Om de communicatie van gegevens te faciliteren is de **servicebus** ontstaan. Om generiek en meervoudig te gebruiken gegevens te persisteren is het **gegevensmagazijn** ontstaan. Daarnaast is er ook een gemeentelijke uitwisselingsstandaard voor ontworpen (**StUF**)

Op StUF komen we in leerlijn 6 terug.

Een **Enterprise Service Bus** (ESB) — in de gemeentewereld vaak **MSB** (Gemeentelijk Service Bus of Message Service Bus) genoemd — is de digitale postbode van de gemeente. Het is een centraal platform dat berichten tussen applicaties ontvangt, interpreteert en doorstuurt naar de juiste ontvangers.

De servicebus zorgt voor:

- **Routering**: bijvoorbeeld het bericht van BRP gaat naar alle geabonneerde systemen
- **Transformatie**: als systeem A StUF-XML stuurt en systeem B JSON verwacht, kan de bus omzetten
- **Logging**: alle berichtenverkeer wordt vastgelegd, wat helpt bij probleemdiagnose en audittrails
- **Foutafhandeling**: bij mislukte bezorging wordt een foutmelding gegenereerd en eventueel opnieuw geprobeerd

De berichten die over de servicebus gaan, volgen standaardformaten. De belangrijkste zijn **StUF** (Standard Uitwisseling Formaat) voor het klassieke landschap en steeds meer **REST API's** voor modernere koppelingen.

### Het gegevensmagazijn

Naast de servicebus — die voor *actuele* gegevensuitwisseling zorgt — hebben gemeenten ook behoefte aan een **historisch overzicht** en aan analyses over meerdere domeinen heen. Daarvoor wordt een **gegevensmagazijn** (ook wel: datawarehouse of datapakhuis) gebruikt.

Een gegevensmagazijn is een aparte gegevensopslag waarin gegevens uit meerdere bronsystemen worden samengevoegd, geharmoniseerd en bewaard — ook historisch. Applicaties schrijven over het algemeen niet rechtstreeks naar het gegevensmagazijn; ze leveren data aan, die vervolgens wordt getransformeerd (waar nodig)  en vastgelegd. 

Een gegevensmagazijn voorziet in mogelijkheden voor 

| Toepassing | Voorbeeld |
|---|---|
| **Managementrapportage** | Hoeveel WMO-indicaties zijn verstrekt dit kwartaal? |
| **Beleidsinformatie** | Hoeveel kinderen in bijstandsgezinnen ontvangen jeugdhulp? |
| **Wettelijke verantwoording** | Aanlevering CBS-statistieken, iv3-rapportage |
| **Kwaliteitscontrole** | Is iedereen die in het gegevensmagazijn staat met een BSN ook bekend bij de BRP |
| **Gegevens voor domeinspecieke taakafhandeling leveren** | Gegevens uit basisregistraties of uit andere domeinen die nodig zijn voor de afhandeling van een taak |


---

### Samenhang in één beeld

Hieronder staat een geabstraheerd overzicht van de componenten die in het gemeentelijk applicatie landschap relevant zijn. 

![Samenhang in beeld](/images/gegevensmagazijn_en_servicebus.png)

---

### Wat is de rol van KenniscentrumArchtiectuur in deze context

Het Kenniscentrum Architectuur van de VNG (Vereniging van Nederlandse Gemeenten) heeft de rol om gemeenschappelijke architectuurkaders voor VNG-projecten en -programma’s te ontwikkelen en uit te dragen, zodat VNG-werk bijdraagt aan een wendbare en effectieve gemeentelijke informatiehuishouding. 

Dat doet het door te kiezen voor het opbouwen, onderhouden en leveren van diepgaande architectuurexpertise op de niet-domeinspecifieke aspecten van de gemeentelijke informatievoorziening. 

KCA onderzoekt en beproeft innovatieve technieken en methoden om toekomstbestendig te ontwerpen en adviseren hieromtrent. 

Daarbij worden vooral andere partijen ondersteund bij het ontwikkelen en beheren van specifieke standaarden.

Op hoofdlijnen zijn kan je voor de volgende onderwerpen bij KCA terecht: 

-   Kennis over architectuur (met name ArchiMate, Modellering, API’s, registers, interactiepatronen)
-   Kaders: GEMMA referentiearchitectuur en Dienstverlening Doelarchitectuur = DIDO (bewaken van het ontwerp)
-   Platform voor alle architecturen: GEMMA online
-   Beheer van standaarden: StUF, RSGB, RGBZ, imZTC

*(Bron: [Will-E](https://will-e.vng.nl/informatie/kenniscentrum-architectuur))*