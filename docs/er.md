
* [Inleiding](inleiding.md)
* [Logische en fysische gegevens](gegevens.md)
* [Entiteit-Relatie diagramma](er.md)
* [Relationele databases](relationeel.md)
* [Normalisatie](normalisatie.md)

# Logische beschrijving van gegevens met het E-R model

![er](img/ervoorbeeld.jpg)

Een van de belangrijkste stappen bij het opzetten van een nieuwe database is het databaseontwerp. Dit ontwerp verloopt in een aantal fasen: eerst moet abstractie gemaakt worden van de probleemstelling en wordt een abstract, conceptueel model ontworpen. Als je beschikt over het conceptueel databaseontwerp, kun je een geschikt databasemodel (vb.relationeel model, of object georiënteerd model) kiezen en ontwikkel je het database schema. Dit noemen we het logische database ontwerp. Daarna implementeer je het databaseschema in een dbms (database Management Systeem, of de software laag boven de fysieke data). Dit noemt met het fysische database ontwerp.

Sinds een aantal jaren tracht men de gegevensanalyse en de gegevensbeschrijving volledig gescheiden
te houden van de fysische opslag. Vandaar dat er naast de fysische terminologie vaak logische termen
worden gebruikt.

Nochtans moet onmiddellijk worden opgemerkt dat in de praktijk de logische en fysische termen vaak
gewoon door elkaar worden gebruikt, en dat zelfs binnen de logische terminologie de vlag niet steeds
dezelfde lading dekt!

Hoewel er al meerdere pogingen werden gedaan om een standaardterminologie door te drukken,
worden in de praktijk nog vaak verschillende termen gebruikt om eenzelfde zaak aan te duiden, en
worden met eenzelfde term soms verschillende zaken aangeduid.

Bij het doornemen van de literatuur is het dan ook zaak eerst goed te kijken wat door de schrijver met
een bepaalde term wordt bedoeld... In deze cursus stellen we "een" terminologie voor, die in de praktijk
vaak wordt gebruikt. Deze terminologie wordt het entiteit-relatiemodel genoemd. 

Het entiteit-relatiemodel (E-R) werd voor het eerst in 1976 beschreven door Peter Chen (1). Nadien
werd het verder uitgebreid, en zijn er dialekten gekomen op het basismodel. Wij zullen hier het meest
voorkomende type bespreken.

Deze techniek legt de voorschriften vast voor de opbouw van een ER-diagram. Het grote voordeel van een dergelijk model is dat het onafhankelijk is van enig databasemodel. Hierdoor kun je het diagram via gepaste omzettingsalgoritmes omzetten naar databaseschema’s..(een relationeel of een object georiënteerd, of een … -schema).

## Het volledige databaseontwerpproces

Het databaseontwerpproces bestaat uit 4 fases:

![ontwerpproces](img/ontwerpproces.jpg)

Bij de informatievergaring moeten we onder meer achterhalen welke verwachtingen er zijn over de database, welke data we al dan niet moeten opnemen en welke betekenis deze data hebben. Daartoe kunnen we interviews afnemen met de opdrachtgever en potentiele gebruikers van de database.
 
Uit deze analyse volgt bijvoorbeeld dat indien we een schilderkunstdatabase willen ontwerpen, er informatie moet worden opgeslagen over schilderijen, schilders en eigenaars. Als relevante data worden de schilderijnaam, de waarde van een schilderij, de periode waarin het werk is geschilderd, de voor-en achternaam van de schilder, het geboortejaar en sterftejaar van de schilder en de naam en het adres van de eigenaar geïdentificeerd.

Daarbij wordt onder meer verduidelijkt dat het jaartal volstaat als informatie voor de periode van het schilderij en dat de stad en het land volstaan als adresinformatie voor de eigenaars.

Verder  blijkt dat er frequent schilderijen worden toegevoegd, dat de verkoopwaarde van een schilderij voortdurend verandert en dat het soms gebeurt dat een schilderij van eigenaar verandert.

Ook volgt er uit de analyse dat het voor de organisatie belangrijk is om een goed overzicht te hebben van de voorhanden zijnde schilderijen. Daarbij moeten we in hoofdzaak rapporteren welke eigenaars welke schilderijen in hun bezit hebben en wat de totale waarde is van alle schilderijen die in het bezit zijn van een bepaalde eigenaar.

Eigenlijk onderscheiden we bij de informatievergaring 3 soorten analyses:

1.	Domein analyse: kennis over welke informatie in de database moet zitten, plus kennis over de context van de data. Dit komt men te weten aan de hand van de klassieke ondervragingsmethoden: vergadering, interviews, email, lezen van handleidingen, rapporten…
2.	Functionele analyse: het ontdekken van de informatiestroom: hoe wordt informatie verwerkt en welke nieuwe informatie wordt aangemaakt.
3.	Behoefte analyse: welke rapporten moeten aangemaakt worden, welke applicaties zullen gebruik maken van de database..

