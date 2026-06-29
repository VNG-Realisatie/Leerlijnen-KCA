---
title: "11.2 JSON Schema's"
date: 2026-05-20
weight: 112
leerlijn: 11
paragraaf: "11.2"
parent: "API-technologie en moderne koppelvlakken"
leerdoel: "Heeft kennis van JSON Schema's."
---


## 11.2 JSON Schema's

Heeft kennis van JSON Schema's.
Doel van deze cursus is het behandelen van de meest essentiële constructies in JSON Schema. Deze workshop pretendeert dus niet volledig noch normatief te zijn.

Doorloop minimaal het ["Get Started"](https://json-schema.org/learn) onderdeel van de [json-schema.org](https://json-schema.org) site en voltooi de oefeningen onder ['Tour of JSON Schema'](https://tour.json-schema.org/).

Hieronder bespreken we nog enkele technieken die in 'json-schema.org' niet aan bod komen.

### Discriminator

> Wellicht deze paragraaf juist opnemen in het onderdeel dat over OpenAPI of yaml gaat.

Met ingang van JSON SChema 2020-12 kunnen dialecten geconfigureerd worden. Meer informatie daarover vind je in ['Validating OpenAPI and JSON Schema'](https://json-schema.org/blog/posts/validating-openapi-and-json-schema#what's-going-on-here). 
Het OpenAPI 3.1 Schema dialect ondersteund in ieder geval het `discriminator` keyword. Een keyword dat m.b.t. Polymorphisme zeer nuttig is.

Polymorphisme houdt in dat een object in een bepaalde situatie twee of meer verschillende vormen aan kan nemen. Hieronder een voorbeeld met een `oneOf` keyword maar ook het `anyOf` mag gebruikt worden:

```json-schema
components:
  responses:
    sampleObjectResponse:
      content:
        application/json:
          schema:
            oneOf:
              - $ref: '#/components/schemas/simpleObject'
              - $ref: '#/components/schemas/complexObject'
  …
  schemas:
    simpleObject:
      type: object
      required:
		- objectType
        - message
        - code
      properties:
        objectType:
          type: string
        message:
          type: string
        code:
          type: integer
          minimum: 100
          maximum: 600
    complexObject:
      type: object
      required:
		- objectType
        - code
		- rootCause
      properties:
        objectType:
          type: string
        code:
          type: integer
          minimum: 700
          maximum: 900
        rootCause:
          type: string
```

Het betreft hier dus een OpenAPI 3.1 Schema en het response object `sampleObjectResponse` kan dus ofwel bestaan uit de properties:
* `objectType`
* `message`
* `code`

ofwel uit de properties
* `objectType`
* `code`
* `rootCause`

Om API consumers te helpen detecteren welk type object nu wordt gebruikt kan aan het schema van het response object `sampleObjectResponse` een `discriminator` property worden toegevoegd. Hieronder hebben we dat voor bovenstaande code gedaan:

```json-schema
components:
  responses:
    sampleObjectResponse:
      content:
        application/json:
          schema:
            oneOf:
              - $ref: '#/components/schemas/simpleObject'
              - $ref: '#/components/schemas/complexObject'
            discriminator:
              propertyName: objectType
  …
  schemas:
    simpleObject:
      type: object
      required:
		- objectType
        - message
        - code
      properties:
        objectType:
          type: string
        message:
          type: string
        code:
          type: integer
          minimum: 100
          maximum: 600
    complexObject:
      type: object
      required:
		- objectType
        - code
		- rootCause
      properties:
        objectType:
          type: string
        code:
          type: integer
          minimum: 700
          maximum: 900
        rootCause:
          type: string
```

Het is van belang dat de property die als `discriminator` is gedefinieerd in alle modellen, die in de `oneOf` of `anyOf` staan, voorkomt. 
De property die als `discriminator` is aangewezen in het OpenAPI 3.1 Schema moet in de instantie van het bericht de waarde van één van de schemamodellen bevatten, in dit geval dus de naam `simpleObject` of `complexObject`.
Daarmee kun je met de `disciminator` property aangeven welk schemamodel toegepast moet worden.

Het zou om de e.o.a. reden kunnen dat je de waarden die de `disciminator` property kan aannemen niet gelijk wil maken aan de naam van de schemamodellen. In dat geval moet je aan de `discriminator` een `mapping` property toevoegen zoals hieronder is gedaan:

```json-schema
components:
  responses:
    sampleObjectResponse:
      content:
        application/json:
          schema:
            oneOf:
              - $ref: '#/components/schemas/simpleObject'
              - $ref: '#/components/schemas/complexObject'
            discriminator:
              propertyName: objectType
              mapping:
                obj1: '#/components/schemas/simpleObject'
                obj2: '#/components/schemas/complexObject'
  …
  schemas:
    simpleObject:
      type: object
      required:
		- objectType
        - message
        - code
      properties:
        objectType:
          type: string
        message:
          type: string
        code:
          type: integer
          minimum: 100
          maximum: 600
    complexObject:
      type: object
      required:
		- objectType
        - code
		- rootCause
      properties:
        objectType:
          type: string
        code:
          type: integer
          minimum: 700
          maximum: 900
        rootCause:
          type: string
```