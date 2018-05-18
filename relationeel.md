# Relationele datbases

## Inleiding

Zowat alle moderne databases worden uitgevoerd als een relationele database. Zonder uitzondering
worden alle grote bedrijven bestuurd met behulp van relationele databanken.

Tot voor kort was het beheer van die databanken het domein van computergoeroes die de harde
schijven rechtstreeks aanstuurden om een maximale performantie uit de database te halen. De dag van
vandaag wordt de database taak zelf overgenomen door gespecialiseerde bedrijven. De databases
worden dan verder beheerd door middel van een standaard taal.

Wellicht de meest bekende is gedefinieerd in de SQL (Standard Query Language) standaard. Een
andere is de XML (eXtended Markup Language) taal, die meer gekoppeld is aan Intranet en Internet
toepassingen.

In de relationele databases wordt het Entity-Relation model, dat we eerder gezien hebben, volledig
uitgewerkt. De term "Relationeel model" werd voor het eerst gebruikt door E.F. Codd. Codd werkte
op dat ogenblik voor IBM, die echter van diens onderzoeksresultaten geen gebruik maakte. De vruchten
van het werk van Codd werden daarom geplukt door een (op dat ogenblik) klein bedrijfje: Oracle.

## DBMS

Een DBMS (Database Management System) is een set van programma’s die kunnen gebruikt worden
om databases aan te maken, te beheren, en te gebruiken.

Grof gesteld bestaat een DBMS uit twee delen:

• Het database beheer gedeelte, waarmee databases kunnen aangemaakt, gewijzigd of
gewist worden. Hier worden ook relaties of tabellen en beperkingen op de data gedefinieerd.
De gegevens van het database beheer gedeelte worden bewaard in het schema. Het
schema bevat metadata die de databases zelf beschrijft.

• Het data beheer gedeelte, waarmee gegevens kunnen ingevoerd, gewist en gewijzigd
worden, eenmaal de database is aangemaakt.

De tendens bestaat om databases op meerdere platforms tegelijk beschikbaar te maken: PC’s,
mainframes, en onder verschillende operating systems. Om die integratie te kunnen verwezenlijken,
wordt gebruik gemaakt van een uniforme taal, meestal SQL.

## Het relationele model

Relationele databases zijn de dag van vandaag niet meer weg te denken. De hoofdreden hiervoor, is het feit dat je de structuur van de onderliggende database kan wijzigen, zonder dat je daarvoor al je programma’s moet aanpassen.

Veronderstel bijvoorbeeld dat je één of meerdere kolommen wil toevoegen aan je database. In dat geval
moet je je bestaande programma’s niet beginnen aanpassen, tenzij deze gebruik maken van de nieuwe
kolommen, uiteraard. Zolang je de namen van de bestaande kolommen niet wijzigt of wist, zal je
programma gewoon blijven verder werken met de database, alsof er nooit een wijziging is geweest.

Bij relationele databases geef je elke kolom een naam, en zal je de kolom enkel benaderen met behulp van die naam. De database zal dan intern de nodige handelingen uitvoeren om met de kolomnaam de juiste data te vinden.

Als gebruiker sta je dus een niveau boven de database zelf.

Het relationele van een database houdt in dat de rijen van de kolommen in één databasetabel, met
elkaar gekoppeld zijn.

Het doel van het relationele model is een betrouwbaar informatiemodel. Alle voorheen beschikbare methoden voor opslag van gegevens vertoonden inherente problemen of anomalieen genoemd. Hieronder enkele voorbeelden van anomalieen. Stel dat een bedrijf een adresboek geïmplementeerd heeft. Aangezien een bedrijf te maken heeft met misschien andere grote bedrijven kan het makkelijk gebeuren dat zich op 1 lokatie meerdere contacten bevinden. Zo kan het dus zijn dat 2 contacten op paardenmarkt 92 bevinden. In eerste instantie lijkt dit geen probleem op te leveren, omdat de beschikbare informatie relatief eenvoudig toegankelijk is. Het probleem ontstaat wanneer dit bedrijf besluit naar een andere lokatie te verhuizen In dat geval zullen we de informatie in 2 verschillende rijen moeten aanpassen. Di t lijkt misschien niet dramatisch, maar stelt u zich eens voor dat de tabel geen 2 maar 20000 rijen telt. Iemand of iets (een programma) moet ervoor zorgen dat de gegevens overal correct worden aangepast.

