### De OAI API Collectie
De Rijksmuseum API Collectie is een set van ruim 111.000 objectenbeschrijvingen (metadata) en digitale beelden uit de collectie van het Rijksmuseum. De kunstwerken en gebruiksvoorwerpen in de set dateren van de oudheid tot de late negentiende eeuw en geven een goed beeld van de rijkheid, diversiteit en schoonheid van ons Nederlands (en internationaal) erfgoed. Helaas kunnen wij, in verband met auteursrechtelijke beperkingen, nog geen werken uit de twintigste en eenentwintigste Eeuw beschikbaar stellen.  

###OAI API
Vraag een OAI API key aan. Dat kan je doen bij bij je geavanceerde instellingen in je Rijksstudio account (www.rijksmuseum.nl/rijksstudio). Geef hier aan of je de API of de OAI API wilt gebruiken. Voor de OAI API ontvang je nog een bevestiging van de activatie. Dit kan tot 3 werkdagen duren.

### De OAI API
De datasets worden aangeboden via een eenvoudige XML web service. Deze is gebaseerd op het OAI/PMH protocol.

De url van de Rijksmuseum OAI API is [http://www.rijksmuseum.nl/api/oai](http://www.rijksmuseum.nl/api/oai).

In het kort werkt het als volgt:

Ieder request moet worden voorzien van de OAI API key. Deze wordt meegegeven in de parameter apikey.

http://www.rijksmuseum.nl/api/oai2/[JOUW_KEY]/

Met de parameter verb kan de OAI API ‘bevraagd worden’ om de data op te halen. Met onderstaande verbs kan je alle data ophalen:

**ListRecords:** vraagt de volledige set aan data op.

Er moet naast het verb ook een set of een resumptiontoken worden meegegeven.

[http://www.rijksmuseum.nl/api/oai2/[JOUW_KEY]/?verb=ListRecords&set=collectie\_online&metadataPrefix=oai\_dc](http://www.rijksmuseum.nl/api/oai2/[JOUW_KEY]/?verb=ListRecords&set=collectie\_online&metadataPrefix=oai\_dc)

Dit geeft de eerste 100 records van de dataset collectie_online terug. Aan het einde staat een element resumptiontoken. Wanneer deze wordt meegegeven worden de volgende 100 records van de dataset terug gegeven.

http://www.rijksmuseum.nl/api/oai2/[JOUW_KEY]/?verb=ListRecords&resumptiontoken=1231-nssdfs2qle-2324

**GetRecord:** vraagt een specfiek record op.

Er moet naast het verb ook een identifier worden meegegeven.

[http://www.rijksmuseum.nl/api/oai2/[JOUW_KEY]/?verb=GetRecord&identifier=oai:rijksmuseum.nl/collection:COLLECT.5216&metadataPrefix=oai\_dc](http://www.rijksmuseum.nl/api/oai2/[JOUW_KEY]/?verb=GetRecord&identifier=oai:rijksmuseum.nl/collection:COLLECT.5216&metadataPrefix=oai\_dc)

Om snel te kunnen starten hebben we een [voorbeeld harvester beschikbaar gesteld op GitHub](https://github.com/Q42/SimpleOAIHarvester).

### Objectbeschrijving

Iedere objectbeschrijving is in het XML bestand opgenomen als een record. De velddefinities van de records zijn gebaseerd op de Dublin Core velddefinities. Meer informatie over dit XML formaat kun je vinden op [www.dublincore.org](http://www.dublincore.org).

Een voorbeeld van een objectbeschrijving van het Rijksmuseum vindt je hier: [De Nachtwacht (SK-C-5)](http://www.rijksmuseum.nl/Modules/Rijksmuseum.Collection.Api/example/sk-c-5.xml).

Wat voor gegevens kun je in onze metadata verwachten?

Wij leveren de volgende velden per object:

header:
    Identfier: een identifier voor iede object
    Datestamp: datum waarop het object voor het laatst aangepast is.

Metadata:

**Dc:identifier**
Ieder object heeft een objectnummer dat wij aan een object toekennen. Dit objectnummer is belangrijk om objecten terug te vinden. Voorbeeld objectnummer: SK-C-5. Incidenteel veranderen objectnummers in het Rijksmuseum.Ieder object heeft tevens een tweede identifier die de naam van de database bevat waar de metadata uit komt en het recordnummer. De combinatie van deze twee gegevens maakt deze identifier uniek en onveranderlijk. Voorbeeld: COLLECT.5216.

**Dc:language**
Al onze objectbeschrijvingen zijn in het Nederlands. De standaardwaarde van dit veld is 'Dutch'.

**Dc:publisher**
Het Rijksmuseum is uitgever van deze bron. De waarde van dit veld is Rijksmuseum.

**Dc: rights**
De metadata en het beeldmateriaal worden onder een  CC0 licentie beschikbaar gesteld.

**Dc: date**
Datering van de bron. Wij dateren onze bronnen met een begin- en einddatum. Als beide data gelijk zijn, dan is het een nauwkeurige datering. Zoals in het geval van de Nachtwacht: 1642 – 1642. Als we de datering niet exact vast hebben kunnen stellen dan verschillen de begin en einddatum. Er zijn ook bronnen die helemaal niet gedateerd konden worden. In dat geval ontbreekt het veld dc:date.

**Dc:description**
Beschrijving van het object.

**Dc:format**
  Wij leveren twee verschillende typen dc:format velden uit. In de eerste twee velden zijn de verwijzingen naar het beeldmateriaal en de objectbeschrijving op onze website opgenomen.
  De eerste verwijzing, http://www.rijksmuseum.nl/assetimage2.jsp?id=SK-A-4878, is de verwijzing naar het beeldmateriaal.
  De tweede verwijzing, http://www.rijksmuseum.nl/collectie/zoeken/asset.jsp?id=SK-A-4878, gaat naar de detailpagina.

In de daaropvolgende format velden worden de afmetingen, materiaal en techniek van een object vastgelegd. In de eerste velden zijn de afmetingen voor het gehele object of per onderdeel Bij complexe voorwerpen (bijvoorbeeld een kast of interieur) kan er een lange lijst met meetgegevens geleverd worden. De meeste schilderijen hebben slechts een hoogte en breedte.Materiaal en techniek zijn als volgt gespecificeerd:
<dc:format>materiaal: papier</dc:format>
<dc:format>materiaal: dekverf</dc:format>
<dc:format>techniek: graveren (drukprocédé)</dc:format>
<dc:format>techniek: etsen</dc:format>
<dc:format>techniek: witte dekverf</dc:format>
<dc:format>techniek: penseel in blauw</dc:format>

**Dc:creator**
In dit veld wordt vastgelegd welke vervaardigers in welke rollen bijgedragen hebben aan het object. De rol van de vervaardiger staat vooraan. Na de dubbele punt volgt de naam van de vervaardiger. Dit kan een persoon maar bijvoorbeeld ook een fabriek zijn.Voorbeelden:
<dc:creator>prentmaker: Coornhert, Dirck Volckertsz</dc:creator>
<dc:creator>naar ontwerp van: Heemskerck, Maarten van</dc:creator>
<dc:creator>uitgever: Cock, Hieronymus</dc:creator>

**dc:title**
Objecten kunnen bekend zijn onder verschillende titels. Met de tag dc:title worden alle titels geleverd. De eerste titel is de huidige titel. De overige titels zijn voormalige titels. De status van de titel staat tussen haakjes achter de titel vermeld.De huidige titel van de Nachtwacht is: Officieren en andere schutters van wijk II in Amsterdam onder leiding van kapitein Frans Banninck Cocq en luitenant Willem van Ruytenburch, bekend als de ‘Nachtwacht’In het verleden werd dit schilderij als volgt betiteld: Het korporaalschap van kapitein Frans Banninck Cocq en luitenant Willem van Ruytenburch, bekend als de ‘Nachtwacht’

**Dc:type**
Type object. Dit veld is hiërarchisch ingevoerd. In onderstaand voorbeeld heb je te maken met een ‘historieprent’, behorende tot het type objecten ‘prent’
<dc:type>prent</dc:type>
<dc:type>historieprent</dc:type>

**Dc:subject**
In dit veld leggen wij personen, plaatsen en onderwerpen vast die op het kunstwerk zijn afgebeeld. Op dit moment hebben wij vooral historische figuren en plaatsen geregistreerd.
In het subjectveld worden tevens Iconclass codes meegegeven. Dit is een veel gebruikt classificatiesysteem voor ontsluiting van kunstwerken. Maar informatie: http://www.iconclass.org/

**Dc:coverage**
In dit veld wordt de plaats van productie en de periode van productie vastgelegd. De periode van productie is altijd per kwart eeuw vastgelegd: eerste kwart 16e eeuw, tweede kwart 16e eeuw, derde kwart 16e eeuw, vierde kwart 16e eeuw.

**Dc: contributor**
In dit veld hebben wij vastgelegd wie (of welke organisatie) bijgedragen heeft aan verwerving van een object. Dit is onze creditline waarmee wij onze schenkers danken voor hun bijdrage.

### Beeldmateriaal
Het beeldmateriaal van het Rijksmuseum is beschikbaar in JPEG formaat. De afbeeldingen zijn opgeslagen op 300 dpi. De bestanden zijn (gemiddeld) 2 tot 5 mb groot. De afbeeldingen zijn gecontroleerd opgenomen en opgeslagen op 300 dpi. De bestanden zijn (gemiddeld) 2 tot 5 mb groot. De afbeeldingen zijn gecontroleerd opgenomen en kleurecht.

Je kunt afbeeldingen downloaden, maar wij raden je aan (als dat mogelijk is) om een verwijzing naar het beeldmateriaal op onze webserver te maken. Daar is altijd het beste en meest actuele beeldmateriaal beschikbaar. Voor publicaties en andere drukvormen hanteert het Rijksmuseum andere kwaliteitsstandaarden en bestandsformaten. Mocht je ons beeldmateriaal voor dergelijke toepassingen willen gebruiken, maak dan gebruik van het formulier op de pagina [Beeld aanvragen](/nl/beeld-aanvragen).

In de metadata wordt de url naar de afbeelding van het object meegegeven. Dit is altijd de url van het grootte beeld binnen 2500x2500 pixels. Aan deze url kan een parameter worden meegegeven om het beeld te schalen en verkleinen naar 100x100 of 200x200.

Volledige afbeelding Nachtwacht: http://www.rijksmuseum.nl/media/assets/SK-C-5

Nachtwacht binnen 100x100: http://www.rijksmuseum.nl/media/assets/SK-C-5&100x100

Nachtwacht binnen 200x200: http://www.rijksmuseum.nl/media/assets/SK-C-5&200x200

Voor andere groottes raden we aan het beeld zelf te schalen.
