---
title: "6.2 StUF folder en XML-Schema structuur"
date: 2026-05-13
weight: 602
leerlijn: 6
paragraaf: "6.2"
parent: "StUF-standaard"
leerdoel: "De folderstructuur van de StUF standaarden kennen en weten hoe de verschillende XML-Schema bestanden met elkaar samenhangen."
---

## 6.2 StUF folder en XML-Schema structuur

### XML-Schema folderstructuur

De StUF standaard en de bijbehorende sectormodellen bestaat naast de documentatie ook uit een set van XML-Schemabestanden die een sterke samenhang hebben met elkaar. De folderstructuur waarin die XML-Schema bestanden zijn opgeslagen is een vast gegeven en de folders, en daarmee ook de XML-Schema bestanden, bevinden zich altijd op dezelfde relatieve locatie van elkaar. We leggen deze structuur hier uit.

**Basisfolderstructuur**

<img width="150" alt="StUF lagenmodel" src="/Leerlijnen-KCA/images/basisfolderstructuur.jpg" />

De XML- en WSDL-schema's behorende bij de onderlaag van de StUF 3.01 standaard bevinden zich in de folder 301. Het gaat daarbij om de volgende bestanden:
* **stuf0301.xsd**<br/>
* **stuf0301mtom.xsd**<br/>Bevat componenten voor het kunnen opnemen van binaire inhoud in de StUF-berichten van de sectormodellen en koppelvlakken.
* **stuf0301_services.wsdl**<br/>Definieert portType en Binding componenten voor het triggerbericht.
* **stuf0301_types.wsdl**<br/>Definieert in WSDL termen de mesages voor de bevestigings-, fout- en triggerberichten.

Deze folder is essentieel voor alle StUF 3.01 XML-Schema's en moet dus ook altijd aanwezig zijn.

**Sectormodellen en hun berichtencatalogi**

<img width="150" alt="StUF lagenmodel" src="/Leerlijnen-KCA/images/sectormodellen.jpg" />

De hier blauw gearceerde folders bevatten de implementaties van de horizontale sectormodellen. Dat is naast documentatie ook XML-Schema en voorbeeld WSDL-Schema componenten waarmee de entiteittypes, attribuuttypes, relatietypes en berichten die gerelateerd zijn met een informatiemodel.

De folder bg0310 betreffen de XML-Schema's en voorbeeld WSDL-Schema's voor het op het informatiemodel RSGB gebaseerde sectormodel StUF-BG 3.10. De folder zkn0310 betreffen de XML-Schema's en voorbeeld WSDL-Schema's voor het op het informatiemodel RGBZ gebaseerde sectormodel StUF-ZKN 3.10. En de folder bg0310 betreffen tenslotte de XML-Schema's en voorbeeld WSDL-Schema's voor het op het informatiemodel ImZTC gebaseerde sectormodel StUF-ZTC 3.10. 

Naast de folder 'entiteiten', waarin de generieke XML-Schema definities per entiteit (zie de informatiemodellen) te vinden zijn, bevatten deze sectormodellen ook nog standaard een tweetal folders die we berichtencatalogi noemen:

* mutatie
* vraagAntwoord 

<img width="210" alt="StUF lagenmodel" src="/Leerlijnen-KCA/images/berichtencatalogi.jpg" />

Deze folders bevatten op de functie van de berichtencatalogus toegespitste aanscherpingen van de in te folder 'entiteiten' gedefinieerde XML-Schema  definities. En daarnaast ook op de functie van de berichtencatalogus betrekking hebbende voorbeeld WSDL-Schema's.

Een berichtcatalogus specificeert samen met zijn voorbeeld-wsdl's een verzameling services waarvan een systeem moet aangeven in hoeverre het deze implementeert in voor dat systeem specifieke wsdl's.

**Ondersteunende standaarden**

In de set van bij StUF benodigde folders komen ook wat folders voor die noodzakelijk zijn omdat de XML-Schema's daarin direct of indirect worden geïmporteerd in de StUF XML-Schema's. Het gaat om die roze gearceerde folders in de onderstaande image:

