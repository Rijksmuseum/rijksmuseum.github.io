---
layout: default
title: API
nav_order: 1
parent: Object metadata
---

# Object metadata APIs
The object metadata APIs make the power of the award-winning [Rijksmuseum website](https://www.rijksmuseum.nl) directly accessible to developers. [Searching the collection](#collection-api) through the API offers a wide range of interesting possibilities, as do the [tiled images](#collection-image-api) used to zoom in to close-ups of objects. The JSON-based service is so easy to use that you can create an application using the Rijksmuseum’s rich and [freely accessible content](https://www.rijksmuseum.nl/en/data/policy) in no time.


## Access to APIs
To start using the data and images, you first need to obtain an API key by registering for a [Rijksstudio account](https://www.rijksmuseum.nl/en/rijksstudio). You will be given a key instantly upon request, which you can find at the advanced settings of your Rijksstudio account.


## Collection API
`GET /api/[culture]/collection` gives access to the collection with brief information about each object. The results are split up in result pages. By using the `p` and `ps` parameters you can fetch more results, up to a total of 10,000. All of the other parameters are identical to the [advanced search page](https://www.rijksmuseum.nl/en/search/advanced) on the Rijksmuseum website. You can use that page to find out what's the best query to use.

| Parameter                  | Format                   | Default | Notes                                                                         |
|:---------------------------|:-------------------------|:--------|:------------------------------------------------------------------------------|
| `key`                      | `a-z|0-9`                |         | Your [API-key](#access-to-apis), mandatory for every request.                 |
| `format`                   | `json` / `jsonp` / `xml` | `json`  | The format of the result.                                                     |
| `culture`                  | `nl` / `en`              |         | The language to search in (and of the results).                               |
| `p`                        | `0-n`                    | `0`     | The result page. Note that `p * ps` cannot exceed 10,000.                     |
| `ps`                       | `1-100`                  | `10`    | The number of results per page.                                               |
| `q`                        | `a-z`                    |         | The search terms that need to occur in one of the fields of the object data.  |
| `involvedMaker`            | `a-z`                    |         | Object needs to be made by this agent.                                        |
| `type`                     | `a-z`                    |         | The type of the object.                                                       |
| `material`                 | `a-z`                    |         | The material of the object.                                                   |
| `technique`                | `a-z`                    |         | The technique used to make the object.                                        |
| `f.dating.period`          | `0-21`                   |         | The century in which the object is made.                                      |
| `f.normalized32Colors.hex` | `Color HEX`              |         | Colors found in the images (mind: The `#` in #FF0000 should be url-encoded!). |
| `imgonly`                  | `True` / `False`         | `False` | Only give results for which an image is available or not.                     |
| `toppieces`                | `True` / `False`         | `False` | Only give works that are top pieces.                                          |
| `s`                        | `relevance`              |         | Sort results on relevance.                                                    |
|                            | `objecttype`             |         | Sort results on type.                                                         |
|                            | `chronologic`            |         | Sort results chronologically (oldest first).                                  |
|                            | `achronologic`           |         | Sort results chronologically (newest first).                                  |
|                            | `artist`                 |         | Sort results on artist (a-z).                                                 |
|                            | `artistdesc`             |         | Sort results on artist (z-a).                                                 |

### Example request Collection API
```http
https://www.rijksmuseum.nl/api/nl/collection?key=[api-key]&involvedMaker=Rembrandt+van+Rijn
```

### Example response Collection API
```json
{
  "elapsedMilliseconds": 0,
  "count": 3491,
  "artObjects": [
    {
      "links": {
        "self": "http://www.rijksmuseum.nl/api/nl/collection/SK-C-5",
        "web": "http://www.rijksmuseum.nl/nl/collectie/SK-C-5"
      },
      "id": "nl-SK-C-5",
      "objectNumber": "SK-C-5",
      "title": "De Nachtwacht",
      "hasImage": true,
      "principalOrFirstMaker": "Rembrandt van Rijn",
      "longTitle": "De Nachtwacht, Rembrandt van Rijn, 1642",
      "showImage": true,
      "permitDownload": true,
      "webImage": {
          "guid": "aa08df9c-0af9-4195-b31b-f578fbe0a4c9",
          "offsetPercentageX": 0,
          "offsetPercentageY": 1,
          "width": 2500,
          "height": 2034,
          "url":"https://lh3.googleusercontent.com/J-mxAE7CPu-DXIOx4QKBtb0GC4ud37da1QK7CzbTIDswmvZHXhLm4Tv2-1H3iBXJWAW_bHm7dMl3j5wv_XiWAg55VOM=s0"
      },
      "headerImage": {
        "guid": "29a2a516-f1d2-4713-9cbd-7a4458026057",
        "offsetPercentageX": 0,
        "offsetPercentageY": 0,
        "width": 1920,
        "height": 460,
        "url": "https://lh3.googleusercontent.com/O7ES8hCeygPDvHSob5Yl4bPIRGA58EoCM-ouQYN6CYBw5jlELVqk2tLkHF5C45JJj-5QBqF6cA6zUfS66PUhQamHAw=s0"
      },
      "productionPlaces": ["Amsterdam"]
    },
    // more results...
  ]
}
```


## Collection Details API
`GET /api/[culture]/collection/[object-number]` gives more details of an object. Object numbers can be obtained from the results given in the [Collection API](#collection-api).

| Parameter       | Format                   | Default | Notes                                                         |
|:----------------|:-------------------------|:--------|:--------------------------------------------------------------|
| `key`           | `a-z|0-9`                |         | Your [API-key](#access-to-apis), mandatory for every request. |
| `format`        | `json` / `jsonp` / `xml` | `json`  | The format of the result.                                     |
| `culture`       | `nl` / `en`              |         | The language of the page.                                     |
| `object-number` | `a-z|0-9|-`              |         | The identifier of the object (case-sensitive).                |

### Example request Collection Details API
```http
https://www.rijksmuseum.nl/api/nl/collection/SK-C-5?key=[api-key]
```

### Example response Collection Details API
```json
{
  "elapsedMilliseconds": 219,
  "artObject": {  
    "links": {  
      "search":"http://www.rijksmuseum.nl/api/nl/collection"
    },
    "id": "nl-SK-C-5",
    "priref": "5216",
    "objectNumber": "SK-C-5",
    "language": "nl",
    "title": "De Nachtwacht",
    "copyrightHolder": null,
    "webImage":{  
      "guid": "aa08df9c-0af9-4195-b31b-f578fbe0a4c9",
      "offsetPercentageX": 50,
      "offsetPercentageY": 100,
      "width": 2500,
      "height": 2034,
     "url": "https://lh3.googleusercontent.com/J-mxAE7CPu-DXIOx4QKBtb0GC4ud37da1QK7CzbTIDswmvZHXhLm4Tv2-1H3iBXJWAW_bHm7dMl3j5wv_XiWAg55VOM=s0"
    },
    "colors": [  
      {  
        "percentage": 81,
        "hex": "#261808"
      },
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
      {  
        "percentage": 81,
        "hex": "#000000"
      },
      // more results...
    ],
    "normalized32Colors": [  
      {  
        "percentage": 81,
        "hex": "#000000"
      },
      // more results...
    ],
    "titles": [  
       "Officieren en andere schutters van wijk II in Amsterdam, onder leiding van kapitein Frans Banninck Cocq en luitenant Willem van Ruytenburch, bekend als ‘De Nachtwacht’",
         "Het korporaalschap van kapitein Frans Banninck Cocq en luitenant Willem van Ruytenburch, bekend als de 'Nachtwacht'"
    ],
    "description": "Officieren en andere schutters van wijk II in Amsterdam onder leiding van kapitein Frans Banninck Cocq en luitenant Willem van Ruytenburch, sinds het einde van de 18de eeuw bekend als ‘De Nachtwacht’. Schutters van de Kloveniersdoelen uit een poort naar buiten tredend. Op een schild aangebracht naast de poort staan de namen van de afgebeelde personen: Frans Banning Cocq, heer van purmerlant en Ilpendam, Capiteijn Willem van Ruijtenburch van Vlaerdingen, heer van Vlaerdingen, Lu[ij]tenant, Jan Visscher Cornelisen Vaendrich, Rombout Kemp Sergeant, Reijnier Engelen Sergeant, Barent Harmansen, Jan Adriaensen Keyser, Elbert Willemsen, Jan Clasen Leydeckers, Jan Ockersen, Jan Pietersen bronchorst, Harman Iacobsen wormskerck, Jacob Dircksen de Roy, Jan vander heede, Walich Schellingwou, Jan brugman, Claes van Cruysbergen, Paulus Schoonhoven. De schutters zijn gewapend met onder anderen pieken, musketten en hellebaarden. Rechts de tamboer met een grote trommel. Tussen de soldaten links staat een meisje met een dode kip om haar middel, rechts een blaffende hond. Linksboven de vaandrig met de uitgestoken vaandel.",
    "labelText": null,
    "objectTypes": [  
      "schilderij"
    ],
    "objectCollection": [  
      "schilderijen"
    ],
    "makers": [ ],
    "principalMakers": [  
      {  
        "name": "Rembrandt van Rijn",
        "unFixedName": "Rijn, Rembrandt van",
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
        "roles":[  
          "schilder"
        ],
        "nationality": "Noord-Nederlands",
        "biography": null,
        "productionPlaces": [  
          "Amsterdam"
        ],
        "qualification": null
      }
    ],
    "plaqueDescriptionDutch": "Rembrandts beroemdste en grootste doek werd gemaakt voor de Kloveniersdoelen. Dit was een van de verenigingsgebouwen van de Amsterdamse schutterij, de burgerwacht van de stad. \r\nRembrandt was de eerste die op een groepsportret de figuren in actie weergaf. De kapitein, in het zwart, geeft zijn luitenant opdracht dat de compagnie moet gaan marcheren. De schutters stellen zich op. Met behulp van licht vestigde Rembrandt de aandacht op belangrijke details, zoals het handgebaar van de kapitein en het kleine meisje op de achtergrond. Zij is de mascotte van de schutters.",
    "plaqueDescriptionEnglish": "Rembrandt’s largest, most famous canvas was made for the Arquebusiers guild hall. This was one of several halls of Amsterdam’s civic guard, the city’s militia and police. \r\nRembrandt was the first to paint figures in a group portrait actually doing something. The captain, dressed in black, is telling his lieutenant to start the company marching. The guardsmen are getting into formation. Rembrandt used the light to focus on particular details, like the captain’s gesturing hand and the young girl in the foreground. She was the company mascot.\r\n",
    "principalMaker": "Rembrandt van Rijn",
    "artistRole": null,
    "associations": [ ],
    "acquisition": {  
      "method": "bruikleen",
      "date": "1808-01-01T00:00:00",
      "creditLine": "Bruikleen van de gemeente Amsterdam"
    },
    "exhibitions": [ ],
    "materials": [
      "doek",
      "olieverf"
    ],
    "techniques":[ ],
    "productionPlaces": [  
      "Amsterdam"
    ],
    "dating":{  
      "presentingDate": "1642",
      "sortingDate": 1642,
      "period": 17,
      "yearEarly": 1642,
      "yearLate": 1642
    },
    "classification": {  
      "iconClassIdentifier": [  
        "45(+26)",
        // more results...
      ],
      // more results...
    },
    "hasImage": true,
    "historicalPersons": [  
      "Banninck Cocq, Frans",
      // more results...
    ],
    "inscriptions": [ ],
    "documentation": [  
      "The Rembrandt Database,  Object information, Rembrandt,  Civic guardsmen of Amsterdam under command of Banninck Cocq,  dated 1642, Rijksmuseum, Amsterdam, inv. no. SK-C-5, http://www.rembrandtdatabase.org/Rembrandt/painting/3063/civic-guardsmen-of-amsterdam-under-command-of-banninck-cocq, accessed 2016 February 01",
        // more results...
    ],
    "catRefRPK": [ ],
    "principalOrFirstMaker": "Rembrandt van Rijn",
    "dimensions": [  
      {  
        "unit": "cm",
        "type": "hoogte",
        "part": null,
        "value": "379,5"
      },
      // more results...
    ],
    "physicalProperties": [ ],
    "physicalMedium": "olieverf op doek",
    "longTitle": "De Nachtwacht, Rembrandt van Rijn, 1642",
    "subTitle": "h 379,5cm × b 453,5cm × g 337kg",
    "scLabelLine": "Rembrandt van Rijn (1606–1669), olieverf op doek, 1642",
    "label": {  
      "title": "De Nachtwacht",
      "makerLine": "Rembrandt van Rijn (1606–1669), olieverf op doek, 1642",
      "description": "Rembrandts beroemdste en grootste schilderij werd gemaakt voor de Kloveniersdoelen. Dit was een van de drie hoofdkwartieren van de Amsterdamse schutterij, de burgerwacht van de stad. Rembrandt was de eerste die op een schuttersstuk alle figuren in actie weergaf. De kapitein, in het zwart, geeft zijn luitenant opdracht dat de compagnie moet gaan marcheren. De schutters stellen zich op. Met behulp van licht vestigde Rembrandt de aandacht op belangrijke details, zoals het handgebaar van de kapitein en het kleine meisje op de voorgrond. Zij is de mascotte van de schutters. De naam Nachtwacht is pas veel later ontstaan, toen men dacht dat het om een nachtelijk tafereel ging.",
      "notes": "Multimediatour, 500. Tekst aangeleverd door Jonathan Bikker.",
      "date": "2019-07-05"
    },
    "showImage": true,
    "location": "HG-2.31"
  },
  // more results...
}
```


## Collection Image API
`GET /api/[culture]/collection/[object-number]/tiles` gives all the information you need to show the image split up in tiles. This is used to implement the zoom functionality on the Rijksmuseum website. This specific API only supports the JSON format.

| Parameter       | Format      | Default | Notes                                                         |
|:----------------|:------------|:--------|:--------------------------------------------------------------|
| `key`           | `a-z|0-9`   |         | Your [API-key](#access-to-apis), mandatory for every request. |
| `object-number` | `a-z|0-9|-` |         | The identifier of the object (case-sensitive).                |

### Example request Collection Image API
```http
https://www.rijksmuseum.nl/api/nl/collection/SK-C-5/tiles?key=[api-key]
```

### Example response Collection Image API
```json
{
  "levels":[
    {
      "name":"z3",
      "width":1771,
      "height":1441,
      "tiles":[
        {
          "x":2,
          "y":2,
          "url":"http://lh3.googleusercontent.com/-I1HN0VxmDySYN5oCqaykuTRukdFh-JemILAmTvHtGsGnBm968CiQpxkfgqQZnbKD5bS1m0tGZYx7v8HFnWjE3kizw=s0"
        },
        // more results...
      ]
    }
    {
      "name":"z4",
      "width":885,
      "height":720,
      "tiles":[
        {
          "x":1,
          "y":0,
          "url":"http://lh3.googleusercontent.com/-fBdzIPG0qlGnIkqKUFaX3dAiEnC9jnfCIR9ib32M1xh7bPHuK6ZTJMxgwn8jYsvymdupCFdtm3vHJg-n10JuhBD7w=s0"
        },
        // more results...
      ]
    },
    // more results...
  ]
}
```

As you can see, this API returns a list of levels. These levels have a number of tiles. The tiles form the full image. You can choose the right level by using the width and height. They describe the total resolution of the chosen level. You can also select a level by name. Level `z0` contains the largest available image and `z6` the smallest.

When you have chosen a level you can construct the image by positioning the tiles. X and Y describe the horizontal and vertical position of the image.
