---
title: "5.3 XML-Schema's (XSD)"
date: 2026-03-04
weight: 5
leerlijn: 5
paragraaf: "5.3"
leerdoel: "Leerdoel nog toe te voegen"
---

## 5.3 XML-Schema's (XSD)

Kan XML-Schema's (XSD's) lezen, begrijpen en opstellen.

---

### Het probleem: XML is te vrij

In sectie 5.1 heb je geleerd hoe je met XML gegevens structureert. Maar XML zelf legt alleen syntaxregels op — *welgevormdheid*. Het zegt niets over **welke** elementen en attributen zijn toegestaan, in welke volgorde ze mogen voorkomen of welke waarden geldig zijn.

Stel: twee gemeentelijke systemen wisselen persoonsgegevens uit via XML. Systeem A stuurt:

```xml
<persoon>
  <voornaam>Jan</voornaam>
  <achternaam>de Vries</achternaam>
  <geboortedatum>1985-03-15</geboortedatum>
</persoon>
```

Maar systeem B verwacht:

```xml
<persoon>
  <naam>
    <voornaam>Jan</voornaam>
    <achternaam>de Vries</achternaam>
  </naam>
  <geboortedatum>15-03-1985</geboortedatum>
</persoon>
```

Beide documenten zijn **welgevormd** XML. Maar ze zijn niet compatibel: de structuur verschilt (wel of geen `<naam>`-omhulsel) en het datumformaat is anders. Hoe spreek je af welke structuur en welke waarden toegestaan zijn? Hoe controleer je dat automatisch?

### De oplossing: een XML-Schema

Een **XML-Schema** is een formele beschrijving van de toegestane structuur en inhoud van een XML-document. Het is als een *blauwdruk* of *contract*: het legt vast welke elementen er mogen zijn, in welke volgorde, hoe vaak, en welk type waarde ze mogen bevatten.

Met een XML-Schema kun je automatisch controleren of een XML-document geldig is — dit heet **validatie**. Als een document niet voldoet aan het schema, wordt het afgekeurd met een foutmelding die precies aangeeft wat er mis is.

### Wat is XSD precies?

**XSD** staat voor **XML-Schema Definition**. Als we het dus over een XSD-bestand of XSD-Schema hebben dan bedoelen we dus gewoon ook een XML-Schema. 

XML-Schema is een taal om schema's mee te schrijven — en het bijzondere is: **een XSD-bestand is zelf ook XML**. Je gebruikt dus XML om te beschrijven hoe andere XML-documenten eruit moeten zien. Het is zelfs zo dat een XML-Schema ook weer aan een XML-Schema moet voldoen.

| Eigenschap | Uitleg |
|---|---|
| **Voluit** | XML-Schema Definition |
| **Bestandsextensie** | `.xsd` |
| **Formaat** | XML (een XSD is zelf een geldig XML-document) |
| **Doel** | Formeel beschrijven welke structuur en waarden een XML-document mag hebben |
| **Toepassing** | Validatie: automatisch controleren of een XML-document aan de regels voldoet |
| **Beheerder** | W3C (World Wide Web Consortium), dezelfde organisatie achter XML zelf |

### Een eerste voorbeeld

Stel, je wilt vastleggen dat een `<persoon>` precies een `<voornaam>`, een `<achternaam>` en een `<geboortedatum>` moet bevatten. Dan zou je dat als volgt kunnen doen:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">

  <xs:element name="persoon">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="voornaam" type="xs:string"/>
        <xs:element name="achternaam" type="xs:string"/>
        <xs:element name="geboortedatum" type="xs:date"/>
      </xs:sequence>
    </xs:complexType>
  </xs:element>

</xs:schema>
```

| Regel | Betekenis |
|---|---|
| `<xs:schema xmlns:xs="...">` | Het root-element van elk XSD-bestand; de prefix `xs` verwijst naar de XML-Schema-namespace |
| `<xs:element name="persoon">` | Op root niveau moet een element `<persoon>` bestaan |
| `<xs:complexType>` | Het element `<persoon>` heeft een complexe opbouw (het bevat kind-elementen en/of attributen) |
| `<xs:sequence>` | De kind-elementen moeten in de opgegeven volgorde voorkomen |
| `<xs:element name="voornaam" type="xs:string"/>` | Er moet een element `<voornaam>` zijn, met een tekstwaarde |
| `<xs:element name="geboortedatum" type="xs:date"/>` | Er moet een element `<geboortedatum>` zijn, met een datumwaarde (formaat `JJJJ-MM-DD`) |

Een volgens dit XML-Schema correct XML-document kan er als volgt uitzien:

```xml
<persoon>
  <voornaam>Jan</voornaam>
  <achternaam>de Vries</achternaam>
  <geboortedatum>1985-03-15</geboortedatum>
</persoon>
```

Hieronder ook een voorbeeld van een XML-document waarin, volgens het XML-Schema, twee fouten staan:

```xml
<persoon>
  <achternaam>de Vries</achternaam>
  <voornaam>Jan</voornaam>
  <geboortedatum>15 maart 1985</geboortedatum>
