---
title: "3.2 Metamodel Informatie Modellering (MIM)"
date: 2026-03-04
weight: 32
leerlijn: 3
paragraaf: "3.2"
parent: "Informatiemodellering"
leerdoel: "Begrijpen wat het Metamodel InfromatieModellen inhoudt"
---

## 3.2 Metamodel Informatie Modellering (MIM)

### Wat is MIM?

Het **Metamodel Informatie Modellering (MIM)** is de Nederlandse standaard voor het maken van informatiemodellen. Het biedt een gemeenschappelijke taal en methodologie voor:

- **Semantische interoperabiliteit**: Eenduidige begrippenkaders
- **Modelconsistentie**: Uniforme modelleringsregels
- **Uitwisselbaarheid**: Modellen die verschillende tools kunnen interpreteren

Het MIM kent vier beschouwingsniveaus:

| Niveau | Naam | Focus | Doelgroep |
|--------|------|-------|-----------|
| **1** | Model van begrippen | Betekenis en definities | Business, beleidsmakers |
| **2** | Conceptueel model | Informatiekundige structuur | Informatieanalist |
| **3** | Logisch model | Implementatie-onafhankelijke gegevensstructuur | Gegevensarchitect |
| **4** | Fysiek model | Technische implementatie | Database-ontwerper |

Van deze 4 lagen concentreren wij de uitleg verder op het Conceptueel informatiemodel. Dat is het niveau waarop de informatiemodellen RSGB en RGBZ zich (zouden moeten) bevinden. 