Bij het conceptueel ontwerp zal een plan van de te ontwerpen database worden opgesteld.  Voor de schilderkunstdatabase zal de informatie worden georganiseerd rond de centrale concepten “Schilderij”, ‘Artiest’, “Eigenaar”. Het conceptueel ontwerp resulteert in een conceptueel diagram (het ontwerp) en een functionele beschrijving van de operaties die nodig zijn om de database consistent en actueel te houden.

In de functionele beschrijving moet bijvoorbeeld worden vastgelegd dat bij het toevoegen van een nieuwe artiest moet worden gecontroleerd of het sterftejaar niet voor het geboortejaar valt.

Bij het logische ontwerp kiezen we voor een databasemodel en zetten we het plan van de database om naar een databaseschema dat comform is met alle voorschriften uit het gekozen databasemodel. (Bijvoorbeeld we kiezen voor een relationeel databasemodel- (zie later) -  of we kiezen voor een object georiënteerd model of …).

Het fysieke ontwerp behelst de implementatie van het logisch databaseontwerp. Omdat we gekozen hebben voor bijvoorbeeld het relationele model worden daartoe de instructies van SQL gebruikt.

### Definities

Bij het conceptueel ontwerp zijn abstrahering en modellering key elementen. Abstrahering heeft tot doel een duidelijk beeld te schetsen van wat belangrijk is en wat minder belangrijk voor de database, en het zoeken naar verwantschappen tussen data. Om dit resultaat vast te leggen  gaan we dit modelleren en maken we daarvoor gebruik van een representatietechniek: ER diagramma. (Je kan ook kiezen voor een UML diagramma, wat gebruikt wordt bij objectgeorienteerde ontwikkeling, terwijl ER zich meer richt tot database ontwikkeling!).

> In een ER-diagramma worden concepten uit de reële wereld gemodelleerd aan de hand van entiteiten en verwantschappen tussen entiteiten.

De belangrijkste elementen van het E-R-model zijn entiteiten, attributen en relaties.
Een entiteit is een begrip uit de werkomgeving van een gebruiker. Het is iets dat betekenis heeft voor
de gebruiker. In de logische terminologie wordt een persoon, zaak, feit waarover we informatie
bijhouden een entiteit (E: entity) genoemd. Andere termen die hiervoor gebruikt worden zijn object of
relatie (E: relation) of entiteit (E: entity), ...

> Een entiteit is een ‘ding’ dat een zelfstandig bestaan leidt in de reële wereld!

Voorbeelden: een klant, een werknemer, een leverancier, een magazijn, een afdeling, een produkt, een
voertuig, een bestelling, een betaling ...

Een entiteit wordt  in een ER-diagram gevisualiseerd door een rechthoek met de naam van de entiteit in.

Wat we over die entiteiten bijhouden noemen we attributen. Een attribuut (E: attribute) is een
eigenschap of karakteristiek van een entiteit. Andere termen die hiervoor gebruikt worden zijn
kenmerk, data-item, ...

Entiteiten komen naar voren tijdens de informatievergaring doordat er gemeenschappelijke karakteristieken, dit zijn dus de attributen, rond een ‘ding’ vormen. Bijvoorbeeld een jaartal, geschilderd door, prijs zijn gemeenschappelijke karakteristieken van de entiteit ‘schilderij’.

Beschouw het voorbeeld van iemand die een rekening heeft bij een bank. Een individueel
rekeninguittreksel vormt een entiteit. Ook de beschrijving van de rekeninghouder en de rekening zelf vormen elk een entiteit. De entiteit REKENINGHOUDER kan als attributen hebben: naam, adres,
telefoon. De entiteit REKENINGUITTREKSEL kan als attributen hebben: nummer van de houder,
bedrag, commentaarveld, rekeningnummer correspondent, ...

Een attribuut wordt in een ER-diagram gevisualiseerd door een ovaal.

Voorbeelden van visualisatie:

![ervisual](img/ervisual.jpg)

Een verzameling van entiteiten wordt bijgehouden in entiteitsklassen – of in deze cursus ook gewoonweg entiteit genoemd. Zo kan de entiteitsklasse STUDENTEN bestaan uit de entiteiten met attributen StudentNaam, StudentAdres, StudentNummer, StudentPostnummer, ...

Indien gegevens worden toegevoegd aan de entiteitsklasse, betekent dit dat we attribuutwaarden gaan
toekennen voor een bepaalde occurrence van een entiteit. Een occurrence (letterlijk "voorkomen")
wordt ook wel exemplaar van een entiteit genoemd.

Indien we dus een nieuwe rekeninghouder zouden toevoegen, betekent dit een nieuwe occurrence van
de entiteit houder, waarbij we voor de verschillende attributen de overeenstemmende attribuutwaarden zullen invullen.

![visual2](img/visual2.jpg)


Hierboven is de entiteit dus "houder", met als attributen "naam", "adres" en "telefoon". Van deze
entiteit zijn er 2 occurrences getoond, waarvoor telkens 3 attribuutwaarden werden toegekend.

## Soorten attributen

Attributen kunnen enkelvoudig of samengesteld zijn:

