---
title: "5.5 SOAP-protocol"
date: 2026-03-04
weight: 7
leerlijn: 5
paragraaf: "5.5"
leerdoel: "Begrijpt SOAP als protocol voor gegevensuitwisseling op basis van XML."
---

## 5.5 SOAP-protocol

Begrijpt SOAP als protocol voor gegevensuitwisseling op basis van XML.

### Wat is SOAP?

SOAP (Simple Object Access Protocol) is een protocol voor communicatie tussen applicaties via een netwerk. Oorspronkelijk ontwikkeld door Microsoft en later gestandaardiseerd door het W3C. SOAP is ontworpen om gestructureerde gegevens uit te wisselen tussen systemen, ongeacht het platform, de programmeertaal of de onderliggende infrastructuur. Dit maakt het bijzonder geschikt voor bedrijfsomgevingen waarin betrouwbaarheid, veiligheid en formele contracten tussen systemen essentieel zijn.

Centraal in SOAP staat het gebruik van XML (eXtensible Markup Language) als berichtformaat. Zie voor meer over XML onderdeel [5.1 XML syntax en structuur](5.1-xml-syntax-en-structuur), [5.2 XML-namespaces](5.2-xml-namespaces) en [5.3 XML-Schema’s (XSD)](5.3-xml-schemas-xsd). SOAP werd vooral populair in de tijd voordat REST zich ontwikkelde tot de dominante standaard voor web‑API’s. Ondanks de opkomst van lichtere alternatieven blijft SOAP breed inzetbaar in sectoren zoals financiële dienstverlening, overheid, gezondheidszorg en zware enterprise IT‑omgevingen.

### Architectuur en opbouw van SOAP‑berichten

Een SOAP‑bericht bestaat uit een XML‑document met een specifieke structuur die uit drie hoofdonderdelen bestaat: de envelop, de header en de body.

**De SOAP Envelope**<br/>
Dit is het hoofdelement dat het gehele bericht omvat. De envelop definieert de begin- en eindstructuur van een SOAP‑bericht en bepaalt dat het document een SOAP‑bericht betreft. Het bevat ook namespace-identifiers die aangeven welke XML‑onderdelen tot welke standaarden behoren.

**De SOAP Header**<br/>
De header is optioneel en bevat meta‑informatie, zoals authenticatiegegevens, transactiedetails, routing‑informatie of beveiligingsparameters. In complexe omgevingen speelt de header een belangrijke rol omdat verschillende tussenliggende systemen (zoals gateways, load balancers of message brokers) deze informatie kunnen gebruiken zonder de eigenlijke boodschap te wijzigen.

**De SOAP Body**<br/>
De body bevat de daadwerkelijke inhoud: het verzoek of de respons. Binnen de body worden één of meerdere XML‑elementen opgenomen die exact beschrijven welke actie een client wil uitvoeren of welk antwoord een server teruggeeft. Een belangrijk element binnen de body is de mogelijke foutmelding, de zogenaamde Fault. Dit onderdeel wordt gebruikt om gestructureerde foutinformatie te communiceren.
Hierdoor biedt SOAP een uniforme manier om zowel succesvolle als mislukte interacties te behandelen.

### Transport en onderliggende protocollen

Hoewel XML de standaard datalaag van SOAP is, staat het protocol zelf los van de transportlaag. HTTP is veruit het meest gebruikte transportmechanisme, maar SOAP kan net zo goed functioneren over SMTP, JMS of andere messaging‑systemen. Dit maakt het geschikt voor situaties waar HTTP niet volstaat of waar een organisatie gebruikmaakt van bestaande message‑queues voor interne processen.

SOAP gebruikt bij communicatie via HTTP meestal POST‑verzoeken. De volledige SOAP‑envelop wordt opgenomen in de body van het HTTP‑verzoek, terwijl HTTP‑headers aanvullende informatie geven over content‑type, encoding en beveiliging.
In omgeving met verhoogde beveiliging kan SOAP bovendien gemakkelijk gecombineerd worden met HTTPS. Hierdoor worden berichten versleuteld en kunnen organisaties voldoen aan strenge compliance‑eisen, bijvoorbeeld binnen de medische of financiële sector.

