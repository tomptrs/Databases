
* [Inleiding](inleiding.md)
* [Logische en fysische gegevens](gegevens.md)
* [Entiteit-Relatie diagramma](er.md)
* [Relationele databases](relationeel.md)
* [Normalisatie](normalisatie.md)

# Normalisatie

## inleiding

![norm1](img/norm1.jpg)

Als een tabel slecht is opgebouwd en verkeerde attributen in de relatie zijn opgenomen loopt de database tal van gevaren:
Bovenstaande tabel bevat zowel info van schilderij als van schilder. Hun gegevens samenbrengen in dezelfde tabel brengt volgende problemen met zich mee:
1.	Bepaalde data wordt overtollig opgeslagen: als er 2 schilderijen van dezelfde schilder worden opgenomen in de tabel worden detailgegevens van de schilder nutteloos gedupliceerd. Zo worden het geboortejaar en sterftejaar van ‘Degas’ dubbel opgeslagen en dus ook overtollig!
2.	Overtollige data kan anomalieen bevatten: als een aanpassing niet wordt doorgevoerd in een duplicaat of als andere data worden ingevoerd voor een duplicaat, wordt de database inconsistent. Zie figuur de jaartallen  1834 en 1832
3.	Gegevens kunnen ongewenst verloren gaan. Als het enige schilderij van een schilder uit de tabel wordt verwijderd, gaan ook de detailgegevens over de schilder verloren. Detailgegevens die het gevaar lopen om ongewenst verloren te gaan, zijn schuin gearceerd in de figuur
à Om deze problemen te vermijnen normaliseren!!
Normalisatie is een bepaalde herschikking van de gegevens en gegevensgroepen, waarbij soms nieuwe groepen worden gevormd door gegevens uit bestaande groepen af te zonderen. Uiteindelijk willen we tot de volgende situatie komen: 
Alle attributen van een groep zijn functioneel afhankelijk van de volledige sleutel, en tussen attributen onderling bestaan geen functionele afhankelijkheden. 

Normalisatie vindt plaats in een aantal stappen (de eerste 3 stappen ofwel eerste, tweede, derde normaalvorm) zijn zeer belangrijk. Hoe hoger de normaalvorm, hoe minder problemen kunnen ontstaan!
1.	Verwijder de zich herhalende deelverzamelingen 
2.	Verwijder de attributen die functioneel afhankelijk zijn van slechts een deel van de sleutel 
3.	Verwijder de attributen die functioneel afhankelijk zijn van andere attributen. 

Met 'verwijderen' bedoelen we hier: in een afzonderlijke gegevensgroep onderbrengen, niet weglaten uit het gegevensmodel. 
Het normalisatieproces steunt op het concept van functionele afhankelijkheid:

> Een verzameling van attributen Y is functioneel afhankelijk van een verzameling van attributen X als de waarden van de attributen van Y op elk moment uniek worden vastgelegd door de waarden van de attributen van X. Als de attribuutwaarden van X bekend zijn, zijn daardoor ook de attribuutwaarden van Y bekend.


## eerste normaalvorm: zich herhalende deelverzamelingen

Een tabel staat in eerste normaalvorm als de attributen atomair zijn of anders gezegd, indien een collectie van attributen verschillende malen kan optreden bij één bepaalde keuze van de sleutel, spreken we van een zich herhalende deelverzameling. We willen echter bereiken, dat sleutelwaarden uniek zijn, met andere woorden, dat alle attributen uniek vastliggen. De attributen die deel uitmaken van de zich herhalende deelverzameling, worden ondergebracht in een nieuwe tabel, samen met de sleutelvelden. De attributen die deel uitmaken van de zich herhalende deelverzameling, worden vervolgens weggelaten uit de oorspronkelijke groep. 
Herhaal dit procédé totdat, bij gegeven sleutelwaarde, de attributen nog slechts één mogelijke waarde kunnen aannemen. 
Een strikte interpretatie van het begrip 'functionele afhankelijkheid' zou reeds impliceren, dat er geen zich herhalende deelverzamelingen bestaan. 
Deze 'verbeterde' toestand van een gegevensgroep heet de eerste normaalvorm. Eventuele nieuwe gegevensgroepen die bij bovenstaand procédé ontstaan, moeten op hun beurt genormaliseerd worden: het is namelijk denkbaar, dat een zich herhalende deelverzameling op haar beurt is opgebouwd uit nog kleinere zich herhalende deelverzamelingen. 