</persoon>
```

Een XML-Parser kan op basis van voorgaand XML-fragment bijv. de volgende foutmelding genereren:

<img width="660" alt="Validate" src="/Leerlijnen-KCA/images/Foutmeldingen.jpg" /> 

Dit betekent zoveel als
1. het element `<achternaam>` komt vóór het element `<voornaam>`. Het schema eist echter een volgorde waarbij `<achternaam>` na het element `<voornaam>` maar ook vóór het element `<geboortedatum>` staat.
2. Het element `<geboortedatum>` heeft de waarde `"15 maart 1985"`. Het schema eist echter een waarde die voldoet aan het datatype`xs:date` wat betekent dat een formaat als `JJJJ-MM-DD` moet worden gebruikt.

> **Let op!** We gaven eerder al aan dat XML case-sensitive is. Definieer je in je XML-Schema dus als volgt een element `<xs:element name="voornaam" type="xs:string"/>` dan kan je in je XML-bestand niet het element `<Voornaam>` gebruiken. Tenminste niet als je wil dat het aan een XML-Schema voldoet. Dit betekent echter ook dat je in je XML-Schema naast het element `<voornaam>` ook een element `<Voornaam>` kan definiëren. Doe dat echter met uiterste terughoudendheid. Voor een computer is het verschil heel duidelijk maar voor een mens die het XML-Bestand moet interpreteren is dat heel wat minder het geval.

### Welgevormd vs. valide

In het onderdeel '5.1 XML syntax en structuur' hebben we de welgevormdheid van een XML-bestand behandelt. Daarbij gaven we aan dat een XML-bestand daarnaast ook nog valide kan zijn. Dat is een cruciaal onderscheid:

| Begrip | Betekenis | Gecontroleerd door |
|---|---|---|
| **Welgevormd** (well-formed) | Het document voldoet aan de XML-syntaxregels (zie 5.1) | Elke XML-Parser |
| **Valide** | Het document voldoet aan de XML-syntaxregels en aan een specifiek schema (XSD) | Een XML-Parser met het bijbehorende XML-Schema |

Een document moet **eerst** welgevormd zijn voordat het gevalideerd kan worden. De volgende beslisboom is dus van toepassing:

```text
Stap 1: Is het welgevormd?  → Nee  → Afgekeurd (syntaxfout)
                            → Ja   → Stap 2: Is het geldig volgens het schema?
                                              → Nee  → Afgekeurd (validatiefout)
                                              → Ja   → Geaccepteerd ✓
```

<!-- ### XSD vs. DTD <-- _Ik twijfel of we dit wel moeten opnemen. Ik ben al meer dan 20 jaar geen DTD meer tegengekomen._

Voordat XSD bestond (W3C-standaard in 2001), werden structuren beschreven met **DTD's** (Document Type Definitions). XSD is de opvolger:

| Eigenschap | DTD | XSD |
|---|---|---|
| **Formaat** | Eigen, niet-XML syntax | XML |
| **Datatypen** | Nauwelijks (alleen tekst) | Uitgebreid: string, integer, date, boolean, etc. |
| **Namespace-ondersteuning** | Geen | Volledig |
| **Restricties** | Zeer beperkt | Uitgebreid: patronen, min/max, enumeraties, etc. |
| **Hergebruik** | Beperkt | Typen, includes, imports, overerving |

> **StUF-context:** StUF gebruikt uitsluitend XSD, DTD's zijn hier niet relevant. -->

### Waarom is XSD belangrijk voor StUF?

StUF-berichten worden gedefinieerd door een set XSD-schema's:

1. **Contract tussen systemen** — Het schema legt exact vast hoe een bericht eruit moet zien. Als een leverancier een systeem bouwt dat StUF-berichten verstuurt, moet het elk bericht valideren tegen het relevante StUF-schema.
2. **Automatische validatie** — Vóórdat een bericht verwerkt wordt, kan het ontvangend systeem het automatisch valideren. Bij een succesvolle validatie weet dat systeem dat het dat bericht zonder problemen kan verwerken.
3. **Documentatie** — De XSD-schema's zijn tegelijk de technische documentatie van de standaard.
4. **Gelaagde opbouw** — StUF-schema's zijn modulair opgebouwd in lagen (basisschema → sectormodel → koppelvlak), mogelijk gemaakt door XSD-mechanismes als `import`, `include` en type-overerving.

### De structuur van een XSD-bestand

Elk XSD-bestand is zelf een XML-document en kan zelf, zoals al eerder opgemerkt, ook weer tegen een XML-Schema (ook wel een meta-schema genaamd) gevalideerd worden. Het root-element is altijd `<xs:schema>`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">

  <!-- Hier komen je definities -->

</xs:schema>
```

| Onderdeel | Betekenis |
|---|---|
| `<xs:schema>` | Het root-element van elk XSD-bestand |
| `xmlns:xs="http://www.w3.org/2001/XMLSchema"` | De namespace-declaratie die de prefix `xs` koppelt aan de XML-Schema-namespace |

De prefix `xs` is conventie — je kunt ook `xsd` kiezen. In de praktijk zie je zowel `xs:` als `xsd:`. Soms zelfs beide in een set van XML-Schema's.

### Elementen definiëren met `xs:element`

De meest fundamentele bouwsteen van XSD is het element om een element mee te definiëren:

```xml
<xs:element name="voornaam" type="xs:string"/>
```

Dit zegt: *"Er moet een element `<voornaam>` bestaan, en de inhoud moet tekst zijn."*

| Attribuut | Betekenis | Voorbeeld |
|---|---|---|
| `name` | De naam van het element in het met het XML-Schema gekoppelde XML-bestand | `name="voornaam"` |
| `type` | Het datatype van de inhoud | `type="xs:string"` |

Een `<xs:element ...>` element direct onder het `<xs:schema>` element definieert een root element, een element waarmee een XML-bestand mag beginnen. Dat mogen er meer dan één zijn zodat je bij het aanmaken van een XML-Bestand op basis van dat schema kunt kiezen welke je root element is.

### Ingebouwde datatypen

In het voorbeeld in de voorgaande paragraaf werd m.b.v. het `type` attribuut het datatype van het `<voornaam>` element gedefinieerd. In dit geval het `xs:string` datatype, tekst dus. Dit is niet het enige datatype dat je kunt definiëren. Het W3C heeft naast de XML-Schema standaard nl. een uitgebreide set van **ingebouwde datatypen** gedefinieerd. Een parser die XSD‑validatie ondersteunt, moet dus ook o.a. de volgende datatypes kennen:

**Teksttypen:**

