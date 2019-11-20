---
layout: default
title: API
nav_order: 1
parent: User-generated content
---

# User-generated content APIs
These APIs give access to sets of objects created by users in [Rijksstudio](https://www.rijksmuseum.nl/en/rijksstudio). The [Usersets API](#usersets-api) provides an overview of available sets. The [Userset Details API](#userset-details-api) returns details about a set, including the list of objects.

## Access to APIs
To start using the user generated content, you first need to obtain an API key by registering for a [Rijksstudio account](https://www.rijksmuseum.nl/en/rijksstudio). You will be given a key instantly upon request, which you can find at the advanced settings of your Rijksstudio account.

## Usersets API
`GET /api/[culture]/usersets` lists the sets made by Rijksstudio users. The following parameters are supported:

| Parameter | Format                   | Default | Notes                                                              |
|:----------|:-------------------------|:--------|:-------------------------------------------------------------------|
| `key`     | `a-z|0-9`                |         | Your [API-key](#access-to-apis), mandatory for every request.      |
| `format`  | `json` / `jsonp` / `xml` | `json`  | The format of the result.                                          |
| `culture` | `nl` / `en`              |         | The language of the page.                                          |
| `page`    | `0-n`                    | `0`     | The result page to fetch. Note that `p * ps` cannot exceed 10.000. |
| `pageSize`| `1-100`                  | `10`    | The number of results per page.                                    |

### Example request Usersets API
```http
https://www.rijksmuseum.nl/api/nl/usersets?key=[api-key]&format=json&page=2
```

### Example response Usersets API
```json
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
```


## Userset Details API
`GET /api/[culture]/usersets/[set-id]` gives more details about a set. The id of a set is composed of a user id, dash and name of set. You can retrieve id's from the [Usersets API](#usersets-api).

| Parameter | Format                   | Default | Notes                                                         |
|:----------|:-------------------------|:--------|:--------------------------------------------------------------|
| `key`     | `a-z|0-9`                |         | Your [API-key](#access-to-apis), mandatory for every request. |
| `format`  | `json` / `jsonp` / `xml` | `json`  | The format of the result.                                     |
| `culture` | `nl` / `en`              |         | The language of the set.                                      |
| `id`      | `0-9`                    |         | The ID of the set.                                            |
| `page`    | `0-n`                    | `0`     | The result page to fetch.                                     |
| `pageSize`| `1-100`                  | `25`    | The number of results per page.                               |

### Example request Userset Details API
```http
https://www.rijksmuseum.nl/api/nl/usersets/1836065-meestermatches?key=[api-key]&format=json
```

### Example response Userset Details API
```json
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
```