Voorbeeld eerste normaalvorm

Artiest (A_ID:char(3), Naam:varchar, Voornaam:varchar,  Verblijfplaats:varchar array [5])
   Primaire sleutel: {A_ID}
   
Door het meerwaardig karakter van het datatype ‘varchar array [5]’  staat de relatie ‘Artiest’ niet in eerste normaalvorm. Bij de eerste normalisatiestap moet het worden opgesplitst. Dit kan als volgt:

Artiest (A_ID:char(3), Naam:varchar, Voornaam:varchar)
Primaire sleutel: {A_ID} 

EN

VerblijfplaatsArtiest (A_ID:char(3), Verblijfplaats:varchar)
Primaire sleutel: {A_ID, Verblijfplaats}
Vreemde sleutel: {A_ID} verwijst naar Artiest


## Tweede normaalvorm: attributen die slechts van een deel van de sleutel afhangen

Uiteindelijk mogen de attributen slechts functioneel afhankelijk zijn van de gehele sleutel, niet van een deel ervan. Het nu volgende normalisatieproces brengt de gegevensgroepen in de tweede normaalvorm. 

Stel dat een aantal attributen functioneel afhankelijk is van een deelverzameling van de sleutelvelden. Breng deze onder in een afzonderlijke gegevensgroep, samen met het kleinste deel van de sleutel waarvan ze nog afhankelijk zijn. Verwijder deze attributen uit de oorspronkelijke gegevensgroep.
Herhaal dit procédé totdat in alle gegevensgroepen de attributen slechts functioneel afhankelijk zijn van de hele sleutel. 

Voorbeeld tweede normaalvorm

Schilderij (S_ID:char(3), Titel:varchar, Periode:integer,Naam:varchar, Geboren:integer, Gestorven:integer)
primaire sleutel {S_ID} en alternatieve sleutel {Titel, Naam}. 

Omdat zowel {Geboren} als {Gestorven} irreducibel functioneel afhankelijk zijn van {Naam} (dus niet van de kandidaatsleutel {Titel, Naam}), staat de relatie niet in tweede normaalvorm. 

Afsplitsing van de probleemattributen levert de volgende relaties op:
Artiest (Naam:varchar,Geboren:integer, Gestorven:integer)
primaire sleutel: {Naam}

Schilderij (S_ID:char(3), Titel:varchar, Periode:integer, Naam:varchar)
primaire sleutel: {S_ID}
vreemde sleutel: {Naam} verwijst naar Artiest

## Derde normaalvorm: attributen die afhangen van attributen

Uiteindelijk mogen de attributen uitsluitend functioneel afhankelijk zijn van de sleutel, niet bovendien van elkaar. Het nu volgende normalisatieproces brengt de gegevensgroepen in de derde normaalvorm. 

Stel dat collectie A van attributen functioneel afhankelijk is van B, een andere collectie attributen. Breng A en B onder in een afzonderlijke gegevensgroep. Verwijder de attributen van A uit de oorspronkelijke gegevensgroep.
Herhaal dit procédé todat in alle gegevensgroepen de attributen slechts functioneel afhankelijk zijn van de sleutel.

## verdere eliminatie van redundantie