### WSDL: het contract van een SOAP‑service

Een belangrijk onderdeel van SOAP is WSDL (Web Services Description Language). WSDL‑bestanden beschrijven exact hoe een service gebruikt moet worden. Dit wordt ook wel het “contract” genoemd. WSDL geeft onder meer aan:

* welke operaties beschikbaar zijn;
* welke parameters verwacht worden;
* welke datatypen gebruikt worden;
* welke structuur de verzoeken en antwoorden moeten hebben;
* welk adres de service gebruikt.

Dit contractuele model maakt SOAP bijzonder geschikt voor grote organisaties waar formele afspraken nodig zijn tussen teams, leveranciers en systemen. Tools zoals Visual Studio, Eclipse en enterprise integratieplatforms kunnen automatisch client‑code genereren op basis van het WSDL‑bestand. Dit vermindert fouten en versnelt ontwikkeling.

> **StUF-context:** In StUF worden de StUF berichtenschema's altijd begeleid door een of meer WSDL bestanden. Zij maken dus onderdeel uit van elk StUF sectormodel en elke StUF-koppelvlakstandaard.

### Veiligheid in SOAP

SOAP is nauw verbonden met een reeks beveiligingsstandaarden, vaak aangeduid als WS‑Security. Deze specificaties bieden ondersteuning voor:

* digitale handtekeningen;
* encryptie;
* tokens voor authenticatie;
* timestamp‑validatie;
* rol‑ en rechtenbeheer.

In omgevingen waar vertrouwelijkheid en integriteit cruciaal zijn, zoals het uitwisselen van patiëntgegevens of financiële transacties, bieden deze mechanismen een belangrijke meerwaarde.
WS‑Security werkt voornamelijk via de SOAP‑header, waar beveiligingsgegevens worden opgenomen zonder de eigenlijke body te verstoren. Hierdoor blijven berichten door verschillende systemen transporteerbaar, waarbij elke laag de informatie kan controleren of aanvullen zonder het functionele deel van het bericht te wijzigen.

### Voordelen van SOAP

SOAP heeft zich jarenlang bewezen in complexe bedrijfsomgevingen. Belangrijke voordelen zijn:

**Platform- en programmeertaalonafhankelijk**<br/>
Doordat SOAP volledig op XML is gebaseerd, kan het gebruikt worden tussen uiteenlopende systemen, zoals Java, .NET, PHP, Python, mainframes en zelfs oudere legacy‑systemen.

**Sterke standaardisatie**<br/>
Via WSDL, WS‑Security, WS‑AtomicTransaction en andere specificaties biedt SOAP een zeer voorspelbare en formele manier om systemen te integreren.

**Betrouwbaarheid en transacties**<br/>
SOAP ondersteunt mechanismen voor gegarandeerde aflevering en transactiebeheer. Hierdoor kunnen meerdere services samen één consistente operatie vormen, wat waardevol is in bijvoorbeeld financiële boekingssystemen.

**Beveiliging op enterprise‑niveau**<br/>
De combinatie van encryptie, digitale handtekeningen en token‑based authenticatie is robuuster dan wat bij veel REST‑implementaties standaard wordt gebruikt.

### Nadelen van SOAP

Ondanks zijn sterke punten heeft SOAP ook beperkingen:

**Complexiteit**<br/>
SOAP‑berichten zijn omvangrijker en moeilijker leesbaar dan moderne alternatieven zoals JSON‑gebaseerde API’s. Dit maakt het minder geschikt voor snelle web‑applicaties of mobiele toepassingen.

**Performance**<br/>
XML is zwaarder dan JSON, en de totale berichtstructuur van SOAP leidt tot grotere berichten. Hierdoor nemen netwerkbelasting en parsing‑tijd toe.

**Moeilijk te debuggen**<br/>
De uitgebreide structuur en het strikte protocol kunnen foutopsporing bemoeilijken. Tools zijn vaak noodzakelijk om berichten te analyseren.