Voor nadere informatie over de andere beschouwings niveaus verwijzen we naar de [documentatie van het MIM](s

### Kernconcepten van een Conceptueel model

Opbouw van een MIM-klassendiagram

Een klasse vertegenwoordigt een objecttype, een relatieklasse of een gegevensgroeptype.

Een attribute vertegenwoordigt een attribuutsoort, een gegevensgrroep of een datatype (enumeratie, referentielijst, enkelvoudig datatype, gestructureerd datatype)

Een attribute beschrijft een eigenschap van een object, een relatieklasse of een gegevensgroeptype.

Veelgebruikte primitieve MIM-datatypen zijn:

CharacterString
Integer
Real
Boolean
Date
DateTime

Daarnaast worden vaak waardelijsten (enumeraties) gebruikt.

Voorbeeld:

<<Enumeratie>>
StatusPand
-------------
InGebruik
BouwvergunningVerleend
Gesloopt
Relaties (Associaties)

Objecttypen worden met elkaar verbonden via associaties.

Voorbeeld:

Gemeente ------------------- Pand
      1                   0..*

Dit betekent:

één gemeente bevat nul of meer panden;
elk pand behoort tot precies één gemeente.

De getallen zijn de multipliciteit.

Veel voorkomende multipliciteiten:

Multipliciteit	Betekenis
1	precies één
0..1	optioneel
*	willekeurig aantal
0..*	nul of meer
1..*	één of meer
Rollen

Aan beide zijden van een relatie staat meestal een rolnaam.

Bijvoorbeeld:

Gemeente
   |
   | omvat
   |
Pand

Pand
   |
   | ligtIn
   |
Gemeente

Daardoor is duidelijk hoe de relatie vanuit beide objecttypen wordt gelezen.

Aggregatie en compositie

MIM gebruikt waar nodig deel-geheelrelaties.

Aggregatie:

Gebouw ◇──── Ruimte

Een ruimte kan los van het gebouw worden beschouwd.

Compositie:

Zaak ◆──── Zaakdocument

Het document bestaat alleen binnen de context van de zaak.

Compositie betekent dus een sterke eigenaarsrelatie.

Generalisatie (overerving)

Wanneer meerdere objecttypen dezelfde eigenschappen hebben, wordt een supertype gebruikt.

          Object
             ▲
      ┌──────┴──────┐
      │             │
    Pand        Verblijfsobject

Gemeenschappelijke attributen worden in het supertype geplaatst.

Enumeraties

Enumeraties beperken toegestane waarden.

<<Enumeratie>>
Geslacht
------------
man
vrouw
onbekend

Een attribuut kan hiervan gebruikmaken.

Persoon
---------
geslacht : Geslacht
Datatypen versus objecttypen

Een belangrijk onderscheid binnen MIM is:

Objecttype

heeft identiteit;
bestaat zelfstandig;
kan relaties hebben.

Voorbeelden:

Persoon
Zaak
Pand

Datatype

heeft geen eigen identiteit;
beschrijft alleen een waarde.

Voorbeelden:

CharacterString
Datum
Adres
GeoPoint
Constraints

Naast de grafische notatie kunnen aanvullende regels worden vastgelegd.

Bijvoorbeeld:

einddatum >= begindatum

of

BSN moet uniek zijn.

Deze constraints worden vaak in natuurlijke taal of met OCL (Object Constraint Language) beschreven.

Stereotypen in MIM

MIM gebruikt UML-stereotypen om de betekenis van modelelementen expliciet te maken.

Veel voorkomende stereotypen zijn:

<<Objecttype>>
<<Attribuutsoort>>
<<Gegevensgroep>>
<<Relatiesoort>>
<<Enumeratie>>
<<Datatype>>
<<Codelijst>>

Deze stereotypen maken duidelijk welke rol een UML-element vervult binnen het informatiemodel.

Voorbeeld van een eenvoudig MIM-model
                    +----------------------+
                    | <<Objecttype>>       |
                    | Gemeente             |
                    +----------------------+
                    | gemeentecode         |
                    | naam                 |
                    +----------------------+
                          1
                          |
                     ligtIn
                          |
                        0..*
                    +----------------------+
                    | <<Objecttype>>       |
                    | Pand                 |
                    +----------------------+
                    | identificatie        |
                    | bouwjaar             |
                    | status               |
                    +----------------------+
                    | status : StatusPand  |
                    +----------------------+

<<Enumeratie>>
StatusPand
-------------------------
InGebruik
Bouw
Gesloopt
Waarom MIM UML gebruikt

Het MIM gebruikt UML als notatie, maar geeft er een specifieke semantiek aan voor informatiemodellering. Daardoor worden modellen zoals RSGB, RGBZ en andere overheidsmodellen op een uniforme manier beschreven. Dat biedt verschillende voordelen:

modellen van verschillende organisaties zijn onderling vergelijkbaar;
dezelfde UML-modellen kunnen worden omgezet naar implementatieformaten zoals XML Schema, JSON Schema, RDF/OWL en OpenAPI;
de betekenis van gegevens wordt eenduidig vastgelegd, los van de techniek waarin ze uiteindelijk worden geïmplementeerd;
leveranciers en overheidsorganisaties kunnen dezelfde modellen hergebruiken.

Kortom, waar een UML-klassendiagram in softwareontwikkeling vaak een blauwdruk voor code is, is het binnen MIM een conceptueel informatiemodel: de nadruk ligt op de betekenis, structuur en samenhang van gegevens, niet op de implementatie. Dat maakt UML onder MIM tot een krachtig instrument voor standaardisatie en interoperabiliteit binnen de Nederlandse overheid.

#### Nederlandse context
MIM wordt gebruikt in:
- **RSGB**: Referentie Semantisch Gegevensmodel Basisregistraties
- **RGBZ**: Referentie Gegevensmodel Burgerzaken
- **iWlz**: Informatiemodel Wet langdurige zorg
- **IMRO**: Informatiemodel Ruimtelijke Ordening

#### Modelleerregels
- **Naamgeving**: Nederlandse conventies voor objecten en attributen
- **Cardinaliteit**: Minimale en maximale aantallen in relaties
- **Multipliciteit**: 0..1, 1..*, etc.
- **Waardebereik**: Toegestane waarden voor attributen

### MIM-specificatie

#### Huidige versie
- **MIM versie**: 1.1.1 (vastgesteld 2022)
- **Beheerder**: Geonovum
- **Status**: Nederlandse standaard

#### Kernprincipes
1. **Platformonafhankelijk**: Niet gebonden aan specifieke technologie
2. **UML-gebaseerd**: Gebruikt UML als basisnotatie
3. **Uitbreidbaar**: Profielen voor domeinspecifieke behoeften
4. **Gestandaardiseerd**: Vaste regels en conventies

### Toolondersteuning

#### Modelleringstools
- **Enterprise Architect**: MIM-profiel beschikbaar
- **Archi**: ArchiMate-gebaseerde modellering
- **GenDoc**: Automatische documentgeneratie
- **ShacMIM**: SHACL-validatie van MIM-modellen

#### Validatie
- **Automatische controles**: Syntactische en semantische validatio
- **Kwaliteitsregels**: Consistentie en volledigheidscontroles
- **Conformiteitstoets**: Naleving van MIM-specificatie

### Leertraject MIM

**Basisniveau:**
- MIM-principes begrijpen
- Beschouwingsniveaus kennen
- Eenvoudige modellen lezen

**Gevorderd:**
- Zelf MIM-conforme modellen maken
- Validatieregels toepassen
- Tooling effectief gebruiken

**Expert:**
- Complexe domeinmodellen ontwikkelen
- MIM-uitbreidingen en profielen maken
- Bijdragen aan MIM-ontwikkeling

### Resources

**Officiële documentatie:**
- [MIM-specificatie Geonovum](https://docs.geostandaarden.nl/mim/mim/)
- [MIM Github Repository](https://github.com/Geonovum/MIM-Werkomgeving)

**Praktische handleidingen:**
- MIM in de praktijk (VNG Realisatie)
- Modelleringshandleidingen per domein
- Tooling-specifieke handleidingen

**Community:**
- MIM-gebruikersgroep
- Expertnetwerk informatiemodellering
- Geonovum kennisplatform

Het beheersen van MIM is essentieel voor het maken van kwalitatief hoogwaardige, interoperabele informatiemodellen binnen de Nederlandse overheid.