<img width="150" alt="StUF lagenmodel" src="/Leerlijnen-KCA/images/ondersteunende-standaarden.jpg" />

Een van die standaarden is 'GML' (Geography Markup Language). Dit is een open, internationaal erkend bestandsformaat (gebaseerd op XML), dat wordt gebruikt om geografische informatie en digitale kaarten op te slaan en uit te wisselen. Deze standaard wordt bijv, gebruikt in de entiteit 'Wegdeel' (StUF-BG 3.10) om de geometrische informatie van zo'n wegdeel mee te kunnen verzenden.

**Koppelvlak berichtcatalogi**

Naast de standaard berichtcatalogi kunnen er in een sectormodel ook berichtencatalogi zijn opgenomen voor specifieke op een sectormodel gebaseerde koppelvlakken. Hieronder zie je voor zowel het sectormodel StUF-BG als StUF-ZKN een voorbeeld:

<img width="200" alt="StUF lagenmodel" src="/Leerlijnen-KCA/images/koppelvlakmappen-berichtencatalogi.jpg" />

In de berichtcatalogus 'bg0310/bag' vind je de definitie van samengestelde berichten, gebaseerd op de werkprocessen BAG, die gebruikt kunnen worden voor het melden van BAG mutaties aan alle andere gemeentelijke applicaties.

In de berichtcatalogus 'zkn0310/zs-dms' vind je de definitie van de berichten waarmee aan zaaksysteem en een document management systeem gevuld en bevraagd kan worden.

### Samenhang XML-Schema's

Laten we eens naar de XML-Schema's van StUF-BG 3.10 (folder 'bg0310') kijken zonder daarbij al te veel te focussen op de inhoudelijke aspecten van de in deze XML-Schema's opgenomen entiteiten maar vooral op de generiek toegepaste principes. We nemen daarvoor als voorbeeld de redelijk eenvoudige entiteit 'Huishouden' (ook wel bekend onder de mnemonic 'HHD') en starten met de basale complexTypes. Daarna kijken we hoe de complexTypes voor de verschillende berichten zich hiertoe verhouden. Daar waar nodig zullen we daar andere entiteiten bij betrekken.

**XML-Schema's in 'entiteiten'**

Deze folder bevat de volgende schema's:
* bg0310_ent_basis.xsd
* bg0310_simpleTypes.xsd
* bg0310_stuf_simpleTypes.xsd

***bg0310_ent_basis.xsd***

*Complextypes voor basis entiteittypes*

In 'bg0310_ent_basis.xsd' zijn alle complexTypes die een rol spelen binnen StUF-BG 3.10 op een generieke wijze gemodelleerd opgenomen. Dus zodanig dat ze als basis kunnen dienen voor alle type berichten. In principe is voor elk entiteittype in het RSGB (zie daarvoor de module over het RSGB informatiemodel) een basis complexType gedefinieerd (`XXX-basis`). 'In principe' omdat we bij het verStUFfen van het RSGB technische keuzes maken. Op het verStUFfen zullen we in een ander onderdeel van deze module in gaan. Voor 'HHD' is in ieder geval de complexType `HHD-basis` opgenomen die er als volgt uitziet:

<img width="400" alt="StUF lagenmodel" src="/Leerlijnen-KCA/images/HHD-basis.jpg" />

Dit is tevens de maximale omvang van een antwoordbericht.

Zoals je ziet zijn alle elementen hierin optioneel. Daardoor kunnen we in restrictions op dit complexType elk element dat we willen weglaten. Binnen een basis complexType zijn de complexTypes voor de gerelateerden van relaties en voor de historie-elementen altijd basis complexTypes.

*Relaties*

Basis entiteiten kunnen relaties bevatten. De wijze waarop relaties worden opgenomen in basis entiteiten is nagenoeg altijd hetzelfde. In de entiteit die de relatie bevat wordt deze relatie als een element met een onderscheidende naam (bijv. `heeftAlsOuders`) opgenomen. Vervolgens bevat de relatie een 'gerelateerde' element dat als typering heeft de complexType van de basis entiteit waar de relatie naartoe gaat.