| Type | Beschrijving | Voorbeeldwaarde |
|---|---|---|
| `xs:string` | Tekenreeksen (ondersteunt spaties, tabs, etc.). | `" Jan de   Vries "` |
| `xs:normalizedString` | Tekenreeksen waarin regeleinden en tabs zijn vervangen door spaties. | `" Jan de Vries "` |
| `xs:token` | Tekenreeksen waarbij ook overtollige spaties aan het begin, einde en dubbele spaties worden verwijderd. | `"Jan de Vries"` |

**Numerieke typen:**

| Type | Beschrijving | Voorbeeldwaarde |
|---|---|---|
| `xs:integer` | Gehele getallen (positief, negatief of nul). | `42`, `-7` |
| `xs:positiveInteger` | Gehele getallen > 0. | `1`, `100` |
| `xs:decimal` | Getallen met een vaste komma. | `3.14`, `-0.5` |

**Datum- en tijdtypen:**

| Type | Beschrijving | Voorbeeldwaarde |
|---|---|---|
| `xs:date` | Datum (JJJJ-MM-DD). | `2026-03-04` |
| `xs:time` | Tijd in de notatie hh:mm:ss). | `14:30:00` |
| `xs:dateTime` | Combinatie van datum en tijd. | `2026-03-04T14:30:00` |
| `xs:gYear` | Alleen een jaar | `2026` |
| `xs:duration` | Tijdsduur (PnYnMnDTnHnMnS). | `P1Y2M3D` (1 jaar, 2 maanden, 3 dagen)<br/> `P1Y2M3DT2H13M30S` (1 jaar, 2 maanden, 3 dagen), 2 uur, 13 minuten en 30 seconden).|

**Overige typen:**

| Type | Beschrijving | Voorbeeldwaarde |
|---|---|---|
| `xs:boolean` | Waar of onwaar | `true`, `false`, `1`, `0` |
| `xs:anyURI` | Een URI/URL/URN | `http://www.example.nl` |

> **Let op:** Het kiezen van het juiste datatype is belangrijk. Als je `xs:string` gebruikt voor een geboortedatum, accepteert het schema elke tekst — ook "gisteren" of "binnenkort". Met `xs:date` dwing je het formaat `JJJJ-MM-DD` af.

### Oefening 5.3.1

[Naar de oefening](../oefening-5-3-1).

### Simpel vs. complex

Een element kan van een complex of simpel type zijn. Elementen van het **simpele** type bevatten alleen een waarde (tekst, getal, datum) maar geen kind-elementen en attributen. Elementen van het **complexe** type kunnen naast een waarde wel kind-elementen en/of attributen bevatten. 

In de volgende paragrafen bouwen we voort op dit inzicht door het beperken van simpele en complexe types of het uitbreiden van complexe types m.b.v. een `<xs:simpleType>` of een `<xs:complexType>`.

### Simpele typen met restricties

Vaak wil je de toegestane waarden verder beperken. Bijvoorbeeld: een postcode moet precies 4 cijfers gevolgd door 2 letters zijn. Daarvoor gebruik je dan een **facet** binnen een `<xs:restriction>`, hieronder een voorbeeld met de facet `<xs:pattern>`:

```xml
<xs:element name="Postcode">
  <xs:simpleType>
    <xs:restriction base="xs:string">
      <xs:pattern value="[0-9]{4}[A-Z]{2}"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```
<br/>

**Enkele beschikbare facets:**

| Facet | Werkt op | Betekenis | Voorbeeld |
|---|---|---|---|
| `xs:minLength` | Tekst | Minimaal aantal tekens. | `<xs:minLength value="1"/>` |
| `xs:maxLength` | Tekst | Maximaal aantal tekens. | `<xs:maxLength value="100"/>` |
| `xs:length` | Tekst | Exact aantal tekens. | `<xs:length value="6"/>` |
| `xs:pattern` | Tekst | Moet voldoen aan een reguliere expressie. | `<xs:pattern value="[0-9]{4}[A-Z]{2}"/>` |
| `xs:enumeration` | Alle typen | Waarde moet uit een hierin gedefinieerde lijst van waarden komen. | `<xs:enumeration value="M"/>` |
| `xs:minExclusive` | Getallen/datums | Minimale waarde (exclusief) | `<xs:minExclusive value="8.23"/>` |
| `xs:maxInclusive` | Getallen/datums | Maximale waarde (inclusief) | `<xs:maxInclusive value="2023-01-01"/>` |
| `xs:totalDigits` | Getallen | Maximaal aantal cijfers totaal | `<xs:totalDigits value="5"/>` |
| `xs:fractionDigits` | Decimalen | Maximaal aantal decimalen | `<xs:fractionDigits value="2"/>` |

**Voorbeeld: enumeratie (vaste keuzelijst)**

```xml
<xs:element name="Geslacht">
  <xs:simpleType>
    <xs:restriction base="xs:string">
      <xs:enumeration value="M"/>
      <xs:enumeration value="V"/>
      <xs:enumeration value="O"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```

Binnen het element `<Geslacht>` zijn alleen de waaden `M`, `V` of `O` toegestaan. Elke andere waarde is ongeldig.

**Voorbeeld: patroon (reguliere expressie)**

```xml
<xs:element name="BSN">
  <xs:simpleType>
    <xs:restriction base="xs:string">
      <xs:pattern value="[1-9]\d{8}"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```

Definieert dat het element `<BSN>` uit 9 cijfers moet bestaan waarvan het eerste cijfer niet de waarde '0' mag hebben.

**Restricties combineren:**

```xml
<xs:element name="Postcode">
  <xs:simpleType>
    <xs:restriction base="xs:string">
      <xs:length value="6"/>
      <xs:pattern value="[0-9]{4}[A-Z]{2}"/>
    </xs:restriction>
  </xs:simpleType>
</xs:element>
```

