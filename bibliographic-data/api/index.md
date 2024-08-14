---
layout: default
title: API
nav_order: 1
parent: Bibliographic data
---

# Bibliographic data APIs
The Rijksmuseum supports the [SRU](#sru) client/server protocol for searching and retrieving bibliographic records from the library database.

## SRU
`http://library.rijksmuseum.nl:9998/biblios?version=1.1&operation=searchRetrieve&maximumRecords=20&query=[QUERY]` gives access to bibliographic data via search clients that support the [SRU standard](http://www.loc.gov/standards/sru/).

| Parameter      | Format                  | Default   | Notes                                                                    |
|:---------------|:------------------------|:----------|:-------------------------------------------------------------------------|
| `recordSchema` | `marcxml` / `dc` / `rm` | `marcxml` | append `dc` for simple Dublin Core or `rm` for a local customized format |
| `startRecord`  | `1`-`n`                 | '1'       | skip a specified number of records in the result set                     |

### Example request SRU
SRU supports CQL (Contextual Query Language). You can use operators like `and`, `or`. Some example search indexes are `title`, `author`, `subject`, `isbn`, `issn`, `editor`, `publisher` and `cql.serverchoice` (any). The following URL allows you to view the second 5 records in a search on subject containing the term rembrandt or title containing the term painting.

```http
http://library.rijksmuseum.nl:9998/biblios?version=1.1&operation=searchRetrieve&query=subject=rembrandt or title=painting&maximumRecords=5&startRecord=6
```

### Example response SRU
Responses are encoded in UTF-8 and by default formatted in [MARCXML](https://www.loc.gov/marc/bibliographic/):

```xml
<?xml version="1.0" encoding="UTF-8"?>
<zs:searchRetrieveResponse xmlns:zs="http://www.loc.gov/zing/srw/"><zs:version>1.1</zs:version><zs:numberOfRecords>3731</zs:numberOfRecords><zs:records><zs:record><zs:recordPacking>xml</zs:recordPacking><zs:recordData><record xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://www.loc.gov/MARC21/slim" xsi:schemaLocation="http://www.loc.gov/MARC21/slim http://www.loc.gov/standards/marcxml/schema/MARC21slim.xsd">
</record></zs:recordData><zs:recordPosition>8</zs:recordPosition></zs:record><zs:record><zs:recordPacking>xml</zs:recordPacking><zs:recordData><record xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://www.loc.gov/MARC21/slim" xsi:schemaLocation="http://www.loc.gov/MARC21/slim http://www.loc.gov/standards/marcxml/schema/MARC21slim.xsd">

  <leader>     nam a22     ui 4500</leader>
  <controlfield tag="001">449</controlfield>
  <controlfield tag="003">NL-AmRIJ</controlfield>
  <controlfield tag="005">20180206085653.0</controlfield>
  <controlfield tag="006">aa   |||||||||||||</controlfield>
  <controlfield tag="007">t|</controlfield>
  <controlfield tag="008">091231s1961    xx a   |||||||||||||eng d</controlfield>
  <datafield tag="029" ind1="0" ind2=" ">
    <subfield code="a">NLGGC</subfield>
    <subfield code="b">334776856</subfield>
  </datafield>
  <datafield tag="040" ind1=" " ind2=" ">
    <subfield code="a">NL-AmRIJ</subfield>
    <subfield code="b">dut</subfield>
    <subfield code="c">NL-AmRIJ</subfield>
  </datafield>
  <datafield tag="100" ind1="1" ind2=" ">
    <subfield code="a">Gerson, Horst Karl</subfield>
    <subfield code="9">41348</subfield>
  </datafield>
  <datafield tag="245" ind1="1" ind2="0">
    <subfield code="a">Seven letters by Rembrandt /</subfield>
    <subfield code="c">H. Gerson; transcription Isabella H. van Eeghen; transl. [from the Dutch] Yda D. Ovink.</subfield>
  </datafield>
  <datafield tag="260" ind1=" " ind2=" ">
    <subfield code="a">The Hague :</subfield>
    <subfield code="b">L.J.C. Boucher,</subfield>
    <subfield code="c">1961.</subfield>
  </datafield>
  <datafield tag="300" ind1=" " ind2=" ">
    <subfield code="a">71 p., 6 bl. pl. :</subfield>
    <subfield code="b">ill. ;</subfield>
    <subfield code="c">4°.</subfield>
  </datafield>
  <datafield tag="490" ind1="0" ind2=" ">
    <subfield code="a">Publicaties van het Rijksbureau voor Kunsthistorische Documentatie te 's-Gravenhage ;</subfield>
    <subfield code="v">1</subfield>
  </datafield>
  <datafield tag="600" ind1="1" ind2="4">
    <subfield code="9">94826</subfield>
    <subfield code="a">Rembrandt,</subfield>
    <subfield code="d">1606-1669</subfield>
  </datafield>
  <datafield tag="700" ind1="1" ind2=" ">
    <subfield code="a">Eeghen, Isabella Henriette van</subfield>
    <subfield code="9">32100</subfield>
  </datafield>
  <datafield tag="700" ind1="1" ind2=" ">
    <subfield code="a">Ovink, Yda D.</subfield>
    <subfield code="9">86761</subfield>
  </datafield>
  <datafield tag="920" ind1=" " ind2=" ">
    <subfield code="a">10-FFFF=452</subfield>
  </datafield>
  <datafield tag="942" ind1=" " ind2=" ">
    <subfield code="c">BKS</subfield>
  </datafield>
  <datafield tag="999" ind1=" " ind2=" ">
    <subfield code="c">449</subfield>
    <subfield code="d">449</subfield>
    <subfield code="x">1</subfield>
  </datafield>
  <datafield tag="952" ind1=" " ind2=" ">
    <subfield code="0">0</subfield>
    <subfield code="1">0</subfield>
    <subfield code="2">z</subfield>
    <subfield code="4">0</subfield>
    <subfield code="6">411_D_18</subfield>
    <subfield code="7">0</subfield>
    <subfield code="9">450</subfield>
    <subfield code="a">RMA</subfield>
    <subfield code="b">RMA</subfield>
    <subfield code="e">aankoop</subfield>
    <subfield code="l">2</subfield>
    <subfield code="m">1</subfield>
    <subfield code="o">411 D 18</subfield>
    <subfield code="p">090052</subfield>
    <subfield code="r">2019-08-26</subfield>
    <subfield code="s">2019-08-12</subfield>
    <subfield code="t">1961/1290</subfield>
    <subfield code="y">BKS</subfield>
  </datafield>
</record>
<!-- more results... -->
</zs:recordData><zs:recordPosition>10</zs:recordPosition></zs:record></zs:records></zs:searchRetrieveResponse>
```
