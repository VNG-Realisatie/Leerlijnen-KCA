# Voorbeeld van een wijziging in een informatiemodel en een StUF standaard.

Voorbeeld is het toevoegen van een tijdelijk verblijfadres aan het RSGB ([Zie GitHub issue 55](https://github.com/VNG-Realisatie/Actualisering-RSGB/issues/55)). Een wijziging die ook gevolgen heeft voor StUF-BG.

## Actiestappen m.b.t. het RSGB

**Uitleg hoe het issue is "ontdekt" of tot stand is gekomen**
* BV. Wetswijziging heeft tot wijziging LO-BRP geleid;
* Of Functionele wens in de gemeente is ontstaan om dit toch op te nemen.

In dit geval is de aanleiding het aanbrengen van een wijziging in de LO-BRP n.a.v. een amendement van de Tweede kamer. 
In dat amendement is bepaald dat gegevens omtrent de bereikbaarheid van tijdelijke arbeidsmigranten (tijdelijk verblijfadres, e-mailadres en telefoonnummer) moeten worden bijgehouden bij niet-ingezetenen.
In principe moeten wij van zo'n wijziging op de hoogte worden gebracht door personen in onze eigen organisatie maar vaak komt het juist via een of meer leveranciers bij ons binnen.
Het kan overigens zijn dat de nieuw te publiceren RSGB versie meerdere wijzigingen zal bevatten dan die hier op basis van [GitHub issue 55](https://github.com/VNG-Realisatie/Actualisering-RSGB/issues/55) worden aangebracht.

**Varianten in modellering uitwerken**<br/>
Deelnemers van de community kunnen in het issue hun mening geven over de wijze waarop de wijziging in het RSGB geïmplementeerd moet worden maar ook zonder dat kunnen we een of meer varianten ontwikkelen.

**Uitleg bepreken in "expertgroep" en tot besluitvorming komen**
* De uitgewerkte varianten in modellering worden getoond, uitgelegd en besproken;
* Keuze voor een variant maken op basis van argumenten. 

**Verwerking gekozen variant** 
* Aanpassen in informatiemodel;
* Aanpassing documenteren in PDF's en publiceren beta versie --> is oude aanpak Wens is documenteren in Respec; 
* Maken en publiceren van een releasenotes.

**Uitvoeren publieke consultatie**
* Consultatie uitzetten;
* Reacties inventariseren + impact van reacties op gemaakte keuzes in beeld brengen;
* Resultaten publieke consultatie in "expertgroep" bespreken en tot besluitvorming komen;
* Evt. verwerken besluit in informatiemodel;
* Bepalen of er nog een publieke consultatieronde nodig is en zo ja publiceren nieuwe beta versie; 
* Indien geen publieke consultatieronde meer nodig publiceren final versie informatiemodel inclusief respec / pdf's en releasenotes;
* Sluiten issues.

## Actiestappen m.b.t. StUF-BG

* Aanmaken GitHub issue op basis van wijziging in het RSGB in de [StUF-standaarden GitHub repository](https://github.com/VNG-Realisatie/StUF-Standaarden/issues).
  Indien aanwezif zullen we overigens wijzigingen aanbrengen op basis van meerdere GitHub issues;
* Onderhoudsverzoek word aangemaakt in de lijst met onderhoudsverzoeken. --> dit doe je om voor 1 specifieke patch alle relevante issues te verzamelen en op basis daarvan releasenotes te maken;
* Implementatie-overweging per issue uitwerken en opnemen in de betreffende issue. Voorstel voor de wijze van oplossing kan ook door community-leden worden aangedragen;
* Community zo nodig over uitwerking informeren en vragen om reactie daarop;
* Bij geen reactie of collectief OK --> Pre-patch maken. Mogelijk daarin op te nemen wijzigingen:
  - Schema's (XSD/WSDL) aanpassen;
  - Documentatie aanpassen (Verstuffingsdocument, StUF standaard, protocol-binding, Lijst extraElementen, etc…);
  - Mapping bestanden (StUF-BG 2.04 vs StUF-BG 3.10) aanpassen;
  - Releasenotes aanpassen.
* Prepatch publiceren en daarmee een openbare consultatie starten (via mail + patch-bestanden);
* Eventuele reacties verwerken / bespreken;
* Bovenstaande kan in 1 of meer iteraties plaatsvinden;
* Na goedkeuring van Prepatch compleet uitwerken van de Patch (dus ook impact op gerelateerde StUF standaarden) en publicatie;
* StUF Expertgroep en Regiegroep op de hoogte brengen van nieuwe Patch;
* Sluiten issues;
* StUF-master bijwerken.
