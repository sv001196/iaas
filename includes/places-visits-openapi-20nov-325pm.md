---
title: Places API
language_tabs:
  - shell: Shell
  - http: HTTP
  - javascript: JavaScript
  - javascript--nodejs: Node.JS
  - ruby: Ruby
  - python: Python
  - java: Java
  - go: Go
toc_footers: []
includes: []
search: true
highlight_theme: darkula
headingLevel: 2

---

<h1 id="places-api">Places API v1.0.0-oas3</h1>

> Scroll down for code samples, example requests and responses. Select a language for code samples from the tabs above or the mobile navigation menu.

Places API returns detailed information about the location of interest. A location of interest is represented by one of specific point co-ordinates (i.e longitude and latitude) or a bounded region (i.e polygon) or a  more complex polygon structure depicting interior and exterior edges.
PlacesAPI provides APIs to fetch the location of interest by passing various search criterion.

Base URLs:

* <a href="/">/</a>

Email: <a href="mailto:api@trufactor.io">Support</a> 
License: <a href="http://www.apache.org/licenses/LICENSE-2.0.html">Apache 2.0</a>

<h1 id="places-api-default">Default</h1>

## place_ids

<a id="opIdplace_ids"></a>

> Code samples

```shell
# You can also use wget
curl -X GET /places \
  -H 'Accept: application/json' \
  -H 'x-api-key: string'

```

```http
GET /places HTTP/1.1

Accept: application/json
x-api-key: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-api-key':'string'

};

$.ajax({
  url: '/places',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'x-api-key':'string'

};

fetch('/places',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'x-api-key' => 'string'
}

result = RestClient.get '/places',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'x-api-key': 'string'
}

r = requests.get('/places', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("/places");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "x-api-key": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/places", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /places`

*Returns the details of one or more places*

Pass one or more comma separated place ids to fetch the details of the places. A single request can return up to 50 place objects.

<h3 id="place_ids-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|x-api-key|header|string|true|Pass the API key|
|ids|query|string|false|Comma separated list of place ids. Up to 50 place ids can be passed. If this parameter is not specified, all the places available in the system will be returned in a paginated manner. To limit the number of places returned per request, specify the query parameter "limit".|
|limit|query|number|false|Limits the number of place objects returned per request. This parameter is used only when ids parameter is not specified in the request. If this parameter is not specified, the API will return 50 place objects per request.|

> Example responses

> Response object containing list of matching place details if the request is successful.

```json
{
  "id": "d290f1ee-6c54-4b01-90e6-d701748f0851",
  "name": "Louvre musuem",
  "categories": [
    {
      "id": "d290f1ee-6c54-4b01-90e6-d701748f0851",
      "name": "Arts & Entertainment",
      "link": "https://api.trufactor.com/categories/d290f1ee-6c54-4b01-90e6-d701748f0851"
    }
  ],
  "contact": {
    "email": [
      "ticket@louvre.fr"
    ]
  },
  "address": {
    "country_code": "FR",
    "country": "France",
    "county": "1st arrondissement",
    "city": "Paris",
    "zip_code": 75001,
    "steet_address": "Rue de Rivoli, 75001"
  },
  "geo": {
    "location": {
      "longitude": 48.51,
      "latitude": 2.2
    }
  }
}
```

> 400 Response

```json
{
  "error": {
    "code": "e3526",
    "message": "Invalid input parameter",
    "description": "Unsupported character(s) :) detected in input parameter \"ids\"",
    "doc_link": "http://doc.trufactor.com/error/e3526.html"
  }
}
```

<h3 id="place_ids-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Response object containing list of matching place details if the request is successful.|[inline_response_200](#schemainline_response_200)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad input parameter. When one of the passed ids is in invalid format (e.g in non UUID format) or when the ids are not sent at all, the server will respond with HTTP 400 status code. Also, if the query parameters "start", "end" are invalid, the request will be rejected with HTTP status code 400.|[inline_response_400](#schemainline_response_400)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|API key is missing or invalid|None|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Credits|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|
|400|X-Request-ID|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|
|401|WWW_Authenticate|string||none|