**Minder flexibel**<br/>
In tegenstelling tot REST, dat vaak gebruikmaakt van HTTP‑methoden en URI‑structuren, werkt SOAP vrijwel altijd via een gestandaardiseerd POST‑mechanisme. Hierdoor is het minder eenvoudig om op natuurlijke wijze te werken met webconcepten zoals caching of resource‑representatie.

### Toepassingen en praktische inzet

SOAP wordt vandaag vooral gebruikt in:

* banken en financiële instellingen
* overheidsdiensten
* verzekeringsmaatschappijen
* zorginstellingen
* enterprise integratieplatforms
* supply‑chain automatisering

In deze sectoren zijn stabiliteit, contractuele afspraken en beveiliging belangrijker dan de flexibiliteit die REST biedt. Veel grote organisaties hebben duizenden toepassingen die SOAP gebruiken voor interne communicatie. Ook moderne integratietools blijven ondersteuning bieden voor SOAP vanwege de continue vraag vanuit enterprise‑markten.
Daarnaast bestaan er talloze commerciële SaaS‑systemen die nog altijd SOAP‑API’s aanbieden, omdat deze al jarenlang bij klanten in gebruik zijn en kritiek bedrijfsproces ondersteunen.

### WSDL: de relaties binnen het document

Aangezien StUF de SOAP 1.1 Standaard gebruikt duiken we hieronder alleen iets dieper in die versie van de standaard.

Een WSDL‑bestand (Web Services Description Language) is een XML‑document dat de interface van een SOAP‑webservice formeel beschrijft. Het fungeert als een contract tussen een service‑aanbieder en service‑consument. De beschrijving is volledig machine‑leesbaar, zodat ontwikkeltools automatisch proxy‑klassen, clients en stub‑implementaties kunnen genereren.
Een SOAP 1.1 WSDL volgt een strikt gedefinieerde structuur. De kracht van WSDL ligt in de scheiding tussen de abstracte beschrijving van een dienst (welke operaties zijn beschikbaar en welke berichten worden uitgewisseld) en de concrete beschrijving (waar is de service bereikbaar en welk protocol en transportbinding worden gebruikt). Hieronder worden alle onderdelen besproken, inclusief hoe zij onderling samenhangen en hoe XML‑Schema’s het geheel structureren.

**De hoofdstructuur van een WSDL 1.1‑document**<br/>
Elk WSDL‑document begint met een `<definitions>`‑element. Dit fungeert als container voor alle andere onderdelen:

```xml
<definitions name="StUF-BG0310"
             targetNamespace="http://www.egem.nl/StUF/sector/bg/0310"
             xmlns="http://schemas.xmlsoap.org/wsdl/"
			 xmlns:BG="http://www.egem.nl/StUF/sector/bg/0310"
			 xmlns:StUF="http://www.egem.nl/StUF/StUF0301" 
			 xmlns:soap="http://schemas.xmlsoap.org/wsdl/soap/" 
			 xmlns:wsi="http://ws-i.org/schemas/conformanceClaim/" 
			 xmlns:xs="http://www.w3.org/2001/XMLSchema">
```

Binnen dit element kunnen de volgende onderdelen voorkomen:
* types;
* message;
* portType;
* binding;
* service.

Deze onderdelen vormen samen zowel de logische definitie van de service (abstract niveau) als de concrete implementatie (technisch niveau).

**Relatie met XML‑Schema (XSD): `types`**<br/>
Het `<types>`‑element bevat of verwijst naar XML‑Schema’s die de datatypen definiëren die worden gebruikt door de berichten van de webservice. Dit kan inline XSD zijn, maar meestal worden externe schema’s geïmporteerd:

```xml
<types>
	<xs:schema>
		<xs:import namespace="http://www.egem.nl/StUF/sector/bg/0310" schemaLocation="bg0310_msg_mutatie.xsd"/>
	</xs:schema>
</types>
```

*Waarom XSD?*<br/>
* XML‑Schema’s beschrijven de structuur van de gegevens: elementen, attributen, complex types, enumeraties, restricties, etc.;
* Zowel client als server kunnen hiermee de berichten valideren;
* Het WSDL‑bestand zelf blijft overzichtelijk door gebruik van externe schema’s.

