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

- **subject:EntirePublicDomainSet** All works in the public domain.
- **subject:PublicDomainImages** All works with an image in the public domain.
- **subject:OnDisplay** All works currently on display in the Rijksmuseum.
- **type:prints** All the works on paper in the Rijksmuseum collection .

-----------------------------------------

## ListRecords
retrieve an entire set of data.

## GetRecord
retrieve a specific record.

## ListMetadataFormats
retrieve the available metadata formats.

## ListSets
retrieve the available sets of objects.

## ListIdentifiers
retrieve headers with identifiers of objects.
