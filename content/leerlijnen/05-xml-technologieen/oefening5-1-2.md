---
title: "Oefening 5-1-2"
date: 2026-03-13
weight: 3.2
leerlijn: 5
paragraaf: "5.1.2"
oefendoel: "Oefen met het toevoegen van attributen aan een XML bestand."
---

## Oefening 5.1.2: Luxe visitekaartje

Het bedrijf heeft besloten voor specifieke functies ook privé informatie op een visitekaartje toe te staan. Het gaat om het adres, het e-Mailadres, het telefoonnummer en het mobielenummer. Het XML-schema is daartoe aangepast.

**Benodigde files**
* Download [Visitekaartje-luxe.zip](/Leerlijnen-KCA/bestanden/oefeningen-5.1/Visitekaartje-luxe.zip) en plaats de inhoud (Visitekaartje-luxe.xsd) op een locatie waar jij er makkelijk bij kunt.

**Opdracht**
* Open 'Altova XMLSpy 2024 Enterprise XML Editor'.;
* Creëer een nieuw XML-document via “File – New” en kies de optie “xml    Extensible Markup language 1.0”;
* Als je nu op OK klikt krijgt je het “Choose Schema or DTD” menu te zien. Selecteer de optie “Assign Schema/DTD file”;
* Klik vervolgens achter het invoerveld op het map icoontje voor “Browse file” en selecteer het bestand “Visitekaartje-luxe.xsd” waar je dat eerder hebt opgeslagen;
* Klik op “Open” en vervolgens op “OK”;
* XMLSPY heeft nu wederom een XML-bestand voor je aangemaakt met dezelfde minimaal benodigde set elementen als eerder en deze geopend in “Text view”. 
Voorzie de elementen weer van inhoud.<br>Valideer indien gewenst weer.;
* Creëer een extra adres, e-Mailadres, telefoonnummer en mobielnummer;
* Definieer op deze elementen het in het XML-Schema gespecificeerde attribuut. Ga daarvoor in de starttag achter de naam staan en voor een spatie in. Je krijgt dan te zien welke attributen je toe kunt voegen. Voorzie deze ook van een waarde die is toegestaan. Negeer het attribuut 'xsi:type';
* Bewaar het bestand ergens als “Visitekaartje-luxe.xml”.