Een enkelvoudig attribuut kan niet op een zinvolle manier verder onderverdeeld worden. Zo zal voor
de entiteit rekening het attribuut saldo zeker enkelvoudig zijn: dit is immers een getal zonder meer, het
heeft geen zin om de afzonderlijke cijfers ervan apart te gebruiken.

Een samengesteld attribuut kan een groep, een vector of een herhaalde groep zijn:


![attr1](img/attr1.jpg)


Een groep is één enkel attribuut dat uit verschillende elementen bestaat die elk op zich een aparte zinvolle betekenis kunnen hebben. Een dergelijk attribuut zou dus eventueel in meerdere afzonderlijke attributen kunnen  opgesplitst worden. In de meeste gevallen zal het wenselijk zijn om een attribuutgroep te  splitsen. Als bij de analyse namelijk blijkt dat je een deel van een groep ooit ergens apart nodig hebt, dan is splitsing van die groep aangewezen. Attribuutwaarden achteraf samenvoegen levert immers geen problemen, terwijl deelinformatie uit een groep eenduidig isoleren vaak onmogelijk is.

In het hoger genoemde voorbeeld is voor de entiteit "houder" het attribuut "naam" een
groep, want het bevat voornaam en familienaam, die elk op zich ook betekenis kunnen
hebben. Voor vele toepassingen kan het echter zinvol zijn de voornaam en familienaam als
aparte attributen te beschouwen. Indien b.v. zowel op voornaam als op familienaam moet
kunnen gesorteerd worden, indien de volgorde van voornaam en familienaam kan wijzigen
(op lijsten b.v. familienaam eerst, maar in een persoonlijke brief de voornaam eerst, ..)

Ook voor het attribuut "adres" lijkt het zinvol om dit verder op te splitsen: indien het
postnummer van een gemeente wijzigt, moet je dit eenvoudig kunnen aanpassen: het is
dan ook wenselijk om dit apart op te slaan. Hetzelfde geldt waarschijnlijk voor de
gemeentenaam: indien sortering hierop gewenst is, moet je deze eveneens als een apart
attribuut definiëren. De rest van het attribuut adres (straat en huisnummer) als een groep
definiëren is waarschijnlijk wel zinvol. Je hebt die gegevens waarschijnlijk nooit apart
nodig, en dan is het eenvoudiger om bij opvragingen naar één attribuut te kunnen
verwijzen.

 Een vector of meerwaardig attribuut is één enkel attribuut dat een willekeurig aantal keren voorkomt binnen een bepaalde entiteit.

Voorbeeld: Indien je van een bepaalde persoon naast de persoonlijke gegevens ook de
namen van zijn/haar kinderen wil bijhouden, dan levert dit een vectorattribuut op, waarbij
het attribuut "naam van kind" dan 0, 1 of meerdere keren kan voorkomen.

Een ander voorbeeld van een meerwaardig attribuut is het bijhouden van Talen en hobby’s. Als binnen de database wordt aangenomen dat een artiest op een gegeven tijdstip verschillende talen kan spreken en een aantal hobby’s kan hebben, worden deze attributen gemodelleerd als meerwaardige attributen.

Binnen het ER-diagram wordt een meerwaardig attribuut gevisualiseerd door een dubbele ovaal.

 

Afgeleid attribuut: voor sommige attributen kun je de actuele waarde op elk moment afleiden of berekenen uit de actuele waarde van andere attributen. Zo’n attribuut noem je een afgeleid attribuut. Een typisch voorbeeld is een attribuut ‘Leeftijd’ waarvan de waarde kan worden berekend als het verschil van de huidige datum en de geboortedatum die wordt bijgehouden in een attribuut ‘Geboortedatum’. Omdat het opslaan van afgeleide data in een database een potentiele bron kan zijn van inconsistentie, moet je afgeleide attributen apart behandelen. 

Een afgeleid attribuut wordt gevisualiseerd door een ovaal in stippellijn. 

Sleutelattributen. Het kan gebeuren dat alle entiteiten door 1 attribuut of verschillende attributen samen op een unieke, irreducibele manier moeten worden geïdentificeerd. Uniciteit wil daarbij zeggen dat er geen 2 entiteiten mogen bestaan die dezelfde waarde hebben voor de beschouwde attributen. Irreducibiliteit zil zeggen dat er geen uniciteit mag gelden als men, in geval van een aantal attributen, 1 van de attributen weglaat. Een verzameling van attributen waarvoor de uniciteit- en irreducibiliteitsrestricties gelden, vormt een sleutel voor het entiteit. Deze attributen noemt men de sleutelattributen. Zo kun je bijvoorbeeld aannemen dat er geen 2 artiesten bestaan met dezelfde naam en voornaam, in welk geval naam en voornaam de sleutelattributen zijn. In dit geval is ‘Geboren’ geen sleutelattribuut want voor ‘Naam’ en ‘Voornaam’ geldt de uniciteitsrestrictie, waardoor de irreducibiliteitsrestrictie niet geldt voor Naam, Voornaam en Geboren. 