<aside class="success">
This operation does not require authentication
</aside>

## search_places

<a id="opIdsearch_places"></a>

> Code samples

```shell
# You can also use wget
curl -X GET /places/search \
  -H 'Accept: application/json' \
  -H 'x-api-key: string'

```

```http
GET /places/search HTTP/1.1

Accept: application/json
x-api-key: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-api-key':'string'

};

$.ajax({
  url: '/places/search',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'x-api-key':'string'

};

fetch('/places/search',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'x-api-key' => 'string'
}

result = RestClient.get '/places/search',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'x-api-key': 'string'
}

r = requests.get('/places/search', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("/places/search");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "x-api-key": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/places/search", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /places/search`

*Searches for the places by the name, business, categories, any of the address fields (city, county, zip) and the geographical co-ordinates.*

Seaches the places by name of the places, names of the businesses, categories of the places, address fields and the geographical co-ordinates.

<h3 id="search_places-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|x-api-key|header|string|true|Pass the API key|
|name|query|string|false|Search by name of the place. This search parameter is typically used to search the prominent places of interests. The returned response will contain results based on partial and exact match. To toggle off partial match, set the query parameter "exact-match" to 1.|
|text|query|string|false|Free form text input to search on any of the supported attributes of the place e.g Name, City, State, Zip, Name of the business|
|categories|query|string|false|Comma separated list of categories of the places.|
|location_type|query|string|false|Defines how the location information about the place is passed to the server. The API accepts one of - "place_id", an identifier of the place (refer /places/ API for the details) - "point", an array of longitude and latitude representing a point, typically the center point of the location of interest. Specify the query parameter "location.radius" to restrict the radius of the look up for locations of interest. - "polygon" an array of longitude and latitude tuples representing a bounded region|
|location|query|string|false|An object representing geographical information associated with a location of interest. This can be represented by a simple TruFactor place ID or a center point the location or a bounded region or by conventional geo name attributes (e.g city, state).|
|radius|query|number(float)|false|Filters the places falling within the bounded radius.|
|boundary|query|array[object]|false|Filters the places falling within the bounded polygon.|
|business.name|query|string|false|Filters the search result matching the name of the specified business|
|city|query|string|false|Full form city name. This field can be used in tandem with other query parameters such as "name", "text" to narrow down the search results.|
|state|query|string|false|Full form state name. This field can be used in tandem with other query parameters such as "name", "text" to narrow down the search results.|
|zip_code|query|string|false|Comma separated list of zip codes. This field can be used in tandem with other query parameters such as "name", "text" to narrow down the search results.|
|county|query|string|false|Comma separated list of counties. This field can be used in tandem with other query parameters such as "name", "text" to narrow down the search results.|
|limit|query|number|false|Limits the number of place objects returned per request. If limit is not specified, the API will return 50 place objects|
|exact_match|query|number(int32)|false|Set this parameter to 1 when you want to disable partial match in fields such as "name", "business.name", "city", "county", "state", "zip_code"|

#### Enumerated Values

|Parameter|Value|
|---|---|
|location_type|place_id|
|location_type|point|
|location_type|polygon|

> Example responses

> list of matching place details

```json
{
  "id": "d290f1ee-6c54-4b01-90e6-d701748f0851",
  "name": "Louvre musuem",
  "categories": [
    {
      "id": "d290f1ee-6c54-4b01-90e6-d701748f0851",
      "name": "Arts & Entertainment",
      "link": "https://api.trufactor.com/categories/d290f1ee-6c54-4b01-90e6-d701748f0851"
    }
  ],
  "contact": {
    "email": [
      "ticket@louvre.fr"
    ]
  },
  "address": {
    "country_code": "FR",
    "country": "France",
    "county": "1st arrondissement",
    "city": "Paris",
    "zip_code": 75001,
    "steet_address": "Rue de Rivoli, 75001"
  },
  "geo": {
    "location": {
      "longitude": 48.51,
      "latitude": 2.2
    }
  }
}
```