De drie normalisatie-stappen die we hier behandeld hebben, elimineren uit ons gegevensmodel alle redundantie die veroorzaakt wordt door functionele afhankelijkheden. Een andere vorm van redundantie, berekende gegevens, werd reeds vroeger geëlimineerd. Er bestaan nog andere, meer complexe vormen van redundantie, die aanleiding geven tot verdere normaalvormen. Hoewel de overeenkomstige normalisaties in de praktijk zelden nodig zijn, moet iedere professionele informaticus van hun bestaan op de hoogte zijn. Men onderscheidt, voorbij de derde normaalvorm, achtereenvolgens: 
*	de normaalvorm van Boyce-Codd 
*	de vierde normaalvorm 
*	de vijfde normaalvorm 
*	
De vijfde normaalvorm elimineert niet alleen overbodige functionele afhankelijkheden, maar ook de meer algemene join-afhankelijkheden. De bijbehorende normalisatieprocedure vertoont enkele theoretische problemen, waardoor ze (voorlopig) niet in een eenvoudig, algemeen geldend algoritme kan worden gegoten. 


## Waarom normalizeren: ziehier een praktijkvoorbeeld

De situatie nu:

![normvb1](img/normvb1.jpg)
 
Voor een goede database is de bovenstaande structuur onaanvaardbaar. Om dit op te kuisen, zullen we moeten normaliseren.

. In dit voorbeeld heeft de programmeur voorzien dat de klant twee goederen tegelijk kan aankopen. Dat is al handig, maar toch zijn er een aantal problemen bij het gebruik van deze tabel.

• Indien die klant de volgende dag terug komt om nog iets bij te kopen, moeten de
klantgegevens opnieuw ingegeven worden.

• Indien de secretaresse besluit om oude aankopen van een klant te wissen, worden eveneens
de klantgegevens gewist.

• Indien twintig klanten hetzelfde produkt kopen, moeten telkens de naam van het produkt
en de prijs opnieuw ingegeven worden.

• Indien de eigenaar van de zaak een lijst wenst, gesorteerd op achternaam, blijkt plots dat
sommigen de naam ingegeven hebben als "Jan De Corthout", terwijl iemand anders "DE
CORTHOUT Jan" zou ingeven. Een derde gebruikte dan weer initialen "Jan D. Corthout".
Kortom: een gesorteerde lijst wordt een onmogelijke taak.

• Meerdere klanten beschikken over een GSM. Daarvoor is er echter geen plaats in de
database.

• Stel dat we een klant willen ingeven om diens telefoonnummer te kennen. Voor deze klant
moet een fictieve verkoop aangemaakt worden.

Zo zijn er nog wel enkele problemen in deze database. Alle dergelijke problemen worden anomalieën
genoemd. In het verleden kwamen databaseprogrammeurs steeds weer anomaliën tegen die de
integriteit van de gegevens in gevaar brachten. 


### De eerste normaalvorm toegepast

Een tabel die voldoet aan de volgende minimale eisen, voldoet aan de eerste normaalvorm:

• Alle velden moeten enkelwaardig zijn. Dat betekent dat er geen samengestelde groepen
meer mogen zijn. Een typisch voorbeeld is het splitsen van voor- en achternaam, en het
splitsen van de straat en nummer.

• Alle elementen in een bepaalde kolom moeten hetzelfde soort gegevens voorstellen. Het
kan dus niet zo zijn dat een kolom in de database een "multifunctionele" betekenis heeft,
waarbij een veld de ene keer dient voor bv. de straatnaam en bij een ander record voor de
gemeente.

• De kolommen moeten unieke namen hebben. Dit is vanzelfsprekend. Geen enkel
databaseproduct zal overigens toestaan dat dubbele namen gebruikt worden.

• In een tabel mogen geen twee rijen voorkomen met identieke gegevens. Het kan gebeuren
bijvoorbeeld gebeuren dat op eenzelfde factuur twee keer identiek hetzelfde artikel
verkocht wordt, met dezelfde hoeveelheid en prijs. Op het eerste zicht kan het dus
gebeuren dat twee rijen identiek dezelfde gegevens bevatten. Zelfs in dat geval moeten de
records van elkaar kunnen onderscheiden worden. Meestal gebeurt dit door elke
factuuritem een unieke ID te geven en deze als primary key te definiëren.