Het is een goede praktijk  om voor elke entiteit 1 sleutel te maken. Hiervoor kan het nodig zijn om een artificieel identificatorattribuut toe te voegen, dat dan op zich de sleutel is van de entiteit.

Een sleutelattribuut wordt gevisualiseerd door hun naam te onderstrepen.

Voorbeeld van attribuut visualisatie:

![attrvisual](img/attrvisual.jpg)


In een zogenaamde genormaliseerde gegevensverzameling zullen namelijk geen merwaardige attributen  voorkomen. Dergelijke informatie kan inderdaad ook op een andere manier worden bijgehouden, namelijk door nieuwe entiteiten te definiëren die op deze data aggregates zijn gebaseerd en de gepaste relaties tussen de entiteiten te voorzien. Dit zien we verder in de cursus.

### Relaties

Tussen verschillende entiteiten kunnen verbanden bestaan. Die verbanden worden relaties of
relationele verbanden genoemd. 

> Als definitie kunnen we zeggen dat een relatie een verwantschap is tussen 2 of meer al dan niet verschillende entiteiten. Men spreekt van een binaire of ternaire of n-aire (n>3) relatie. Verder wordt elke relatie gekenmerkt door een naam.

Relaties worden gevisualiseerd door een ruit (eventueel met de naam van de relatie).

Bij relaties spreken  we over  kardinaliteitsrestricties: beperkt het aantal entiteiten dat op een gegeven tijdstip maximaal kan voorkomen in een relatie ( mogelijke waarden zijn: 1 of N(meerdere)). Bij binaire relaties spreken we over een-een relatie (1-1), een-op-meerdere (1:N) relatie, meerdere-op-meerdere (M:N) relatie.

De eerste relatie is de één-één relatie, voorgesteld als volgt. In dit voorbeeld wordt elke werknemer
gekoppeld aan een foto. Geen enkele werknemer heeft meer dan één foto, en van elke werknemer
bestaat er een foto in de database.

![relatie11](img/relatie11.jpg)


Bij de één-op-N relatie wordt een occurence of voorkomen van een entiteit gekoppeld aan meerdere
occurences van  een andere entiteit. In dit voorbeeld kan elk huis meerdere inwoners hebben,
terwijl een inwoner slechts in één huis kan wonen.


![relatie1N](img/relatie1N.jpg)


Bij de N-op-M relatie worden meerdere occurences van een entiteitsklasse gekoppeld aan meerdere
occurences in een andere entiteitsklasse. In dit voorbeeld kan een student meerdere vakken hebben,
terwijl een vak kan gegeven worden aan meerdere studenten.


![relatieNM](img/relatieNM.jpg)


Men spreekt ook van een binair, ternair of n-air (n>3) relatietype.  Er kunnen meer dan 2 entiteiten betrokken zijn in de verwantschap.  Relaties kunnen net als entiteiten worden gekarakteriseerd door attributen. Dit komt voor wanneer een attribuut eigen is aan de verwantschap en niet aan 1 van de betrokken entiteiten. Een voorbeeld van een attribuut van een relatie is het attribuut dat uitdrukt voor hoeveel procent van een voltijdse betrekking een werknemer werkt bij een bepaald bedrijf. Dit percentage hoort bij de ‘werkt voor’ verwantschap tussen werknemer en bedrijf en kun je niet associeren met de werknemer (die voor verschillende bedrijen kan werken) of het bedrijf (dat doorgaans meer werknemers heeft).

Voorbeeld van een ternaire relatie type:

Een student volgt een bepaalde opleidingsactiviteit en haalt bij testen hierop een bepaald resultaat.  Hoe kan je de relatie tussen het entiteittype student voorstellen ten opzichte van het entiteittype opleidingsonderdeel?

![relatieTernair](img/relatieTernair.jpg)

Relaties worden gevisualiseerd in een ER-diagram door een ruit met de naam van de relatie. Elke betrokken entiteit wordt via een lijn verbonden met de ruit. Als er attributen bestaan voor de relatie, worden deze ook gemodelleerd door een ovaal met de naam van het attribuut, die via een lijn met de ruit van de relatie is verbonden.

Voorbeelden zijn:

![erVB](img/erVB.jpg)

In Figuur (a) wordt een binaire relatie ‘werkt’ gevisualiseerd die gedefineerd is tussen de entiteiten werknemer en bedrijf. Deze relatie heeft een attribuut procent, dat aangeeft voor hoeveel procent de werknemer werkt bij het bedrijf.

In figuur (b) visualiseren we een binaire relatie ‘is partner’ waarbij alleen de entiteit persoon betrokken is. Hiermee geven we aan dat er een verwantschap ’is partner’ bestaat tussen personen.

Figuur ( c ) is een voorbeeld van een 1 op veel relatie.

HET DIAGRAM

Soms is het ook wenselijk om een minimale cardinaliteit aan te geven. Dit wordt volgens de standaard
gedaan door de aanduiding van het mininum aantal occurences, zoals getoond in figuur 3-5. Hier wordt
aangegeven dat elke Inwoner een huis MOET hebben, terwijl een huis niet noodzakelijk inwoners moet
hebben.