> 400 Response

```json
{
  "error": {
    "code": "e3526",
    "message": "Invalid input parameter",
    "description": "Unsupported character(s) :) detected in input parameter \"ids\"",
    "doc_link": "http://doc.trufactor.com/error/e3526.html"
  }
}
```

<h3 id="search_places-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|list of matching place details|[inline_response_200](#schemainline_response_200)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad input parameter. When one of the passed ids is in invalid format (e.g in non UUID format) or when the ids are not sent at all, the server will respond with HTTP 400 status code. Also, if the query parameters "start", "end" are invalid, the request will be rejected with HTTP status code 400.|[inline_response_400](#schemainline_response_400)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|API key is missing or invalid|None|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Credits|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|
|400|X-Request-ID|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|
|401|WWW_Authenticate|string||none|

<aside class="success">
This operation does not require authentication
</aside>

## get__visits_summary

> Code samples

```shell
# You can also use wget
curl -X GET /visits/summary \
  -H 'Accept: application/json' \
  -H 'x-api-key: string'

```

```http
GET /visits/summary HTTP/1.1

Accept: application/json
x-api-key: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-api-key':'string'

};

$.ajax({
  url: '/visits/summary',
  method: 'get',

  headers: headers,
  success: function(data) {
    console.log(JSON.stringify(data));
  }
})

```

```javascript--nodejs
const fetch = require('node-fetch');

const headers = {
  'Accept':'application/json',
  'x-api-key':'string'

};

fetch('/visits/summary',
{
  method: 'GET',

  headers: headers
})
.then(function(res) {
    return res.json();
}).then(function(body) {
    console.log(body);
});

```

```ruby
require 'rest-client'
require 'json'

headers = {
  'Accept' => 'application/json',
  'x-api-key' => 'string'
}

result = RestClient.get '/visits/summary',
  params: {
  }, headers: headers

p JSON.parse(result)

```

```python
import requests
headers = {
  'Accept': 'application/json',
  'x-api-key': 'string'
}

r = requests.get('/visits/summary', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("/visits/summary");
HttpURLConnection con = (HttpURLConnection) obj.openConnection();
con.setRequestMethod("GET");
int responseCode = con.getResponseCode();
BufferedReader in = new BufferedReader(
    new InputStreamReader(con.getInputStream()));
String inputLine;
StringBuffer response = new StringBuffer();
while ((inputLine = in.readLine()) != null) {
    response.append(inputLine);
}
in.close();
System.out.println(response.toString());

```

```go
package main

import (
       "bytes"
       "net/http"
)

func main() {

    headers := map[string][]string{
        "Accept": []string{"application/json"},
        "x-api-key": []string{"string"},
        
    }

    data := bytes.NewBuffer([]byte{jsonReq})
    req, err := http.NewRequest("GET", "/visits/summary", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /visits/summary`

*Returns the aggregated count of visitors and unique visitors that visited the given place of interests.*

Computes and returns the aggregated count of visitors and unique visitors that visited the given place of interest. Place of interest can be one or more TruFactor place id or a location co-ordinate of the place or a bounded region or a polygon.

<h3 id="get__visits_summary-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|x-api-key|header|string|true|Pass the API key|
|location_type|query|string|false|Defines how the location information about the place is passed to the server. The API accepts one of - "place_id", an identifier of the place (refer /places/ API for the details) - "point", an array of longitude and latitude representing a point, typically the center point of the location of interest. Specify the query parameter "location.radius" to restrict the radius of the look up for locations of interest. - "polygon" an array of longitude and latitude tuples representing a bounded region|
|location|query|string|false|An object representing geographical information associated with a location of interest. This can be represented by a simple TruFactor place ID or a center point the location or a bounded region or by conventional geo name attributes (e.g city, state).|
|business_id|query|string|false|none|
|category_ids|query|array[string]|false|none|
|start|query|number(int64)|false|none|
|end|query|number(int64)|false|none|