• De volgorde van rijen en kolommen heeft geen inherente betekenis. Twee records mogen
omgewisseld worden, zonder dat dit effect heeft op de werking van de database. Het
sorteren van gegevens mag dus niet binnen de database zelf gebeuren, maar bv. door
middel van een index.

Belangrijker is de eigenschap dat twee kolommen mogen omgedraaid worden. Dit
betekent dat er bv. niet automatisch van uitgegaan mag worden dat de kolom die na de
voornaam komt, wel de achternaam zal zijn. Kolommen moeten altijd benaderd worden op basis van hun naam. Indien bv. op een zeker moment besloten wordt om een kolom tussen te voegen met de initialen, zal de software probleemloos blijven werken.

Gebruik makend van de normalisatiestappen van Codd, krijgen we de volgende stappen

1. Inventariseer alle elementaire gegevens (bv. voornaam, initialen, achternaam, straatnaam,
huisnummer, ...). Breng de kolommen in de database terug tot deze elementaire gegevens.

2. Verwijder alle procesgegevens. Procesgegevens zijn gegevens die rechtstreeks afhankelijk zijn
van één of meer elementaire gegevens. Zo is het postnummer een procesgegeven voor de
gemeente. Zodra een gemeente bekend is, is het postnummer geweten. Het veld "Totaalbedrag"
van een factuur is eveneens een procesgegeven, zodra de subtotalen van de individuele
onderdelen bekend zijn.

3. Herhaal de volgende stappen totdat er geen herhaalde groepen meer bestaan

• Bepaal (of creëer) een primaire sleutel voor de tabel.
• Zoek de deelverzameling die een herhaald aantal keren voorkomt (de herhaalde groep).
• Vorm een nieuwe tabel die bestaat uit de sleutelgegevens van de oorspronkelijke groep,
samen met de gegevens van de herhaalde groep.
• Verwijder de herhaalde groep.

Passen we punt 1) toe op het eerder gegeven voorbeeld, is het duidelijk dat we de naam en het adres
moeten splitsen in hun minimale elementen. De database wordt dan:

![normvb2](img/normvb2.jpg)

Bemerk dat de database inherent groter wordt. Per record worden immers meer karakters
voorbehouden. Normalisatie betekent houdt dus niet noodzakelijk in dat de database kleiner wordt.
Vervolgens passen we normalisatiestap 2) toe. Dit betekent in de eerste plaats dat de kolom Totaalprijs
kan gewist worden, aangezien de prijzen gekend zijn van de individuele onderdelen.

Verder kunnen we de gemeente en het land in een aparte tabel kunnen zetten. Daarvoor creëren we eerst een nieuwe tabel:

![normvb3](img/normvb3.jpg)

Bemerk dat elke gemeente dus een unieke ID krijgt. Deze wordt de primaire sleutel. In principe is het
ook mogelijk om een primaire sleutel aan te maken, die de combinatie is van de postnummer, de
gemeente en het land. In deze cursus houden we het principe aan dat elke tabel een ID veld krijgt.
Dikwijls zijn deze ID’s automatisch gegenereerd.

De tabel Klanten wijzigt dan naar:

![normvb4](img/normvb4.jpg)

In deze definitie bevindt zich nog een herhaalde groep, met name de aangekochte goederen. Gebruik
makend van de derde normalisatiestap stellen we hiervoor een nieuwe tabel samen, welke we Verkopen noemen.
 
De tabel Klanten heeft reeds een unieke primaire sleutel, dus die moet niet meer voorzien
worden. We krijgen :

![normvb5](img/normvb5.jpg)

Bemerk dat uit de tabel Klanten eenvoudig de verkopen kunnen gehaald worden. Immers, in de tabel
verkopen wordt het Klanten_ID vermeld. Een selectie is dus eenvoudig mogelijk. Bemerk dat de kolom
Klanten_ID in de tabel Verkopen een refererende sleutel is.

###tweede normaalvorm toegepast

Een tabel heeft de tweede normaalvorm als alle attributen die niet in de sleutel zijn opgenomen, van
de ganse sleutel afhankelijk zijn.