Definieert dat het element `<Postcode>` uit 4 cijfers bestaat gevolgd door 2 hoofdletters. Daarnaast mag het niet uit meer dan 6 karakters bestaan. In feite is de facet `<xs:length>` hier overbodig aangezien het facet `<xs:pattern>` al definieert dat de maximale lengte 6 karakters is.

> **StUF-context:** In StUF-schema's worden restricties veelvuldig gebruikt. BSN's moeten precies 9 cijfers zijn, postcodes hebben een vast patroon, en geslachtsaanduidingen komen uit een vaste lijst.

### Oefening 5.3.2

[Naar de oefening](../oefening-5-3-2).

### Complexe typen: elementen met structuur

In de praktijk bevatten de meeste elementen **kind-elementen** en/of **attributen**. Om dat te kunnen definiëren heb je een `<xs:complexType>` nodig.

Hieronder enkele voorbeelden:
* Een element met één of meer kind-elementen:
  ```xml
  <xs:element name="persoon">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="voornaam" type="xs:string"/>
        <xs:element name="achternaam" type="xs:string"/>
      </xs:sequence>
    </xs:complexType>
  </xs:element>
  ```
* Een element met kind-elementen en attributen:
  ```xml
  <xs:element name="kostprijs">
    <xs:complexType>
      <xs:sequence>
	    <xs:element name="btw" type="xs:positiveInteger"/>
	    <xs:element name="prijs" type="xs:nonNegativeInteger"/>
        <xs:element name="totaal" type="xs:nonNegativeInteger"/>
      </xs:sequence>
      <xs:attribute name="valuta" type="xs:string"/>
    </xs:complexType>
  </xs:element>
  ```
* Een element met alleen een attribuut:
  ```xml
  <xs:element name="klantRef">
    <xs:complexType>
      <xs:attribute name="id" type="xs:string"/>
    </xs:complexType>
  </xs:element>
  ```
  Het volgende XML fragment voldoet daaraan:
  ```xml
  <bedrag valuta="EUR">1500.00</bedrag>
  ```

Het volgende valt hier op:
* Voor het toekennen van kind-elementen is een `<xs:sequence>` nodig. Dit element is een van de drie te gebruiken **compositors**. In de volgende paragraaf gaan we hier iets dieper op in;
* De definitie van een attribuut vindt direct plaats binnen een `<xs:complexType>` element behalve als het element zelf alleen tekstuele content (xs:sring, xs:integer, etc...) kan bevatten. In dat geval wordt een `<xs:simpleContent>` element geplaatst in het `<xs:complexType>` element.

### Compositors: de volgorde van kind-elementen

XML-Schema kent drie compositors die beschrijven hoe kind-elementen zich tot elkaar verhouden. We benoemen ze hieronder en illustreren ze met een voorbeeld:

**xs:sequence**
De elementen moeten in de gedefinieerde volgorde worden geplaatst.

```xml
<xs:complexType name="PersoonType">
  <xs:sequence>
    <xs:element name="voornaam" type="xs:string"/>
    <xs:element name="achternaam" type="xs:string"/>
    <xs:element name="geboortedatum" type="xs:date"/>
  </xs:sequence>
</xs:complexType>
```

> **StUF-context:** StUF-schema's gebruiken vrijwel uitsluitend `xs:sequence`. De volgorde van elementen in StUF-berichten is altijd vast.

**xs:choice**
Er moet een keuze uit de gedefinieerde elementen worden gemaakt. Later zullen we zien dat er mechanismes zijn waarmee we deze keuze meerdere keren achter elkaar kunnen maken.

```xml
<xs:complexType name="ContactType">
  <xs:choice>
    <xs:element name="email" type="xs:string"/>
    <xs:element name="telefoon" type="xs:string"/>
    <xs:element name="postadres" type="xs:string"/>
  </xs:choice>
</xs:complexType>
```

**xs:all**
Alle elementen mogen in een willekeurige volgorde worden geplaatst. Ze kunnen echter maar één keer geplaatst worden maar mogen ook achterwege blijven.

```xml
<xs:complexType name="AdresType">
  <xs:all>
    <xs:element name="straat" type="xs:string"/>
    <xs:element name="huisnummer" type="xs:positiveInteger"/>
    <xs:element name="postcode" type="xs:string"/>
  </xs:all>
</xs:complexType>
```

Het is toegestaan compositors in elkaar op te nemen. Het volgende is dus correct:

```xml
<xs:complexType name="AdresType">
  <xs:choice>
    <xs:sequence>
      <xs:element name="postbusnummer" type="xs:positiveInteger"/>
      <xs:element name="postcode" type="xs:string"/>
    </xs:sequence>
    <xs:sequence>
      <xs:element name="straat" type="xs:string"/>
      <xs:element name="huisnummer" type="xs:positiveInteger"/>
      <xs:element name="postcode" type="xs:string"/>
    </xs:sequence>
   </xs:choice>
</xs:complexType>
```

### Attributen definiëren in XSD

Zoals je in een van de voorgaande paragrafen al in de voorbeelden zag definieer je attributen m.b.v. `<xs:attribute>`, **na** de compositor:

```xml
<xs:complexType name="AdresType">
  <xs:sequence>
    <xs:element name="straat" type="xs:string"/>
    <xs:element name="huisnummer" type="xs:positiveInteger"/>
  </xs:sequence>
  <xs:attribute name="type" type="xs:string"/>
</xs:complexType>
```

Net als elementen kan je attributen met een eigen restrictie-type definiëren. Zoals bij hieronder met een enumeration:

```xml
<xs:simpleType name="MutatiesoortType">
  <xs:restriction base="xs:string">
    <xs:enumeration value="T"/>
    <xs:enumeration value="W"/>
    <xs:enumeration value="V"/>
  </xs:restriction>
</xs:simpleType>

<xs:attribute name="mutatiesoort" type="MutatiesoortType"/>
```

