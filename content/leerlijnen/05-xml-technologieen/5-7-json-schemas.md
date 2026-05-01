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

### Basisstructuur van een JSON Schema

Een JSON Schema is zelf ook een JSON‑document.

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "type": "object"
}
```

Belangrijkste top-level velden

| Veld | Betekenis |
| --- | --- |
| $schema | Welke versie van JSON Schema |
| $idU | nieke identifier (optioneel maar aanbevolen) |
| type | Verwacht JSON-type |
| properties | Beschrijving van objectvelden |
| required | Verplichte velden |
| additionalProperties | Zijn extra velden toegestaan? |

### Het type-keyword

JSON Schema kent deze basistypes:

* object
* array
* string
* number
* integer
* boolean
* null

**Voorbeelden**

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

➡️ Staat meerdere types toe (bijv. optionele waarde).

### Objecten valideren: properties en required

Eenvoudig object

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

✅ Geldig:

```json
{
  "name": "Robert",
  "age": 42 
}
```

⚠️ Ook geldig:

```json
{
  "name": "Robert" 
}
```

Waarom? age is niet verplicht.

Verplichte velden (required)

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
  
❌ Ongeldig:

```json
{
  "name": "Robert" 
}
```

### Strings: lengte, patronen en formats

Lengtebeperkingen

```json
{
  "type": "string",
  "minLength": 3,
  "maxLength": 20
}
```

Regex met pattern

```json
{
  "type": "string",
  "pattern": "^[A-Z]{2}[0-9]{2}$"
}
```

✅ Geldig:

```json
"AB12"
```

❌ Ongeldig:

```json
"ab12"
```

format
JSON Schema kent bekende formats:

```json
{
  "type": "string",
  "format": "email"
}
```

Andere veelgebruikte formats:

date
date-time
uri
uuid

⚠️ Let op: format is optioneel afdwingbaar afhankelijk van de validator.

### Getallen: grenzen en veelvouden

```json
{
  "type": "number",
  "minimum": 0,
  "maximum": 100,
  "multipleOf": 5
}
```

✅ Geldig:

```json
25
```

❌ Ongeldig:

```json
23
```

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