Zo bevat `HHD-basis` een tweetal relaties `BG:isGehuisvestIn` en `BG:heeftAlsLeden` en hebben deze een `BG:gerelateerde` element. Normaliter krijgen de `BG:gerelateerde` elementen een complexType toegekend met de naam `xxx-basis`. In dit geval . Relatie elementen worden in een basis complexType altijd na de `StUF:tijdvakGeldigheid`, `StUF:tijdstipRegistratie`, `StUF:extraElementen`, `historieMaterieel` en/of `historieFormeel` elementen geplaatst. 

Een relatie wordt altijd gemodelleerd in een eigen complexType waarvan de naamgeving (in de basis complexType) aan de volgende syntax voldoet:

> [Mnemonic van het entiteittype dat de relatie bevat][Mnemonic van het entiteittype waar de relatie naartoe loopt of een specialisatie daarvan]-basis 

Voor de relatie `BG:heeftAlsLeden` heet de complexType dus `HHDNPS-basis` die er als volgt uitziet:

<img width="400" alt="StUF lagenmodel" src="/Leerlijnen-KCA/images/HHDNPS-basis.jpg" />

De mnemonic 'NPS' betekent overigens 'Natuurlijk Persoon'.

Een relatie element bevat altijd minimaal het `gerelateerde` element maar mag ook andere elementen bevatten die dan iets zeggen over de relatie (maar niet de `gerelateerde` entiteit). Zo kan de relatie `BG:heeftAlsEchtgenootPartner` die 2 'NPS' entiteiten met elkaar verbindt ook de elementen `BG:soortVerbintenis` en `BG:datumSluiting` bevatten. Daarnaast kan een relatie ook nog elementen als `StUF:tijdvakGeldigheid`, `tUF:tijdstipRegistratie`, `StUF:extraElementen` en `historieMaterieel` bevatten en zelfs eigen relaties.

*Andere gebruikelijke elementen*

Naast relaties kunnen basis entiteiten ook nog de volgende elementen bevatten:
* `StUF:tijdvakGeldigheid`
* `StUF:tijdstipRegistratie`
* `StUF:extraElementen`
* `historieMaterieel`
* `historieFormeel`

De functie van de eerste en de laatste twee heeft te maken met temporele aspecten van het vastleggen van gegevens. Voor een aantal entiteiten, attributen en relaties is het van belang vast te leggen op welk tijdstip een gegeven welke waarde had. Niet alleen m.b.t. de waarde in de werkelijkheid (materiële historie) maar ook m.b.t. de waarde in de registratie (formele historie). Dit is bijv. van belang wanneer in juridische procedures moet worden aangetoond dat op een bepaald tijdstip bekend was dat iets een bepaalde waarde had. Het element `StUF:tijdvakGeldigheid` heeft daarbij betrekking op tijdstippen in de werkelijkheid en `StUF:tijdstipRegistratie` op tijdstippen in de registratie.

Het element `StUF:extraElementen` is tenslotte bedoelt om te voorzien in enige flexibiliteit in de XML-Schema's zodat leveranciers t.b.v. eigen behoeftes extra informatie met een bericht mee kunnen sturen. Tevens wordt dit op het moment veelvuldig gebruikt om XML-Schema's wel aan te kunnen passen aan nieuwe wetgeving zonder de backwardse compatibiliteit van de XML-Schema's aan te tasten. Dat dit zonder duidelijke regels de interoperabiliteit aan kan tasten moge duidelijk zijn.

*Complextypes voor kerngegevens*

Naast de complexType 'HHD-basis' is ook het complexType `HHD-kerngegevens` aanwezig:  

<img width="400" alt="StUF lagenmodel" src="/Leerlijnen-KCA/images/HHD-kerngegevens.jpg" />