Dit probleem stelt zich enkel indien de primaire sleutel gevormd wordt uit meerdere kolommen. Dit
betekent dat alle relaties met een sleutel die maar uit één kolom bestaan, automatisch in de tweede
normaalvorm staan. Dit is ook het geval in ons voorbeeld.

Indien de sleutel toch uit meerdere kolommen bestaat, kan de tabel als volgt in de tweede normaalvorm
gebracht worden:

1. Duid de kolommen aan die niet functioneel afhankelijk zijn van de volledige sleutel.
2. Vorm voor ieder deel van de sleutel een aparte tabel, waarvan er attributen afhankelijk zijn.
3. Splits de kolommen van de bestaande tabel op in de twee nieuwe tabellen, waarbij de kolommen
telkens afhankelijk zijn van de overeenkomstige sleutel.




### De derde normaalvorm toegepast

In de derde normaalvorm worden die gegevens verwijderd die functioneel afhankelijk zijn van andere
kolommen.

Dit wordt gedaan als volgt:

1. Duid de kolommen aan die functioneel afhankelijk zijn van andere kolommen.

2. Maak een aparte tabel voor elke kolom (of combinatie van kolommen), waarvan andere
kolommen afhankelijk zijn.

3. Vervang deze kolommen in de oorspronkelijke tabel door de sleutel van de nieuwe tabel.
In ons voorbeeld doet dit probleem zich voor in de tabel Verkopen. AangekochtNaam en Prijs (1) zijn
kolommen die functioneel afhankelijk zijn van AangekochtCode. Hiervoor stellen we dus een aparte
tabel Goederen op. De kolom AangekochtCode hernoemen we naar Verkoop_ID om consistent te
blijven met de naamgeving.

![normvb6](img/normvb6.jpg)

Opmerking

De nu bestaande tabellen bevinden zich strict genomen in de normaalvorm. Toch is er nog een
potentieel gevaar dat de telefoonnummers niet gebruikt worden zoals het hoort, wegens gebrek aan
ruimte. Aangezien er slechts één plaats voorzien is voor de telefoonnummer, zal je in praktijk
tegenkomen dat soms meerdere telefoonnummers worden ingevuld in dit veld.

In dat geval wordt niet meer voldaan aan de eerste normaalvorm! Een mogelijke aanpassing is dus het
toevoegen van een tabel ContactNummers, die gekoppeld wordt aan de Klanten tabel. Deze ziet er dan
uit als

![normvb7](img/normvb7.jpg)


## Denormalisatie

Hoewel er in eerste instantie sterk op aangedrongen wordt om een normalisatie volledig door te voeren, is het soms toch handig (of zelfs noodzakelijk) om een denormalisatie toe te passen. Dit wordt vooral gedaan om redenen van performantie.

Soms kan het gebeuren dat een normalisatie meer kost dan het opbrengt. 


## Twaalf veel voorkomende fouten

### De klanten weten wat ze willen

Nee, de klanten weten dat niet.

Het is uiterst zelden of nooit dat iemand die een database-ontwerp vraagt, ook weet hoe die er uit moet
zien. In het beste geval weet de klant (1) dat de database een middel is om bestaande gegevens
performanter op te slaan. In het slechtste geval denkt die klant dat zijn slabakkende organisatie, warrige
structuren en ontbrekende gegevens gered zullen worden nu jij er een database bij zet.
Dikwijls vertellen de klanten je niet welke gegevens voor hen van cruciaal belang zijn. Dat blijft zo,
zelfs indien je er herhaald om vraagt.

Iemand die al twintig jaar een dierenwinkel houdt, zal je niet vertellen dat honden een oormerk hebben,
of dat er invoerdocumenten nodig zijn voor sommige exotische diersoorten, of dat een levering bij een
bedrijf met een leverbon gebeurt terwijl dat niet geval is voor een particulier. Dat zijn toch dingen die
iedereen weet?