> **StUF-context:** Het attribuut `mutatiesoort` is een van de meest kenmerkende attributen in StUF-berichten. Het geeft aan wat voor soort wijziging het bericht vertegenwoordigd (Toevoeging, Wijziging, Verwijdering, etc.).

### Oefening 5.3.3

[Naar de oefening](../oefening-5-3-3).

### Lokaal vs globaal

Tot nu toe heeft het wijzigen van de simpele en complexe types steeds lokaal plaats gevonden. Daarmee bedoelen we dat deze binnen het `<xs:element>` element heeft plaatsgevonden. In oefening 3 heb je echter vast wel opgemerkt dat het schema niet heel efficient in elkaar zit. Verschillende onderdelen hebben we tijdens het vervaardigen van het XML-Schema gekopieerd naar andere elementdefinities, bijv. de klantgegevens. Als we nu een wijziging aan moeten brengen in die klantgegevens dan moeten we dat op 3 plaatsen doen. Dit kan leiden tot fouten of onzorgvuldigheden. Je zal vast bedacht hebben dat dat beter moet kunnen en ja, gelukkig biedt XML-Schema daar voorzieningen voor. In dit geval is het handiger het type globaal te definiëren en er vanuit de elementen naar te verwijzen.

Daartoe definieer je direct binnen het `<xs:schema>` element een `<xs:simpleType>` danwel `<xs:complexType>` met daarin een `name` attribuut. Het `<xs:element>` element waarvan je wil dat het dit moet gaan gebruiken i.p.v. een `<xs:simpleType>` danwel `<xs:complexType>` een `type` attribuut met als waarde een verwijzing naar dat `<xs:simpleType>` danwel `<xs:complexType>` element.

Hieronder een voorbeeld met een globaal gedefinieerde `<xs:complexType.`:

```xml
<xs:complexType name="PersoonType">
  <xs:sequence>
    <xs:element name="voornaam" type="xs:string"/>
    <xs:element name="achternaam" type="xs:string"/>
  </xs:sequence>
</xs:complexType>

<xs:element name="persoon" type="PersoonType"/>
<xs:element name="contactpersoon" type="PersoonType"/>
```

> **StUF-context:** StUF-schema's werken we voornamelijk met **globale definities**. De typen voor personen, adressen, zaken worden centraal gedefinieerd en vervolgens hergebruikt in meerdere berichtdefinities.

> **Let op!** Tot nu toe hebben we steeds XML-Schema fragmenten gecreëerd die niet aan een namespace zijn gekoppeld. Later zulen we zien dat je in een XML-Schema aan kunt geven op welke namespace dat XML-Schema betrekking heeft. Dat heeft direct gevolgen voor de wijze waarop je in een `type` attribuut verwijst naar een globaal gedefinieerde `<xs:simpleType>` danwel `<xs:complexType>`.

### Geneste vs. globale definities

Er kunnen verschillende redenen zijn om globale of juist lokale definities te gebruiken. Hieronder enkele veel voorkomende redenen:

| Gebruik **globaal** wanneer... | Gebruik **lokaal** wanneer... |
|---|---|
| Het type op meerdere plekken gebruikt wordt | Het type maar op één plek gebruikt wordt |
| Andere schema's ernaar moeten kunnen verwijzen | Het type specifiek is voor dit ene element |
| Je een duidelijk overzicht wilt van alle typen | Je het schema compact wilt houden |

### Oefening 5.3.4

[Naar de oefening](../oefening-5-3-4).

### Kardinaliteit

De **kardinaliteit** van een element of attribuut zegt iets over hoe vaak dat element of attribuut mag (of moet) voorkomen.

**Bij elementen**

Bij elementen gebruiken we daar de XML-Schema attributen `minOccurs` en `maxOccurs` voor.

| Attribuut | Betekenis | Mogelijke waarden | Standaard |
|---|---|---|---|
| `minOccurs` | Minimaal aantal keer | Geheel getal groter of gelijk aan 0 | `1` |
| `maxOccurs` | Maximaal aantal keer | Geheel getal groter of gelijk aan 1 of de waarde 'unbounded'  | `1` |

De waarde in de kollom 'Standaard' geldt als het betreffende attribuut niet is gedefinieerd. Een `<xs:element>` dat geen attribuut `minOccurs` heeft is dus standaard verplicht.

Veelgebruikte combinaties:

| Combinatie | Betekenis |
|---|---|
| *(standaard)* | Verplicht, precies 1 keer |
| `minOccurs="0"` | Optioneel (0 of 1 keer) |
| `minOccurs="0" maxOccurs="unbounded"` | 0 of meer keer |
| `minOccurs="1" maxOccurs="unbounded"` | 1 of meer keer |

Voorbeeld:

```xml
<xs:complexType name="PersoonType">
  <xs:sequence>
    <xs:element name="voornaam" type="xs:string"/>                          <!-- Verplicht, 1x -->
    <xs:element name="tussenvoegsel" type="xs:string" minOccurs="0"/>       <!-- Optioneel -->
    <xs:element name="achternaam" type="xs:string"/>                        <!-- Verplicht, 1x -->
    <xs:element name="telefoonnummer" type="xs:string"
                minOccurs="0" maxOccurs="unbounded"/>                       <!-- 0 of meer -->
    <xs:element name="adres" type="AdresType"
                minOccurs="1" maxOccurs="3"/>                               <!-- 1 tot 3 -->
  </xs:sequence>
</xs:complexType>
```

> **StUF-context:** In StUF-schema's zijn veel elementen optioneel (`minOccurs="0"`) omdat niet elk bericht alle gegevens bevat. Het begrijpen van `minOccurs` en `maxOccurs` is essentieel voor het lezen van StUF-schema's.

**Bij attributen**