![erVBx](img/erVBx.jpg)


### Wanneer relatie, wanneer attribuut?

Relaties helpen mee om de verwante entiteiten te karakteriseren en kunnen in zekere zin worden beschouwd als een speciale vorm van attributen. Het verschil tussen een attribuut en een relatie wordt dan ook enkel bepaald door het abstraheringsproces: als alle betrokken entiteiten bestaan en dus als dusdanig werden geïdentificeerd, wordt de verwantschap gemodelleerd als relatie. Als een betrokken entiteit ontbreekt, wordt de verwantschap doorgaans gemodelleerd als attribuut. Kijk eens naar de entiteit “schilderij”. Als er een entiteit “Artiest” bestaat, zoals aangegeven dan moeten we de verwantschap tussen schilderij en artiest modelleren met een relatie. Mocht bij de abstrahering worden geconcludeerd dat er geen behoefte is aan detailgegevens over artiesten en dat de entiteit ‘Artiest’ dus niet wordt beschouwd, dan kun je de verwantschap tussen schilderijen en artiesten modelleren door een “extra artiest attribuut” toe te voegen aan de entiteit “schilderij”.


## RECURSIEVE RELATIES

Ook tussen entiteiten uit dezelfde klasse kunnen relaties bestaan. Zo kan bij studenten de relatie bestaan
ZIT_IN_DEZELFDE_GROEP, en gedefinieerd als volgt:

![recursieveRelatie](img/recursieveRelatie.jpg)

## Zwakke Entiteiten

Een zwakke entiteit zijn entiteiten die niet op zichzelf kunnen bestaan, maar die voor hun bestaan afhankelijk zijn van het bestaan van andere, identificerende entiteiten.

Omdat zwakke entiteiten niet op zichzelf kunnen bestaan, kun je ze ook niet uniek identificeren zonder dat hun identificerende entiteiten bij de identificatie zijn betrokken.  De verwantschap tussen het zwakke entiteittype en de identificerende entiteit wordt door 1 of meer relatietypes gedefinieerd. De entiteit schilderij kan worden gezien als een zwakke entiteit, daar deze samenhangt aan de entiteit Artiest. Een schilderij kan immers niet bestaan tenzij iemand het heeft geschilderd. Andere voorbeelden zijn  een Medisch dossier met een identificerende entiteit patient, of profrenner en wielerploeg, of examen en student,Cursus.

Zwakke entiteiten worden gevisualiseerd door een dubbele rechthoek, hun identificerende relatietype door een dubbele ruit.

![zwakkeEntiteit](img/zwakkeEntiteit.jpg)


Zwakke entiteiten kan je niet uniek identificeren zonder hun identificerende entiteit, en kunnen dus geen sleutel hebben. Ze zullen wel sleutelattributen hebben die samen met de sleutelattributen van de identificerende identiteit voor een unieke, irreducibele identificatie van de zwakke entiteit zorgt.

## Subtypes en supertypes

Om de realiteit beter te kunnen weergeven, worden de modelleringsfaciliteiten voor entiteiten verder uitgebreid, door gemeenschappelijke eigenschappen te modelleren. Het kan voorkomen dat sommige collecties moeten worden onderverdeeld in subcollecties omdat deze belangrijk zijn voor de gebruikers of toepassingen, en apart moeten kunnen worden beschouwd. Zo kan het bijvoorbeeld nuttig zijn om bij schilderijen een expliciet onderscheid te maken op basis van het materiaal waarop geschilderd wordt (doek, hout , papier, perkament) of op basis van het materiaal waarmee geschilderd wordt (olieverf, acryl, waterverf). Kunstwerken kunnen we onderverdelen in soorten (schilderij, beeldhouwwerk, wandtapijt, juweel). Werknemers kunnen we onderverdelen op basis van hun functie (technicus, administratief, kaderlid). Om subcollecties te karakteriseren, worden aparte entiteiten aangemaakt die fungeren als subtype.  De oorspronkelijke entiteit fungeert dan als supertype voor deze subtype.


> Een subtype is een entiteit dat een subcollectie van entiteiten karakteriseert. De entiteit van de collectie waarbinnen deze subcollectie wordt beschouwd, wordt het supertype genoemd.

Een subtype erft alle attributen en verwante relaties van zijn supertype. Hiermee wordt bedoeld dat alle attributen en relaties die verwant zijn aan het supertype ook gelden en van toepassing zijn op het subtype, zonder dat we deze apart moeten kopieren naar het subtype. Een subtype kan zelf ook expliciet vermelde attributen en verwante relaties hebben. Deze gelden niet voor het supertype en noemen we daarom specifieke attributen en relaties! Zo erft het subtype Hout voor schilderijen op hout bijvoorbeeld het attribuut periode van zijn supertype schilderij. Daarnaast kan hout een specifiek attribuut houtsoort hebben.