Klanten weten ook niets af van het bestaan van sleutels. Zij weten niet dat je een extra (boolean) veld
moet creëren om aan te geven of een factuur al dan niet met BTW moet afgedrukt worden (leveringen
aan het buitenland). Zij begrijpen niet waarom je een halve dag moet programmeren indien ze je enkel
maar gevraagd hebben dat sommige goederen vanaf nu niet meer in de lijsten zouden voorkomen (en
waarom mag ik die goederen niet gewoon schrappen, ook al heb ik er al van verkocht?).

### Sla de informatie-analyse over

Je klanten hebben geen tijd. Jij hebt geen tijd. Alle tijd die niet gespendeerd wordt aan het
programmeren, is dus verloren geld.

Dikwijls wordt daarom de informatie-analyse wat ingekort. Niemand ziet het belang van langdradige
vergaderingen vooraf. Bovendien wordt de klant voortdurend weggeroepen, want hij/zij moet nog
iemand bedienen, of er is een belangrijke telefoon.

Het gevaar is dan ook reëel dat je gevraagd wordt om al te beginnen met de programmatie, waarbij je
moet toevoegen wat er nog opborrelt aan ideeën. Het gevaar is reëel dat je dat nog doet ook.
De aanvullingen nemen al snel het grootste deel van de tijd in beslag. Bovendien komt de klant
voortdurend met nieuwe wijzigingen en toevoegingen voor de pinnen. Dikwijls zal je grote stukken van
de programmatie moeten overdoen omdat elementaire dingen gewijzigd worden.

Als je niet per uur (maar per project) werkt, is deze manier van werken een garantie voor het mislukken
van het project.

### Kijk enkel naar de technische factoren

Het ontwerp van je database hangt van meer af dan van het ontwerpen van tabellen en de bijkomende
software om die tabellen in te vullen.

Je moet ook een idee hebben van de organisatiestructuur van het bedrijf dat je database gebruikt. Welke gegevens moeten on-line ingevuld worden? Welke gegevens zijn pas na een dag noodzakelijk? Kan hetmanagement meteen beschikken over de gegevens die ze nodig heeft, op het moment dat ze daaromvraagt?

Kijk ook naar het niveau van opleiding van de gebruikers. Indien je de secretaresse de kans geeft om
rechtstreeks te knoeien met de sleutels van de database, kan je je aan grote problemen verwachten.

###  Sla de feedback van de werkvloer over

De eigenaar van het bedrijf heeft je een opdracht gegeven. Dus voer je zijn idee uit omtrent hoe het
programma er moet uitzien. Juist? Fout!
Dikwijls zijn het de mensen op de werkvloer die een klare kijk hebben omtrent hoe de user-interface
van het programma er moet uit zien. Zelfs als dat niet het geval zou zijn, mag je hun opmerkingen niet
overslaan. Zij zijn het die de ganse dag met het programma moeten werken. Indien je het programma
dus niet afstemt op hun noden, zullen zij in de eerste plaats de nadelen van je database ondervinden.
Erger nog, sommige werknemers zouden er wel eens toe kunnen besluiten om je database te boycotten
of te saboteren. Onderschat dit gevaar niet. Niet zelden moet je een programma ontwikkelen dat de
goedkeuring van de werknemers zelf niet heeft. Een voorbeeld is een tijdslogging programma dat
gebruikt wordt om de facturatie naar de klanten te doen, maar dat ook kan gebruikt worden om de ijver
van het personeel te controleren.

Hoe dan ook, zorg er voor dat je de wensen kent van de werkvloer. Laat hen minstens meebeslissen in
de user interface.

###  Gebruik enkel je favoriete ontwikkelingsomgeving

Het zit er dik in dat je al jaren werkt met C# of mysql en php. Dan kan je zonder meer database applicaties schrijven die bestuurd worden vanuit C# of php. 

Meer nog, een connectie met een Access .MDB bestand is eenvoudig en snel geprogrammeerd.
Het gevaar bestaat dat je zo lang mogelijk bij deze omgeving wil blijven. Dat is niet onlogisch! Indien
je elk jaar opnieuw de laatste nieuwe ontwikkeling op databasegebied wil blijven volgen, moet je
zodanig bijstuderen, dat het programmeren zelf er volledig bij inschiet. Het is verstandig om af en toe je
kennis te laten renderen.

