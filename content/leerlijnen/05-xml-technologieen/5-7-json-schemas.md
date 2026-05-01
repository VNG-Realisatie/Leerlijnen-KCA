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
| integer | Primitief Type | Een geheel getal zonder decimalen, bijvoorbeeld `10` of `-5`. |
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
  "name": "Martijn",
  "age": 42 
}
```

Maar ook het volgende en het daaropvolgende is geldig:

```json
{
  "age": 42 
  "name": "Martijn",
}
```

```json
{
  "name": "Martijn" 
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
  "name": "Martijn" 
}
```

