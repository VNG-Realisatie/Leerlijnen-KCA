---
title: "5.7 JSON Schema's"
date: 2026-03-04
weight: 9
leerlijn: 5
paragraaf: "5.7"
leerdoel: "Heeft kennis van JSON Schema's."
---


## 5.7 JSON Schema's

Heeft kennis van JSON Schema's.
Doel van deze cursus is het behandelen van de meest essentiële constructies in JSON Schema. Deze workshop pretendeert dus niet volledig noch normatief te zijn.


### Basisstructuur van een JSON Schema

Bij de behandeling van [XML-Schema](5-3-xml-schemas-xsd.md) zagen we al dat zo'n schema zelf ook een XML-document is. Voor een JSON Schema geldt dat het zelf ook een JSON‑document is.

In [sectie 5.6 XML vs. JSON](5-6-xml-vs-json) zagen we hoe je in vergelijking met XML gegevens structureert in JSON. Ook daar kan je, net als in XML, spreken over *welgevormdheid* op basis van opgelegde syntaxregels.
Hieronder zie je een minimale versie van een JSON Schema.

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "type": "object"
}
```

De belangrijkste velden op top-level niveau zijn:

| Veld | Betekenis |
| --- | --- |
| $schema | Welke versie van JSON Schema |
| $id | Unieke identifier (optioneel maar aanbevolen) |
| type | Verwacht JSON-type |
| properties | Beschrijving van objectvelden |
| required | Verplichte velden |
| additionalProperties | Zijn extra velden toegestaan? |

In de JSON Schema voorbeelden binnen de onderstaande paragrafen tonen we steeds slechts de betreffende JSON Schema fragmenten. Deze fragmenten zijn op zichzelf geen valide JSON Schema, daarvoor moeten ze minimaal de `$schema` property bevatten.

### Het type-keyword

JSON Schema kent een aantal basistypes, primitieve en samengestelde types. Primitieve bevatten slechts een enkelvoudige waarde, samengestelde types bevatten structuren. hieronder een lijstje met daarachter de uitleg:

| Type | Soort type | Uitleg |
| --- | --- | --- |
| string | Primitief Type | Een reeks Unicode-tekens, bijvoorbeeld `"hallo"` of `"2026-05-01"`. |
| number | Primitief Type | Elk numeriek getal, inclusief drijvende-kommagetallen (floating point), zoals `42`, `3.14` of `-1.5`. |
| integer | Primitief Type | Een geheel getal zonder decimalen, bijvoorbeeld `10` of `-5`.
| boolean | Primitief Type | Een logische waarde, ofwel `true` of `false`. |
| null | Primitief Type | De waarde null, gebruikt om de afwezigheid van een waarde aan te geven. |
| object | Samengesteld Type | Een ongeordende set van key/value-paren (een JSON-object), bijvoorbeeld `{"naam": "Jan", "leeftijd": 30}`. |
| array | Samengesteld Type | Een geordende lijst van waarden, bijvoorbeeld `["appel", "banaan", "kers"]`. |

Hieronder enkele voorbeelden:

```json
{
  "type": "string" 
}
```

```json
{
  "type": ["string", "null"] 
}
```

In het laatste voorbeeld zie dat meerdere types worden toegestaan (hier geldt bijv. een optionele waarde).

### Objecten valideren: properties en required

Laten we eens een eenvoudig JSON object modelleren.

```json
{
  "type": "object",
  "properties": {
    "name": {
      "type": "string" 
	},
    "age": {
      "type": "integer"
	}
  }
}
```

Een JSON-document volgens dit schema kan er als volgt uitzien:

```json
{
  "name": "Robert",
  "age": 42 
}
```

Maar ook het volgende en het daaropvolgende is geldig:

```json
{
  "age": 42 
  "name": "Robert",
}
```

```json
{
  "name": "Robert" 
}
```

In vergelijking met XML-Schema en het resulterende XML-document valt het volgende op:
* In JSON Schema definiëren we geen root property. De root wordt gevormd door de alles omringende '{' en '}' delimiters;
* JSON Schema definieert geen volgorde;
* In JSON Schema zijn properties standaard optioneel.

Het definiëren van verplichte velden (required) gebeurd met de `required` property. Hieronder een voorbeeld:

```json
{
  "type": "object",
  "properties": {
    "name": {
      "type": "string" 
	},
    "age": {
      "type": "integer" 
	}  
  },
  "required": ["name", "age"]
}
```
  
In de `required` property wordt dus heel specifiek aangegeven welke properties verplicht voor moeten komen.

Het volgende JSON-fragment is dus volgens het bovenstaande JSON Schema ongeldig:

```json
{
  "name": "Robert" 
}
```

### Primitieve waarden begrenzen

Net zoals we bij XML-Schema de mogelijk te gebruiken waarden kunnen beperken met facets kunnen we dat in JSON Schema ook. Hieronder hebben we er enkele opgesomd:

| facet | toepasbaar op | uitleg |
| --- | --- | --- |
| maxLength | String | Beperkt de maximale lengte tot het de aangegeven lengte. Waarde is altijd een niet negatief nummer. |
| minLength | String | Beperkt de minimale lengte tot het de aangegeven lengte. Waarde is altijd een niet negatief nummer. |
| pattern | String | Bevat een reguliere expressie waaraan de waarde moet voldoen. |
| maximum | Number, Integer | De maximale waarde die een nummerieke property kan aannemen. |
| exclusiveMaximum | Number, Integer | De bovengrens vanaf waar de waarde ongeldig is voor een nummerieke property. De waarde zelf mag dus niet gebruikt worden. |
| minimum | Number, Integer | De minimale waarde die een nummerieke property kan aannemen |
| exclusiveMinimum | Number, Integer | De ondergrens vanaf waar de waarde geldig is voor een nummerieke property. De waarde zelf mag dus niet gebruikt worden. |
| multipleOf | Number, Integer | Nummerieke waarden kunnen beperkt worden tot een veelvoud van een gegeven nummer. Dit mag elk positief nummeriek getal aannemen, ook floating point getallen. |


Hieronder geven we enkele voorbeelden. Om te beginnen met `maxLength` en `minLength`. 

```json
{
  "type": "string",
  "minLength": 3,
  "maxLength": 20
}
```

Een pattern met een reguliere expressie:

```json
{
  "type": "string",
  "pattern": "^[A-Z]{2}[0-9]{2}$"
}
```

We gaan hier niet dieper op reguliere expressies in.


```json
{
  "type": "number",
  "minimum": 0,
  "maximum": 100,
  "multipleOf": 5
}
```

Een geldig JSON fragment volgens dit schema is:

```json
25
```

25 is immers een veelvoud van 5. Het volgende is dus ongeldig:

```json
23
```

Primitieve waarden kunnen ook nog met de property `format` begrensd worden. Dit is een semantische aanduiding die wordt gebruikt om een string te valideren of te annoteren als een specifiek type data, zoals datums, e-mailadressen of URI's. 
Het biedt betekenis bovenop het basistype (string), maar werkt standaard vaak als documentatie (annotatie) in plaats van strikte validatie. Hieronder een voorbeeld met het format `email`:

```json
{
  "type": "string",
  "format": "email"
}
```

Andere veelgebruikte formats zijn:

* date
* date-time
* uri
* uuid

⚠️ Let op: format is optioneel afdwingbaar afhankelijk van de validator.

### Arrays: items, minItems, uniqueItems

Array van strings

```json
{
  "type": "array",
  "items": {
    "type": "string" 
  }
}
```

✅

```json
["rood", "groen", "blauw"]
```

Beperkingen

```json
{
  "type": "array",
  "items": {
    "type": "integer" 
  },
  "minItems": 1,
  "maxItems": 5,
  "uniqueItems": true
}
```

Tuple-validatie (vaste volgorde)

```json
{
  "type": "array",
  "items": [
    {
	  "type": "string"
	},
    {
	  "type": "integer" 
	}  
  ]
}
```

✅

```json
["Jan", 30]
```

### Extra velden beperken: additionalProperties

Standaard zijn extra velden toegestaan.

```json
{
  "type": "object",
  "properties": {
    "id": {
      "type": "integer" 
	}  
  },
  "additionalProperties": false
}
```

❌

```json
{
  "id": 1,
  "extra": "niet toegestaan" 
}
```

### Combinatie‑keywords (allOf, anyOf, oneOf, not)

allOf (EN)

```json
{
  "allOf": [
    {
	  "type": "string"
	},
    {
	  "minLength": 5
	}  
  ]
}
```

anyOf (OF)

```json
{
  "anyOf": [
    {
	  "type": "string"
	},
    {
	  "type": "integer"
	}  
  ]
}
```

oneOf (exact één)

```json
{
  "oneOf": [
    {
	  "type": "integer"
	},
    {
      "type": "string",
	  "pattern": "^[0-9]+$" 
	}  
  ]
}
```

not

```json
{
  "not": {
    "type": "null"
  }
}
```

### Enumeraties: enum en const

enum

```json
{
  "type": "string",
  "enum": ["draft", "active", "archived"]
}
```

const

```json
{
  "const": "NL"
}
```

### Hergebruik met $ref en definitions / $defs

Schema met herbruikbaar adres

```json
{  "$defs": {    "address": {      "type": "object",      "properties": {        "street": { "type": "string" },        "city": { "type": "string" }      },      "required": ["street", "city"]    }  },  "type": "object",  "properties": {    "homeAddress": { "$ref": "#/$defs/address" }  }
}
```

### documentatie en metadata

Deze keywords hebben geen effect op validatie, maar zijn cruciaal voor tooling:

```json
{
  "type": "string",
  "title": "Gebruikersnaam",
  "description": "Unieke zichtbare naam van de gebruiker",
  "examples": ["rmelskens"]
}
```

### Compleet praktijkvoorbeeld

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "https://example.com/user.schema.json",
  "type": "object",
  "properties": {
    "id": {
      "type": "integer",
      "minimum": 1    
	},
    "email": {
      "type": "string",
	  "format": "email"
	},
    "roles": {
	  "type": "array",
      "items": {
	    "type": "string",
        "enum": ["admin", "user", "viewer"]
	  },
      "minItems": 1
	}
  },
  "required": ["id", "email"],
  "additionalProperties": false
}
```

### Waar JSON Schema vaak voor gebruikt wordt

* OpenAPI / Swagger
* Event schemas (Kafka, EventBridge)
* Config‑bestanden
* Validatie in frontend & backend
* Low‑code / form generators