Op een dag komt er dan toch een bedrijf waarvoor je een toch bijzonder grote database moet
ontwikkelen. Het aantal records kan in de vele honderdduizenden lopen voor sommige tabellen.
Bovendien is de geschatte database al snel een halve Gigabyte groot. Het aantal inputschermen loopt
dik aan.

De kans bestaat dat je dit probleem opgelost krijgt. De kans is veel groter dat performantieproblemen
en overdadig coderen het project op de helling zetten.

Op dat ogenblik heb je twee mogelijkheden. De eerste mogelijkheid is dat een gekozen wordt voor een
zwaardere ontwikkelomgeving met bv. een centrale SQL server. Dit betekent dat je je zult moeten
instuderen in een nieuwe programmeeromgeving met nieuwe technieken en valkuilen. De tweede
mogelijkheid is dat je tegen de klant zegt dat dit project te groot is voor jou, en dat ze iemand anders
moeten zoeken.

Wat je ook doet, kies een van deze twee mogelijkheden.
Onthoud de regel: "If the only tool you have is a hammer, then every problem looks like a nail."

###  Gebruik enkel je favoriete computerarchitectuur

Niemand kan verwachten dat je expert bent in alles. Ook in de computerwereld is de tijd voorbij dat
iemand kon zeggen dat hij alles van het beroep beheerst.

Het werk dat gebeurt op stand-alone systemen, is verschillend van het werk dat je moet doen in multiuser client-server toepassingen. PC-Windows systemen verschillen van unix omgevingen.

Indien een oplossing nodig is voor je automatisatieproject, kies dan de beste oplossing. Probeer niet om
ten alle prijze binnen je favoriete omgeving te blijven. Indien een klant je een oplossing vraagt waarbij
de beste infrastructuur een client-server systeem is met een zware unix-server, stel dit dan ook zo voor.
Als dan blijkt dat je zelf die oplossing niet kan beheren, trek dan je conclusies.

###  Design de tabellen op zichzelf

Zowat alle tabellen in een database zijn gerelateerd ten opzicht van mekaar. Indien je daar niet vanaf
het begin rekening mee houdt, introduceer je fouten in de database, waardoor zelfs gegevens kunnen
kwijt geraken.

Zorg er voor dat je de tabellen ontwerpt met het zicht op de toekomst, en rekening houdend met het
verleden. Hiervoor bestaat geen standaard ontwerpregel. Het vraagt wat ervaring

### Je doet het goed, niemand hoeft je te controleren

Hoeveel jaren ervaring je ook hebt, het loont de moeite om iemand te vragen om je ontwerp te
controleren. Met twee weet je inderdaad meer dan alleen.

De persoon die je ontwerp controleert, kan iemand binnen het bedrijf zijn, of een externe expert.

###  Sla het beta-testen over

Elke database applicatie die complex genoeg is om echt bruikbaar te zijn, is complex genoeg om bugs
te bevatten.

Zelfs als je je database applicatie op alle mogelijke manieren getest hebt, dan nog kan je er zeker van
zijn dat ze vol fouten steekt. Het is onder programma-ontwikkelaars algemeen geweten dat een
programma in zijn V1.00 versie, gemiddeld 15 fouten bevat per 1000 lijnen code.

Beta-testen houdt in dat iemand de database gebruikt, die totaal geen idee heeft van de programmatie.
Die gebruiker zal fouten vinden waar jij nooit aan gedacht had, simpelweg omdat jij te veel weet. Die
fouten moeten uit de database gehaald worden voordat het product effectief in productie gaat.

###  Laat de beta-test software maar staan

Je hebt een eerste, rudimentaire versie af van je programma. Dit demonstreer je bij de gebruiker, en je
laat de mensen al wat beta-testen.