*Relaties met de rest van de WSDL:*<br/>
* Het `<message>`-element verwijst naar `<part>`‑elementen die op hun beurt verwijzen naar XSD‑typen;
* Het `<portType>` en `<binding>`-element beschrijven slechts het gedrag (operaties, richtingen), maar typen komen altijd uit XSD.

**Beschrijving van de gegevensstructuren in berichten: `message`**<br/>
Een `<message>`-element in WSDL vertegenwoordigt een bericht dat wordt verstuurd of ontvangen. Het wordt opgebouwd uit één of meerdere `<part>`‑elementen.

Voorbeeld:

```xml
<message name="acdLk01">
	<part name="body" element="BG:acdLk01"/>
</message>
<message name="acdSa01">
	<part name="body" element="BG:acdSa01"/>
</message>
```

*Belangrijk:*
* Een part verwijst rechtstreeks naar een type uit het XSD‑schema (via `element` of `type`);
* Binnen SOAP 1.1 is het gebruik van element de standaard, zodat het bericht overeenkomt met een XML‑element uit de schema’s.

**De abstracte interface: `portType`**<br/>
Het `portType`‑element definieert de operaties die een webservice aanbiedt, zonder details over transport of binding.

```xml
<portType name="OntvangAsynchroon">
	<operation name="acdLk01">
		<input message="BG:acdLk01"/>
		<output message="StUF:Bv03"/>
		<fault name="fout" message="StUF:Fo03"/>
	</operation>
</portType>
```

*Kenmerken:*<br/>
* De operaties vormen de *abstracte contractlaag*.
* Elke operatie definieert een input en output‑message.
* Eventuele foutberichten worden via een fault‑element beschreven.

*Relaties:*<br/>
* Verwijst naar `message` elementen.
* Wordt zelf weer gebruikt in de `binding` en `service`.


**Koppeling abstracte operaties aan concrete protocollen: `binding`**<br/>
Het `binding`‑element beschrijft hoe de operaties uit `portType` moeten worden uitgevoerd via een protocol. Voor SOAP 1.1 betekent dit:

```xml
<binding name="SOAPOntvangAsynchroon" type="BG:OntvangAsynchroon">
	<soap:binding style="document" transport="http://schemas.xmlsoap.org/soap/http"/>
	<operation name="acdLk01">
		<soap:operation soapAction="http://www.egem.nl/StUF/sector/bg/0310/acdLk01"/>
		<input>
			<soap:body use="literal"/>
		</input>
		<output>
			<soap:body use="literal"/>
		</output>
		<fault name="fout">
			<soap:fault name="fout" use="literal"/>
		</fault>
	</operation>
</binding>
```

*Belangrijk:*<br/>
* `type` verwijst naar het `portType`.
* SOAP 1.1 vereist een `soap:binding`.
* De `style` is meestal document/literal (WS‑I standaard).
* Elke operatie krijgt een soapAction, belangrijk voor routing binnen SOAP 1.1.

*Relaties:*<br/>
* Abstracte operaties → concrete SOAP‑operaties.
* SOAP 1.1 specificaties bepalen hoe berichten via HTTP worden verstuurd.

**Eindpuntinformatie: `service`**<br/>
Het laatste element, `<service>`, definieert waar de service daadwerkelijk te bereiken is:

```xml
<service name="OntvangAsynchroon">
	<port name="OntvangAsynchroon" binding="BG:SOAPOntvangAsynchroon">
		<soap:address location="http://example.com/OntvangAsynchroon"/>
	</port>
</service>
```

*Belangrijk:*<br/>
* `binding` koppelt de service aan de eerder beschreven SOAP‑binding.
* `soap:address` bevat de URL van de endpoint.

**Overzicht van de onderlinge samenhang**<br/>
| WSDL‑onderdeel | Doel | Relatie met andere onderdelen | 
| --- | --- | --- |
| types | Definieert XML‑typen (via XSD) | Gebruikt door `message` | 
| message | Definieert de structuur van input, output, fault | Gebruikt door `portType` | 
| portType | Abstracte operaties | Gebruikt door `binding` | 
|binding | Concrete SOAP‑implementatie van operaties | Gebruikt door `service` | 
| service | Endpointinformatie | Verwijst naar `binding` | 