Dit definieert de kerngegevens van het 'HHD' entiteittype en wordt gedefinieerd als een restriction op het “HHD-basis” complexType met als elementen diens kerngegevens en de kernrelaties. Ook hierin zijn alle elementen optioneel omdat niet altijd alle kerngegevens beschikbaar hoeven te zijn. Binnen een kerngegevens complexType zijn de complexTypes voor de gerelateerden van relaties en voor de historie-elementen altijd kerngegevens complexTypes.

Tenslotte bevat het XML-Schema 'bg0310_ent_basis.xsd' ook nog complexTypes voor elementgroepen en tabel entiteiten.

*Relaties tussen complexTypes*

Hieronder hebben we nog even de relaties op hoofdlijnen en in generieke zin tussen de diverse complexTypes binnen de XML-Schema's in de 'entiteiten' folder gevisualiseerd.

<img width="300" alt="StUF lagenmodel" src="/Leerlijnen-KCA/images/Structuur-entiteiten.jpg" />

***bg0310_stuf_simpleTypes.xsd***

Dit schema bevat een aantal datatypes en extensions daarop in de StUF namespace maar specifiek bedoelt voor toepassing in StUF-BG 3.10.
Denk aan datatypes voor de elementen `BG:ingangsdatumObject` en `BG:einddatumObject` binnen het entiteittype 'HHD'. Dit soort datatypes komen in meerdere sectormodellen terug en om die reden zijn ze in de StUF namespace ondergebracht.

Daarnaast importeert het t.b.v. toepassing in StUF-BG 3.10 bijv. ook een aantal constructs uit de StUF namespace die worden gebruikt om een aantal standaard StUF attributen te definiëren op elke StUF-BG 3.10 basis complexType. Hieronder een voorbeeld m.b.t. het 'HHD' entiteittype:

<img width="300" alt="StUF lagenmodel" src="/Leerlijnen-KCA/images/HHD-StUF-attributes.jpg" />

Het attribuut `StUF:entiteittype` krijgt altijd een fixed waarde mee die gelijk is aan de mnemonic die voorkomt in de naam van het objecttype of relatietype.

***bg0310_simpleTypes.xsd***

Als je kijkt naar het complexType `HHD-basis` dan zie je dat daarin enkele elementen worden gedefinieerd voor het entiteittype HHD maar die geen relaties vertegenwoordigen. Elementen die binnen de StUF-BG namespace vallen zoals `nummer`, `soort` en `grootte`. Sommige daarvan kunnen ook in andere StUF-BG entiteittypes voorkomen. De datatypes van deze elementen worden in dit XML-Schema en dus ook in de StUF-BG namespace gedefinieerd.

Die definitie gebeurd in 2 stappen. 
* Eerst wordt het simpleType voor het basis datatype gedefinieerd waarbij wordt vastgelegd of het datatype gebaseerd is op een string, integer, boolean of nog ander basisttype. Daarnaast wordt daarin facetten als lengte, minimale waarde, regular expression, enumeratie waarde, etc... vastgelegd. Naamgeving van deze datatypes zijn over het algemeen gebaseerd op de naam van het element dat ze gebruikt;
* Dan wordt een complexType gedefinieerd dat het simpleType uitbreidt met een aantal standaard XML attributes. De naam van deze datatypes bestaat uit de naam van het basis datatype aangevuld met de extensie '-e'.

Hieronder zie je het datatype `HuishoudenSoort-e` dat wordt gebruikt in het element `soort` binnen het 'HHD' entiteittype.

<img width="600" alt="StUF lagenmodel" src="/Leerlijnen-KCA/images/HHD-e-type.jpg" />

Zoals je ziet is het gebaseerd op het basis datatype `BG:HuishoudenSoort`, betreft het een enumeration en beschikt het over een tweetal StUF attributes.

***Opdracht***

Bestudeer de XML-Schema's in de folder 'bg0310/entiteiten' en probeer de in deze paragraaf beschreven principes terug te vinden in andere entiteiten dan 'HHD'.

**XML-Schema's in 'mutaties'**

