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

**De SOAP Envelope**

Dit is het hoofdelement dat het gehele bericht omvat. De envelop definieert de begin- en eindstructuur van een SOAP‑bericht en bepaalt dat het document een SOAP‑bericht betreft. Het bevat ook namespace-identifiers die aangeven welke XML‑onderdelen tot welke standaarden behoren.

**De SOAP Header**

De header is optioneel en bevat meta‑informatie, zoals authenticatiegegevens, transactiedetails, routing‑informatie of beveiligingsparameters. In complexe omgevingen speelt de header een belangrijke rol omdat verschillende tussenliggende systemen (zoals gateways, load balancers of message brokers) deze informatie kunnen gebruiken zonder de eigenlijke boodschap te wijzigen.

**De SOAP Body**

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

> **StUF-context:** Un StUF worden de StUF berichtenschema's altijd begeleid door een of meer WSDL bestanden. Zij maken dus onderdeel uit van elk StUF sectormodel en elke StUF-koppelvlakstandaard.

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

**Platform- en programmeertaalonafhankelijk**
Doordat SOAP volledig op XML is gebaseerd, kan het gebruikt worden tussen uiteenlopende systemen, zoals Java, .NET, PHP, Python, mainframes en zelfs oudere legacy‑systemen.

**Sterke standaardisatie**

Via WSDL, WS‑Security, WS‑AtomicTransaction en andere specificaties biedt SOAP een zeer voorspelbare en formele manier om systemen te integreren.

**Betrouwbaarheid en transacties**

SOAP ondersteunt mechanismen voor gegarandeerde aflevering en transactiebeheer. Hierdoor kunnen meerdere services samen één consistente operatie vormen, wat waardevol is in bijvoorbeeld financiële boekingssystemen.

**Beveiliging op enterprise‑niveau**

De combinatie van encryptie, digitale handtekeningen en token‑based authenticatie is robuuster dan wat bij veel REST‑implementaties standaard wordt gebruikt.

### Nadelen van SOAP

Ondanks zijn sterke punten heeft SOAP ook beperkingen:

**Complexiteit**

SOAP‑berichten zijn omvangrijker en moeilijker leesbaar dan moderne alternatieven zoals JSON‑gebaseerde API’s. Dit maakt het minder geschikt voor snelle web‑applicaties of mobiele toepassingen.

**Performance**

XML is zwaarder dan JSON, en de totale berichtstructuur van SOAP leidt tot grotere berichten. Hierdoor nemen netwerkbelasting en parsing‑tijd toe.

**Moeilijk te debuggen**

De uitgebreide structuur en het strikte protocol kunnen foutopsporing bemoeilijken. Tools zijn vaak noodzakelijk om berichten te analyseren.

**Minder flexibel**

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