De kardinaliteit van attributen wordt in een XML-Schema op een afwijkende wijze gedefinieerd, met het XML-Schema attribuut `use`. Een attribuut kan echter nooit meer dan één keer op een element gespecificeerd worden.
Het volgende is dus **niet** toegestaan in een XML-bestand:

`<afbeeldingen href="images/afbeelding1.jpg" href="images/afbeelding2.jpg"/>`

Om die reden zijn alleen de in de eerste kolom van de volgende tabel gedefinieerde waarden toegestaan op het `use` attribuut.

| `use`-waarde | Betekenis |
|---|---|
| `optional` | Het attribuut is optioneel (standaard) |
| `required` | Het attribuut is verplicht |
| `prohibited` | Het attribuut mag niet voorkomen (gebruikt bij overerving) |


**Bij compositors**
Op compositors kan op dezelfde wijze als op `<xs:element>` elementen kardinaliteiten worden gedefinieerd.
Binnen een `<xs:all>` compositor mogen de attributen `minOccurs` en `maxOccurs` op het `<xs:element>` echter geen waarde hebben die hoger is dan 1. 

### Oefening 5.3.5

[Naar de oefening](../oefening-5-3-5).

### Nillable: expliciet "geen waarde"

Soms moet een element aanwezig zijn, maar hoeft het geen waarde te hebben. In een XML-Schema wordt dat als volgt gedefinieerd:

```xml
<xs:element name="overlijdensdatum" type="xs:date" nillable="true"/>
```

en in een XML-document kan je dat vervolgens als volgt gebruiken:

```xml
<overlijdensdatum xsi:nil="true"/>
```

> **LET OP!** De namespace declaratie `xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"` moet dan wel in het XML-document aanwezig zijn.

> **StUF-context:** Het `nillable`-mechanisme wordt in StUF gebruikt om aan te geven dat een gegeven bewust niet gevuld is. Een leeg element kan "nog niet ingevuld" betekenen, terwijl `xsi:nil="true"` betekent "er is vastgesteld dat er geen waarde is."

### Type-afleiding: extension en restriction

Een van de krachtigste features van XSD is **type-afleiding**: een nieuw type baseren op een bestaand type, vergelijkbaar met overerving in objectgeoriënteerd programmeren. 
We zagen al eerder hoe je simpele types kon restricten. Ook complexe Types kun je restricten. We kijken echter eerst hoe je zowel simpele als complexe types kunt extenden.

Een **`xs:extension`** is een uitbreiding van een type en levert altijd een complex type op. Bij een extension wordt er nl. middels een `<xs:element>` en/of `<xs:attribute>` element een 'element' en /of attribuut aan een simpleType

* Een element met een waarde en een attribuut:
  ```xml
  <xs:element name="bedrag">
    <xs:complexType>
      <xs:simpleContent>
        <xs:extension base="xs:decimal">
          <xs:attribute name="valuta" type="xs:string"/>
        </xs:extension>
      </xs:simpleContent>
    </xs:complexType>
  </xs:element>
  ```


```xml
<!-- Basistype -->
<xs:complexType name="PersoonType">
  <xs:sequence>
    <xs:element name="naam" type="xs:string"/>
    <xs:element name="geboortedatum" type="xs:date"/>
  </xs:sequence>
</xs:complexType>

<!-- Afgeleid type: voegt elementen toe -->
<xs:complexType name="MedewerkerType">
  <xs:complexContent>
    <xs:extension base="PersoonType">
      <xs:sequence>
        <xs:element name="functie" type="xs:string"/>
        <xs:element name="afdeling" type="xs:string"/>
      </xs:sequence>
    </xs:extension>
  </xs:complexContent>
</xs:complexType>
```

`MedewerkerType` bevat nu alle elementen van `PersoonType` **plus** de extra elementen:

```text
PersoonType          (basistype)
  ├── naam
  └── geboortedatum
       │
       ▼
MedewerkerType       (afgeleid = extends PersoonType)
  ├── naam            ← geërfd
  ├── geboortedatum   ← geërfd
  ├── functie         ← toegevoegd
  └── afdeling        ← toegevoegd
```

**`xs:restriction`** — een type beperken:

```xml
<!-- Basistype: alles optioneel -->
<xs:complexType name="PersoonType">
  <xs:sequence>
    <xs:element name="naam" type="xs:string"/>
    <xs:element name="geboortedatum" type="xs:date" minOccurs="0"/>
    <xs:element name="adres" type="xs:string" minOccurs="0"/>
  </xs:sequence>
</xs:complexType>

<!-- Restrictietype: naam en geboortedatum verplicht, geen adres -->
<xs:complexType name="KernPersoonType">
  <xs:complexContent>
    <xs:restriction base="PersoonType">
      <xs:sequence>
        <xs:element name="naam" type="xs:string"/>
        <xs:element name="geboortedatum" type="xs:date"/>
      </xs:sequence>
    </xs:restriction>
  </xs:complexContent>
</xs:complexType>
```

> **StUF-context:** StUF maakt intensief gebruik van `xs:restriction`. Het basistype bevat alle denkbare elementen (vaak optioneel), en per berichttype wordt een restriction gemaakt die alleen de relevante elementen overhoudt. Dit is het zogenaamde **"Russische poppetjes-model"** (matryoshka-model) van StUF.

| Techniek | Wat doet het? | Richting |
|---|---|---|
| `xs:extension` | Voegt elementen/attributen toe | Basistype → **ruimer** |
| `xs:restriction` | Beperkt of verwijdert optionele delen | Basistype → **strikter** |

### Oefening 5.3.6

[Naar de oefening](../oefening-5-3-6).

### Groepen: `xs:group` en `xs:attributeGroup`

**`xs:group`** — herbruikbare elementgroep:

```xml
<xs:group name="NaamGroep">
  <xs:sequence>
    <xs:element name="voornaam" type="xs:string"/>
    <xs:element name="tussenvoegsel" type="xs:string" minOccurs="0"/>
    <xs:element name="achternaam" type="xs:string"/>
  </xs:sequence>
</xs:group>

<xs:complexType name="PersoonType">
  <xs:sequence>
    <xs:group ref="NaamGroep"/>
    <xs:element name="geboortedatum" type="xs:date"/>
  </xs:sequence>
</xs:complexType>
```

**`xs:attributeGroup`** — herbruikbare attribuutgroep:

```xml
<xs:attributeGroup name="StUFMetadata">
  <xs:attribute name="mutatiesoort" type="xs:string"/>
  <xs:attribute name="indicatorOvername" type="xs:string"/>
  <xs:attribute name="noValue" type="xs:string"/>
</xs:attributeGroup>

<xs:complexType name="PersoonType">
  <xs:sequence>
    <xs:element name="naam" type="xs:string"/>
  </xs:sequence>
  <xs:attributeGroup ref="StUFMetadata"/>
</xs:complexType>
```

> **StUF-context:** `xs:attributeGroup` wordt in StUF-schema's veelvuldig gebruikt. De basismetadata-attributen die bij elk StUF-element horen (zoals `mutatiesoort`, `noValue`) worden als `attributeGroup` gedefinieerd en overal hergebruikt.

### Schema's opsplitsen: `xs:include` en `xs:import`

Een groot schema in één bestand wordt al snel onoverzichtelijk. XSD biedt twee mechanismen om schema's over meerdere bestanden te verdelen.

**`xs:include`** — bestanden samenvoegen (zelfde namespace):

```xml
<!-- persoon.xsd -->
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"
           targetNamespace="http://www.example.nl/schema">

  <xs:include schemaLocation="typen-basis.xsd"/>

  <xs:complexType name="PersoonType">
    <xs:sequence>
      <xs:element name="naam" type="xs:string"/>
      <xs:element name="adres" type="tns:AdresType"/>  <!-- Uit typen-basis.xsd -->
    </xs:sequence>
  </xs:complexType>

</xs:schema>
```

**`xs:import`** — schema's uit een andere namespace:

```xml
<!-- persoon.xsd (namespace: http://www.example.nl/persoon) -->
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"
           targetNamespace="http://www.example.nl/persoon"
           xmlns:adr="http://www.example.nl/adres">

  <xs:import namespace="http://www.example.nl/adres"
             schemaLocation="adres.xsd"/>

  <xs:complexType name="PersoonType">
    <xs:sequence>
      <xs:element name="naam" type="xs:string"/>
      <xs:element name="adres" type="adr:AdresType"/>  <!-- Uit adres.xsd -->
    </xs:sequence>
  </xs:complexType>

</xs:schema>
```

| Kenmerk | `xs:include` | `xs:import` |
|---|---|---|
| Namespace | Zelfde of geen | Andere |
| Attribuut `namespace` | Niet nodig | Verplicht |
| Analogie | Bestanden samenvoegen | Bibliotheek importeren |
| Gebruik | Opknippen van groot schema | Hergebruik van extern schema |

> **StUF-context:** StUF-schema's zijn zeer modulair. Het basisschema `stuf0302.xsd` definieert fundamentele StUF-typen, en domeinschema's importeren deze om hun eigen berichttypes te definiëren. Je zult tientallen `import`- en `include`-regels tegenkomen.

### Modulaire schema-architectuur

In echte projecten (en zeker in StUF) zie je een gelaagde opzet:

```text
basis-typen.xsd
├── Simpele typen (Postcode, BSN, Datum, etc.)
└── Attribuutgroepen (metadata)
        │
        ▼
domein-typen.xsd
├── include basis-typen.xsd
├── Complexe typen (PersoonType, AdresType, etc.)
└── Elementgroepen (NaamGroep, etc.)
        │
        ▼
berichten.xsd
├── include domein-typen.xsd
├── Berichttypen (met restriction op domeintypen)
└── Root-elementen
```

In StUF concreet:

```text
stuf0302.xsd                 ← Basis StUF-types en attributen
    │
    ├── import ──→ bg0310_stuf_simpleTypes.xsd
    ├── import ──→ bg0310_ent_basis.xsd      ← Entiteittypen (persoon, adres, etc.)
    │                 │
    │                 └── import ──→ gml.xsd  ← Geometrie
    │
    └── bg0310_msg_vraagAntwoord.xsd         ← Berichtstructuren
```

---

### Namespaces in XSD

In sectie 5.2 leer je wat XML-namespaces zijn. Hier zie je hoe namespaces werken **aan de schema-kant**.

**`targetNamespace`** — de namespace van je schema:

```xml
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"
           targetNamespace="http://www.example.nl/persoon"
           xmlns:per="http://www.example.nl/persoon">

  <xs:element name="persoon" type="per:PersoonType"/>

  <xs:complexType name="PersoonType">
    <xs:sequence>
      <xs:element name="naam" type="xs:string"/>
    </xs:sequence>
  </xs:complexType>
</xs:schema>
```

Alle globale definities (`persoon`, `PersoonType`) behoren tot de `targetNamespace`. Als je ernaar verwijst, heb je de prefix nodig: `type="per:PersoonType"`.

**`elementFormDefault`** — bepaalt of lokale elementen een namespace-prefix nodig hebben:

| Waarde | Betekenis |
|---|---|
| `unqualified` (standaard) | Lokale elementen hebben **geen** prefix in XML |
| `qualified` | Lokale elementen **moeten** in de namespace staan |

> **StUF-context:** StUF-schema's gebruiken `elementFormDefault="qualified"`. In de praktijk wordt vaak de default namespace gebruikt zodat niet alle elementen een prefix nodig hebben.

**Schema koppelen aan een XML-document:**

Met `xsi:schemaLocation` (paren van namespace + bestandslocatie):

```xml
<persoon xmlns="http://www.example.nl/persoon"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://www.example.nl/persoon persoon.xsd">
  <naam>Jan</naam>
</persoon>
```