Deze folder bevat de volgende schema's:
* bg0310_msg_mutatie.xsd
* bg0310_ent_mutatie.xsd
* bg0310_msg_stuf_mutatie.xsd

***bg0310_msg_mutatie.xsd***

Dit XML-Schema bevat de elementen die de StUF-BG 3.10 kennisgeving- en synchronisatieberichten vertegenwoordigen en de complexTypes met de elementen die het eerste niveau van die berichten vormen. Op de synchronisatieberichten ga ik in de rest van deze paragraaf niet verder in.

***bg0310_ent_mutatie.xsd***

Bevat alle complexTypes met de specifieke kennisgevingstructuren van de diverse entiteittypen. In deze paragraaf kijken we even naar hoe `HHD-basis` wordt gebruikt binnen een kennisgevingbericht (soms ook mutatieberichten genoemd). In de bestudering van de StUF standaard heb je al gezien dat er verschillende types kennisgevingberichtsoorten bestaan en wat de onderdelen daarvan zijn. Hier proberen we je inzicht te geven in de principes die ten grondslag liggen aan de vorm van de complexTypes die de payload, dus de inhoud van het 'BG:object' element, van het bericht vormen. Wij gebruiken hiervoor het Lk01 bericht en specifiek het `hhdLk01` bericht als voorbeeld.

De inhoud van het `BG:object` element in dat bericht is gedefinieerd in het complexType `HHD-kennisgeving` op basis van het `HHD-basis` complexType. Deze kent t.o.v. dat '-basis' type een aantal verschillen. Een aantal daarvan hebben te maken met een generiek toegepast principe om het geschikt te maken voor een kennisgevingbericht:

1. Het element `BG:historieMaterieel`, dat wel in `HHD-basis` aanwezig was, komt daar niet voor. Voor een evt. in het '-basis' type aanwezige `BG:historieFormeel` element zou hetzelfde hebben gegolden. Historische gegevens worden niet met deze elementen doorgegeven, daar hebben we de synchronisatieberichten voor. In kennisgevingberichten komen deze elementen dus niet voor;
2. De attributen `StUF:noValue` en `StUF:scope` zijn verwijderd in `HHD-kennisgeving`. Deze hebben alleen een functie in vraagAntwoord berichten;
3. De attributen `StUF:entiteittype` en `StUF:verwerkingssoort` op het `BG:object` element zijn verplicht gemaakt. Als we een kennisgevingbericht sturen moeten we de ontvangende applicatie immers wel vertellen over welk entiteitype het gaat en hoe de verstrekte gegevens moeten worden verwerkt (toevoegen, wijzigen, verwijderen, etc...);
4. In de complexTypes van de relaties is het element `BG:gerelateerde` verplicht gemaakt. Een relatie zonder een gerelateerde is immers geen relatie en er hoeft dan ook niets over worden vastgelegd;
5. De attributen `StUF:entiteittype` en `StUF:verwerkingssoort` zijn op het relatie element verplicht gemaakt. Ook hier moet immers duidelijk zijn om welk entiteittype het gaat en hoe dat verwerkt moet worden;
6. De complexTypes voor de 'gerelateerde' elementen zijn gebaseerd op de '-kerngegevens' complexTypes van de bijbehorende entiteittypes. De achtergrond voor de keuze voor kerngegevens in een gerelateerde in een mutatie is dat het voor een mutatie voldoende is om de gerelateerde te kunnen identificeren c.q. te kunnen vastleggen met gegevens die de gerelateerde uniek identificeren. In een latere mutatie kunnen de gegevens van een gerelateerde altijd nog aangevuld worden;
7. De attributen `StUF:noValue` en `StUF:scope` zijn op de `gerelateerde` elementen verwijderd om dezelfde reden als genoemd bij 2. Op de `BG:gerelateerde` binnen `BG:heeftAlsLeden` is dat echter, waarschijnlijk abusievelijk, achterwege gebleven;
8. De attributen `StUF:entiteittype` en `StUF:verwerkingssoort` zijn op de `gerelateerde` elementen verplicht gemaakt om dezelfde reden als genoemd bij 3 en 5.