#### Enumerated Values

|Parameter|Value|
|---|---|
|location_type|place_id|
|location_type|point|
|location_type|polygon|

> Example responses

> 200 Response

```json
{
  "data": {
    "summary": {
      "visits_count": 302140,
      "unique_users_count": 132445
    },
    "extrapolated_summary": {
      "visits_count": 6002140,
      "unique_users_count": 121254,
      "error_metrics": {
        "visits_count": 1.3,
        "unique_users_count": 0.9
      }
    }
  }
}
```

<h3 id="get__visits_summary-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Response object. Typically, the status of the request is returned in HTTP status code. If the request is successful, the response object will contain "result" object. If the request did not succeed, the response will contain "error" object which will in turn contain the error code, message description and detailed description of the error for debugging.|[inline_response_200_1](#schemainline_response_200_1)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad input parameter. When the passed place_id is in invalid format (e.g in non UUID format) or when the place_id is not sent at all, the server will respond with HTTP 400 status code. Also, if the query parameters "start", "end" are invalid, the request will be rejected with HTTP status code 400.|[inline_response_400](#schemainline_response_400)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|Unauthorized access|None|
|429|[Too Many Requests](https://tools.ietf.org/html/rfc6585#section-4)|Raised when too many requests have been sent.|[inline_response_400](#schemainline_response_400)|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Credits|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|
|400|RequestId|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|
|401|RequestId|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|
|429|RequestId|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|

<aside class="success">
This operation does not require authentication
</aside>

# Schemas

<h2 id="tocSplace">Place</h2>

<a id="schemaplace"></a>

```json
{
  "id": "d290f1ee-6c54-4b01-90e6-d701748f0851",
  "name": "Louvre musuem",
  "parent_place_id": "string",
  "brands": [
    {
      "id": "59b6675b-660f-44c3-93e7-1c031758fb15",
      "name": "Toyota",
      "link": "https://api.trufactor.com/brands/59b6675b-660f-44c3-93e7-1c031758fb15"
    }
  ],
  "business": {
    "id": "eb3698d4-a27c-4d93-9f48-fb4355c0e63c",
    "name": "McDonalds",
    "link": "https://api.trufactor.com/businesses/eb3698d4-a27c-4d93-9f48-fb4355c0e63c"
  },
  "categories": [
    {
      "id": "152f84ff-1f88-4e04-a406-d1bd4358105b",
      "name": "Shopping mall",
      "link": "https://api.trufactor.com/categories/eb3698d4-a27c-4d93-9f48-fb4355c0e63c"
    }
  ],
  "contact": {
    "phone": [
      14153622004,
      14153622005
    ],
    "mobile": "[\"+14153622004\",\"+14153622005\"]",
    "email": [
      "hello@example.com",
      "feedback@example.com"
    ],
    "www": [
      "[\"https://www.example.com\"]"
    ]
  },
  "address": {
    "country_code": "US",
    "country": "USA, United States of America",
    "state_code": "Tx",
    "state": "Texas",
    "county": "Travis",
    "city": "Austin",
    "zip_code": "78701",
    "steet_address": "2100, Barton Springs Rd",
    "locality": "South Austin",
    "neighbourhood": "Barton Creek"
  },
  "geo": {
    "type": "point",
    "coordinates": [
      0
    ]
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string(uuid)|true|none|An unique Trufactor place identifier|
|name|string|true|none|Name of the place|
|parent_place_id|string(uuid)|false|none|Reference to parent Trufactor place identifier. This attribute is available when a place is contained within an another place. For example, a restaurant within a shopping mall.|
|brands|[[Place_brands](#schemaplace_brands)]|false|none|List of brands that this place is associated with.|
|business|[Place_business](#schemaplace_business)|false|none|The business that own this place or a tenant operating out of this place|
|categories|[[Place_categories](#schemaplace_categories)]|false|none|The Trufactor categories associated with this place|
|contact|[Contact](#schemacontact)|false|none|Object representing various contact attributes such as phone, mobile and email addresses.|
|address|[Address](#schemaaddress)|false|none|Object representing various address attributes of the place such as street, county, city, state and country.|
|geo|[Geo](#schemageo)|false|none|Object representing a point or a bounded region (i.e Polygon)|

<h2 id="tocScontact">Contact</h2>

<a id="schemacontact"></a>

```json
{
  "phone": [
    14153622004,
    14153622005
  ],
  "mobile": "[\"+14153622004\",\"+14153622005\"]",
  "email": [
    "hello@example.com",
    "feedback@example.com"
  ],
  "www": [
    "[\"https://www.example.com\"]"
  ]
}

```

*Object representing various contact attributes such as phone, mobile and email addresses.*

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|phone|[string]|false|none|List of phone numbers|
|mobile|string|false|none|List of mobile numbers|
|email|[string]|false|none|List of email addresses|
|www|[string]|false|none|List of web sites|

<h2 id="tocSaddress">Address</h2>

<a id="schemaaddress"></a>

```json
{
  "country_code": "US",
  "country": "USA, United States of America",
  "state_code": "Tx",
  "state": "Texas",
  "county": "Travis",
  "city": "Austin",
  "zip_code": "78701",
  "steet_address": "2100, Barton Springs Rd",
  "locality": "South Austin",
  "neighbourhood": "Barton Creek"
}

```

*Object representing various address attributes of the place such as street, county, city, state and country.*

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|country_code|string|false|none|Two or three digit short codes as defined in ISO 3166-1, 2 or 3 letter code, https://en.wikipedia.org/wiki/ISO_3166-1|
|country|string|false|none|Full form country name|
|state_code|string|false|none|Two or three digit short codes as defined in ISO 3166-2 https://en.wikipedia.org/wiki/ISO_3166-2|
|state|string|false|none|Full form state name|
|county|string|false|none|Full form county name|
|city|string|false|none|Name of the city|
|zip_code|string|false|none|Usually contains 5-8 digit numerical values|
|steet_address|string|false|none|Well formatted multi line stree addresses|
|locality|string|false|none|Officially recognised area within county or city|
|neighbourhood|string|false|none|Collaquially known area withing country or city or district|

<h2 id="tocSgeo">Geo</h2>

<a id="schemageo"></a>

```json
{
  "type": "point",
  "coordinates": [
    0
  ]
}

```

*Object representing a point or a bounded region (i.e Polygon)*

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|type|string|false|none|Supported values are "point" and "polygon"|
|coordinates|object|false|none|Either a point represented by an array of longitude and latitude or a bounded region represented by an array of longitude and latitude array|

*oneOf*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|[Point](#schemapoint)|false|none|none|

*xor*

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|» *anonymous*|[Polygon](#schemapolygon)|false|none|Describes a polygon i.e a list of longitude and latitude co-ordinates representing a bounded region|

#### Enumerated Values

|Property|Value|
|---|---|
|type|point|
|type|polygon|

<h2 id="tocSpoint">Point</h2>

<a id="schemapoint"></a>

```json
[
  0
]

```

### Properties

*None*

<h2 id="tocSpolygon">Polygon</h2>

<a id="schemapolygon"></a>

```json
[
  [
    55.2796,
    25.1988
  ],
  [
    52.2796,
    22.1988
  ]
]

```

*Describes a polygon i.e a list of longitude and latitude co-ordinates representing a bounded region*

### Properties

*None*

<h2 id="tocSinline_response_200">inline_response_200</h2>

<a id="schemainline_response_200"></a>

```json
{
  "data": [
    {
      "id": "d290f1ee-6c54-4b01-90e6-d701748f0851",
      "name": "Louvre musuem",
      "parent_place_id": "string",
      "brands": [
        {
          "id": "59b6675b-660f-44c3-93e7-1c031758fb15",
          "name": "Toyota",
          "link": "https://api.trufactor.com/brands/59b6675b-660f-44c3-93e7-1c031758fb15"
        }
      ],
      "business": {
        "id": "eb3698d4-a27c-4d93-9f48-fb4355c0e63c",
        "name": "McDonalds",
        "link": "https://api.trufactor.com/businesses/eb3698d4-a27c-4d93-9f48-fb4355c0e63c"
      },
      "categories": [
        {
          "id": "152f84ff-1f88-4e04-a406-d1bd4358105b",
          "name": "Shopping mall",
          "link": "https://api.trufactor.com/categories/eb3698d4-a27c-4d93-9f48-fb4355c0e63c"
        }
      ],
      "contact": {
        "phone": [
          14153622004,
          14153622005
        ],
        "mobile": "[\"+14153622004\",\"+14153622005\"]",
        "email": [
          "hello@example.com",
          "feedback@example.com"
        ],
        "www": [
          "[\"https://www.example.com\"]"
        ]
      },
      "address": {
        "country_code": "US",
        "country": "USA, United States of America",
        "state_code": "Tx",
        "state": "Texas",
        "county": "Travis",
        "city": "Austin",
        "zip_code": "78701",
        "steet_address": "2100, Barton Springs Rd",
        "locality": "South Austin",
        "neighbourhood": "Barton Creek"
      },
      "geo": {
        "type": "point",
        "coordinates": [
          0
        ]
      }
    }
  ],
  "next": "http:/api.trufactor.co/places/search/?request-id=3953400a-a934-4b4b-8d3c-f8faa5a97bda&limit=50&offset=2"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|data|[[Place](#schemaplace)]|false|none|none|
|next|string|false|none|URL pointing to the next page of results.|

<h2 id="tocSinline_response_400_error">inline_response_400_error</h2>

<a id="schemainline_response_400_error"></a>

```json
{
  "code": "e3526",
  "message": "Invalid input parameter",
  "description": "Unsupported character(s) :) detected in input parameter \"ids\"",
  "doc_link": "http://doc.trufactor.com/error/e3526.html"
}

```

*Response will contain this field only when HTTP status code is 400.*

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|code|string|true|none|Error code|
|message|string|true|none|Error message|
|description|string|true|none|Detailed description of the error for debugging purposes.|
|doc_link|string|false|none|URL pointing to documentation describing the error|

<h2 id="tocSinline_response_400">inline_response_400</h2>

<a id="schemainline_response_400"></a>

```json
{
  "error": {
    "code": "e3526",
    "message": "Invalid input parameter",
    "description": "Unsupported character(s) :) detected in input parameter \"ids\"",
    "doc_link": "http://doc.trufactor.com/error/e3526.html"
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|error|[inline_response_400_error](#schemainline_response_400_error)|false|none|Response will contain this field only when HTTP status code is 400.|

<h2 id="tocSboundary">boundary</h2>

<a id="schemaboundary"></a>

```json
{
  "coordinates": [
    0
  ]
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|coordinates|[number]|false|none|none|

<h2 id="tocSinline_response_200_1_data_summary">inline_response_200_1_data_summary</h2>

<a id="schemainline_response_200_1_data_summary"></a>

```json
{
  "visits_count": 302140,
  "unique_users_count": 132445
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|visits_count|number|false|none|Total number of visitors that visited the place|
|unique_users_count|number|false|none|Total number of unique visitors that visited the place|

<h2 id="tocSinline_response_200_1_data_extrapolated_summary_error_metrics">inline_response_200_1_data_extrapolated_summary_error_metrics</h2>

<a id="schemainline_response_200_1_data_extrapolated_summary_error_metrics"></a>

```json
{
  "visits_count": 1.3,
  "unique_users_count": 0.9
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|visits_count|number|false|none|Error metric in percentage while extrapolating the total number of visitors count|
|unique_users_count|number|false|none|Error metric in percentage while extrapolating the total number of unique visitors count|

<h2 id="tocSinline_response_200_1_data_extrapolated_summary">inline_response_200_1_data_extrapolated_summary</h2>

<a id="schemainline_response_200_1_data_extrapolated_summary"></a>

```json
{
  "visits_count": 6002140,
  "unique_users_count": 121254,
  "error_metrics": {
    "visits_count": 1.3,
    "unique_users_count": 0.9
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|visits_count|number|false|none|Extrapolated total number of visitors who visited the place|
|unique_users_count|number|false|none|Extrapolated total number of unique vistors who visited the place|
|error_metrics|[inline_response_200_1_data_extrapolated_summary_error_metrics](#schemainline_response_200_1_data_extrapolated_summary_error_metrics)|false|none|none|

<h2 id="tocSinline_response_200_1_data">inline_response_200_1_data</h2>

<a id="schemainline_response_200_1_data"></a>

```json
{
  "summary": {
    "visits_count": 302140,
    "unique_users_count": 132445
  },
  "extrapolated_summary": {
    "visits_count": 6002140,
    "unique_users_count": 121254,
    "error_metrics": {
      "visits_count": 1.3,
      "unique_users_count": 0.9
    }
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|summary|[inline_response_200_1_data_summary](#schemainline_response_200_1_data_summary)|false|none|none|
|extrapolated_summary|[inline_response_200_1_data_extrapolated_summary](#schemainline_response_200_1_data_extrapolated_summary)|false|none|none|

<h2 id="tocSinline_response_200_1">inline_response_200_1</h2>

<a id="schemainline_response_200_1"></a>

```json
{
  "data": {
    "summary": {
      "visits_count": 302140,
      "unique_users_count": 132445
    },
    "extrapolated_summary": {
      "visits_count": 6002140,
      "unique_users_count": 121254,
      "error_metrics": {
        "visits_count": 1.3,
        "unique_users_count": 0.9
      }
    }
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|data|[inline_response_200_1_data](#schemainline_response_200_1_data)|false|none|none|

<h2 id="tocSplace_brands">Place_brands</h2>

<a id="schemaplace_brands"></a>

```json
{
  "id": "59b6675b-660f-44c3-93e7-1c031758fb15",
  "name": "Toyota",
  "link": "https://api.trufactor.com/brands/59b6675b-660f-44c3-93e7-1c031758fb15"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string|false|none|An unique TruFactor identifier of the brand|
|name|string|false|none|Name of the brand|
|link|string|false|none|Hypermedia link to fetch the details of the brand|

<h2 id="tocSplace_business">Place_business</h2>

<a id="schemaplace_business"></a>

```json
{
  "id": "eb3698d4-a27c-4d93-9f48-fb4355c0e63c",
  "name": "McDonalds",
  "link": "https://api.trufactor.com/businesses/eb3698d4-a27c-4d93-9f48-fb4355c0e63c"
}

```

*The business that own this place or a tenant operating out of this place*

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string(uuid)|false|none|An unique Trufactor identifier of the business|
|name|string|false|none|Name of the business|
|link|string(uri)|false|none|Hypermedia link to fetch the details of the business|

<h2 id="tocSplace_categories">Place_categories</h2>

<a id="schemaplace_categories"></a>

```json
{
  "id": "152f84ff-1f88-4e04-a406-d1bd4358105b",
  "name": "Shopping mall",
  "link": "https://api.trufactor.com/categories/eb3698d4-a27c-4d93-9f48-fb4355c0e63c"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string(uuid)|false|none|An unique Trufactor identifier of the caetegory|
|name|string|false|none|Name of the category|
|link|string(url)|false|none|Hypermedia link to fetch the details of the category|