Een ander probleem stelt zich dat we een databank voor contactgegevens van personen (onze adresboek) hebben gemaakt, maar we willen enkel contact gegevens van een bedrijf invoegen. Dit gaat niet omdat onze applicatie personen vraagt. Dus moeten we wachten tot we een naam van een specifiek persoon hebben die aan het bedrijf gelinkt kan worden.

Deze voorbeelden van anomalieen worden dus voorkomen door het relationeel model.

## De structurele elementen van een relationele databasemodel

Het relationele model was innoverend door zijn eenvoud en wiskundige onderbouwing. Veel informatie wordt in tabelvorm gestructureerd en tabellen kunnen wiskundig worden weergegeven door middel van relaties. (we onderscheiden enerzijds basistabellen, anderzijds afgeleide relaties ( of views zie later). Onderstaand wordt het relationele model uit de doeken gedaan, met als basis:

•	structureel aspect : gebruikers zien de data als tabellen.
•	integriteitsaspect : de tabellen voldoen aan integriteitsbeperkingen.
•	manipulatief aspect : de operators leiden tabellen van tabellen af.

## Structurele Aspect

### Basistabellen

De bouwstenen van een tabel zijn atomaire datatypes. Met atomair bedoelen we dat de gegevens, voor wat betreft het relationeel databasemodel, als 1 eenheid en dus als niet verder opdeelbaar worden beschouwd. Met andere woorden, kan men atomaire gegevens niet verder opsplitsen in deelgegevens. (atomaire gegevens kunnen hierdoor niet samengesteld of meerwaardig zijn!).
Bijvoorbeeld de tabel ‘Artiest’ uit een relationele schildersdatabase. Het schema is:
Artiest (A_ID :char(3), Naam:varchar, Voornaam:varchar, Geboren:integer,Gestorven:integer).

Deze tabel is opgebouwd uit de naam Artiest en 5 attributen, die elk een atomair datatype hebben. Op een bepaald tijdstip bestaat deze tabel bijvoorbeeld uit 4 rijen:
 
Zoals reeds gezegd wordt een tabel op deze manier gevisualiseerd in het relationele model:

![tabel](img/tabel1.jpg)

Het aantal attributen (of kolommen) van een tabel noemen we de graad van de relatie. Het datatype van een attribuut noemen we het attribuuttype. 
De waarden uit de rijen heten attribuutwaarden.
Het aantal rijen van de tabel wordt de kardinaliteit van de tabel genoemd.
Eigenschappen

1.	Binnen een tabel kunnen geen dubbele rijen voorkomen.
2.	De rijen van een tabel zijn niet geordend.
3.	De attributen van een tabel zijn niet geordend.
4.	Alle attribuutwaarden van een tabel zijn atomair.

### Afgeleide tabel of Views

Naast tabellen beschouwen we in het relationeel database model ook views. 

> Een view is een virtuele tabel die is afgeleid van basistabellen en/of andere views


Views maken het mogelijk om de tabellen op een alternatieve manier te bekijken. Van de view wordt enkel de naam in de catagolus van de database bijgehouden en worden de rijen van de view dus niet (redundant) opgeslagen, maar worden telkens opnieuw gereconstrueerd uit de betrokken tabellen.
Views worden voornamelijk gebruikt om te ingewikkelde instructies op basistabellen te vermijden. Er wordt eerst een view aangemaakt, en op deze view worden verder sql instructies op toegepast.

### Ontbrekende informatie

In reële situaties komt het voor dat informatie ontbreekt. Twee hoofdredenen voor dit ontbreken zijn:

-	Onbekende informatie: de gegevens bestaan, maar zijn niet voorhanden. Zodra de gegevens beschikbaar zijn, is er geen sprake meer van ontbrekende informatie.

-	Niet gedefinieerde informatie: de gegevens bestaan niet of zijn niet van toepassing. Ze zullen dus niet beschikbaar komen.
Het ontbreken van data moet op een gepaste manier worden behandeld in een database. Hiervoor bestaan er twee technieken, namelijk het gebruik van NULL-waarden en DEFAULT-waarden.

#### Null – waarden

Een null waarde geeft aan dat de actuele attribuutwaarde ontbreekt. Bij de meeste database systemen wordt verondersteld dat de attributen null-waarden kunnen bevatten, tenzij dit expliciet verboden wordt. Een verbod voor null-waarden wordt vastgelegd binnen de sql –in structie CREATE TABLE (deze wordt gebruikt om een nieuwe tabel aan te maken). Bij het desbetreffende attribuut worden de woorden  NOT NULL opgegeven.

#### Defaultwaarden

Een alternatief is om bij de opbouw van de database een zogenoemde defaultwaarde te definieren voor een attribuut waarvoor data kunnen ontbreken. Een defaultwaarde wordt vastgelegd met de sql instructie CREATE TABLE en met het woord DEFAULT.
Bijvoorbeeld, bij de specificatie van het attribuut Geboren met datatype integer van de tabel Artiest kan bijvoorbeeld opgegeven worden dat de defaultwaarde 0 is.
Let wel, defaultwaarden hebben als nadeel dat zij slechts een benadering of model voor de attribuutwaarde geven, wat tot verkeerde resultaten kan leiden bij het afleiden van data zoals minimum, maximum, som , gemiddelde.

## Integriteitsaspecten - Sleutels

Het relationele model heeft mogelijkheden om semantische correctheid van data in de database te helpen garanderen (sleutels, integriteitsregels). Wel te weten dat een dbms niet alle fouten kan opvangen en de zorg van de correctheid van data grotendeels bij de gebruiker of toepassingsprogramma ligt dat de data invoert.

### Sleutels

Verwantschappen tussen tabellen wordt in het relationeel model weergegeven via sleutels. Drie essentiele sleutelconcepten worden onderscheiden:

-	Kandidaatsleutel
-	Primaire sleutel
-	Vreemde sleutel


#### Kandidaatsleutel

Als K een deelverzameling is van de verzameling van alle attributen van een gegeven tabel T, dan is K een kandidaatsleutel voor T als en slechts als voldaan is aan:

-	Uniciteiteigenschap: In R bevatten geen 2 rijen dezelfde waarde voor alle attributen uit K.
-	Irreducibiliteiteigenschap: wanneer uit K attributen worden weggelaten, mag niet meer voldaan zijn aan de uniciteitseigenschap.

Een kandidaatsleutel kan enkelvoudig of samengesteld zijn!
Bijvoorbeeld uit een tabel Artiest uit de schilderskunstdatabase kunnen 2 kandidaatsleutels worden beschouwd:

-	De kandidaatsleutel A_ID(char(3)): want deze is een unieke arteistenidentificator.

-	De kandidaatsleutel: {Naam:varchar, voornaam:varchar, Geboren:integer}


### Primaire sleutel

Het relationeel model schrijft voor dat er voor elke tabel precies 1 primaire sleutel gekozen moet worden uit de kandidaatsleutels van de tabel. De overige kandidaatsleutels noemen we alternatieve sleutels. (in de praktijk heeft men er baat bij om een kandidaatsleutel met een zo klein mogelijk aantal attributen als primaire sleutel te kiezen.
Omdat de combinatie van attribuutwaarden van een primaire sleutel of alternatieve sleutel uniek moeten zijn, mogen de attributen van een primaire sleutel geen null-waarden bevatten.


### Vreemde sleutel

Om een verwantschap tussen een rij uit tabel T1 en nul of meer rijen uit tabel T2 weer te geven worden vreemde sleutels gebruikt.
Een vreemde sleutel F van tabel T2 is een verzameling van attributen van T2 waarvoor geldt:

-	Er bestaat een tabel T1 (T1 niet noodzakelijk verschillend van T2° met een kandidaatsleutel K1, die evenveel attributen bevat als F en waarbij er een 1 op 1 correspondentie is tussen de attributen van F, zodat corresponderende attributen dezelfde datatypes hebben

-	Op elke tijdstip komt elke waarde van F in T2 eveneens voor als waarde van K in een rij van T1.
In de praktijk worden vreemde sleutels meestal gedefinieerd over een primaire sleutel!

Bijvoorbeeld: 


![vreemdesleutel](img/vreemdesleutel.jpg)

### Integriteitrestricties

Een tweede mogelijkheid ter ondersteuning van data-integriteit in relationele databases betreft de mogelijkheid om integriteitsrestricties te specifieren voor de tabellen.

Een integriteitsrestrictie is een voorwaarde waaraan alle data uit een database op elk moment moeten voldoen.


Een integriteitsrestrictie wordt gekarakteriseerd door een naam en een logische expressie (waar, onwaar, null). Als de evaluatie onwaar oplevert zal het dbms in actie schieten door een foutboodschap aan te geven.

Bijvoorbeeld:

![assertion](img/assertion.jpg)


## Manipulatief aspect 

De operators leiden tabellen van tabellen af. De gedragsaspecten van een relationeel databasemodel zijn onderbouwd uit de traditionele verzamelingenleer, met als operaties: vereniging, doorsnede, verschil en cartesiaans product, plus enkele toegevoegde namelijk select, projectie en join (er zijn er nog andere , maar in deze cursus bespreken we deze). 
basisoperatoren van de relationele algebra: vereniging, doorsnede, verschil en cartesiaans product

### De verenigingsoperator (T1 union T2)

De vereniging van 2 tabellen (met schema’s van hetzelfde type!) is een tabel  met een schema van hetzelfde type die bestaat uit rijen die ofwel voorkomen in T1, ofwel voorkomen in T2, ofwel in T1 en T2. (Nota: tabellen kunnen geen dubbele rijen bevatten!)

### De doorsnede operator (T1 intersect T2)

Als T1 en T2 twee tabellen zijn met schema’s van hetzelfde type, dan is de doorsnede van deze tabel een tabel met een schema van hetzelfde type en met rijen die zowel in T1 als T2 voorkomen.

### De verschil operator (T1 minus T2)

Als T1 en T2 twee tabellen zijn met schema’s van hetzelfde type, dan is het verschil van deze tabellen een tabel met een schema van hetzelfde type en met rijen die wel voorkomen in T1 maar niet in T2


![manipulatief1](img/manipulatief1.jpg)

### Cartesiaans productoperator

Als T1 en T2 twee tabellen zijn die geen gemeenschappelijke  attributen hebben, dan is het cartesisch product, 
                                     T1 TIMES T2
 
van deze tabellen een nieuwe tabel waarvan de attributen uit hetschema worden bekomen door de unie te nemen van de verzameling van de attributen van T1 en de verzameling van de attributen van T2. 
De rijen die hier bestaan is een rij verkregen uit T1 samen te voegen met een rij uit T2.


![carhesis](img/carhesis.jpg)


### Selectie operator (where)

Als T een tabel is en e een logische expresie is waarvan alle parameters attributen zijn van T dan resulteert de selectie:

R where e

In een nieuwe tabel die dezelfde attributen heeft als T en waarvan de rijen bestaan uit de rijen van T waarvoor de expressie e geëvalueerd is naar ‘waar’.


![selectie](img/selectie.jpg)

### Project operator

De project operator wordt gebruikt om attributen te selecteren uit een relatie. Als 
AlsT  een relatie is en {A1:T1, A2:T2, …, Ap:Tp} een deelverzameling is van de attributen van R dan resulteert de projectie, 
                                      T {A1, A2, …, Ap}
in een nieuwe tabel waarvan het schema bekomen wordt uit het schema van T door enkel de attributen uit {A1:T1, A2:T2, …, Ap:Tp} te behouden en waarbij de rijen bestaan uit alle rijen t=(A1:w1, A2:w2, …, Ap:wp) waarvoor een rij voorkomt in TR met attribuutwaarde w1 voor A1, w2 voor A2,…, en wp voor Ap. 


![projectie](img/projectie.jpg)

### De Join operator

De Join bestaat uit een aantal varieten, we bespreken hier de inner – join.
Als T1 een tabel is met attributen 
           {X1:TX1, X2:TX2, …, Xm:TXm, Y1:TY1, Y2:TY2, …, Yn:TYn}
en T2 een tabel is met attributen 
             {Y1:TY1, Y2:TY2, …, Yn:TYn, Z1:TZ1, Z2:TZ2, …, Zp:TZp}
dan resulteert de join, 
                                                T1 JOIN T2 
in een nieuwe tabel waarvan het schema bestaat uit de attributen {X1:TX1, X2:TX2, …, Xm:TXm, Y1:TY1, Y2:TY2, …, Yn:TYn,Z1:TZ1, Z2:TZ2, …, Zp:TZp} en waarvan de rijen bestaan uit alle rijen die worden bekomen door een rij van T1 samen te voegen met een rij van T2 onder de voorwaarde dat alle gemeenschappelijke attributen gelijke waarden moeten hebben. 


![join](img/join.jpg)
 

## Relationeel database ontwerp

### inleiding

In dit hoofdstuk bespreken we kort de analyse van databaseproblemen.

We vertrekken van een vraagstelling door een gebruiker. We bepalen de input-output flow en
onderzoeken welke processen binnen bv. een bedrijf werkzaam zijn. Wie moet op welk moment de data
behandelen? Welke gegevens moeten zeker bewaard worden? Welke rapporten moet afgedrukt
worden? Welke problemen kunnen zich voordoen bij het behandelen van de gegevens (bestellingen die
geannuleerd worden, beschadigde of verdwenen goederen, kortingsacties, werknemers die ontslag
nemen, ...)? Dit gedeelte wordt de informatie-analyse genoemd, wat we reeds gezien hebben voor het maken van een ER-diagram.

Eenmaal een programmeur een goed beeld heeft van de informatie-analyse binnen een bedrijf, kan hij
starten met de design van de database. Dit is nog steeds een design op een hoog niveau. Welke
datatypes zullen gebruikt worden voor de gegevens? Welke gegevens worden in één tabel bewaard?
Welke gegevens moeten snel kunnen benaderd worden? Welke gegevens moeten snel kunnen
gesorteerd worden? Wat zijn de relaties tussen de tabellen onderling? Hoeveel records kunnen
maximaal opgeslagen worden voor een gegeven schijfgebruik? Dit onderdeel wordt de
gegevensanalyse genoemd.

Nadien wordt pas de vraag gesteld welke databasestructuur het meest geschikt is om de gevraagde data
te bewaren. Voor grotere databases zal in praktijk meer en meer blijken dat de beste aanpak voor de
database, het relationele model is. 


### de informatie analyse

Nemen we als voorbeeld het informatiesysteem van een bank.
De gebeurtenissen die aan het informatiesysteem moeten bekendgemaakt worden zijn:

• overschrijvingen van rekeningen
• openen van nieuwe rekeningen
• opzeggen van bestaande rekeningen

Merk op dat ook stortingen en afhalingen kunnen beschouwd worden als een speciale manier van
overschrijven, nl. naar of van een fictieve rekening.

Later moet informatie gegeven worden, zoals:

• een directe melding, indien het saldo ten gevolge van een transactie onder een bepaald
minimum komt.
• saldo van een rekening, wanneer de houder hierom vraagt.
• éénmaal per week een rekeningoverzicht voor alle rekeninghouders van rekeningen waarop sedert het vorige overzicht mutaties werden doorgevoerd. Dit overzicht bevat de mutaties in kwestie en het nieuwe saldo.

Het vastleggen van de behoefte aan informatie bij de gebruikers, is de informatie-analyse. Met de
bovenstaande (eenvoudige) specificatie kunnen we ons al een beeld vormen van welke "dingen" voor
de bank belangrijk zijn, en wat de bank over die dingen moet bijhouden:

![analyse1](img/analyse1.jpg)


In deze tabel vinden we de basisgegevens die voor de bank belangrijk zijn, met daarbij telkens een
opsplitsing in deelgegevens (2e kolom) , die samen belangrijk zijn om elk van de elementen uit de 1e
kolom te bepalen.

Naast dit overzicht kunnen we nog regels formuleren die betrekking hebben op de samenhang tussen
deze dingen: zo kan een rekeninghouder meer dan één rekening hebben, een rekening kan niet bestaan
zonder dat er een houder bekend is, ...

Het resultaat van de informatie-analyse is een model van de werkelijkheid, waarin wordt vastgelegd
"wat" er is, en niet hoe er vanuit computer-toepassingen naar wordt gekeken.

Deze informatie-analyse komt tot stand door de informatie-analisten in samenspraak met de gebruikers.
Zonder enige twijfel is de informatie-analyse het belangrijkste moment in de aanmaak van de database.
Indien een database een belangrijke structurele fout bevat, is dit meestal te wijten aan een fout bij de
informatie-analyse.

Het oplossen van een fout in de informatie-analyse is in de meeste gevallen een tijdrovende en dure
zaak. Om die reden zullen heel wat bedrijven eisen dat de opdrachtgever een document ondertekent
waarin de informatie-analyse gedetailleerd beschreven staat. Dit heeft twee redenen. De eerste reden is
dat de klant daarmee de goedkeuring geeft voor de analyse. De tweede reden is dat de klant zo belet
wordt om de eisen telkens te wijzigen in de loop van het project.

In de fase van de informatie-analyse, komt de functie van de analyst het meest tot uiting. Het is
namelijk van uitzonderlijk belang dat de analyst een goede kennis heeft van het productieproces en de
onderliggende problemen.

Het maken van een goede informatie-analyse, is een kunst. De analyst moet in staat zijn om de
informatie te doorgronden die in het bedrijf rond gaat. Dit omvat ook de informatie die de mensen je
niet vertellen omdat ze die gegevens als "evident" beschouwen. Als analyst moet je mensen kunnen
uitvragen en interviewen, zonder dat ze hun geduld verliezen en zonder dat de analyst zijn geduld
verliest.

Waar moet je op letten bij het maken van de analyse ?

• Wat zijn de gegevens die moeten opgeslagen worden? Klanten, leveranciers, goederen,
magazijnen, facturen, componenten, gemeenten, ...

• Welke zijn de verschillende fasen in de behandeling? Wie moet allemaal onafhankelijk
met de database werken? Dit worden aparte modules in de database. O.a. klantenbeheer,
stockbeheer, behandeling van goederen, ...

• Wat is de input-output flow in elk van de verschillende fazen? Wat zijn de noodzakelijke
gegevens en wat wordt gevraagd als output?

• Maak een lijst met alle rapporten die moeten kunnen gemaakt worden in elke fase van het
productieproces. Dikwijls vormen deze rapporten een zeer goede basis voor een doorzicht
in het databaseprobleem.

• Moet er automatisch gemeten worden, of zijn sommige onderdelen machine-afhankelijk?
Moet er compatibiliteit zijn met andere databaseproducten? Moet import en export van
gegevens mogelijk zijn? ...


#### de analyse

De eerste fase in de gegevensanalyse is het omzetten van de individuele gegevens naar een
databaseformaat.

Nemen we als voorbeeld de zeer klassieke structuur van een klantenbestand. Stel dat de informatieanalyse aangaf dat de volgende gegevens belangrijk zijn voor het klantenbestand:

![analyse2](img/analyse2.jpg)

De eerste taak is het toevoegen van een uniek nummer. Dit wordt doorgaans een ID genoemd en moet
ruim genoeg bemeten zijn. In veel gevallen wordt een "long integer" nummer genomen.

Verder voorzien we bijvoorbeeld 50 karakters voor de naam, en 100 karakters voor het adres. De
telefoonnummers worden gesplitst in een telefoon- en telefaxnummer. Als fiscale gegevens wordt enkel
het BTWnummer weerhouden. We krijgen dan al voorlopig:

![analyse3](img/analyse3.jpg)

In deze gegevensanalyse zitten reeds enkele stevige problemen. Zo is het best mogelijk dat een
Telefoonnummer karakters bevat (bv. +32 om de landcode aan te duiden). Veel mensen houden er
verder van om puntjes te plaatsen in het telefoonnummer. Ook het BTW-nummer kan alfanumerieke
karakters bevatten (bv. BE 334.232.100 om een Belgisch BTW nummer aan te geven).

Om die reden houden we de volgende regel aan: een veld krijgt pas een numerieke waarde indien er
ook effectief met dat veld gerekend wordt. In alle andere gevallen gebruiken we een alfanumeriek veld.
De structuur wordt dan bijvoorbeeld

![analyse4](img/analyse4.jpg)

Deze analyse is nog ver van ideaal. We zullen nog moeten normaliseren. Dit zien we in het volgende
hoofdstuk. Toch kan je je al een idee vormen van hoe de kolommen van de tabellen moeten gevormd
worden. Bij de volledige gegevensanalyse zullen zo alle tabellen gedefinieerd zijn. 

Bij kleinere designs wordt rechtstreeks het relationeel model – (tabel – relatie structuur) ontworpen. Doch wordt in vele gevallen steeds vertrokken vanuit een conceptueel plan – gerepresenteerd met een ER diagram. Onderstaand hoofdstuk geeft het algoritme om vertrekkende vanuit een ER- diagram een relationeel model te ontwerpen. (een goed ontworpen ER diagram laat weinig fouten toe met betrekking tot data redundantie…)

## het omzettingsalgoritme voor relationele databases

Het omzettingsalgoritme bestaat uit een aantal stappen (8):

### Omzetting van reguliere entiteiten

Voor elke reguliere entiteit (rechthoek) maken we een tabel aan.

-	Als tabel naam wordt de naam van de entiteit gekozen
-	Alle enkelvoudige, niet afgeleide attributen voegen we toe als kolom van de tabel
-	Voor alle samengestelde attributen voegen we alleen de enkelvoudige, niet afgeleide componentattributen toe aan de tabel.
-	Alle attributen uit de sleutel van de entiteit vormen de primaire sleutel van de tabel. Als er samengestelde attributen voorkomen in de sleutel, maken enkel hun enkelvoudige componenten deel uit van de primaire sleutel.

Merk op dat afgeleide attributen niet worden opgenomen in de tabel, en hun data dus ook niet wordt opgeslagen in de database!

Bijvoorbeeld de entiteit Artiest:

![reguliere](img/reguliere.jpg)

### Omzetting van zwakke entiteiten

Voor elke zwakke entiteit (dubbele rechthoek) maken we ook een tabel aan. Daarbij ga je als volgt te werk:
-	Kies een relatienaam. 

-	Alle enkelvoudige, enkelwaardige, niet-afgeleide attributen van het zwak
  entiteittype worden toegevoegd als kolom van de tabel. 

-	 Voor alle samengestelde attributen worden enkel de enkelvoudige, 
  enkelwaardige, niet-afgeleide attributen toegevoegd. 

-	 Voeg vreemde sleutel(s) toe: voeg de primaire sleutel(s) toe van de identificerende tabel aan de tabel van de zwakke entiteit.
 
-	Voeg de enkelvoudige, enkelwaardige, niet-afgeleide (componenten 
  van de) attributen van de relatie toe.
 

Bijvoorbeeld:

![zwakke](img/zwakke.jpg)


### Omzetting van super/sub types

We veronderstellen hier wel m subtypes en 1 supertype. (De tabellen zijn in stap 1 reeds aangemaakt). Dus moeten we enkel de verwantschappen of relaties nog modelleren. Hier zijn verschillende mogelijkheden voor:

#### Verschillende tabellen voor sub en super type
De attributen van de primaire sleutel van het supertype worden toegevoegd aan het subtype en vormen hier een vreemde sleutel


![supersub](img/supersub1.jpg)

#### Verschillende tabellen, maar enkel voor de subtypes

-	Alle attributen van het supertype worden toegevoegd als kolom in het subtype ( en de primaire sleutel wordt nu primaire sleutel in het subtype)
-	De supertype tabel wordt verwijderd.


![supersub](img/supersub1.jpg)

### Omzetting van 1:1 relaties

We hebben hier 3 mogelijke werkwijzen waaruit kan gekozen worden:

#### Samenvoegen van beide tabellen

-	Kies een tabel die totaal participeert in de binaire relatie.
-	Voeg alle attributen van de andere tabel toe aan de gekozen tabel
-	Verwijder de andere tabel
-	Voeg de enkelvoudige , niet-afgeleide attributen toe aan de tabel

![relatieOmzet11](img/relatieOmzet11.jpg)


#### Behoud van beide tabellen

-	Kies een tabel : voeg de primaire sleutel van de andere toe als vreemde sleutel (kies een tabel die totaal participeert in de tabel)
-	De attributen van de tabel toevoegen aan de gekozen tabel

![relatieOmzet112](img/relatieOmzet112.jpg)

#### Behoud van beide tabellen met een extra tabel

-	Een extra tabel wordt toegevoegd
-	Kies de primaire sleutels van beide en voeg deze als vreemde sleutels toe
-	De enkelvoudige , niet-afgeleide attributen toevoegen
-	Als primaire sleutels kan 1 van de vreemde sleutels gekozen worden


![relatieOmzet113](img/relatieOmzet113.jpg)

### Omzetting van een 1:N relatie

-	Kies de tabel met kardinaliteit “meerdere”. Voeg de primaire sleutel van de andere tabel toe als vreemde sleutel van de gekozen tabel.
-	Voeg de attributen toe aan de gekozen tabel


![relatie1Nomzet](img/relatie1Nomzet.jpg)

### Omzetting van M:N Relaties

- Maak een nieuwe tabel aan. (Kies een gepaste naam). 
- Voeg de primaire sleutels van de tabellen van de betrokken 
  relatie toe als vreemde sleutels aan de nieuwe tabel.
- Voeg de enkelvoudige, enkelwaardige, niet-afgeleide attributen van de relatie toe aan de nieuwe tabel. 
-  De primaire sleutel van de nieuwe tabel  bestaat uit de 
  samenvoeging van de attributen van beide vreemde sleutels.


![mnomzet](img/mnomzet.jpg)

### Omzetting van meerwaardige attributen

Voor elk niet afgeleid, meerwaardig attribuut wordt een nieuwe 
tabel aangemaakt!

- Kies een gepaste naam voor de nieuwe tabel!
- Voeg de primaire sleutel van de tabel waar het meerwaardig attribuut voorkomt toe als vreemde sleutel van de nieuwe tabel
- Voeg de nodige attributen toe om 1 waarde van het meerwaardig attribuut op te slaan.
- De primaire sleutel ontstaat door alle attributen samen te nemen

![meerwaardigomzet](img/meerwaardigomzets.jpg)


### Omzetting van N-are (n>2) relaties

Voor elk n-air relatietype waarbij n>2, wordt een nieuwe tabel aangemaakt!
- Kies een gepaste naam voor de tabel! 
-  Voeg de primaire sleutels van de tabellen van de betrokken 
  relatie als vreemde sleutels toe.
- Voeg de enkelvoudige, enkelwaardige, niet-afgeleide attributen van de relatie toe. 
- De primaire sleutel van de nieuwe tabel bestaat uit de 
  samenvoeging van de attributen van alle vreemde sleutels, tenzij er entiteittypes voorkomen waarvoor de kardinaliteitrestrictie 1 is. In dat geval best een unieke identifier aanmaken! 
  
![naire](img/naire.jpg)





