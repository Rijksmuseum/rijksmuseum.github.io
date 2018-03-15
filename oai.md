---
layout: default
---

For more information about the Rijksmuseum API's, please read [www.rijksmuseum.nl/en/api](https://www.rijksmuseum.nl/en/api).

The use of the Rijksmuseum API have these [terms and conditions](https://www.rijksmuseum.nl/en/api/terms-and-conditions-of-use).

Issues regarding this API can be discussed in the [oai-issues repository](https://github.com/Rijksmuseum/oai-issues/).

## The Rijksmuseum OAI-PMH API
The Rijksmuseum offers an API featuring the [OAI-PMH protocol](https://www.openarchives.org/OAI/openarchivesprotocol.html) (Open Archives Initiative Protocol for Metadata Harvesting). In the cultural heritage sector, OAI-PMH is a standard that is used to harvest metadata. The Rijksmuseum OAI-PMH API provides access to more than 600,000 descriptions of objects (metadata) and digital images from the Rijksmuseum collection. An [example harvester](https://github.com/Q42/SimpleOAIHarvester) is available on GitHub to help you get started quickly.

## Access to the OAI-PMH API
To access the data, you will first need to request an API key. You can do this via the advanced settings of your [Rijksstudio account](https://www.rijksmuseum.nl/en/rijksstudio/my/profile). You will be given a key immediately. Every request to the OAI-PMH API must be accompanied by this key:

http://www.rijksmuseum.nl/api/oai/[API_KEY]

## Documentation
Below you find the documentation for the Rijksmuseum OAI-PMH API.

### Verbs
A verb is used to indicate what data to retrieve. The following verbs can be used:

- **ListRecords:** retrieve an entire set of data.
- **GetRecord:** retrieve a specific record.
- **ListMetadataFormats:** retrieve the available metadata formats.
- **ListSets:** retrieve the available sets of objects.
- **ListIdentifiers:** retrieve headers with identifiers of objects.

Every request to the OAI-PMH API must be accompanied by a verb parameter:

http://www.rijksmuseum.nl/api/oai/[API_KEY]?verb=[VERB]

### Example request
The following request will fetch all of the public data of The Nightwatch, in the Dublin Core format:

```
https://www.rijksmuseum.nl/api/oai/[API_KEY]?verb=GetRecord&metadataPrefix=oai_dc&identifier=oai:rijksmuseum.nl:sk-c-5
```

### Metadata formats
The datasets are provided via a simple XML web service. The following metadata formats are available:

- **oai_dc** [Dublin Core](http://dublincore.org)
- **europeana_edm** [Europeana Data Model](https://pro.europeana.eu/resources/standardization-tools/edm-documentation)
- **lido** [Lightweight Information Describing Objects](http://lido-schema.org/)

The repository [conversion_oai_formats](https://github.com/Rijksmuseum/conversion_oai_formats) can provide insights in how Rijksmuseum data is mapped to these metadata formats.

### Sets of objects
The following sets of objects can be retrieved using the ListRecords and ListIdentifiers verbs:

- **subject:EntirePublicDomainSet** All public domain objects.
- **subject:PublicDomainImages** All public domain objects with an image.
- **subject:OnDisplay** All objects currently on display in the Rijksmuseum.
- **type:prints** All the works on paper.

-----------------------------------------

## ListRecords
`GET /oai/[API_KEY]?verb=ListRecords` retrieves an entire set of metadata.

<table>
  <thead>
    <tr>
      <th>Parameter</th>
      <th>Format</th>
      <th>Default</th>
      <th>Notes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>set</code></td>
      <td><code>a-z|0-9|:</code></td>
      <td>all objects</td>
      <td>The set of objects to harvest.</td>
    </tr>
    <tr>
      <td><code>metadataPrefix</code></td>
      <td><code>oai_dc</code> / <code>europeana_edm</code> / <code>lido</code></td>
      <td></td>
      <td>Required: the metadata format of the result.</td>
    </tr>
    <tr>
      <td><code>resumptionToken</code></td>
      <td><code>a-z|0-9</code></td>
      <td></td>
      <td>The flow control token returned by a previous ListRecords request.</td>
    </tr>
  </tbody>
</table>


### Request
```
https://www.rijksmuseum.nl/api/oai/[API_KEY]?verb=ListRecords&set=subject:EntirePublicDomainSet&metadataPrefix=oai_dc
```

This request will return the first 100 records in the dataset of all public domain objects. A `resumptionToken` element is included at the end, which can be used to return the next 100 records in the dataset:

```
https://www.rijksmuseum.nl/api/oai/[API_KEY]?verb=ListRecords&set=subject:EntirePublicDomainSet&metadataPrefix=oai_dc&resumptionToken=MXxvYWlfZGN8MjAxOC0wMy0xNFQxMzo0MToyMnxzdWJqZWN0OkVudGlyZVB1YmxpY0RvbWFpblNldHwyMDE2LTAzLTEwVDEwOjAxOjA5fERYRjFaWEo1UVc1a1JtVjBZMmdCQUFBQUFBUG1YMWNXV2xwNlNFVm1ZMWxVZWpJNFIyZzNXVUZSTlVzdFVRPT18MjA=
```

Resumption tokens expire over time, which is why it is recommended to use a [script to harvest data](https://github.com/Q42/SimpleOAIHarvester).

### Response
Each object description is included in the XML file as a record. The header includes an identifier and date stamp. The metadata element includes fields based on the metadata format definitions.

{% highlight xml %}
<record>
    <oai:header>
        <oai:identifier>oai:rijksmuseum.nl/collection:BK-1975-81</oai:identifier>
        <oai:datestamp>2017-07-31T17:34:40Z</oai:datestamp>
    </oai:header>
    <oai:metadata>
        <oai_dc:dc>
            <dc:format>https://lh3.googleusercontent.com/tGI4dOAfJLBbewwspzXpUnSZxEKFACv9Y3FHqAxQUtN2p4AXt2MS9oFv6eJyIBtr7gvzmv58vSitMFVeHY0TGsfOfDN2=s0</dc:format>
            <dc:identifier>http://hdl.handle.net/10934/RM0001.COLLECT.293793</dc:identifier>
            <dc:format>eikenhout, belijmd met ebbenhout en parelmoer</dc:format>
            <dc:identifier>BK-1975-81</dc:identifier>
            <dc:language>Dutch</dc:language>
            <dc:publisher>Rijksmuseum</dc:publisher>
            <dc:rights>http://creativecommons.org/publicdomain/mark/1.0/</dc:rights>
            <dc:title>meubilair</dc:title>
            <dc:description>Eiken- en ebbenhouten kast belijmd met meerdere materialen. De vier deuren van de onder- en terugspringende bovenkast tonen verdiepte velden met kussens. De deuren en de schelpnis van de bovenkast worden gescheiden door hermatlanten. In het midden bevindt zich een lade met ramskop. De onderregel met lade vertoont verkroppingen. Op de hoeken geslingerde Corintische losstaande zuilen die een hoofdgestel dragen met versierde verkroppingen. Ingelegde paarlemoeren bloemen op de deuren, zuilen en hermschachten.</dc:description>
            <dc:creator>meubelmaker: Doomer, Herman</dc:creator>
            <dc:type>meubilair</dc:type>
            <dc:format>hoogte: 220,5 cm</dc:format>
            <dc:format>breedte: 206,0 cm</dc:format>
            <dc:format>diepte: 83,5 cm</dc:format>
            <dc:subject>Iconclasscode: 48A9833</dc:subject>
            <dc:date>1635 - ca.1645</dc:date>
        </oai_dc:dc>
    </oai:metadata>
</record>
{% endhighlight %}

## GetRecord
retrieve a specific record.

## ListMetadataFormats
retrieve the available metadata formats.

## ListSets
retrieve the available sets of objects.

## ListIdentifiers
retrieve headers with identifiers of objects.
