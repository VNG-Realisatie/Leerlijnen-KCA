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