In essentie kun je het zien als lagen:
**DATA (XSD) → BERICHTEN (message) → OPERATIES (portType) → PROTOCOL/TECHNIEK (binding) → LOCATIE (service)**

**Hoe het XML‑Schema het WSDL‑contract versterkt**<br/>
Het XSD is cruciaal omdat het:

* alle datastandaarden afdwingt (types, structuren, enumeraties).
* interoperabiliteit garandeert doordat elke client dezelfde datadefinities gebruikt.
* validatie mogelijk maakt van SOAP‑berichten.
* ontkoppeling biedt: de service‑definitie verandert niet als alleen datatypen worden uitgebreid.

In de praktijk staat ongeveer 70–80% van de functionele inhoud van een SOAP‑service in de XSD’s, niet in de WSDL zelf.

**Samenvatting**<br/>
Een SOAP 1.1 WSDL bestaat uit een hiërarchisch model:

1. **types** – definieert XSD‑typen
2. **message** – maakt berichten met verwijzing naar XSD
3. **portType** – definieert abstracte operaties
4. **binding** – legt SOAP‑protocolregels vast
5. **service** – geeft endpointinformatie

De centraliteit van XML‑Schema zorgt voor strakke, formele en valideerbare berichtenuitwisseling.

<!--SOAP 1.1 is de oudere, maar nog altijd zeer wijdverbreide versie van het SOAP‑protocol. Hoewel SOAP 1.2 later een officieel W3C‑recommendation werd, blijft 1.1 actief in veel enterprise‑systemen, integratietools en commerciële API’s.

**De SOAP 1.1 Envelope: structuur en namespace**

In SOAP 1.1 begint elk bericht met een <Envelope>‑element in de namespace:
```xml
http://schemas.xmlsoap.org/soap/envelope/
```

Deze envelope is verplicht en vormt de volledige container van het bericht. SOAP 1.1 is niet officieel gebonden aan een formeel W3C‑model, maar de structuur is wel strikt gedefinieerd in de oorspronkelijke specificatie. De Envelope bevat exact twee mogelijke subelementen:

* Het `<Header>` element – optioneel
<Body> – verplicht

De volgorde staat vast: header eerst, body daarna.
Het doel van de envelope in SOAP 1.1 is:

een uniforme structuur afdwingen
namespaces introduceren voor verschillende componenten
interoperabiliteit creëren tussen platformen

SOAP 1.1 definieert daarnaast geen expliciet verwerkingsmodel zoals 1.2 dat later deed, maar verwijst impliciet naar de volgorde van verwerking en de betekenis van bepaalde attributen zoals mustUnderstand.

2. De SOAP 1.1 Header: extensies en verwerkingsregels
De SOAP 1.1‑header bevat meta‑informatie die door tussenliggende nodes en eindpunten verwerkt kan worden zonder dat de body hoeft te worden geopend. Header‑elementen kunnen afkomstig zijn uit verschillende namespaces — vaak geïmporteerde XML‑Schema’s — en bieden ruimte voor:

authenticatie‑tokens
routing‑informatie
beveiligingsgegevens (zoals WS‑Security)
transactionele metadata
sessie‑ of correlatie‑ID’s

2.1 Het mustUnderstand‑attribuut
SOAP 1.1 introduceert het attribuut:
soap:mustUnderstand="1"

Hiermee kan een service aangeven dat een header verplicht verwerkt moet worden; anders moet de ontvanger een fout genereren. Bij SOAP 1.2 veranderde de syntaxis, maar in 1.1 blijft dit een eenvoudige boolean in tekstvorm (0/1).
2.2 Relatie tussen Envelope en Header
De header staat logisch los van de body, maar beide maken deel uit van dezelfde envelop‑structuur. De header is de laag waarin verwerkingsregels, policies en beveiligings‑extensies kunnen worden ingebed — allemaal gebaseerd op XML‑Schema’s die bepalen welke elementen toegestaan zijn en welke vorm ze moeten hebben.