*Relaties tussen complexTypes*

Hieronder hebben we nog even de relaties op hoofdlijnen en in generieke zin tussen de diverse complexTypes binnen de XML-Schema's in de 'mutatie' folder gevisualiseerd. Daarin zijn ook de afleidingen van de basis entiteiten meegenomen.

<img width="600" alt="StUF lagenmodel" src="/Leerlijnen-KCA/images/Structuur-mutaties.jpg" />

***bg0310_msg_stuf_mutatie.xsd***

In dit schema worden specifieke per berichttype gedefinieerde complexTypes uit het 'stuf0301.xsd' XML-Schema verder aangescherpt voor gebruik in de kennisgevingberichten. Dat aanscherpen betreft eigenlijk niet meer dan het beperken van de waarde van het XML attribute 'StUF:entiteittype' zodat die niet conflicteert met het entiteittype waar het bericht betrekking op heeft.

***Opdracht***

Bestudeer de XML-Schema's in de folder 'bg0310/mutaties' en probeer de in deze paragraaf beschreven principes terug te vinden in andere entiteiten dan 'HHD'.

**XML-Schema's in 'vraagAntwoord'**

Deze folder bevat de volgende schema's:
* bg0310_msg_vraagAntwoord.xsd
* bg0310_ent_vraagAntwoord.xsd
* bg0310_msg_stuf_vraagAntwoord.xsd

***bg0310_msg_vraagAntwoord.xsd***

Dit XML-Schema bevat de elementen die de vraag- en antwoordberichten vertegenwoordigen en de group definities met de vraagbodies.

***bg0310_ent_vraagAntwoord.xsd***

Dit XML-Schema kan de volgende complexTypes per entiteittype bevatten:

1. de body voor het antwoordbericht (`XXX-antwoord`);
2. de body voor de selectie EN de scope elementen van het vraagbericht (`XXX-vraag`);
6. de body voor alleen de selectie elementen van het vraagbericht (`XXX-vraagSelectie`);
7. de body voor alleen het scope element van het vraagbericht (`XXX-vraagScope`).
3. de body van `gerelateerde` elementen in vraag- en antwoordberichten (`XXX-gerelateerdeVraag`, `XXX-gerelateerdeVraagSelectie`, `XXX-gerelateerdeVraagScope` en `XXX-gerelateerdeAntwoord`);
4. de body van een evt. `historieMaterieel` element (`XXX-historieMaterieel`);
5. de body van een evt. `historieFormeel` en `historieFormeelRelatie` element (resp. `XXX-historieFormeel`, `XXX-historieFormeelRelatie`);

Het aantal verschillende complexTypes geeft al aan dat de structuur van de vraag- en antwoordberichten wat uitgebreider zijn, m.n. de vraagberichten.

*vraagberichten*

Zoals je waarschijnlijk al aan de group definities in het XML-Schema 'bg0310_msg_vraagAntwoord.xsd' hebt kunnen zien bestaat deze uit een vijftal verschillende elementen waarmee:

* de selectiecriteria voor het terug te leveren object of objecten kunnen worden gedefinieerd;
* de terug te leveren gegevens (elementen) kunnen worden aangegeven;
* kan worden aangegeven bij welk object in de selectie gestart moet worden.

Hieronder nog even de verschillende elementen

<img width="300" alt="StUF lagenmodel" src="/Leerlijnen-KCA/images/HHD-VraagBody.jpg" />

Met de `BG:gelijk`, `BG:vanaf` of `BG:totEnMet` kunnen de selectiecriteria in een vraagbericht worden gedefinieerd. Deze elementen hebben altijd een `XXX-vraag` of `XXX-vraagSelectie` complexType als body. Een `XXX:vraagSelectie` complexType is alleen van toepassing als de inhoud van het `BG:scope` element afwijkt van de inhoud van de selectie elementen. Met het `G:scope` element kunnen de terug te leveren elementen worden gedefinieerd. Dit element heeft altijd een `XXX-vraag` of `XXX:vraagScope` complexType als body waarbij de laatste natuurlijk alleen van toepassing is op `BG:scope` elementen die een andere inhoud hebben dan de selectie elementen. 

