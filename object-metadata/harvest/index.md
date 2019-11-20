---
layout: default
title: Harvest
nav_order: 2
parent: Object metadata
redirect_from: "/oai"
---

# Object metadata harvesting API
The Rijksmuseum offers an API featuring the [OAI-PMH protocol](https://www.openarchives.org/OAI/openarchivesprotocol.html) (Open Archives Initiative Protocol for Metadata Harvesting). The OAI-PMH standard is widely used in the cultural heritage sector to support harvesting metadata of collections. The Rijksmuseum OAI-PMH API provides access to more than 600,000 descriptions of objects (metadata) and digital images from the Rijksmuseum collection. An [example harvester](https://github.com/Q42/SimpleOAIHarvester) is available on GitHub to help you get started quickly.


## Access to the OAI-PMH API
To access the data, you will first need to obtain an API key. You can do this via the advanced settings of your [Rijksstudio account](https://www.rijksmuseum.nl/en/rijksstudio/my/profile). You will be given a key instantly upon request.


## Metadata formats
The datasets are provided via a simple XML web service. The following metadata formats are available:

- **lido** Lightweight Information Describing Objects [documentation](http://lido-schema.org/)
- **edm_dc** Europeana Data Model [documentation](https://pro.europeana.eu/edm-documentation)
- **dc** Dublin Core [documentation](https://www.dublincore.org/specifications/dublin-core/)

The [conversion_oai_formats](https://github.com/Rijksmuseum/conversion_oai_formats) repository can provide insights in how Rijksmuseum data is mapped to these metadata formats.


## Sets of objects
The following sets of objects can be retrieved using the ListRecords and ListIdentifiers verbs:

- **subject:EntirePublicDomainSet** All public domain objects.
- **subject:PublicDomainImages** All public domain objects with an image.
- **subject:OnDisplay** All objects currently on display in the Rijksmuseum.
- **type:prints** All the works on paper.

Omitting the set parameter will default to the set of all available objects.


## Verbs
A verb is used to indicate what data to retrieve. The following verbs can be used:

- [ListRecords](#listrecords) retrieve an entire set of data.
- [GetRecord](#getrecord) retrieve a specific record.
- [ListMetadataFormats](#listmetadataformats) retrieve the available metadata formats.
- [ListSets](#listsets) retrieve the available sets of objects.
- [ListIdentifiers](#listidentifiers) retrieve headers with identifiers of objects.

Every request to the OAI-PMH API must be accompanied by your API key and a verb parameter:

```http
http://www.rijksmuseum.nl/api/oai/[api-key]?verb=[verb]
```


## ListRecords
`GET /oai/[api-key]?verb=ListRecords` retrieves an entire set of metadata.

| Parameter        | Format                                | Default               | Notes                                                                                                                             |
|:-----------------|:--------------------------------------|:----------------------|:----------------------------------------------------------------------------------------------------------------------------------|
| `set`            | `a-z|0-9`                             | all objects           | The [set of objects](#sets-of-objects) to harvest.                                                                                |
| `metadataPrefix` | `dc` / `edm_dc` / `lido`              |                       | Required: the [metadata format](#metadata-formats) of the result.                                                                 |
| `resumptionToken`| `a-z|0-9`                             |                       | The flow control token returned by a previous ListRecords request.                                                                |
| `from`           | `YYYY-MM-DD` / `YYYY-MM-DDThh:mm:ssZ` | earliest datestamp    | Parameter for selective harvesting, based on a specified date range. Specifies a bound interpreted as "greater than or equal to". |
| `until`          | `YYYY-MM-DD` / `YYYY-MM-DDThh:mm:ssZ` | most recent datestamp | Parameter for selective harvesting, based on a specified date range. Specifies a bound interpreted as "less than or equal to".    |


### Example request ListRecords
```http
https://www.rijksmuseum.nl/api/oai/[api-key]?verb=ListRecords&set=subject:EntirePublicDomainSet&metadataPrefix=dc
```
This request will return the first 20 records in the dataset of all public domain objects. A `resumptionToken` element is included at the end of the response, which can be used as a parameter to request the next 20 records in the database. Resumption tokens expire over time, which is why it is recommended to use a [script to harvest data](https://github.com/Q42/SimpleOAIHarvester).

### Example response ListRecords
Each object description is included in the XML response as a record. The header includes an identifier and date stamp. The metadata includes fields based on the metadata format definitions, in this case [Dublin Core](http://dublincore.org):

```xml
<ListRecords>
<record>
  <header>
    <identifier>oai:rijksmuseum.nl:SK-A-3580</identifier>
    <datestamp>2019-09-04T11:13:53Z</datestamp>
  </header>
  <metadata>
    <oai_dc:dc>
      <dc:identifier>http://hdl.handle.net/10934/RM0001.COLLECT.6274</dc:identifier>
      <dc:identifier>SK-A-3580</dc:identifier>
      <dc:title>De Singelbrug bij de Paleisstraat in Amsterdam</dc:title>
      <dc:creator>Breitner, George Hendrik</dc:creator>
      <dc:subject>Paleisstraat</dc:subject>
      <dc:subject>Singel</dc:subject>
      <dc:description>Breitner maakte vaak zelf foto’s als voorbereiding op zijn schilderijen. Ook van dit schilderij is een aantal van zulke voorstudies bekend. De manier waarop de vrouw recht op ons af loopt en de afsnijding van het beeld doen heel fotografisch aan. Aanvankelijk was hier een dienstmeid geschilderd, maar na een negatieve kritiek vond de kunsthandel die zijn schilderijen verkocht het maar beter dat Breitner er een dame van maakte.</dc:description>
      <dc:date>1896</dc:date>
      <dc:date>1898</dc:date>
      <dc:type>schilderij</dc:type>
      <dc:format>olieverf</dc:format>
      <dc:format>doek</dc:format>
      <dc:language>nl</dc:language>
      <dc:publisher>Rijksmuseum</dc:publisher>
      <dc:rights>http://creativecommons.org/publicdomain/mark/1.0/</dc:rights>
      <dc:coverage>Amsterdam</dc:coverage>
    </oai_dc:dc>
  </metadata>
</record>
<!-- more results... -->
<resumptionToken completeListSize="581445">MXxkY3wyMDE4LTA3LTEyVDEzOjA5OjE2fHN1YmplY3Q6RW</resumptionToken>
</ListRecords>
```


## GetRecord
`GET /oai/[api-key]?verb=GetRecord` retrieves an individual metadata record.

| Parameter        | Format                   | Default   | Notes                                                                              |
|:-----------------|:-------------------------|:----------|:-----------------------------------------------------------------------------------|
| `identifier`     | `a-z|0-9`                |           | Required: specifies the identifier of the object (e.g. oai:rijksmuseum.nl:sk-c-5). |
| `metadataPrefix` | `dc` / `edm_dc` / `lido` |           | Required: the [metadata format](#metadata-formats) of the result.                  |

### Example request GetRecord
```http
https://www.rijksmuseum.nl/api/oai/[api-key]?verb=GetRecord&metadataPrefix=dc&identifier=oai:rijksmuseum.nl:sk-c-5
```
This request will return the object description of the Nightwatch (SK-C-5).

#### Example response GetRecord
An object description is included in the XML response as a record. The header includes an identifier and date stamp. The metadata includes fields based on the metadata format definitions, in this case [Dublin Core](http://dublincore.org):

```xml
<GetRecord>
<record>
  <header>
    <identifier>oai:rijksmuseum.nl:sk-c-5</identifier>
    <datestamp>2019-07-31T05:12:59Z</datestamp>
  </header>
  <metadata>
    <record>
      <header>
        <identifier>oai:rijksmuseum.nl:SK-C-5</identifier>
        <datestamp>2019-07-31T07:12:59Z</datestamp>
      </header>
      <metadata>
        <oai_dc:dc>
          <dc:identifier>http://hdl.handle.net/10934/RM0001.COLLECT.5216</dc:identifier>
          <dc:identifier>SK-C-5</dc:identifier>
          <dc:title>De Nachtwacht</dc:title>
          <dc:creator>Rijn, Rembrandt van</dc:creator>
          <dc:subject>Amsterdam</dc:subject>
          <dc:subject>Banninck Cocq, Frans</dc:subject>
          <dc:subject>Ruytenburch, Willem van</dc:subject>
          <dc:subject>Visscher Cornelisen, Jan</dc:subject>
          <dc:subject>Kemp, Rombout</dc:subject>
          <dc:subject>Engelen, Reijnier Janszn</dc:subject>
          <dc:subject>Bolhamer, Barent Harmansen</dc:subject>
          <dc:subject>Keijser, Jan Adriaensen</dc:subject>
          <dc:subject>Willemsen, Elbert</dc:subject>
          <dc:subject>Leijdeckers, Jan Claesen</dc:subject>
          <dc:subject>Ockersen, Jan</dc:subject>
          <dc:subject>Bronchorst, Jan Pietersen</dc:subject>
          <dc:subject>Wormskerck, Harman Jacobsen</dc:subject>
          <dc:subject>Roy, Jacob Dircksen de</dc:subject>
          <dc:subject>Heede, Jan van der</dc:subject>
          <dc:description>Rembrandts beroemdste en grootste schilderij werd gemaakt voor de Kloveniersdoelen. Dit was een van de drie hoofdkwartieren van de Amsterdamse schutterij, de burgerwacht van de stad. Rembrandt was de eerste die op een schuttersstuk alle figuren in actie weergaf. De kapitein, in het zwart, geeft zijn luitenant opdracht dat de compagnie moet gaan marcheren. De schutters stellen zich op. Met behulp van licht vestigde Rembrandt de aandacht op belangrijke details, zoals het handgebaar van de kapitein en het kleine meisje op de voorgrond. Zij is de mascotte van de schutters. De naam Nachtwacht is pas veel later ontstaan, toen men dacht dat het om een nachtelijk tafereel ging.</dc:description>
          <dc:date>1642</dc:date>
          <dc:type>schilderij</dc:type>
          <dc:format>doek</dc:format>
          <dc:format>olieverf</dc:format>
          <dc:language>nl</dc:language>
          <dc:publisher>Rijksmuseum</dc:publisher>
          <dc:rights>http://creativecommons.org/publicdomain/mark/1.0/</dc:rights>
          <dc:coverage>Amsterdam</dc:coverage>
        </oai_dc:dc>
      </metadata>
    </record>
  </metadata>
</record>
</GetRecord>
```


## ListMetadataFormats
`GET /oai/[api-key]?verb=ListMetadataFormats` retrieves a list of available metadata formats.

### Example request ListMetadataFormats
```
https://www.rijksmuseum.nl/api/oai/[api-key]?verb=ListMetadataFormats
```
This request will return a list of available metadata formats.

### Example response ListMetadataFormats
Each metadata format element includes the prefix that can be used as a parameter in other requests, the schema and the name space.

```xml
<ListMetadataFormats>
  <metadataFormat>
    <metadataPrefix>lido</metadataPrefix>
    <schema>http://www.lido-schema.org/schema/v1.0/lido-v1.0.xsd</schema>
    <metadataNamespace>http://www.openarchives.org/OAI/2.0/</metadataNamespace>
  </metadataFormat>
  <metadataFormat>
    <metadataPrefix>dc</metadataPrefix>
    <schema>http://www.openarchives.org/OAI/2.0/oai_dc.xsd</schema>
    <metadataNamespace>http://www.openarchives.org/OAI/2.0/</metadataNamespace>
  </metadataFormat>
  <metadataFormat>
    <metadataPrefix>edm_dc</metadataPrefix>
    <schema>http://www.europeana.eu/schemas/edm/EDM.xsd</schema>
    <metadataNamespace>http://www.openarchives.org/OAI/2.0/</metadataNamespace>
  </metadataFormat>
  <!-- more results... -->
</ListMetadataFormats>
```


## ListSets
`GET /oai/[api-key]?verb=ListSets` retrieves the available sets of objects.

### Example request ListSets
```http
https://www.rijksmuseum.nl/api/oai/[api-key]?verb=ListSets
```
This request will return a list of available sets of objects.

### Example response ListSets
Each set includes a descriptive name and a set identifier, that can be used as a parameter in other requests.

```xml
<ListSets>
  <set>
    <setSpec>subject:EntirePublicDomainSet</setSpec>
    <setName>EntirePublicDomainSet</setName>
  </set>
  <set>
    <setSpec>subject:PublicDomainImages</setSpec>
    <setName>PublicDomainImages</setName>
  <set>
    <setSpec>type:prints</setSpec>
    <setName>Prints</setName>
  </set>
  <set>
    <setSpec>type:fashion</setSpec>
    <setName>Fashion</setName>
  </set>
  <!-- more results... -->
</ListSets>
```


## ListIdentifiers
`GET /oai/[api-key]?verb=ListIdentifiers` retrieves headers with identifiers of objects. This verb is an abbreviated form of ListRecords, retrieving only headers rather than records.

| Parameter        | Format                                | Default               | Notes                                                                                                                             |
|:-----------------|:--------------------------------------|:----------------------|:----------------------------------------------------------------------------------------------------------------------------------|
| `set`            | `a-z|0-9`                             | all objects           | The [set of objects](#sets-of-objects) to harvest.                                                                                |
| `metadataPrefix` | `dc` / `edm_dc` / `lido`              |                       | Required: the [metadata format](#metadata-formats) of the result.                                                                 |
| `resumptionToken`| `a-z|0-9`                             |                       | The flow control token returned by a previous ListRecords request.                                                                |
| `from`           | `YYYY-MM-DD` / `YYYY-MM-DDThh:mm:ssZ` | earliest datestamp    | Parameter for selective harvesting, based on a specified date range. Specifies a bound interpreted as "greater than or equal to". |
| `until`          | `YYYY-MM-DD` / `YYYY-MM-DDThh:mm:ssZ` | most recent datestamp | Parameter for selective harvesting, based on a specified date range. Specifies a bound interpreted as "less than or equal to".    |

### Example request ListIdentifiers
```http
https://www.rijksmuseum.nl/api/oai/[api-key]?verb=ListIdentifiers&set=subject:EntirePublicDomainSet&metadataPrefix=dc
```
This request will return the first 20 headers in the dataset of all public domain objects. A `resumptionToken` element is included at the end, which can be used as parameter to return the next headers in the dataset. Resumption tokens expire over time, which is why it is recommended to use a [script to harvest data](https://github.com/Q42/SimpleOAIHarvester).

### Example response ListIdentifiers
Each header includes the identifier of the object and a date stamp. A date stamp indicates when a record was created, deleted, or modified.

```xml
<ListIdentifiers>
  <header>
    <identifier>BK-1975-81</identifier>
    <datestamp>2017-07-31T19:34:40Z</datestamp>
  </header>
  <header>
    <identifier>NG-NM-7687</identifier>
    <datestamp>2017-09-21T18:48:05Z</datestamp>
  </header>
  <!-- more results... -->
  <resumptionToken completeListSize="540886">MXxvYWlfZGN8MjAxOC0wMy0xNFQxMzo</resumptionToken>
</ListIdentifiers>
```