Na een week zijn de mensen al aan het programma gewoon, en het diensthoofd vraagt je om de
software te laten staan voor "tijdelijk" gebruik. Terwijl jij de hoekjes van de software afrondt, kunnen
zij dan al aan de slag. Ze weten wel dat nog niet alles in orde is, je hebt hen voldoende gewaarschuwd.
De verleiding is groot om de software inderdaad te laten staan. Het resultaat is dat de gebruikers
allerleid fouten tegenkomen waar je gewoon nog niet de tijd voor gehad hebt. Sporadisch wordt data
verloren. Het vertrouwen daalt snel en de klachten beginnen binnen te komen. Na twee maanden wordt
er nog enkel geklaagd. Het feit dat je het diensthoofd gewaarschuwd had voor de onvolledige software,
is intussen allang vergeten.

Zodra je dan de nieuwe software installeert, zijn de gebruikers sceptisch. Sommige delen zullen niet of
weinig gebruikt worden. In die delen zaten in het verleden nog te veel bugs en nu is het vertrouwen
zoek.

Bovendien blijkt dat je dagen werk hebt om de gegevens van de oude database om te zetten naar de
nieuwe database. Alle gegevens moeten opnieuw nagekeken worden, want inmiddels heb je enkele
kolommen bijgemaakt, die er vroeger niet waren. Soms ben je verplicht om aparte software te
schrijven, enkel om de conversie te kunnen uitvoeren. Het ganse project loopt gegarandeerd vertraging
op.

###  De gebruiker klaagt niet, dus alles is in orde

In praktijk klaagt de gebruiker pas zodra hij/zij niet meer kan verder werken.

Om verder te kunnen werken, zijn alle middelen toegelaten. Desnoods wordt met een ander programma
even in de data zelf ingegrepen om een fout te herstellen. Immers, als system administrator kan je ook
aan de SQL datatabellen aan, zonder dat je daarvoor via jouw software moet gaan.

Heel wat gebruikers zijn ook vergevend. Is het niet mogelijk om in edit-mode te gaan bij de goederen?
Geen probleem, de secretaresse weet een truukje. Eerst op de Print-knop drukken en onmiddellijk de
printopdracht annuleren. Daarna kan je wel editeren.

Zo is een invulveld dat op de verkeerde moment geactiveerd wordt, lastig. Echter, zolang het werk
verder kan gaan, vindt niemand het nodig om daarover een bug-report door te sturen.
Foutboodschappen zijn ook geen beletsel om verder te werken. Gewoon op de OK knop drukken. Zo
kon het gebeuren dat maandenlang gewerkt wordt met een corrupt databestand. De software gaf wel
een waarschuwing, maar liet daarbij de mogelijk om "op eigen risico" verder te werken. Pas toen het
databestand te veel was beschadigd, gaven ook de indextabellen het op. Ook de backup-tapes bevatten
nog enkel de corrupte gegevens, aangezien het probleem al zo lang bezig was.

### Documentatie van je code is niet nodig

Het lastigste onderdeel van een database-toepassing (eigenlijk van elk software-pakket), is het schrijven
van de handleiding, kort daarop gevolgd door het schrijven van documentatie in de software.

Morgen weet je waarschijnlijk nog wel hoe je programma in elkaar steekt. Volgende week ook. De
maand daarop misschien. Volgend jaar niet meer, zeker niet indien je intussen al enkele andere
programma’s achter de rug hebt.

In het gunstigste geval win je de loterij, en kan je voor de rest van je leven op vakantie. Je
ongedocumenteerde database komt dan in handen van iemand die zich in wanhoop afvraagt hoe je
databaserelaties in elkaar steken.

Het is niet de eerste keer dat een bedrijf verplicht is om een gans databasepakket opnieuw te schrijven,
omdat de hoofdprogrammeur (die nu in een ander bedrijf werkt wegens ruzie met het
departementshoofd) het nagelaten had om zijn code te documenteren.

Soms wordt wel eens gewezen op de gevaren van over documentatie. Die gevaren bestaan niet! Over
x maanden zal je blij zijn dat je de software zo goed gedocumenteerd hebt…