3. De SOAP 1.1 Body: operaties en payload
De SOAP 1.1‑body bevat de applicatieve inhoud van het bericht: de parameters van een verzoek of het antwoord van een service. De body volgt de schema’s die via de WSDL of via expliciet geïmporteerde XSD’s worden opgelegd.
3.1 Operationele elementen
Elk request of response in SOAP 1.1 wordt beschreven als een afzonderlijk XML‑element, vaak in een eigen namespace. Voorbeeld:
XML<soapenv:Body>   <m:GetOrderDetails xmlns:m="http://example.com/orders">       <m:OrderID>4455</m:OrderID>   </m:GetOrderDetails></soapenv:Body>Meer regels weergeven
De structuur van dit element wordt volledig bepaald door een XSD‑schema, dat ofwel in een WSDL wordt opgenomen of via import‑regels wordt toegevoegd.
3.2 Het SOAP 1.1 Fault‑element
SOAP 1.1 heeft een andere foutstructuur dan SOAP 1.2. Het Fault‑element bevat:

faultcode
faultstring
faultactor (optioneel)
detail (optioneel, voor toepassingsspecifieke foutdata)

Ook deze elementen worden doorgaans door schema’s beschreven, maar de SOAP 1.1‑specificatie zelf is minder strikt dan die van 1.2.

4. De hiërarchische relatie tussen Envelope, Header en Body
De interne samenhang is als volgt:
Envelope  
 ├── Header  (optioneel, extensiepunt)  
 └── Body    (verplichte payload)

Alle elementen binnen Header en Body delen dezelfde SOAP‑namespace voor de SOAP‑structuur, maar gebruiken vaak aanvullende namespaces voor hun eigen inhoud. Hierdoor kan een enkel bericht informatie uit meerdere schema’s combineren zonder conflicten.
SOAP 1.1 vertrouwt zwaar op namespaces om verschillende XSD‑typen gescheiden te houden. De Envelope biedt de kapstok waarop alle verschillende schema’s worden “opgehangen”.

5. De relatie tussen SOAP 1.1 en XML‑Schema’s (XSD)
XML‑Schema’s zijn essentieel voor SOAP 1.1. Ze bepalen:

welke elementen mogen voorkomen
datatypes (string, int, complex types)
restricties op datatypes
volgorde en cardinaliteit van subelementen

5.1 WSDL en XSD binnen SOAP 1.1
De WSDL (vaak versie 1.1 bij SOAP‑1.1‑services) verwijst via <types> naar XSD‑schema’s waarin de message‑structuren zijn gedefinieerd. Dit vormt een contract tussen partijen:

de WSDL beschrijft operaties, bindingen en endpoints
de XSD’s definiëren parameters en responsstructuren
SOAP 1.1 zorgt voor transport via Envelope/Header/Body

Een typisch SOAP‑request is dus een samenstelling van:

de SOAP‑envelope (op basis van de SOAP 1.1‑namespace)
een operationele payload (op basis van een XSD‑schema)
optionele header‑informatie (vaak op basis van andere schema’s)

5.2 Namespaces en imports
SOAP 1.1‑berichten gebruiken doorgaans meerdere namespaces tegelijk:

SOAP‑namespace voor de envelop
applicatie‑schema’s voor payload
beveiligings‑ of routing‑schema’s voor header‑elementen

Dit maakt SOAP 1.1 zeer modulair en uitbreidbaar.

6. Conclusie
SOAP 1.1 blijft een fundament binnen enterprise‑integraties. Hoewel SOAP 1.2 formeler en consistenter is, biedt SOAP 1.1 dezelfde kernstructuur:

een verplichte Envelope
een optionele Header voor meta‑informatie
een verplichte Body voor functionele inhoud
een sterke koppeling met XML‑Schema’s voor datadefinities

Het is deze combinatie van strikte structuur, schema‑gedreven validatie en uitbreidbaarheid via namespaces die SOAP 1.1 geschikt maakt voor langdurige, betrouwbare en formele systeem‑integraties.-->