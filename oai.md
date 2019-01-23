---
layout: default
---

For more information about the Rijksmuseum API, please read [www.rijksmuseum.nl/en/api](https://www.rijksmuseum.nl/en/api).

The use of the Rijksmuseum API is subject to these [terms and conditions](https://www.rijksmuseum.nl/en/api/terms-and-conditions-of-use).

Issues regarding this API can be discussed in the [oai-issues repository](https://github.com/Rijksmuseum/oai-issues/).

## The Rijksmuseum OAI-PMH API
The Rijksmuseum offers an API featuring the [OAI-PMH protocol](https://www.openarchives.org/OAI/openarchivesprotocol.html) (Open Archives Initiative Protocol for Metadata Harvesting). The OAI-PMH standard is widely used in the cultural heritage sector to support harvesting metadata of collections. The Rijksmuseum OAI-PMH API provides access to more than 600,000 descriptions of objects (metadata) and digital images from the Rijksmuseum collection. An [example harvester](https://github.com/Q42/SimpleOAIHarvester) is available on GitHub to help you get started quickly.

## Access to the OAI-PMH API
To access the data, you will first need to obtain an API key. You can do this via the advanced settings of your [Rijksstudio account](https://www.rijksmuseum.nl/en/rijksstudio/my/profile). You will be given a key instantly upon request. Every request to the OAI-PMH API must be accompanied by this key:

```
http://www.rijksmuseum.nl/api/oai/[API_KEY]
```

## Documentation
Below you find the documentation for the Rijksmuseum OAI-PMH API.

### Verbs
A verb is used to indicate what data to retrieve. The following verbs can be used:

- **ListRecords** retrieve an entire set of data.
- **GetRecord** retrieve a specific record.
- **ListMetadataFormats** retrieve the available metadata formats.
- **ListSets** retrieve the available sets of objects.
- **ListIdentifiers** retrieve headers with identifiers of objects.

Every request to the OAI-PMH API must be accompanied by a verb parameter:

```
http://www.rijksmuseum.nl/api/oai/[API_KEY]?verb=[VERB]
```

### Example request
The following request will fetch all of the public data of The Nightwatch, in the Dublin Core format:

```
https://www.rijksmuseum.nl/api/oai/[API_KEY]?verb=GetRecord&metadataPrefix=oai_dc&identifier=oai:rijksmuseum.nl:sk-c-5
```

### Metadata formats
The datasets are provided via a simple XML web service. The following metadata formats are available:

- **oai_dc** Dublin Core [documentation](http://dublincore.org)
- **europeana_edm** Europeana Data Model [documentation](https://pro.europeana.eu/resources/standardization-tools/edm-documentation)
- **lido** Lightweight Information Describing Objects [documentation](http://lido-schema.org/)

The repository [conversion_oai_formats](https://github.com/Rijksmuseum/conversion_oai_formats) can provide insights in how Rijksmuseum data is mapped to these metadata formats.

### Sets of objects
The following sets of objects can be retrieved using the ListRecords and ListIdentifiers verbs:

- **subject:EntirePublicDomainSet** All public domain objects.
- **subject:PublicDomainImages** All public domain objects with an image.
- **subject:OnDisplay** All objects currently on display in the Rijksmuseum.
- **type:prints** All the works on paper.

Omitting the set parameter will default to the set of all available objects.

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
    <tr>
      <td><code>from</code></td>
      <td><code>YYYY-MM-DD</code> / <code>YYYY-MM-DDThh:mm:ssZ</code></td>
      <td>earliest datestamp</td>
      <td>Optional argument for selective harvesting, based on a specified date range. The from parameter specifies a bound interpreted as "greater than or equal to".</td>
    </tr>
    <tr>
      <td><code>until</code></td>
      <td><code>YYYY-MM-DD</code> / <code>YYYY-MM-DDThh:mm:ssZ</code></td>
      <td>most recent datestamp</td>
      <td>Optional argument for selective harvesting, based on a specified date range. The until parameter specifies a bound interpreted as "less than or equal to".</td>
    </tr>
  </tbody>
</table>


### Request
```
https://www.rijksmuseum.nl/api/oai/[API_KEY]?verb=ListRecords&set=subject:EntirePublicDomainSet&metadataPrefix=oai_dc
```

This request will return the first 20 records in the dataset of all public domain objects. A `resumptionToken` element is included at the end of the response, which can be used to request the next 20 records in the dataset:

```
https://www.rijksmuseum.nl/api/oai/[API_KEY]?verb=ListRecords&set=subject:EntirePublicDomainSet&metadataPrefix=oai_dc&resumptionToken=MXxvYWlfZGN8MjAxOC0wMy0xNFQxMzo0MToyMnxzdWJqZWN0OkVudGlyZVB1YmxpY0RvbWFpblNldHwyMDE2LTAzLTEwVDEwOjAxOjA5fERYRjFaWEo1UVc1a1JtVjBZMmdCQUFBQUFBUG1YMWNXV2xwNlNFVm1ZMWxVZWpJNFIyZzNXVUZSTlVzdFVRPT18MjA=
```

Resumption tokens expire over time, which is why it is recommended to use a [script to harvest data](https://github.com/Q42/SimpleOAIHarvester).

### Response
Each object description is included in the XML response as a record. The header includes an identifier and date stamp. The metadata includes fields based on the metadata format definitions, in this case [Dublin Core](http://dublincore.org):

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
`GET /oai/[API_KEY]?verb=GetRecord` retrieves an individual metadata record.

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
      <td><code>identifier</code></td>
      <td><code>a-z|0-9|:|-</code></td>
      <td></td>
      <td>Required: specifies the identifier of the object (e.g. oai:rijksmuseum.nl:sk-c-5)</td>
    </tr>
    <tr>
      <td><code>metadataPrefix</code></td>
      <td><code>oai_dc</code> / <code>europeana_edm</code> / <code>lido</code></td>
      <td></td>
      <td>Required: the metadata format of the result.</td>
    </tr>
  </tbody>
</table>

### Request
```
https://www.rijksmuseum.nl/api/oai/[API_KEY]?verb=GetRecord&metadataPrefix=oai_dc&identifier=oai:rijksmuseum.nl:sk-c-5
```

This request will return the object description of the Nightwatch (SK-C-5).

### Response
An object description is included in the XML response as a record. The header includes an identifier and date stamp. The metadata includes fields based on the metadata format definitions, in this case [Dublin Core](http://dublincore.org):

{% highlight xml %}
<record>
    <header>
        <identifier>oai:rijksmuseum.nl:sk-c-5</identifier>
        <datestamp>2018-02-02T14:51:53Z</datestamp>
    </header>
    <metadata>
        <oai:record>
            <oai:header>
                <oai:identifier>oai:rijksmuseum.nl/collection:SK-C-5</oai:identifier>
                <oai:datestamp>2018-02-02T15:51:53Z</oai:datestamp>
            </oai:header>
            <oai:metadata>
                <oai_dc:dc>
                    <dc:format>http://lh3.googleusercontent.com/J-mxAE7CPu-DXIOx4QKBtb0GC4ud37da1QK7CzbTIDswmvZHXhLm4Tv2-1H3iBXJWAW_bHm7dMl3j5wv_XiWAg55VOM=s0</dc:format>
                    <dc:identifier>http://hdl.handle.net/10934/RM0001.COLLECT.5216</dc:identifier>
                    <dc:format>olieverf op doek</dc:format>
                    <dc:identifier>SK-C-5</dc:identifier>
                    <dc:language>Dutch</dc:language>
                    <dc:publisher>Rijksmuseum</dc:publisher>
                    <dc:rights>http://creativecommons.org/publicdomain/mark/1.0/</dc:rights>
                    <dc:date>1642</dc:date>
                    <dc:title>Officieren en andere schutters van wijk II in Amsterdam onder leiding van kapitein Frans Banninck Cocq en luitenant Willem van Ruytenburch, bekend als de ‘Nachtwacht’</dc:title>
                    <dc:description>Het korporaalschap van kapitein Frans Banninck Cocq en luitenant Willem van Ruytenburch, bekend als de 'Nachtwacht'. Schutters van de kloveniersdoelen uit een poort naar buiten tredend. Op een schild aangebracht naast de poort staan de namen van de afgebeelde personen: Frans Banninck Cocq, heer van purmerlant en Ilpendam, Capiteijn Willem van Ruijtenburch van Vlaerdingen, heer van Vlaerdingen, Lu[ij]tenant, Jan Visscher Cornelisen Vaendrich, Rombout Kemp Sergeant, Reijnier Engelen Sergeant, Barent Harmansen, Jan Adriaensen Keyser, Elbert Willemsen, Jan Clasen Leydeckers, Jan Ockersen, Jan Pietersen bronchorst, Harman Iacobsen wormskerck, Jacob Dircksen de Roy, Jan vander heede, Walich Schellingwou, Jan brugman, Claes van Cruysbergen, Paulus Schoonhoven. De schutters zijn gewapend met lansen, musketten en hellebaarden. Rechts de tamboer met een grote trommel. Tussen de soldaten links staat een meisje met een dode kip om haar middel, rechts een blaffende hond. Linksboven de vaandrig met de uitgestoken vaandel.</dc:description>
                    <dc:creator>schilder: Rijn, Rembrandt van</dc:creator>
                    <dc:type>schilderij</dc:type>
                    <dc:format>hoogte: 379,5 cm</dc:format>
                    <dc:format>breedte: 453,5 cm</dc:format>
                    <dc:format>gewicht: 337 kg, gewicht met lijst</dc:format>
                    <dc:subject>Iconclasscode: 45(+26)</dc:subject>
                    <dc:subject>Banning Cocq, Frans (ca. 1605 - 1655)</dc:subject>
                    <dc:coverage>Amsterdam</dc:coverage>
                </oai_dc:dc>
            </oai:metadata>
        </oai:record>
    </metadata>
</record>
{% endhighlight %}

## ListMetadataFormats
`GET /oai/[API_KEY]?verb=ListMetadataFormats` retrieves a list of available metadata formats.

### Request
```
https://www.rijksmuseum.nl/api/oai/[API_KEY]?verb=ListMetadataFormats
```

This request will return a list of available metadata formats.

### Response
Each metadata format element includes the prefix that can be used as a parameter in other requests, the schema and the name space.

{% highlight xml %}
<ListMetadataFormats>
    <metadataFormat>
        <metadataPrefix>oai_dc</metadataPrefix>
        <schema>http://www.openarchives.org/OAI/2.0/oai_dc.xsd</schema>
        <metadataNamespace>http://www.openarchives.org/OAI/2.0/</metadataNamespace>
    </metadataFormat>
    <metadataFormat>
        <metadataPrefix>europeana_edm</metadataPrefix>
        <schema>http://www.openarchives.org/OAI/2.0/oai_dc.xsd</schema>
        <metadataNamespace>http://www.openarchives.org/OAI/2.0/</metadataNamespace>
    </metadataFormat>
    <metadataFormat>
        <metadataPrefix>lido</metadataPrefix>
        <schema>http://www.lido-schema.org/schema/v1.0/lido-v1.0.xsd</schema>
        <metadataNamespace>http://www.lido-schema.org</metadataNamespace>
    </metadataFormat>
</ListMetadataFormats>
{% endhighlight %}


## ListSets

`GET /oai/[API_KEY]?verb=ListSets` retrieves the available sets of objects.

### Request
```
https://www.rijksmuseum.nl/api/oai/[API_KEY]?verb=ListSets
```

This request will return a list of available sets of objects.

### Response
Each set includes a descriptive name and a set identifier, that can be used as a parameter in other requests.

{% highlight xml %}
<ListSets>
    <set>
        <setSpec>subject:EntirePublicDomainSet</setSpec>
        <setName>EntirePublicDomainSet</setName>
    </set>
    <set>
        <setSpec>subject:OnDisplay</setSpec>
        <setName>OnDisplay</setName>
    </set>
    <set>
        <setSpec>subject:PublicDomainImages</setSpec>
        <setName>PublicDomainImages</setName>
    </set>
    <set>
        <setSpec>type:prints</setSpec>
        <setName>Prints</setName>
    </set>
</ListSets>
{% endhighlight %}

## ListIdentifiers
`GET /oai/[API_KEY]?verb=ListIdentifiers` retrieves headers with identifiers of objects. This verb is an abbreviated form of ListRecords, retrieving only headers rather than records.

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
      <td>The set of object identifiers to harvest.</td>
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
    <tr>
      <td><code>from</code></td>
      <td><code>YYYY-MM-DD</code> / <code>YYYY-MM-DDThh:mm:ssZ</code></td>
      <td>earliest datestamp</td>
      <td>Optional argument for selective harvesting, based on a specified date range. The from parameter specifies a bound interpreted as "greater than or equal to".</td>
    </tr>
    <tr>
      <td><code>until</code></td>
      <td><code>YYYY-MM-DD</code> / <code>YYYY-MM-DDThh:mm:ssZ</code></td>
      <td>most recent datestamp</td>
      <td>Optional argument for selective harvesting, based on a specified date range. The until parameter specifies a bound interpreted as "less than or equal to".</td>
    </tr>
  </tbody>
</table>


### Request
```
https://www.rijksmuseum.nl/api/oai/[API_KEY]?verb=ListIdentifiers&set=subject:EntirePublicDomainSet&metadataPrefix=oai_dc
```

This request will return the first 20 headers in the dataset of all public domain objects. A `resumptionToken` element is included at the end, which can be used to return the next 20 headers in the dataset:

```
https://www.rijksmuseum.nl/api/oai/[API_KEY]?verb=ListIdentifiers&set=subject:EntirePublicDomainSet&metadataPrefix=oai_dc&resumptionToken=MXxvYWlfZGN8MjAxOC0wMy0xNFQxMzo0MToyMnxzdWJqZWN0OkVudGlyZVB1YmxpY0RvbWFpblNldHwyMDE2LTAzLTEwVDEwOjAxOjA5fERYRjFaWEo1UVc1a1JtVjBZMmdCQUFBQUFBUGdMUzhXUmpkc1pteEdaVEpTVUZOMU5uQm9PVFF6Vm5KNVFRPT18MjAw
```

Resumption tokens expire over time, which is why it is recommended to use a [script to harvest data](https://github.com/Q42/SimpleOAIHarvester).

### Response
Each header includes the identifier of the object and a date stamp. A date stamp indicates when a record was created, deleted, or modified.

{% highlight xml %}
<ListIdentifiers>
    <header>
        <identifier>BK-1975-81</identifier>
        <datestamp>2017-07-31T19:34:40Z</datestamp>
    </header>
    <header>
        <identifier>NG-NM-7687</identifier>
        <datestamp>2017-09-21T18:48:05Z</datestamp>
    </header>
    <resumptionToken completeListSize="540886">MXxvYWlfZGN8MjAxOC0wMy0xNFQxMzo0MToyMnxzdWJqZWN0OkVudGlyZVB1YmxpY0RvbWFpblNldHwyMDE2LTAzLTEwVDEwOjAxOjA5fERYRjFaWEo1UVc1a1JtVjBZMmdCQUFBQUFBUGdMUzhXUmpkc1pteEdaVEpTVUZOMU5uQm9PVFF6Vm5KNVFRPT18MjAw</resumptionToken>
</ListIdentifiers>
{% endhighlight %}