De belangrijkste regels voor de vraag complexTypes zijn:
* ze bevatten geen van allen historie-elementen (`historieMaterieel` en`historieFormeel`);
* het attribute `StUF:verwerkingssoort` mag er niet in voorkomen;
* de elementen voor attributen en relaties mogen maximaal één keer voorkomen. 
* alleen in de topfundamenteel van een vraag complexType mag het attribute `StUF:scope` voorkomen. Dit is een alternatief voor het gebruik van het `BG:scope` element.

Welke gerelateerde complexTypes gebruikt moeten worden (`XXX-gerelateerdeVraag`, `XXX-gerelateerdeVraagSelectie` of `XXX-gerelateerdeVraagScope`) is afhankelijk van hetzelfde criterium als hierboven bij de `XXX-vraag`, `XXX-vraagSelectie` of `XXX-vraagScope` is beschreven. Soms kan in al deze situaties echter een `XXX-gerelateerde` worden gebruikt.

Met het `BG:start` element kan het object waarmee moet worden gestart worden gedefinieerd. Dit element heeft altijd een `XXX-antwoord` complexType als body.

*antwoordberichten*

In tegenstelling tot vraagberichten kunnen antwoordberichten wel historie-elementen voorkomen. We willen met de vraagberichten Lv07 t/m Lv14 immers juistde materiële danwel formele historie opvragen. Over het algemeen hebben 'gerelateerde' elementen in antwoordberichten  het complexType `XXX-gerelateerdeAntwoord` maar ook hier kan soms een `XXX-gerelateerde` worden gebruikt.

In de topfundamenteel, een relatie element of een `gerelateerde` element binnen een antwoordbericht mogen de attributes `StUF:verwerkingssoort` en `StUF:scope` niet voorkomen. De gegevens in een antwoordbericht hoeven immers niet verwerkt te worden en dienen ook niet voor het bepalen van een scope. Ook het attribute `StUF:noValue` mag  niet voorkomen in het element voor de topfundamenteel en het `gerelateerde` element.

*Relaties tussen complexTypes*

Hieronder hebben we nog even de relaties op hoofdlijnen en in generieke zin tussen de diverse complexTypes binnen de XML-Schema's in de 'vraagAntwoord' folder gevisualiseerd. Daarin zijn ook de afleidingen van de basis entiteiten meegenomen.

<img width="750" alt="StUF lagenmodel" src="/Leerlijnen-KCA/images/Structuur-vraagAntwoord.jpg" />

***bg0310_msg_stuf_vraagAntwoord.xsd***

In dit schema worden specifieke per berichttype gedefinieerde complexTypes uit het 'stuf0301.xsd' XML-Schema verder aangescherpt voor gebruik in de vraag- en antwoordberichten. Dat aanscherpen betreft:
* de parameters voor synchrone danwel asynchrone berichttypes (met of zonder voorzieningen voor formele- en materiële historie). 
* de stuurgegevens per berichttype/entiteittype combinatie waarin o.a. weer de waarde van het XML attribute `StUF:entiteittype` wordt beperkt zodat die niet conflicteert met het entiteittype waar het bericht betrekking op heeft.

Daarnaast voorziet dit XML-Schema nog in simpleTypes t.b.v. sortering.

***Opdracht***

Bestudeer de XML-Schema's in de folder 'bg0310/vraagAntwoord' en probeer de in deze paragraaf beschreven principes terug te vinden in andere entiteiten dan 'HHD'.

### Verdere verdieping

Lees voor een verdere verdieping in de folderstructuren, XML-Schema structuren en naamgevingsconventies de [Ontwerpregels en best practices voor op StUF 3.01 gebaseerde berichten](https://vng-realisatie.github.io/StUF-onderlaag/documenten/Diversen/Stuf_best_practices.pdf).