De supertype/subtype-verwantschap wordt in een ER-diagram gevisualiseerd door een verbindingslijn met het symbool voor deelverzamelingen ‘C’, waarbij de boog van het symbool gericht is naar het subtype. (dit geeft aan dat alle entiteiten van een subtype ook entiteiten zijn van het supertype (het omgekeerde geldt niet noodzakelijk). Zo zijn bijvoorbeeld alle schilderijen kunstwerken, maar niet alle 
kunstwerken schilderijen.


## Case studies

Algemeen: de werkwijze:

1.	Identificeer de entiteiten
2.	Identificeer de zwakke entiteiten
3.	Identificeer de attributen
4.	Identificeer de relaties

### Database voor een jeugdvereniging

Beschrijving: 

Een jeugdvereniging wenst een database op te zetten, ter ondersteuning van haar ledenadministratie en werking. Daarbij moet rekening worden gehouden met de volgende aspecten. Bij de inschrijving krijgt elk lid een uniek lidnummer. Gegevens zoals naam, voornaam, adres, geslacht en geboortedatum worden geregistreerd. In het begin van het werkjaar worden de leden ingedeeld in verschillende groepen volgens leeftijdsklassen.

 Er kunnen meerdere groepen zijn voor één leeftijdsklasse. Elke groep heeft een leid(st)er. Een leid(st)er is maximaal verantwoordelijke voor één groep. De leiding vormt zelf ook een groep, die correspondeert met de hoogste leeftijdsklasse.

De leid(st)ers organiseren allerhande activiteiten voor de leden. Een dergelijke activiteit kan bestemd zijn voor één of meerdere groepen tegelijkertijd. Tevens kunnen meerdere activiteiten voor dezelfde groep worden gepland (op verschillende uren). 

Aan sommige activiteiten kunnen extra kosten verbonden zijn. Los daarvan kan het zijn dat de leden zich op voorhand voor een activiteit moeten inschrijven (en de kosten vereffenen). 

Werkwijze:

Stap 1 : Identificeer de entiteiten. Uit voorgaande tekst kunnen de volgende entiteiten worden gedistilleerd: ‘Lid’, ‘Groep’, en ‘Activiteit’. Deze types beschrijven de entiteiten waarover informatie moet worden bijgehouden.

Stap 2:  identificatie van zwakke entiteiten en hun identificerende relatietypes. Er zijn geen zwakke entiteiten.

Stap 3: Identificatie van de attributen, hun karakteristieken en restricties. De entiteit ‘lid’ heeft als enig sleutelattribuut ‘lidnummer’, verder zijn er nog de attributen ‘geboortedatum’, ‘geslacht’, ‘naam ‘en ‘voornaam’, het samengesteld attribuut ‘adres’ dat bestaat uit de componentenattributen ‘straat’, ‘nummer’ en ‘postcode’ en het afgeleid attribuut ‘leeftijd’ dat nodig is om de groep van het ‘lid’ te kunnen bepalen. De entiteit ‘groep’ heeft als enig sleutelattribuut ‘naam’. Verder is er nog een samengesteld attribuut ‘leeftijd’ met componentattributen ‘minimum’ en ‘maximum’. Het enige sleutelattribuut van de entiteit activiteit is ‘nummer’. Verder zijn er nog de attributen ‘tijdstip’,’ kost’ en ‘omschrijving’.

Stap 4: Identificatie van de relaties, hun eventuele attributen, hun karakteristieken en restricties. Er zijn 4 relatietypes die allemaal binair zijn. De relatie “lid van” wordt gebruikt om weer te geven dat groepen bestaan uit nul of meer leden en dat elk lid deel uitmaakt van precies 1 groep. De relatie ‘leider van’ wordt gebruikt om aan te geven dat elke groep precies 1 leider heeft en dat een lid maar leider kan zijn van ten hoogste 1 groep. De relatie voor wordt gebruikt om de verwantschappen tussen activiteiten en groepen aan te geven. Er kunnen nul of meer activiteiten gepland zijn voor een groep en elke activiteit is gepland voor minstens 1 groep. Verder is er nog de relatie “schrijft in” dat wordt gebruikt om weer te geven dat meerdere leden kunnen inschrijven voor een activiteit en dat een lid kan inschrijven voor diverse activiteiten. Het relatietype heeft een attribuut “betaald” waarmee wordt bijgehouden of een lid voor zijn inschrijving al heeft betaald (als er extra kosten zijn).

ER-diagram:

![jeugdvereniging](img/jeugdvereniging.jpg)

### Reservatiesysteem voor een theater

In een theaterzaal worden verschillende stukken opgevoerd (toneel, ballet, opera enzovoort). Doorgaans worden verschillende voorstellingen van een bepaald stuk opgevoerd. Voor elk stuk wordt de titel, de duur, de soort, de organisator, de uitvoerder en een uniek nummer bewaard. Van iedere voorstelling wordt de datum en het beginuur opgeslagen. Aangezien er maar één zaal is, kan op hetzelfde ogenblik maar één voorstelling worden geprogrammeerd.
De zitplaatsen in de zaal worden doorlopend genummerd en zijn ingedeeld in zones die een aparte naam hebben. De toegangsprijs is afhankelijk van de zone van de zitplaats.
De verkoop van tickets verloopt uitsluitend via reservering. De klant moet hierbij zijn naam en adres opgeven en kan dan één of meerdere zitplaatsen reserveren voor een voorstelling. Er wordt bijgehouden of voor deze reservering reeds werd betaald. 

Werkwijze

Stap 1: identificatie van de reguliere entiteiten. We kunnen 4 entiteiten onderscheiden: ‘Stuk’, ‘Klant’, ‘Zitplaats’, ‘Zone’.

Stap 2: Identificatie van de zwakke entiteiten en hun identificerende relatie. Er is 1 zwakke entiteit, namelijk ‘Voorstelling’. Een voorstelling kan immers niet bestaan zonder dat er een stuk is. 

Stap 3: Identificatie van attributen, hun karakteristieken en hun restricties. De entiteit ‘stuk’ heeft als enig sleutelattribuut stuknummer. Verder zijn er nog de attributen titel, soort, organisator, uitvoerder en duur. 

De entiteit ‘klant’ heeft als enig sleutelattribuut klantnummer. De andere attributen zijn naam en adres. In deze toepassing worden deze attributen niet meer verder opgesplitst, waardoor namen en adressen als een geheel worden gemodelleerd. Dit impliceert dat de database later bijvoorbeeld niet rechtstreeks onderzocht zal kunnen worden op postcode. Uiteraard kan de postcode wel uit het adres worden gefilterd via programmacode. Als echter vooral bekend is dat statistische informatie over de woonplaats van de klanten moet kunnen worden afgeleid uit de database, is het beter om het adres als samengesteld attribuut weer te geven zoals in de vorige casestudie. Dit illustreert het belang van een goede communicatie met de opdrachtgever. De entiteit ‘zone’ heeft het sleutelattribuut naam als enig attribuut. De entiteit zitplaats heeft als enig attribuut het sleutelattribuut plaatsnummer. Toch is het nodig om zowel zitplaats, als zone als entiteit weer te geven, want beide blijken betrokken te zijn in de definitie van aparte relatie.

Stap 4: Identificatie van de relaties, hun eventuele attributen , hun karakteristieken en hun restricties. Er zijn 3 relaties. De relatie ‘tarief’ is binair en heeft een attribuut prijs. Het geeft aan dat er bij verschillende voorstellingen tarieven worden gehanteerd voor verschillende zones. De relatie’in’ is eveneens binair en geeft aan in welke zone elke zitplaats zich bevindt en welke zitplaatsen in elke zone voorkomen. De relatie reservering is ternair en heeft een attribuut betaald voor een gegeven reservering. Met deze relatie wordt gemodelleerd dat een klant per reservering meerdere plaatsen voor verschillende voorstellingen kan reserveren.

ER-diagram:

![reservatie](img/reservatie.jpg)


## Oefeningen

### Opgave 1.Bepaal het ERD voor de volgende 

A:	opleiding		(opleidingscode, omschrijving, duur)
	afdeling			(afdelingnr, naam-afdeling)
	medewerker		(medewerkernr, naam, adres, afdelingnr)
	gevolgde opleiding	(medewerkernr, opleidingcode, datum, voltooing)

B:	kamerbestand		(kamernr, adres, plaats, huurprijs, faciliteitcode)
	faciliteiten		(faciliteitcode, kookgelegenheid, douche/bad, aantal kamers)
	huurcontract		(studentnr, kamernr, contractduur, datum contractafloop)
	student			(studentnr, naam, studentadres, studentplaats)	


### Opgave 2: ERD

Geef de verschillende relaties weer tussen studenten, klassen en lectoren.


### Opgave 3: ERD en occurences

Gegeven zijn de volgende entiteittypen:
leverancier	(levnr, levnaam, woonplaats)
artikel		(artnr, artnaam, kleur)
klant		(klnr, klnaam, woonplaats)
levering		(levnr, artnr, klnr, hoeveelheid)

Leverancier
Levnr	levnaam	Woonplaats
L1	Smeets	Antwerpen
L2	Eggen	Ekeren
L3	Wagemans	Antwerpen
L4	Van Holle	Utrecht
L5	Schavey	Aken

Artikel
Artnr	artnaam	Kleur
a1	stoel	Bruin
a2	tafel	Wit
a3	stoel	Rood
a4	bureau	Groen
a5	kapstok	Rood

Klant
Klnr	klnaam	Woonplaats
k1	Aerts	Geel
k2	Beerts	Zutendaal
k3	Claes	Hemiksem
k4	Decat	Ronse
k5	Egmont	Hemiksem
k6	Faes	Antwerpen

Levering
Levnr	artnr	klnr	Hoeveelheid
L1	a1	k1	10
L1	a1	k3	20
L2	a4	k1	10
L2	a4	k2	20
L2	a4	k3	10
L2	a4	k4	15
L2	a4	k5	15
L2	a4	k6	5
L3	a3	k2	5
L3	a4	k4	10
L4	a2	k4	5
L4	a1	k3	10
L4	a2	k3	15
L4	a3	k3	5
L4	a4	k3	5
L4	a5	k3	10
L4	a2	k4	20
L5	a3	k6	20

a.	Geef het ERD
b.	Bepaal de levnrs voor die leveranciers die aan klant k6 een rood artikel leveren
c.	Bepaal de artnrs die aan een klant in Hemiksem geleverd worden
d.	Bepaal de artnrs die aan een klant in Hemiksem door een leverancier in Ekeren geleverd worden
e.	Bepaal de namen van de klanten waaraan artikelen worden geleverd door ten minste één leverancier uit de woonplaats zelf
f.	Bepaal de klnrs van die klanten waaraan door alle leveranciers die een rood artikel leveren (aan wie dan ook), wordt geleverd
g.	Bepaal de artnrs die aan alle klanten in Hemiksem worden geleverd

### Opgave 4 

Een softwarefirma wil een database opzetten als hulp bij het controleren en corrigeren van fouten die ontdekt worden in haar softwareproducten. Aan elk softwareproduct wordt een uniek productnummer toegekend en een beschrijving toegevoegd. Van een product worden verschillende versies uitgebracht, die per product een versienummer krijgen. Daarnaast wordt ook de datum waarop de versie werd uitgebracht bewaard. Een versie van een product kan zowel door externe als door interne gebruikers (bijvoorbeeld programmeurs en systeemtesters) worden gebruikt. Interne gebruikers mogen alle versies van alle producten gebruiken zonder voorafgaande aanvraag. Externen dienen de versie van het product eerst aan te kopen. Bij de verkoop wordt voor elk verkocht exemplaar een uniek registratienummer –dat geldt voor één of meerdere externe gebruikers– en de registratiedatum vastgelegd.
Wanneer een gebruiker een probleem constateert, kan hij of zij hierover een probleemrapport opstellen (en overmaken aan de onderhoudsafdeling). Zo’n rapport kan zowel door een interne als door een externe gebruiker worden opgemaakt en vermeldt naast een verwijzing naar het product en de versie, ook de datum en een omschrijving van het probleem. Aan elk rapport wordt verder een uniek rapportnummer, een prioriteit en een status (aan te passen door de onderhoudsafdeling) toegekend. Aangezien externe gebruikers enkel een rapport mogen sturen in verband met de versies waarvoor zij geregistreerd zijn, dienen zij steeds hun registratienummer te vermelden.
Interne gebruikers dienen enkel hun werknemernummer op te geven, terwijl externen geïdentificeerd worden via de combinatie van hun naam en de naam van hun bedrijf. Van alle gebruikers wordt tenslotte ook nog het telefoonnummer, adres en e-mail adres bijgehouden (indien bekend). 



### Opgave 5

Ontwerp een ER-diagram voor de volgende opdracht. Een sportvereniging telt een aantal leden (spelers) waarvan de naam, adres, geboortejaar, geslacht en jaar van toetreding geregistreerd zijn. De vereniging telt twee spelerscategorieën: recreatiespelers en wedstrijdspelers. Wedstrijdspelers spelen in teamverband tegen spelers van andere verenigingen/clubs. Elke speler krijgt bij toetreding een uniek spelersnummer. Elke wedstrijdspeler is (verplicht) ook bij de bond geregistreerd en heeft aldus eveneens een uniek bondsnummer. 

Elke wedstrijdspeler is ingedeeld bij één team, afhankelijk van zijn/haar leeftijd en sekse. Elk team heeft een unieke teamcode. Voor een bepaalde leeftijdklasse (nieuwelingen, juniores, …) en sekse kunnen er meerdere teams zijn. Elk team heeft een vaste trainer, die ook lid is van de vereniging. Een lid kan maar trainer zijn van één team. De trainingen verlopen volgens een vast wekelijks trainingrooster, dat verschilt van team tot team. Hierin zijn voor elk van de wekelijkse trainingen vastgelegd: de dag van de week, de tijd, de duur en de sportzaal waar de training doorgaat. Van eenzelfde team kunnen er nooit meerdere trainingen op dezelfde dag plaatsvinden. Van alle beschikbare zalen worden de volgende gegevens bijgehouden: de naam (uniek), het adres en het telefoonnummer. Geregeld spelen teams wedstrijden tegen teams van andere verenigingen. Een wedstrijd, gekenmerkt door een uniek wedstrijdnummer, gaat door op een bepaalde datum en tijdstip in de zaal die daarvoor wordt gereserveerd. Bij elke wedstrijd is een scheidsrechter aanwezig, die eveneens lid is van de vereniging (maar niet behoort tot het team dat de wedstrijd speelt). De bond kan naar aanleiding van een gespeelde wedstrijd één of meerdere boetes uitdelen aan spelers of aan de vereniging zelf. Bij elke uitgedeelde boete wordt door de bond een toelichting verstrekt en het te betalen bedrag bekend gemaakt. 


### Opgave 6

Wat zijn zwakke entiteittypes? Waarom zijn deze nodig? 





