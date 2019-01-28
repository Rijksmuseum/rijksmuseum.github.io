---
layout: default
---

For more information about the Rijksmuseum API, please read [www.rijksmuseum.nl/en/api](https://www.rijksmuseum.nl/en/api).

For live code examples demonstrating the use of the Rijksmuseum API, please checkout the [demo's page](demos).

The use of the Rijksmuseum API is subject to these [terms and conditions](https://www.rijksmuseum.nl/en/api/terms-and-conditions-of-use).

Issues regarding this API can be discussed in the [api-issues repository](https://github.com/Rijksmuseum/api-issues/).


## The Rijksmuseum API
The live website API (which has a live link to the website platform) makes the full power of the award-winning [Rijksmuseum website](https://www.rijksmuseum.nl) directly accessible to developers. Searching the collection through the API offers a wide range of interesting possibilities, as do features such as the “explore the collection” pages, the Rijksstudio users’ collections, and the tiled images used to zoom in to close-ups of works of art. Other kinds of data are also available, such as information from the Rijksmuseum's events calendar. The JSON-based service is so easy to use that you can create an application using the Rijksmuseum’s rich and freely accessible content in no time.


## Access to the API
To access the data and images, you will first need to obtain an API key. You can do this via the advanced settings of your [Rijksstudio account](https://www.rijksmuseum.nl/en/rijksstudio/my/profile). You will be given a key instantly upon request. Every request to the API must be accompanied by this key.


## Documentation
Below you find the documentation for the live website API.

### Parameters
Each API endpoints varies a bit in the options available.
In general for each API request you can make use of the following parameters:

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
      <td><code>key</code></td>
      <td><code>a-z|0-9</code></td>
      <td></td>
      <td>Mandatory for every request.</td>
    </tr>
    <tr>
      <td><code>format</code></td>
      <td><code>xml</code> / <code>json</code> / <code>jsonp</code></td>
      <td><code>xml</code></td>
      <td>The format of the result.</td>
    </tr>
  </tbody>
</table>

### Culture
Most of the endpoints are language dependent. Use one of the following language codes:

- `nl` : Dutch  
- `en` : English  

Please note that choosing a particular locale might impact the obtained result set. This is due to the fact that many objects have more thorough descriptions in Dutch.

### Example request
The following request will fetch all of the public data of The Nightwatch, in Dutch using the format JSON:

```
https://www.rijksmuseum.nl/api/nl/collection/SK-C-5?key=[API_KEY]&format=json
```


## Endpoints
There are API's available for the following elements:

- **Collection:** The complete online collection of the Rijksmuseum with all public data.  
- **Content pages:** Static pages as used on the website.
- **Usersets:** Sets from Rijksstudio users.
- **Calendar:** Calendar and availability of expositions, tours, etc.


## Collection
`GET /api/[culture]/collection` gives the full collection with brief information about each work. The results are split up in result pages. By using the `p` and `ps` parameters you can fetch more results. All of the other parameters are identical to the [advanced search page](https://www.rijksmuseum.nl/en/search/advanced) on the Rijksmuseum website. You can use that page to find out what's the best query to use.


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
      <td><code>culture</code></td>
      <td><code>nl</code> / <code>en</code></td>
      <td></td>
      <td>The language to search in (and of the results)</td>
    </tr>
    <tr>
      <td><code>p</code></td>
      <td><code>0-n</code></td>
      <td><code>0</code></td>
      <td>The result page. Note that <code>p * ps</code> cannot exceed 10.000</td>
    </tr>
    <tr>
      <td><code>ps</code></td>
      <td><code>1-100</code></td>
      <td><code>10</code></td>
      <td>The number of results per page</td>
    </tr>
    <tr>
      <td><code>q</code></td>
      <td><code>a-z</code></td>
      <td></td>
      <td>The search terms that need to occur in one of the fields of the artwork data </td>
    </tr>
    <tr>
      <td><code>maker</code></td>
      <td><code>a-z</code></td>
      <td></td>
      <td>Works need to be made by this artist</td>
    </tr>
    <tr>
      <td><code>type</code></td>
      <td><code>a-z</code></td>
      <td></td>
      <td>The type of the artwork</td>
    </tr>
    <tr>
      <td><code>material</code></td>
      <td><code>a-z</code></td>
      <td></td>
      <td>The material of the artwork</td>
    </tr>
    <tr>
      <td><code>technique</code></td>
      <td><code>a-z</code></td>
      <td></td>
      <td>The technique used to make the works</td>
    </tr>
    <tr>
      <td><code>f.dating.period</code></td>
      <td><code>0-21</code></td>
      <td></td>
      <td>The century in which the work is made</td>
    </tr>
    <tr>
      <td><code>f.normalized32Colors.hex</code></td>
      <td><code>Color HEX</code></td>
      <td></td>
      <td>Colors found in the images (mind: The `#` in #FF0000 should be url-encoded!)</td>
    </tr>  
    <tr>
      <td><code>imgonly</code></td>
      <td><code>True</code></td>
      <td><code>False</code></td>
      <td>Only give results for which an image is available or not</td>
    </tr>
    <tr>
      <td><code>toppieces</code></td>
      <td><code>True</code></td>
      <td><code>False</code></td>
      <td>Only give works that are top pieces</td>
    </tr>
    <tr>
      <td><code>s</code></td>
      <td><code>relevance</code></td>
      <td></td>
      <td>Sort results on relevance</td>
    </tr>
    <tr>
      <td></td>
      <td><code>objecttype</code></td>
      <td></td>
      <td>Sort results on type</td>
    </tr>
    <tr>
      <td></td>
      <td><code>chronologic</code></td>
      <td></td>
      <td>Sort results chronologically (oldest first)</td>
    </tr>
    <tr>
      <td></td>
      <td><code>achronologic</code></td>
      <td></td>
      <td>Sort results chronologically (newest first)</td>
    </tr>
    <tr>
      <td></td>
      <td><code>artist</code></td>
      <td></td>
      <td>Sort results on artist (a-z)</td>
    </tr>
    <tr>
      <td></td>
      <td><code>artistdesc</code></td>
      <td></td>
      <td>Sort results on artist (z-a)</td>
    </tr>
  </tbody>
</table>

### Request
```
https://www.rijksmuseum.nl/api/nl/collection?key=[API_KEY]&format=json&type=schilderij&f.normalized32Colors.hex=%20%23367614
```

### Response
{% highlight json %}
{
  "elapsedMilliseconds": 164,
  "count": 359,
  "artObjects": [
    {
      "links": {
        "self": "https://www.rijksmuseum.nl/api/nl/collection/SK-C-5",
        "web": "https://www.rijksmuseum.nl/nl/collection/SK-C-5"
      },
      "id": "nl-SK-C-5",
      "objectNumber": "SK-C-5",
      "title": "Schutters van wijk II onder leiding van kapitein Frans Banninck Cocq, bekend als de ‘Nachtwacht’",
      "hasImage": true,
      "principalOrFirstMaker": "Rembrandt Harmensz. van Rijn",
      "longTitle": "Schutters van wijk II onder leiding van kapitein Frans Banninck Cocq, bekend als de ‘Nachtwacht’, Rembrandt Harmensz. van Rijn, 1642",
      "showImage": true,
      "permitDownload": true,
      "webImage": {
        "guid": "92253da1-794d-49f4-9e3c-e4c160715f53",
        "offsetPercentageX": 50,
        "offsetPercentageY": 100,
        "width": 2500,
        "height": 2034,
        "url": "http://lh6.ggpht.com/wwx2vAS9DzFmmyeZefPjMtmCNOdjD80gvkXJcylloy40SiZOhdLHVddEZLBHtymHu53TcvqJLYZfZF7M-uvoMmG_wSI=s0"
      },
      "headerImage": {
        "guid": "29a2a516-f1d2-4713-9cbd-7a4458026057",
        "offsetPercentageX": 50,
        "offsetPercentageY": 50,
        "width": 1920,
        "height": 460,
        "url": "http://lh5.ggpht.com/SgH3Qo-vYI8GGm7-b-Qt6lXgsCAIoU2VDRwO5LYSBVNhhbZCetcvc88ZPi518MTy0MHDrna4X4ZC1ymxVJVpzps8gqw=s0"
      },
      "productionPlaces": []
    },
    // more results...
  ]
}
{% endhighlight %}


## Collection details
`GET /api/[culture]/collection/[object-number]` gives more details of a work. The object number can be found in the results given in /api/[culture]/collection.


<table>
  <thead>
    <tr>
      <th>Parameter</th>
      <th>Format</th>
      <th>Notes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>culture</code></td>
      <td><code>nl</code> / <code>en</code></td>
      <td>De language to give the results in</td>
    </tr>
    <tr>
      <td><code>object-number</code></td>
      <td><code>a-z|0-9|-</code></td>
      <td>The identifier of the work (case-sensitive)</td>
    </tr>
  </tbody>
</table>

### Request
```
https://www.rijksmuseum.nl/api/nl/collection/SK-C-5?key=[API_KEY]&format=json
```

### Response
{% highlight javascript %}
{
  "elapsedMilliseconds": 27,
  "artObject": {
    "links": {
      "search": "https://www.rijksmuseum.nl/api/nl/collection"
    },
    "id": "nl-SK-C-5",
    "priref": "5216",
    "objectNumber": "SK-C-5",
    "language": "nl",
    "title": "Schutters van wijk II onder leiding van kapitein Frans Banninck Cocq, bekend als de ‘Nachtwacht’",
    "tags": [
      {
        "userId": 3530,
        "name": "margaret barrett my first collection",
        "lang": "en",
        "objectNumber": "SK-C-5"
      },
      // more results...
    ],
    "copyrightHolder": null,
    "webImage": {
      "guid": "92253da1-794d-49f4-9e3c-e4c160715f53",
      "offsetPercentageX": 50,
      "offsetPercentageY": 100,
      "width": 2500,
      "height": 2034,
      "url": "http://lh6.ggpht.com/wwx2vAS9DzFmmyeZefPjMtmCNOdjD80gvkXJcylloy40SiZOhdLHVddEZLBHtymHu53TcvqJLYZfZF7M-uvoMmG_wSI=s0"
    },
    "colors": [
      "#261808",
      // more results...
    ],
    "colorsWithNormalization": [
      {
        "originalHex": "#261808",
        "normalizedHex": "#000000"
      },
      // more results...
    ],
    "normalizedColors": [
      "#000000",
      // more results...
    ],
    "normalized32Colors": [
      "#000000",
      // more results...
    ],
    "titles": [
      "Officieren en andere schutters van wijk II in Amsterdam onder leiding van kapitein Frans Banninck Cocq en luitenant Willem van Ruytenburch, bekend als de ‘Nachtwacht’",
      "Het korporaalschap van kapitein Frans Banninck Cocq en luitenant Willem van Ruytenburch, bekend als de 'Nachtwacht'"
    ],
    "description": "Het korporaalschap van kapitein Frans Banninck Cocq en luitenant Willem van Ruytenburch, bekend als de 'Nachtwacht'. Schutters van de kloveniersdoelen uit een poort naar buiten tredend. Op een schild aangebracht naast de poort staan de namen van de afgebeelde personen: Frans Banninck Cocq, heer van purmerlant en Ilpendam, Capiteijn Willem van Ruijtenburch van Vlaerdingen, heer van Vlaerdingen, Lu[ij]tenant, Jan Visscher Cornelisen Vaendrich, Rombout Kemp Sergeant, Reijnier Engelen Sergeant, Barent Harmansen, Jan Adriaensen Keyser, Elbert Willemsen, Jan Clasen Leydeckers, Jan Ockersen, Jan Pietersen bronchorst, Harman Iacobsen wormskerck, Jacob Dircksen de Roy, Jan vander heede, Walich Schellingwou, Jan brugman, Claes van Cruysbergen, Paulus Schoonhoven. De schutters zijn gewapend met lansen, musketten en hellebaarden. Rechts de tamboer met een grote trommel. Tussen de soldaten links staat een meisje met een dode kip om haar middel, rechts een blaffende hond. Linksboven de vaandrig met de uitgestoken vaandel.",
    "labelText": null,
    "objectTypes": [
      "schilderij"
    ],
    "objectCollection": [
      "schilderijen"
    ],
    "makers": [
      {
        "name": "Rembrandt Harmensz. van Rijn",
        "unFixedName": "Rembrandt Harmensz. van Rijn",
        "placeOfBirth": "Leiden",
        "dateOfBirth": "1606-07-15",
        "dateOfBirthPrecision": null,
        "dateOfDeath": "1669-10-08",
        "dateOfDeathPrecision": null,
        "placeOfDeath": "Amsterdam",
        "occupation": [
          "prentmaker",
          "tekenaar",
          "schilder"
        ],
        "roles": [
          "schilder"
        ],
        "nationality": "Noord-Nederlands",
        "biography": null,
        "productionPlaces": [],
        "schoolStyles": [],
        "qualification": null
      }
    ],
    "principalMakers": [
      {
        "name": "Rembrandt Harmensz. van Rijn",
        "unFixedName": "Rembrandt Harmensz. van Rijn",
        "placeOfBirth": "Leiden",
        "dateOfBirth": "1606-07-15",
        "dateOfBirthPrecision": null,
        "dateOfDeath": "1669-10-08",
        "dateOfDeathPrecision": null,
        "placeOfDeath": "Amsterdam",
        "occupation": [
          "prentmaker",
          "tekenaar",
          "schilder"
        ],
        "roles": [
          "schilder"
        ],
        "nationality": "Noord-Nederlands",
        "biography": null,
        "productionPlaces": [],
        "schoolStyles": [],
        "qualification": null
      }
    ],
    "plaqueDescriptionDutch": "Rembrandts beroemdste en grootste doek werd gemaakt voor de Kloveniersdoelen. Dit was een van de verenigingsgebouwen van de Amsterdamse schutterij, de burgerwacht van de stad. \r\nRembrandt was de eerste die op een groepsportret de figuren in actie weergaf. De kapitein, in het zwart, geeft zijn luitenant opdracht dat de compagnie moet gaan marcheren. De schutters stellen zich op. Met behulp van licht vestigde Rembrandt de aandacht op belangrijke details, zoals het handgebaar van de kapitein en het kleine meisje op de achtergrond. Zij is de mascotte van de schutters.",
    "plaqueDescriptionEnglish": null,
    "principalMaker": "Rembrandt Harmensz. van Rijn",
    "artistRole": null,
    "associations": [],
    "acquisition": {
      "method": "bruikleen",
      "date": "1808-01-01T00:00:00Z",
      "creditLine": "Bruikleen van de gemeente Amsterdam"
    },
    "exhibitions": [],
    "materials": [
      "doek",
      "olieverf"
    ],
    "techniques": [],
    "productionPlaces": [],
    "dating": {
      "presentingDate": "ca. 1642",
      "sortingDate": 1642,
      "period": 17
    },
    "classification": {
      "iconClassIdentifier": [
        "45(+26)",
        "45C1",
        "48C7341",
        "31D11222",
        "45D12",
        "34B11"
      ],
      "motifs": [],
      "events": [],
      "periods": [],
      "places": [
        "Amsterdam"
      ],
      "people": []
    },
    "hasImage": true,
    "historicalPersons": [],
    "inscriptions": [
      "Rembrandt f 1642",
      "signatuur en datum",
      "Frans Banning Cocq, heer van purmerlant en Ilpendam, Capiteijn Willem van Ruijtenburch van Vlaerdingen, heer van Vlaerdingen, Lu[ij]tenant, Jan Visscher Cornelisen Vaendrich, Rombout Kemp Sergeant, Reijnier Engelen Sergeant, Barent Harmansen, Jan Adriaensen Keyser, Elbert Willemsen, Jan Clasen Leydeckers, Jan Ockersen, Jan Pietersen bronchorst, Harman Iacobsen wormskerck, Jacob Dircksen de Roy, Jan vander heede, Walich Schellingwou, Jan brugman, Claes van Cruysbergen, Paulus Schoonhoven",
      "inscriptie"
    ],
    "documentation": [
      "Inzoomer object op zaal, 2013 (Nederlands/English).",
      "A. Jensen Adams, Public Faces and Private Identities in Seventeenth-Century Holland, Portraiture and the Production of Community, New York 2009, p. 211-217, fig. 60.",
      "M. Rayssac, 'l'Exode des Musées, Histoire des oeuvres d'art sous l'Occupation', Parijs 2007.",
      // more results...
    ],
    "catRefRPK": [],
    "principalOrFirstMaker": "Rembrandt Harmensz. van Rijn",
    "dimensions": [
      {
        "unit": "cm",
        "type": "hoogte",
        "part": null,
        "value": "379,5"
      },
      {
        "unit": "cm",
        "type": "breedte",
        "part": null,
        "value": "453,5"
      },
      {
        "unit": "kg",
        "type": "gewicht",
        "part": null,
        "value": "337"
      },
      {
        "unit": "kg",
        "type": "gewicht",
        "part": null,
        "value": "170"
      }
    ],
    "physicalProperties": [],
    "physicalMedium": "olieverf op doek",
    "longTitle": "Schutters van wijk II onder leiding van kapitein Frans Banninck Cocq, bekend als de ‘Nachtwacht’, Rembrandt Harmensz. van Rijn, 1642",
    "subTitle": "h 379,5cm × b 453,5cm × g 337kg",
    "scLabelLine": "Rembrandt Harmensz. van Rijn (15-jul-1606 - 08-okt-1669), 1642, olieverf op doek",
    "label": {
      "title": "Schutters van wijk II onder leiding van kapitein Frans Banninck Cocq, bekend als de ‘Nachtwacht’",
      "makerLine": "Rembrandt Harmensz van Rijn (1606–1669), olieverf op doek, 1642",
      "description": null,
      "notes": null,
      "date": "2013-05-22"
    },
    "showImage": true
  },
  "artObjectPage": {
    "id": "nl-sk-c-5",
    "similarPages": [],
    "lang": "nl",
    "objectNumber": "sk-c-5",
    "tags": [],
    "plaqueDescription": null,
    "audioFile1": null,
    "audioFileLabel1": null,
    "audioFileLabel2": null,
    "createdOn": "0001-01-01T00:00:00Z",
    "updatedOn": "0001-01-01T00:00:00Z",
    "adlibOverrides": {
      "titel": null,
      "maker": null,
      "etiketText": null
    }
  }
}
{% endhighlight %}


## Collection images
`GET /api/[culture]/collection/[object-number]/tiles` gives all the information you need to show the image split up in tiles. This is used to implement the zoom functionality on the Rijksmuseum website. This specific API only supports the JSON format.

<table>
  <thead>
    <tr>
      <th>Parameter</th>
      <th>Format</th>
      <th>Notes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>object-number</code></td>
      <td><code>a-z|0-9|-</code></td>
      <td>The identifier of the work (case-sensitive)</td>
    </tr>
  </tbody>
</table>

### Request
```
https://www.rijksmuseum.nl/api/nl/collection/SK-C-5/tiles?key=[API_KEY]&format=json
```

### Response
{% highlight javascript %}
{
  "levels": [{
    "name": "z4",
    "width": 885,
    "height": 720,
    "tiles": [{
      "x": 1,
      "y": 0,
      "url": "http://lh6.ggpht.com/pA_7SmGBE7N60aZu5PD5emVDobNJ424v2eDWJGoZ_cDbTquRT7QukK3a4I6K-nHieHIMFBVsNiwHrJRjOAutVYiswg=s0"
    }, {
      "x": 1,
      "y": 1,
      "url": "http://lh6.ggpht.com/9aGsFd_D0wiQXVYuTNxW56XhVUKgJuxMZD6zr9vGb2bdu6uOa3PcTqkXCyzTBDVHQCBqtPcYypVNVBxSMwU5TuXCWxwP=s0"
    }, {
      "x": 0,
      "y": 0,
      "url": "http://lh4.ggpht.com/QE4p5uoLiFD_4d7djBlAk5e8c8DrEIMcAiCJ01TjSxW44vWIK8vlD2OkXmzdVlFIRa6RQ8QxlyNCbqEgRr1K8OVBuYo=s0"
    }, {
      "x": 0,
      "y": 1,
      "url": "http://lh3.ggpht.com/yifWBj1IqXGRfesLL3xbA-57UwZ6ZoDSJKUkH86ziuY0I2V91oCYIp56ToUR4JlCdNfR4aqkQVo_AGUMOPF_3UZfbO8=s0"
    }]
  }, {
    "name": "z3",
    "width": 1771,
    "height": 1441,
    "tiles": [{
      "x": 2,
      "y": 1,
      "url": "http://lh4.ggpht.com/J4T4QRMwUrA00AjhQ49GkRTTQ6VsY61Mfg7ZbefYDErI7qBX2V-DALH4fckZJ1xXBqoyQerVAJJrM7_FHo_8WOCP3nsP=s0"
    }, {
      "x": 2,
      "y": 0,
      "url": "http://lh3.ggpht.com/UaQ8A1oQWO3Q_0wYmepftwN2ltxfvdUnZwxrGKjxQcJRxEhx5jd4iixF-TipbBRLzYOOoYNfayHFd1WYjNvQAPcTmRY=s0"
    }, {
      "x": 1,
      "y": 2,
      "url": "http://lh4.ggpht.com/ra5cl71d2gSR9aK8KlUbLnuV3BUoVw07A7Bo5Muun0n4iyI2-4DpHKC5R9lHwnoZgiUW8DnKQVUuhglJMw0aK9LM54Y=s0"
    }] // 9 more results...
  }, {
    "name": "z2",
    "width": 3542,
    "height": 2882,
    "tiles": [{
      "x": 2,
      "y": 0,
      "url": "http://lh4.ggpht.com/Zw2gLc54TbRrfRfO8oN9q3WOWztp5-P5o99vCCy5ypeg9jIlmXFuZAuw8r0mfVj7eH73Or84SYDURntqHFVSrsIGDwFO=s0"
    }, {
      "x": 5,
      "y": 1,
      "url": "http://lh6.ggpht.com/5Tadf-5EMg8G68Og84GUvuY9eA30gTRXG-tvhOiGPpnyWGBOiUo37k1mwTcI7epzY23YrCTwYa5KzMx4b_gqCUWsrg=s0"
    }, {
      "x": 1,
      "y": 3,
      "url": "http://lh4.ggpht.com/Oq5MjLJbE8jroHYvAtUy3-5DAsKSc3ihOYjP5c3z398g26DEpX4fDwd5tc8Z_dznJdYw-1mKxEsuH0DHwLid5Ho9-qA=s0"
    }] // 39 more results...
  }, {
    "name": "z1",
    "width": 7084,
    "height": 5764,
    "tiles": [{
      "x": 9,
      "y": 0,
      "url": "http://lh5.ggpht.com/6IJ5jbYWD0xh2iz4Pr02LRDC5kWkku-Ua4U8LRVrG3KYuzu-9VMAIyM5tQAL-L-KoU78N-zwn3BhGsDvxzwbPfQ9fzJN=s0"
    }, {
      "x": 7,
      "y": 3,
      "url": "http://lh4.ggpht.com/2LNscS7X823dgIcjFiQTfCtgCIvOx-KFxPgOKjZKJE5AHvcPKO1KF3h01em2-9MVvGhWaxaLJ1eg8wlLw4H33m1ollU=s0"
    }, {
      "x": 2,
      "y": 3,
      "url": "http://lh3.ggpht.com/n6LmzcC-3xZxUUyZhP4SNE9G-VhNrU5UJGcal0kJ2ZqWfSlPRpRs46YfJ6kjMWwX1Buoh6XqNuXmB5pHZzn2iO1DAg=s0"
    }] // 165 more results...
  }, {
    "name": "z0",
    "width": 14168,
    "height": 11528,
    "tiles": [{
      "x": 27,
      "y": 17,
      "url": "http://lh3.ggpht.com/mwNzQh8UnMdVpp6SQZkhrUfl1S4XJIovuAlTUdWYKHm_ZANVfiW_bK2LAVUa-6wHDOgvOeqI11V1js0ZQ-yGk543Bag=s0"
    }, {
      "x": 1,
      "y": 18,
      "url": "http://lh6.ggpht.com/jtW5dhxmMVuI8TZcGxAD707t1z7AZTFpy0WnZW0OSuZegrtGEz9d-q2D1E2cNzZ1AB_m0X4-jkh0bvkuvUhST4xXTA=s0"
    }, {
      "x": 9,
      "y": 18,
      "url": "http://lh6.ggpht.com/XAXUqfk38nZZH6gQNATOuA5yPxF4dmDwtMZRhlUykxlVvQU5UM2bNvKgo-rm-05cxDeA-tT0ZRglKrOPkdTeqIDb_OEM=s0"
    }] // 641 more results...
  }, {
    "name": "z6",
    "width": 221,
    "height": 180,
    "tiles": [{
      "x": 0,
      "y": 0,
      "url": "http://lh5.ggpht.com/QW85I8bF1SapVN1Noq8rl3NxXt0A5Wc1ab97rjI6RZ0_H-8v-SnMp-wRVXM7apOl7g0BgTcinuvP-1sTguW52K5iWBA=s0"
    }]
  }, {
    "name": "z5",
    "width": 442,
    "height": 360,
    "tiles": [{
      "x": 0,
      "y": 0,
      "url": "http://lh4.ggpht.com/Bx9vzycaNg7wX_uDiQy7QL0UN8CNxJWvfUBSxydXGYuqMjxqPr7m7iuCzP7AvNVLmOcrNni6i5nDr3hzr7f4_TKCuBN2=s0"
    }]
  }]
}
{% endhighlight %}

As you can see, this API returns a list of `levels`. These levels have a number of `tiles`. The tiles form the full image. You can choose the right level by using the width and height. They describe the total resolution of the chosen level. You can also select a level by name. Level `z0` contains the largest available image and `z6` the smallest.

When you have chosen a level you can construct the image by positioning the tiles. X and Y describe the horizontal and vertical position of the image.

See the [demo's page](demos) for an example.


## Content pages
`GET /api/pages/[culture]/[slug]` returns all public data of a content page as found on the website.

<table>
  <thead>
    <tr>
      <th>Parameter</th>
      <th>Format</th>
      <th>Notes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>culture</code></td>
      <td><code>nl</code> / <code>en</code></td>
      <td>The language of the page</td>
    </tr>
    <tr>
      <td><code>slug</code></td>
      <td><code>a-z|0-9|-/</code></td>
      <td>The slug that identifies the page. You can find this in the url of the page itself. For the <a href="https://www.rijksmuseum.nl/en/rijksstudio">explore the collection page</a> this is: <code>rijksstudio</code>.
    </td>
    </tr>
  </tbody>
</table>

### Request
```
https://www.rijksmuseum.nl/api/pages/nl/rijksstudio/kunstenaars/rembrandt-van-rijn?key=[API_KEY]&format=json
```

### Response
{% highlight javascript %}
{
  "elapsedMilliseconds": 15,
  "contentPage": {
    "thumbnailLandscape": {
      "name": "SK-C-5-thumblandscape",
      "url": "http://lh4.ggpht.com/Sks__T1Smc7LY_GwCCNpe7a2ldFc0LobT-vXVbwF0zg8rGRtZ27a-K0Ajlekr2INt3xfXD98exLrhfq7BDlsWFfeflNO=s0"
    },
    "inOverview": true,
    "isHighlightedOnOverview": true,
    "artistBio": null,
    "maker": {
      "name": "Rembrandt Harmensz. van Rijn",
      "unFixedName": "Rembrandt Harmensz. van Rijn",
      "placeOfBirth": "Leiden",
      "dateOfBirth": "1606-07-15",
      "dateOfBirthPrecision": null,
      "dateOfDeath": "1669-10-08",
      "dateOfDeathPrecision": null,
      "placeOfDeath": "Amsterdam",
      "occupation": [
        "prentmaker",
        "tekenaar",
        "schilder"
      ],
      "roles": [
        "schilder"
      ],
      "nationality": "Noord-Nederlands",
      "biography": "Rembrandt Harmensz. van Rijn (1606-1669) is ongetwijfeld de bekendste Nederlandse schilder uit de 17de eeuw. Hij werd geboren in Leiden. Hij ging daar in de leer bij Jacob van Swanenburch. Bij Pieter Lastman in Amsterdam maakte hij vervolgens kennis met de sterke licht-donkercontrasten in het werk van Caravaggio. Terug in Leiden vestigde hij zich met Jan Lievens als zelfstandig schilder. Gerard Dou was zijn eerste leerling. In 1631 verhuisde hij naar Amsterdam. Hij kreeg steeds meer opdrachten voor portretten en had talloze leerlingen onder wie Ferdinand Bol en Govert Flinck. [Rijkscanon 2007]",
      "productionPlaces": [],
      "schoolStyles": [],
      "qualification": null
    },
    "subject": "Rembrandt Harmensz. van Rijn",
    "callToAction": "Alle werken",
    "callToActionQuery": "?s=objecttype&p=1&ps=12&f.principalMaker.sort=Rembrandt%20Harmensz.%20van%20Rijn",
    "artObjectSet": [
      "SK-A-4691",
      "SK-C-5",
      "SK-C-216",
      "SK-C-597",
      "SK-A-4050",
      "SK-C-6",
      "SK-A-4885",
      "SK-A-3981",
      "SK-A-3340",
      "SK-A-3982",
      "SK-A-1935",
      "SK-A-4674",
      "SK-A-4833",
      "SK-A-4057",
      "SK-A-4717",
      "SK-A-3276",
      "SK-A-3137",
      "SK-A-3477",
      "SK-A-3138",
      "SK-A-3066",
      "RP-T-1961-81",
      "RP-P-OB-601"
    ],
    "mediaBlocks": [],
    "artobjects_on_this_page": [
      "SK-C-5",
      "SK-A-4691",
      "SK-C-216",
      "SK-C-597",
      "SK-A-4050",
      "SK-C-6",
      "SK-A-4885",
      "SK-A-3981",
      "SK-A-3340",
      "SK-A-3982",
      "SK-A-1935",
      "SK-A-4674",
      "SK-A-4833",
      "SK-A-4057",
      "SK-A-4717",
      "SK-A-3276",
      "SK-A-3137",
      "SK-A-3477",
      "SK-A-3138",
      "SK-A-3066",
      "RP-T-1961-81",
      "RP-P-OB-601"
    ],
    "id": "nl-b795083b-c053-4cc2-8e78-752a0919da5d",
    "guid": "b795083b-c053-4cc2-8e78-752a0919da5d",
    "lang": "nl",
    "compactHeader": false,
    "shortcutKeywords": [],
    "otherLangs": [
      "en"
    ],
    "headerImage": "http://lh6.ggpht.com/UoWlbtkM-hOPv0avneJdvq878asW_4G1aJ3T2M8dJujGkXplrRLNVikh9C4QPyZsOAdRPMGGJwlFRRFzlY7lMdTgJbc=s0",
    "thumbnail": "http://lh5.ggpht.com/L8HzuruPR6HqTYWiUaYjpXNc1PgPrneq9UAco8I0IANQMdQTtyAEz6vcGtB6UvSNOVap50ohPTun1V_MoyIwfEI3Tw=s0",
    "title": "Rembrandt Harmensz. van Rijn",
    "description": null,
    "body": {
      "markdown": "## Rembrandt van Rijn (1606-1669) \r\n\r\nRembrandt van Rijn werd als molenaarszoon geboren in Leiden. Na de Latijnse school schreven zijn ouders hem in 1620 in aan de universiteit. Rembrandt haakte al snel af. Hij werd schildersleerling bij Jacob van Swanenburch in Leiden en daarna bij Pieter Lastman in Amsterdam. Terug in Leiden vestigde hij zich, met Jan Lievens, als zelfstandig schilder. In die tijd schilderde Rembrandt veel bijbeltaferelen in een precieze stijl met bonte kleuren. \r\n\r\nIn 1631 verhuisde hij naar Amsterdam, waar hij veel portretopdrachten kreeg. Onder zijn vele leerlingen waren Ferdinand Bol, Govert Flinck en Carel Fabritius. In Rembrandts eigen werk werd het licht-donkercontrast steeds sterker, de toets losser, de composities dramatischer. Naast portretten schilderde hij veel historiestukken en maakte etsen en tekeningen. \r\n\r\nRembrandt trouwde in 1634 met Saskia Uylenburgh. In 1641 werd hun zoon Titus geboren, een jaar later stierf Saskia. Met Hendrickje Stoffels kreeg Rembrandt in 1654 een dochter. Hij had toen al hoge schulden en moest huis en bezit verkopen. Hij stierf in 1669 en werd begraven in de Amsterdamse Westerkerk.\r\n",
      "html": "<h2>Rembrandt van Rijn (1606-1669)</h2>\n\n<p>Rembrandt van Rijn werd als molenaarszoon geboren in Leiden. Na de Latijnse school schreven zijn ouders hem in 1620 in aan de universiteit. Rembrandt haakte al snel af. Hij werd schildersleerling bij Jacob van Swanenburch in Leiden en daarna bij Pieter Lastman in Amsterdam. Terug in Leiden vestigde hij zich, met Jan Lievens, als zelfstandig schilder. In die tijd schilderde Rembrandt veel bijbeltaferelen in een precieze stijl met bonte kleuren. </p>\n\n<p>In 1631 verhuisde hij naar Amsterdam, waar hij veel portretopdrachten kreeg. Onder zijn vele leerlingen waren Ferdinand Bol, Govert Flinck en Carel Fabritius. In Rembrandts eigen werk werd het licht-donkercontrast steeds sterker, de toets losser, de composities dramatischer. Naast portretten schilderde hij veel historiestukken en maakte etsen en tekeningen. </p>\n\n<p>Rembrandt trouwde in 1634 met Saskia Uylenburgh. In 1641 werd hun zoon Titus geboren, een jaar later stierf Saskia. Met Hendrickje Stoffels kreeg Rembrandt in 1654 een dochter. Hij had toen al hoge schulden en moest huis en bezit verkopen. Hij stierf in 1669 en werd begraven in de Amsterdamse Westerkerk.</p>\n"
    },
    "createdOn": "0001-01-01T00:00:00Z",
    "updatedOn": "2013-02-11T13:46:38.6078522Z"
  },
  "similarPages": null
}
{% endhighlight %}


## Usersets
`GET /api/[culture]/usersets` shows the sets made by Rijksstudio users. The following parameters are supported:

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
      <td><code>culture</code></td>
      <td><code>nl</code> / <code>en</code></td>
      <td>The language of the page</td>
    </tr>
    <tr>
      <td><code>page</code></td>
      <td><code>0-n</code></td>
      <td><code>0</code></td>
      <td>The result page to fetch. Note that <code>p * ps</code> cannot exceed 10.000.</td>
    </tr>
    <tr>
      <td><code>pageSize</code></td>
      <td><code>1-100</code></td>
      <td><code>10</code></td>
      <td>The number of results per page</td>
    </tr>
  </tbody>
</table>

### Request
```
https://www.rijksmuseum.nl/api/nl/usersets?key=[API_KEY]&format=json&page=2
```

### Response
{% highlight javascript %}
{
  "count": 97957,
  "elapsedMilliseconds": 631,
  "userSets": [
    {
      "links": {
        "self": "https://www.rijksmuseum.nl/api/usersets/123-setname-3",
        "web": "https://www.rijksmuseum.nl/nl/mijn/verzamelingen/321--john/setname-3"
      },
      "id": "123-setname-3",
      "count": 25,
      "type": "Default",
      "name": "setname (3)",
      "slug": "setname-3",
      "description": null,
      "user": {
        "id": 321,
        "name": "John",
        "lang": "nl",
        "avatarUrl": null,
        "headerUrl": null,
        "initials": "B"
      },
      "createdOn": "2012-11-02T12:28:21.9070376Z",
      "updatedOn": "2013-04-10T10:50:21.7559145Z"
    },
    // more results...
  ]
}
{% endhighlight %}



## Userset details
`GET /api/[culture]/usersets/[id]` gives more details about a set. The id of a set is composed of a user id, dash and name of set. You can retrieve id's from the /api/usersets.

<table>
  <thead>
    <tr>
      <th>Parameter</th>
      <th>Format</th>
      <th>Notes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>culture</code></td>
      <td><code>nl</code> / <code>en</code></td>
      <td>The language of the set</td>
    </tr>
    <tr>
      <td><code>id</code></td>
      <td><code>0-9</code></td>
      <td>The ID of the set</td>
    </tr>
    <tr>
      <td><code>page</code></td>
      <td><code>0-n</code></td>
      <td><code>0</code></td>
      <td>The result page to fetch</td>
    </tr>
    <tr>
      <td><code>pageSize</code></td>
      <td><code>1-100</code></td>
      <td><code>25</code></td>
      <td>The number of results per page</td>
    </tr>
  </tbody>
</table>

### Request
```
https://www.rijksmuseum.nl/api/nl/usersets/1836065-meestermatches?key=[API_KEY]&format=json
```

### Response
{% highlight javascript %}
{
  "elapsedMilliseconds": 505,
  "userSet": {
    "links": {
      "overview": "https://www.rijksmuseum.nl/api/usersets",
      "web": "https://www.rijksmuseum.nl/nl/mijn/verzamelingen/321--john/setname-3"
    },
    "id": "123-setname-3",
    "count": 25,
    "type": "Default",
    "name": "setname (3)",
    "slug": "setname-3",
    "description": null,
    "user": {
      "id": 321,
      "name": "John",
      "lang": "nl",
      "avatarUrl": null,
      "headerUrl": null,
      "initials": "B"
    },
    "setItems": [
      {
        "links": {
          "artobject": "https://www.rijksmuseum.nl/api/nl/collection/SK-A-3148",
          "web": "https://www.rijksmuseum.nl/nl/collection/SK-A-3148"
        },
        "id": "8c6e3ec4-08d9-4547-b72a-36907c0a3823",
        "objectNumber": "SK-A-3148",
        "relation": "None",
        "relationDescription": "Held",
        "cropped": false,
        "cropX": 0,
        "cropY": 0,
        "cropWidth": 0,
        "cropHeight": 0,
        "origWidth": 0,
        "origHeight": 0,
        "image": {
          "guid": "6d40dc7d-e58c-4e13-812d-60cff190a3d5",
          "parentObjectNumber": "SK-A-3148",
          "cdnUrl": "http://lh4.ggpht.com/X6E9IJ33ioVI1W7x0XgDedCmAu5NizMlLuX2f6gSgmpFqMxCCU1qOSCOqc2ORrLw-nHLtaph1zStxZFKKWqlnRU1IUw=s0",
          "cropX": 0,
          "cropY": 0,
          "width": 1824,
          "height": 2500,
          "offsetPercentageX": 50,
          "offsetPercentageY": 36
        }
      },
      // more results...
    ],
    "createdOn": "2012-11-02T12:28:21.9070376Z",
    "updatedOn": "2013-04-10T10:50:21.7559145Z"
  }
}
{% endhighlight %}




## Events calendar
`GET /api/[culture]/agenda/[date]` shows all events for the given date.

<table>
  <thead>
    <tr>
      <th>Parameter</th>
      <th>Format</th>
      <th>Notes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>culture</code></td>
      <td><code>nl</code> / <code>en</code></td>
      <td>The language of the events</td>
    </tr>
    <tr>
      <td><code>date</code></td>
      <td><code>yyyy-mm-dd</code></td>
      <td>The date for which to fetch the events</td>
    </tr>
  </tbody>
</table>

### Request
```
https://www.rijksmuseum.nl/api/nl/agenda/2018-05-31?key=[API_KEY]&format=json
```

### Response
{% highlight javascript %}
{
  "elapsedMilliseconds": 296,
  "options": [
    {
      "links": {
        "availability": "https://www.rijksmuseum.nl/api/nl/agenda/2013-10-18/expostition/0ee170d3-9604-48ac-b15f-014d911bf065/availability/e2b108b3-52b0-4a89-ac64-19514f8c5434",
        "web": "https://www.rijksmuseum.nl/nl/groepsreservering/deeplink?groupTypeId=a66a5578-6d5b-41cb-a714-f1b90b5a172c&expositionTypeId=18a54ce0-1f09-45ec-924f-59bbdeb30ba8&expositionId=0ee170d3-9604-48ac-b15f-014d911bf065&expositionPeriodId=e2b108b3-52b0-4a89-ac64-19514f8c5434&shortdate=2013-10-18"
      },
      "id": "0ee170d3-9604-48ac-b15f-014d911bf065-e2b108b3-52b0-4a89-ac64-19514f8c5434",
      "lang": "nl",
      "date": "2013-10-18T00:00:00Z",
      "period": {
        "id": "e2b108b3-52b0-4a89-ac64-19514f8c5434",
        "startDate": "2013-10-18T10:30:00Z",
        "endDate": "2013-10-18T11:30:00Z",
        "current": 0,
        "maximum": 15,
        "remaining": 15,
        "code": null,
        "text": "10:30 - 11:30"
      },
      "exposition": {
        "id": "0ee170d3-9604-48ac-b15f-014d911bf065",
        "name": "Familierondleiding Met sprongen vooruit (instap)",
        "description": "Ga met het hele gezin op ontdekkingsreis langs de hoogtepunten uit de Nederlandse kunst en geschiedenis, en maak kennis met de uitvindingen van onze voorvaders. De rondleiding start bij de Informatiebalie in het Atrium van het museum. U kunt zich voor aanvang van de rondleiding daar melden.",
        "code": "E100000",
        "price": {
          "id": "c0367018-6e1f-47f4-9c2f-901b9ea6887b",
          "calculationType": 2,
          "amount": 5.00
        }
      },
      "groupType": {
        "type": "GroupTypeRef",
        "guid": "a66a5578-6d5b-41cb-a714-f1b90b5a172c",
        "friendlyName": "Families en Kinderen"
      },
      "pageRef": {
        "title": "Familierondleiding Met sprongen vooruit",
        "url": "https://www.rijksmuseum.nl/nl/met-kinderen-klas-of-groep/families-en-kinderen/familierondleiding-met-sprongen-vooruit"
      },
      "expositionType": {
        "type": "ExpositionTypeRef",
        "guid": "18a54ce0-1f09-45ec-924f-59bbdeb30ba8",
        "friendlyName": "Familie activiteiten"
      }
    },
    // more results...
  ]
}
{% endhighlight %}



## Calendar event availability
`GET /api/[culture]/agenda/[date]/exposition/[exposition-id]/availability/[period-id]` gives the availability details for a specific event. The ID's of the events are found in the Events API.

<table>
  <thead>
    <tr>
      <th>Parameter</th>
      <th>Format</th>
      <th>Notes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>culture</code></td>
      <td><code>nl</code> / <code>en</code></td>
      <td>The language</td>
    </tr>
    <tr>
      <td><code>date</code></td>
      <td><code>yyyy-mm-dd</code></td>
      <td>The date of the event</td>
    </tr>
    <tr>
      <td><code>exposition-id</code></td>
      <td><code>a-z|0-9</code></td>
      <td>The ID of the event. (all events are expositions)</td>
    </tr>
    <tr>
      <td><code>period-id</code></td>
      <td><code>a-z|0-9</code></td>
      <td>The ID of the period</td>
    </tr>
  </tbody>
</table>

### Request
```
https://www.rijksmuseum.nl/api/nl/agenda/2018-05-31/expostition/5d63626e-7f05-e711-80cd-5820b1e20440/availability/afe24e88-8205-e711-80cd-5820b1e20440?key=[API_KEY]&format=json
```

### Response
{% highlight javascript %}
{
  "elapsedMilliseconds": 155,
  "total": 15,
  "available": 11
}
{% endhighlight %}