Met meerdere schema's:

```xml
<bericht xmlns="http://www.example.nl/bericht"
         xmlns:per="http://www.example.nl/persoon"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="
           http://www.example.nl/bericht  bericht.xsd
           http://www.example.nl/persoon  persoon.xsd">
  <!-- ... -->
</bericht>
```

> **Let op:** `xsi:schemaLocation` is een **hint** voor de validator, geen verplichting. De validator mág een ander schema gebruiken.

---

### Compleet voorbeeld: alles samen

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">

  <!-- Simpele typen met restricties -->
  <xs:simpleType name="BSN">
    <xs:restriction base="xs:string">
      <xs:pattern value="[0-9]{9}"/>
    </xs:restriction>
  </xs:simpleType>

  <xs:simpleType name="Postcode">
    <xs:restriction base="xs:string">
      <xs:pattern value="[0-9]{4}[A-Z]{2}"/>
    </xs:restriction>
  </xs:simpleType>

  <xs:simpleType name="Geslacht">
    <xs:restriction base="xs:string">
      <xs:enumeration value="M"/>
      <xs:enumeration value="V"/>
      <xs:enumeration value="O"/>
    </xs:restriction>
  </xs:simpleType>

  <!-- Complexe typen -->
  <xs:complexType name="AdresType">
    <xs:sequence>
      <xs:element name="straat" type="xs:string"/>
      <xs:element name="huisnummer" type="xs:positiveInteger"/>
      <xs:element name="huisletter" type="xs:string" minOccurs="0"/>
      <xs:element name="postcode" type="Postcode"/>
      <xs:element name="woonplaats" type="xs:string"/>
    </xs:sequence>
    <xs:attribute name="type" type="xs:string" use="required"/>
  </xs:complexType>

  <xs:complexType name="PersoonType">
    <xs:sequence>
      <xs:element name="voornaam" type="xs:string" maxOccurs="unbounded"/>
      <xs:element name="tussenvoegsel" type="xs:string" minOccurs="0"/>
      <xs:element name="achternaam" type="xs:string"/>
      <xs:element name="geslacht" type="Geslacht"/>
      <xs:element name="geboortedatum" type="xs:date"/>
      <xs:element name="overlijdensdatum" type="xs:date" nillable="true" minOccurs="0"/>
      <xs:element name="adres" type="AdresType" minOccurs="0" maxOccurs="unbounded"/>
    </xs:sequence>
    <xs:attribute name="bsn" type="BSN" use="required"/>
  </xs:complexType>

  <!-- Root-element -->
  <xs:element name="persoon" type="PersoonType"/>

</xs:schema>
```

Een geldig XML-document:

```xml
<persoon bsn="123456789">
  <voornaam>Jan</voornaam>
  <voornaam>Pieter</voornaam>
  <tussenvoegsel>de</tussenvoegsel>
  <achternaam>Vries</achternaam>
  <geslacht>M</geslacht>
  <geboortedatum>1985-03-15</geboortedatum>
  <overlijdensdatum xsi:nil="true"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"/>
  <adres type="woonadres">
    <straat>Kerkstraat</straat>
    <huisnummer>12</huisnummer>
    <postcode>3511AB</postcode>
    <woonplaats>Utrecht</woonplaats>
  </adres>
</persoon>
```

In dit ene voorbeeld komen alle behandelde concepten samen: simpele typen met restricties (BSN, Postcode, Geslacht), complexe typen (AdresType, PersoonType), kardinaliteit (`minOccurs`, `maxOccurs`), verplichte attributen (`use="required"`), nillable elementen, en de boomstructuur van geneste elementen.

### Samenvatting

| Concept | Uitleg |
|---|---|
| **XSD** | XML-Schema Definition — beschrijft de toegestane structuur van XML in XML-formaat |
| **Welgevormd vs. geldig** | Welgevormd = syntax OK; geldig = voldoet aan schema |
| **Ingebouwde datatypen** | `xs:string`, `xs:integer`, `xs:date`, `xs:boolean`, etc. |
| **Restricties (facets)** | `pattern`, `enumeration`, `minLength`, `maxInclusive`, etc. |
| **Compositors** | `xs:sequence` (volgorde), `xs:choice` (keuze), `xs:all` (vrij) |
| **Kardinaliteit** | `minOccurs` / `maxOccurs` — hoe vaak een element mag voorkomen |
| **`xs:include` / `xs:import`** | Schema's samenvoegen (zelfde ns) / importeren (andere ns) |
| **Extension / restriction** | Type uitbreiden of beperken (overerving) |
| **`xs:group` / `xs:attributeGroup`** | Herbruikbare groepen elementen of attributen |
| **`targetNamespace`** | Namespace waaraan het schema zijn definities toekent |
| **`elementFormDefault`** | Bepaalt of lokale elementen gekwalificeerd moeten zijn |
| **`xsi:schemaLocation`** | Koppelt namespace aan schema-bestand in XML |

> **Kernpunt:** XSD is een taal (zelf ook XML) waarmee je exact vastlegt hoe een XML-document eruit moet zien. StUF is volledig gedefinieerd in XSD-schema's — het begrijpen van XSD is daarom essentieel voor het werken met StUF. De belangrijkste concepten zijn: datatypen met restricties, compositors voor structuur, kardinaliteit voor optionaliteit, en modulaire schema-opzet met include/import en type-afleiding.

### Tot slot

Zoals gezegd is XML-Schema een standaard van het W3C. Een volledige specificatie van de standaard vind je dan ook op hun site:
* [W3C XML Schema Definition Language (XSD) 1.1 Part 1: Structures](https://www.w3.org/TR/xmlschema11-1/)
* [W3C XML Schema Definition Language (XSD) 1.1 Part 2: Datatypes](https://www.w3.org/TR/xmlschema11-2/)
