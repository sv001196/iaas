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

## get__visits_physical_store_summary

> Code samples

```shell
# You can also use wget
curl -X GET /visits/physical_store_summary \
  -H 'Accept: application/json' \
  -H 'x-api-key: string'

```

```http
GET /visits/physical_store_summary HTTP/1.1

Accept: application/json
x-api-key: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-api-key':'string'

};

$.ajax({
  url: '/visits/physical_store_summary',
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

fetch('/visits/physical_store_summary',
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

result = RestClient.get '/visits/physical_store_summary',
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

r = requests.get('/visits/physical_store_summary', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("/visits/physical_store_summary");
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
    req, err := http.NewRequest("GET", "/visits/physical_store_summary", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /visits/physical_store_summary`

*Returns the 25th Percentile, 50th Percentile, 75th Percentile and 90th Percentile user and visit counts for the passed stores.*

Returns the 25th Percentile, 50th Percentile, 75th Percentile and 90th Percentile user and visit counts for the passed stores. The location of the store can specified in the form of one or more TruFactor place id or a location co-ordinate of the place or a bounded region or a polygon.

<h3 id="get__visits_physical_store_summary-parameters">Parameters</h3>

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
  "data": [
    {
      "percentile": 25,
      "visits_count": 2933,
      "unique_users_count": 1023
    },
    {
      "percentile": 50,
      "visits_count": 3432,
      "unique_users_count": 809
    },
    {
      "percentile": 75,
      "visits_count": 234,
      "unique_users_count": 92
    }
  ]
}
```

<h3 id="get__visits_physical_store_summary-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|list of insights as specified in the results parameter|[inline_response_200_2](#schemainline_response_200_2)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad input parameter. When the passed place_id is in invalid format (e.g in non UUID format) or when the place_id is not sent at all, the server will respond with HTTP 400 status code. Also, if the query parameters "start", "end" are invalid, the request will be rejected with HTTP status code 400.|[inline_response_400](#schemainline_response_400)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|API key is missing or invalid|None|
|429|[Too Many Requests](https://tools.ietf.org/html/rfc6585#section-4)|Raised when too many requests have been sent.|[inline_response_400](#schemainline_response_400)|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Credits|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|
|400|RequestId|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|
|401|WWW_Authenticate|string||none|
|429|RequestId|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|

<aside class="success">
This operation does not require authentication
</aside>

## get__visits_top_stores

> Code samples

```shell
# You can also use wget
curl -X GET /visits/top_stores \
  -H 'Accept: application/json' \
  -H 'x-api-key: string'

```

```http
GET /visits/top_stores HTTP/1.1

Accept: application/json
x-api-key: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-api-key':'string'

};

$.ajax({
  url: '/visits/top_stores',
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

fetch('/visits/top_stores',
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

result = RestClient.get '/visits/top_stores',
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

r = requests.get('/visits/top_stores', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("/visits/top_stores");
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
    req, err := http.NewRequest("GET", "/visits/top_stores", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /visits/top_stores`

*Returns the top or bottom N stores based on the absolute as well as a multiple of the 50th percentile visits and user counts*

Returns the top or bottom N stores based on the absolute as well as a multiple of the 50th percentile visits and user counts. Place of interest can be one or more TruFactor place id or a location co-ordinate of the place or a bounded region or a polygon.

<h3 id="get__visits_top_stores-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|x-api-key|header|string|true|Pass the API key|
|place_ids|query|string|false|Comma separated list of place IDs. Use /places/ API to fetch a place ID by passing any attributes of a place (e.g city, county, state, zip code). If the query parameter "bounded_region" or "location" is specified, this parameter will be ignored.|
|location|query|array[number]|false|Location co-ordinates representing the place. Pass an array of longitude and latitude e.g [20.23, 28.12]. If the query parameter "bounded_region" is specified, this parameter will be ignored.|
|bounded_region|query|array[array]|false|Bounded region or a polygon representing the place of interest. Pass an array of array of longitude and latitude e.g [[20.23, 28.12], [20.23, 28.12] ]|
|start|query|number(int64)|false|Start time in epoch timestamp. This parameter is optional. The timestamp should be specified in millisecond. If left unspecified, the default start time is applied. The valid start time stamp should be greater than start of current day minus 395 days (roughly current date minus 13 months).|
|end|query|number(int64)|false|End time in epoch timestamp. This parameter is optional. The timestamp should be specified in millisecond. If left unspecified, start time of the current day is applied.|
|bottom|query|number|false|To fetch bottom N stores, specify the value of this parameter as 1. The API fetchs top N stores by default.|
|top_N|query|boolean|false|Number of top or bottom stores to fetch. If unspecified, the default value is 25. Per request, 25 result data set is returned. Refer "next" parameter in the response body to fetch the next set of results.|

#### Enumerated Values

|Parameter|Value|
|---|---|
|bottom|0|
|bottom|1|

> Example responses

> 200 Response

```json
{
  "data": [
    {
      "store_id": "bfc2c04e-3db7-4f80-9b80-7167746d02a1",
      "store_display_name": "cvs pharmacy",
      "link": "http://api.trufactor.io/store/bfc2c04e-3db7-4f80-9b80-7167746d02a1",
      "visits_count": 9832,
      "unique_users_count": 8904,
      "percentile": 90
    },
    {
      "store_id": "239192ba-8933-4e87-9157-e2ec58596af7",
      "store_display_name": "Plaza square mall",
      "link": "http://api.trufactor.io/store/239192ba-8933-4e87-9157-e2ec58596af7",
      "visits_count": 11837,
      "unique_users_count": 8032,
      "percentile": 90
    }
  ],
  "next": "http://api.trufactor.io/visits/top_stores/239192ba-8933-4e87-9157-e2ec58596af7/"
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

<h3 id="get__visits_top_stores-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|list of insights as specified in the results parameter|[inline_response_200_3](#schemainline_response_200_3)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad input parameter. When the passed place_id is in invalid format (e.g in non UUID format) or when the place_id is not sent at all, the server will respond with HTTP 400 status code. Also, if the query parameters "start", "end" are invalid, the request will be rejected with HTTP status code 400.|[inline_response_400](#schemainline_response_400)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|API key is missing or invalid|None|
|429|[Too Many Requests](https://tools.ietf.org/html/rfc6585#section-4)|Raised when too many requests have been sent.|[inline_response_400](#schemainline_response_400)|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Credits|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|
|400|RequestId|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|
|401|WWW_Authenticate|string||none|
|429|RequestId|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|

<aside class="success">
This operation does not require authentication
</aside>

## get__visits_demography

> Code samples

```shell
# You can also use wget
curl -X GET /visits/demography \
  -H 'Accept: application/json' \
  -H 'x-api-key: string'

```

```http
GET /visits/demography HTTP/1.1

Accept: application/json
x-api-key: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-api-key':'string'

};

$.ajax({
  url: '/visits/demography',
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

fetch('/visits/demography',
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

result = RestClient.get '/visits/demography',
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

r = requests.get('/visits/demography', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("/visits/demography");
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
    req, err := http.NewRequest("GET", "/visits/demography", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /visits/demography`

*Returns the aggregated percentage of users by demography (gender, age group, income, ethnicity) for the given place of interests.*

Returns the aggregated percentage of users by demography (gender, age group, income, ethnicity) for the given place of interests. Place of interest can be one or more TruFactor place id or a location co-ordinate of the place or a bounded region or a polygon.

<h3 id="get__visits_demography-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|x-api-key|header|string|true|Pass the API key|
|location_type|query|string|false|Defines how the location information about the place is passed to the server. The API accepts one of - "place_id", an identifier of the place (refer /places/ API for the details) - "point", an array of longitude and latitude representing a point, typically the center point of the location of interest. Specify the query parameter "location.radius" to restrict the radius of the look up for locations of interest. - "polygon" an array of longitude and latitude tuples representing a bounded region|
|location|query|string|false|An object representing geographical information associated with a location of interest. This can be represented by a simple TruFactor place ID or a center point the location or a bounded region or by conventional geo name attributes (e.g city, state).|
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
    "gender": [
      {
        "type": "male",
        "value": 43.1
      },
      {
        "type": "female",
        "value": 33.1
      },
      {
        "type": "unknown",
        "value": 23.7
      }
    ],
    "age_group": [
      {
        "type": "18-25",
        "value": 21
      },
      {
        "type": "26-35",
        "value": 28.1
      },
      {
        "type": "36-50",
        "value": 20.7
      },
      {
        "type": "51-60",
        "value": 20.3
      },
      {
        "type": "61-75",
        "value": 10.1
      }
    ],
    "income_group": [
      {
        "type": "0-25000",
        "value": 18.1
      },
      {
        "type": "25000-50000",
        "value": 20.1
      },
      {
        "type": "50000-100000",
        "value": 30.1
      },
      {
        "type": "100000-500000",
        "value": 10.1
      },
      {
        "type": "500000-750000",
        "value": 10.1
      },
      {
        "type": "> 750000",
        "value": 4.1
      }
    ],
    "ethnicity": [
      {
        "type": "asian",
        "value": 7.4
      },
      {
        "type": "african american",
        "value": 31.1
      },
      {
        "type": "hispanic",
        "value": 20.2
      },
      {
        "type": "native american",
        "value": 33.9
      }
    ]
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

<h3 id="get__visits_demography-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|list of insights as specified in the results parameter|[inline_response_200_4](#schemainline_response_200_4)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad input parameter. When the passed place_id is in invalid format (e.g in non UUID format) or when the place_id is not sent at all, the server will respond with HTTP 400 status code. Also, if the query parameters "start", "end" are invalid, the request will be rejected with HTTP status code 400.|[inline_response_400](#schemainline_response_400)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|API key is missing or invalid|None|
|429|[Too Many Requests](https://tools.ietf.org/html/rfc6585#section-4)|Raised when too many requests have been sent.|[inline_response_400](#schemainline_response_400)|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Credits|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|
|400|RequestId|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|
|401|WWW_Authenticate|string||none|
|429|RequestId|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|

<aside class="success">
This operation does not require authentication
</aside>

## get__visits_app_insights_summary

> Code samples

```shell
# You can also use wget
curl -X GET /visits/app_insights_summary \
  -H 'Accept: application/json' \
  -H 'x-api-key: string'

```

```http
GET /visits/app_insights_summary HTTP/1.1

Accept: application/json
x-api-key: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-api-key':'string'

};

$.ajax({
  url: '/visits/app_insights_summary',
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

fetch('/visits/app_insights_summary',
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

result = RestClient.get '/visits/app_insights_summary',
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

r = requests.get('/visits/app_insights_summary', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("/visits/app_insights_summary");
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
    req, err := http.NewRequest("GET", "/visits/app_insights_summary", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /visits/app_insights_summary`

*Returns the percentage of users split by top apps used or the top apps visited by the users that visited the given place of interests*

Returns the percentage of users split by top apps used or the top apps visited by the users that visited the given place of interests. Place of interest can be one or more TruFactor place id or a location co-ordinate of the place or a bounded region or a polygon.

<h3 id="get__visits_app_insights_summary-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|x-api-key|header|string|true|Pass the API key|
|location_type|query|string|false|Defines how the location information about the place is passed to the server. The API accepts one of - "place_id", an identifier of the place (refer /places/ API for the details) - "point", an array of longitude and latitude representing a point, typically the center point of the location of interest. Specify the query parameter "location.radius" to restrict the radius of the look up for locations of interest. - "polygon" an array of longitude and latitude tuples representing a bounded region|
|location|query|string|false|An object representing geographical information associated with a location of interest. This can be represented by a simple TruFactor place ID or a center point the location or a bounded region or by conventional geo name attributes (e.g city, state).|
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
  "data": [
    {
      "app_id": "7287d23d-a3a5-41e6-84c8-b2eafe5ce9e1",
      "app_category_id": "339192ba-8933-4e87-9157-e2ec58596af7",
      "link": "http://api.trufactor.io/metadata/app/",
      "app_display_name": "TikTok",
      "app_publisher_name": "TikTok Pte Ltd",
      "app_publisher_logo": "https://play.google.com/store/apps/developer?id=TikTok+Pte.+Ltd.",
      "app_icon": "https://lh3.googleusercontent.com/2kdv4gGWKchMkThhxMYlWlkSouhx6BP50X1b7O7_Yl78fFCitAe3t4hLACuCyC9tsJA=s180-rw",
      "ios_link": "string",
      "android_link": "https://play.google.com/store/apps/details?id=com.ss.android.ugc.trill&hl=en_IN",
      "users_in_percentage": 40.9
    },
    {
      "app_id": "90272a48-949e-4614-93ef-0f6b024fa036",
      "link": "http://api.trufactor.io/metadata/app/",
      "app_category_id": "339192ba-8933-4e87-9157-e2ec58596af7",
      "app_display_name": "Google Maps",
      "app_publisher_name": "Google",
      "app_publisher_logo": "https://play.google.com/store/apps/developer?id=TikTok+Pte.+Ltd.",
      "app_icon": "https://lh3.googleusercontent.com/2kdv4gGWKchMkThhxMYlWlkSouhx6BP50X1b7O7_Yl78fFCitAe3t4hLACuCyC9tsJA=s180-rw",
      "ios_link": "string",
      "android_link": "https://play.google.com/store/apps/details?id=com.ss.android.ugc.trill&hl=en_IN",
      "users_in_percentage": 20.9
    }
  ]
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

<h3 id="get__visits_app_insights_summary-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|list of insights as specified in the results parameter|[inline_response_200_5](#schemainline_response_200_5)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad input parameter. When the passed place_id is in invalid format (e.g in non UUID format) or when the place_id is not sent at all, the server will respond with HTTP 400 status code. Also, if the query parameters "start", "end" are invalid, the request will be rejected with HTTP status code 400.|[inline_response_400](#schemainline_response_400)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|API key is missing or invalid|None|
|429|[Too Many Requests](https://tools.ietf.org/html/rfc6585#section-4)|Raised when too many requests have been sent.|[inline_response_400](#schemainline_response_400)|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Credits|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|
|400|RequestId|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|
|401|WWW_Authenticate|string||none|
|429|RequestId|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|

<aside class="success">
This operation does not require authentication
</aside>

## get__visits_web_insights_summary

> Code samples

```shell
# You can also use wget
curl -X GET /visits/web_insights_summary \
  -H 'Accept: application/json' \
  -H 'x-api-key: string'

```

```http
GET /visits/web_insights_summary HTTP/1.1

Accept: application/json
x-api-key: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-api-key':'string'

};

$.ajax({
  url: '/visits/web_insights_summary',
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

fetch('/visits/web_insights_summary',
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

result = RestClient.get '/visits/web_insights_summary',
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

r = requests.get('/visits/web_insights_summary', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("/visits/web_insights_summary");
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
    req, err := http.NewRequest("GET", "/visits/web_insights_summary", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /visits/web_insights_summary`

*Returns the percentage of users split by the websties visited by the users that visited the given place of interests*

Returns the percentage of users split by the websties visited by the users that visited the given place of interests. Place of interest can be one or more TruFactor place id or a location co-ordinate of the place or a bounded region or a polygon.

<h3 id="get__visits_web_insights_summary-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|x-api-key|header|string|true|Pass the API key|
|location_type|query|string|false|Defines how the location information about the place is passed to the server. The API accepts one of - "place_id", an identifier of the place (refer /places/ API for the details) - "point", an array of longitude and latitude representing a point, typically the center point of the location of interest. Specify the query parameter "location.radius" to restrict the radius of the look up for locations of interest. - "polygon" an array of longitude and latitude tuples representing a bounded region|
|location|query|string|false|An object representing geographical information associated with a location of interest. This can be represented by a simple TruFactor place ID or a center point the location or a bounded region or by conventional geo name attributes (e.g city, state).|
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
  "data": [
    {
      "website_category_id": "7287d23d-a3a5-41e6-84c8-b2eafe5ce9e1",
      "publisher_name": "Google",
      "url": "http://www.maps.google.com",
      "users_in_percentage": 40.9
    },
    {
      "website_category_id": "beecd6c6-dcd4-4fde-9ed7-3ada43b088f5",
      "publisher_name": "Facbook",
      "url": "http://www.facebook.com",
      "users_in_percentage": 37.1
    }
  ]
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

<h3 id="get__visits_web_insights_summary-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|list of insights as specified in the results parameter|[inline_response_200_6](#schemainline_response_200_6)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad input parameter. When the passed place_id is in invalid format (e.g in non UUID format) or when the place_id is not sent at all, the server will respond with HTTP 400 status code. Also, if the query parameters "start", "end" are invalid, the request will be rejected with HTTP status code 400.|[inline_response_400](#schemainline_response_400)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|API key is missing or invalid|None|
|429|[Too Many Requests](https://tools.ietf.org/html/rfc6585#section-4)|Raised when too many requests have been sent.|[inline_response_400](#schemainline_response_400)|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Credits|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|
|400|RequestId|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|
|401|WWW_Authenticate|string||none|
|429|RequestId|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|

<aside class="success">
This operation does not require authentication
</aside>

## get__visits_area_summary

> Code samples

```shell
# You can also use wget
curl -X GET /visits/area_summary \
  -H 'Accept: application/json' \
  -H 'x-api-key: string'

```

```http
GET /visits/area_summary HTTP/1.1

Accept: application/json
x-api-key: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-api-key':'string'

};

$.ajax({
  url: '/visits/area_summary',
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

fetch('/visits/area_summary',
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

result = RestClient.get '/visits/area_summary',
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

r = requests.get('/visits/area_summary', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("/visits/area_summary");
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
    req, err := http.NewRequest("GET", "/visits/area_summary", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /visits/area_summary`

*Returns the percentage of users split by the home or work census block and distance from work or home*

Returns the percentage of users split by the home or work census block and distance from work or home. Place of interest can be one or more TruFactor place id or a location co-ordinate of the place or a bounded region or a polygon.

<h3 id="get__visits_area_summary-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|x-api-key|header|string|true|Pass the API key|
|location_type|query|string|false|Defines how the location information about the place is passed to the server. The API accepts one of - "place_id", an identifier of the place (refer /places/ API for the details) - "point", an array of longitude and latitude representing a point, typically the center point of the location of interest. Specify the query parameter "location.radius" to restrict the radius of the look up for locations of interest. - "polygon" an array of longitude and latitude tuples representing a bounded region|
|location|query|string|false|An object representing geographical information associated with a location of interest. This can be represented by a simple TruFactor place ID or a center point the location or a bounded region or by conventional geo name attributes (e.g city, state).|
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
"{\"data\":{\"by_home_census_block_group\":[{\"block_group_id\":\"101001\",\"users_in_percentage\":47.3}],\"by_work_census_block_group\":[{\"block_group_id\":\"101002\",\"users_in_percentage\":40.1}],\"by_distance_between_home_and_place\":[{\"radius_in_miles\":5,\"users_in_percentage\":0},{\"radius_in_miles\":15,\"users_in_percentage\":0},{\"radius_in_miles\":25,\"users_in_percentage\":0}],\"by_time_between_home_and_place\":[{\"time_range\":\"5-15\",\"users_in_percentage\":12.4},{\"time_range\":\"15-30\",\"users_in_percentage\":21.4},{\"time_range\":\"30-45\",\"users_in_percentage\":28.1},{\"time_range\":\"45-60\",\"users_in_percentage\":20.4},{\"time_range\":\"> 60\",\"users_in_percentage\":11.4}]}}"
```

<h3 id="get__visits_area_summary-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|list of insights as specified in the results parameter|[inline_response_200_7](#schemainline_response_200_7)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad input parameter. When the passed place_id is in invalid format (e.g in non UUID format) or when the place_id is not sent at all, the server will respond with HTTP 400 status code. Also, if the query parameters "start", "end" are invalid, the request will be rejected with HTTP status code 400.|[inline_response_400](#schemainline_response_400)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|API key is missing or invalid|None|
|429|[Too Many Requests](https://tools.ietf.org/html/rfc6585#section-4)|Raised when too many requests have been sent.|[inline_response_400](#schemainline_response_400)|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Credits|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|
|400|RequestId|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|
|401|WWW_Authenticate|string||none|
|429|RequestId|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|

<aside class="success">
This operation does not require authentication
</aside>

## get__visits_activities

> Code samples

```shell
# You can also use wget
curl -X GET /visits/activities \
  -H 'Accept: application/json' \
  -H 'x-api-key: string'

```

```http
GET /visits/activities HTTP/1.1

Accept: application/json
x-api-key: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-api-key':'string'

};

$.ajax({
  url: '/visits/activities',
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

fetch('/visits/activities',
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

result = RestClient.get '/visits/activities',
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

r = requests.get('/visits/activities', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("/visits/activities");
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
    req, err := http.NewRequest("GET", "/visits/activities", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /visits/activities`

*Returns the percentage of users split by the activity i.e hour\day of the week, frequency of visit and dwell time*

Returns the percentage of users split by the activity i.e hour\day of the week, frequency of visit and dwell time. Place of interest can be one or more TruFactor place id or a location co-ordinate of the place or a bounded region or a polygon.

<h3 id="get__visits_activities-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|x-api-key|header|string|true|Pass the API key|
|location_type|query|string|false|Defines how the location information about the place is passed to the server. The API accepts one of - "place_id", an identifier of the place (refer /places/ API for the details) - "point", an array of longitude and latitude representing a point, typically the center point of the location of interest. Specify the query parameter "location.radius" to restrict the radius of the look up for locations of interest. - "polygon" an array of longitude and latitude tuples representing a bounded region|
|location|query|string|false|An object representing geographical information associated with a location of interest. This can be represented by a simple TruFactor place ID or a center point the location or a bounded region or by conventional geo name attributes (e.g city, state).|
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
  "data": [
    {
      "by_day_of_week": [
        {
          "day": "1",
          "users_in_percentage": 12
        },
        {
          "day": "2",
          "users_in_percentage": 17.2
        },
        {
          "day": "3",
          "users_in_percentage": 9.3
        },
        {
          "day": "4",
          "users_in_percentage": 8.2
        },
        {
          "day": "5",
          "users_in_percentage": 13.5
        },
        {
          "day": "6",
          "users_in_percentage": 23.1
        },
        {
          "day": "7",
          "users_in_percentage": 21.1
        }
      ],
      "by_hour_of_day": [
        {
          "hour_range": "00-06",
          "users_in_percentage": 0
        },
        {
          "hour_range": "06-12",
          "users_in_percentage": 13.4
        },
        {
          "hour_range": "12-18",
          "users_in_percentage": 33.7
        },
        {
          "hour_range": "18-00",
          "users_in_percentage": 41.5
        }
      ],
      "by_visit_frequency": [
        {
          "frequency_range": "1-3",
          "users_in_percentage": 40.1
        },
        {
          "frequency_range": "3-5",
          "users_in_percentage": 37.2
        },
        {
          "frequency_range": "5-10",
          "users_in_percentage": 5.1
        }
      ],
      "by_dwell_time": [
        {
          "dwell_time_range": "1-10",
          "users_in_percentage": 3.5
        },
        {
          "dwell_time_range": "10-20",
          "users_in_percentage": 34.2
        },
        {
          "dwell_time_range": "20-30",
          "users_in_percentage": 21.6
        },
        {
          "dwell_time_range": "30-40",
          "users_in_percentage": 14.6
        },
        {
          "dwell_time_range": "40-60",
          "users_in_percentage": 5.7
        }
      ]
    }
  ]
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

<h3 id="get__visits_activities-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|list of insights as specified in the results parameter|[inline_response_200_8](#schemainline_response_200_8)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad input parameter. When the passed place_id is in invalid format (e.g in non UUID format) or when the place_id is not sent at all, the server will respond with HTTP 400 status code. Also, if the query parameters "start", "end" are invalid, the request will be rejected with HTTP status code 400.|[inline_response_400](#schemainline_response_400)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|API key is missing or invalid|None|
|429|[Too Many Requests](https://tools.ietf.org/html/rfc6585#section-4)|Raised when too many requests have been sent.|[inline_response_400](#schemainline_response_400)|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Credits|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|
|400|RequestId|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|
|401|WWW_Authenticate|string||none|
|429|RequestId|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|

<aside class="success">
This operation does not require authentication
</aside>

## get__visits_places

> Code samples

```shell
# You can also use wget
curl -X GET /visits/places \
  -H 'Accept: application/json' \
  -H 'x-api-key: string'

```

```http
GET /visits/places HTTP/1.1

Accept: application/json
x-api-key: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-api-key':'string'

};

$.ajax({
  url: '/visits/places',
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

fetch('/visits/places',
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

result = RestClient.get '/visits/places',
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

r = requests.get('/visits/places', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("/visits/places");
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
    req, err := http.NewRequest("GET", "/visits/places", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /visits/places`

*Returns the percentage of users split by the other places they visited*

Returns the percentage of users split by the other places they visited. Place of interest can be one or more TruFactor place id or a location co-ordinate of the place or a bounded region or a polygon.

<h3 id="get__visits_places-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|x-api-key|header|string|true|Pass the API key|
|location_type|query|string|false|Defines how the location information about the place is passed to the server. The API accepts one of - "place_id", an identifier of the place (refer /places/ API for the details) - "point", an array of longitude and latitude representing a point, typically the center point of the location of interest. Specify the query parameter "location.radius" to restrict the radius of the look up for locations of interest. - "polygon" an array of longitude and latitude tuples representing a bounded region|
|location|query|string|false|An object representing geographical information associated with a location of interest. This can be represented by a simple TruFactor place ID or a center point the location or a bounded region or by conventional geo name attributes (e.g city, state).|
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
  "result": {
    "other_places_visited_by_category": [
      {
        "category_id": "bfc2c04e-3db7-4f80-9b80-7167746d02a1",
        "category_name": "Restaurants"
      },
      {
        "category_id": "f4d2e1f0-89b2-4c58-ad9b-90bf3f0738e5",
        "category_name": "Shopping Mall"
      }
    ],
    "top_visited_pois": [
      {
        "place_id": "44d38505-a67f-4861-81ab-a8dc9c72c136",
        "place_name": "Baldwin Square",
        "link": "http://api.trufactor.io/place/44d38505-a67f-4861-81ab-a8dc9c72c136",
        "users_in_percentage": 20.3
      }
    ]
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

<h3 id="get__visits_places-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|list of insights as specified in the results parameter|[inline_response_200_9](#schemainline_response_200_9)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad input parameter. When the passed place_id is in invalid format (e.g in non UUID format) or when the place_id is not sent at all, the server will respond with HTTP 400 status code. Also, if the query parameters "start", "end" are invalid, the request will be rejected with HTTP status code 400.|[inline_response_400](#schemainline_response_400)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|API key is missing or invalid|None|
|429|[Too Many Requests](https://tools.ietf.org/html/rfc6585#section-4)|Raised when too many requests have been sent.|[inline_response_400](#schemainline_response_400)|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Credits|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|
|400|RequestId|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|
|401|WWW_Authenticate|string||none|
|429|RequestId|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|

<aside class="success">
This operation does not require authentication
</aside>

## get__visits_journeys_physical

> Code samples

```shell
# You can also use wget
curl -X GET /visits/journeys/physical \
  -H 'Accept: application/json' \
  -H 'x-api-key: string'

```

```http
GET /visits/journeys/physical HTTP/1.1

Accept: application/json
x-api-key: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-api-key':'string'

};

$.ajax({
  url: '/visits/journeys/physical',
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

fetch('/visits/journeys/physical',
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

result = RestClient.get '/visits/journeys/physical',
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

r = requests.get('/visits/journeys/physical', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("/visits/journeys/physical");
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
    req, err := http.NewRequest("GET", "/visits/journeys/physical", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /visits/journeys/physical`

*Returns the percentage of users split by the other places visited by the users before and after the store visit*

Returns the percentage of users split by the other places visited by the users before and after the store visit. Place of interest can be one or more TruFactor place id or a location co-ordinate of the place or a bounded region or a polygon.

<h3 id="get__visits_journeys_physical-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|x-api-key|header|string|true|Pass the API key|
|location_type|query|string|false|Defines how the location information about the place is passed to the server. The API accepts one of - "place_id", an identifier of the place (refer /places/ API for the details) - "point", an array of longitude and latitude representing a point, typically the center point of the location of interest. Specify the query parameter "location.radius" to restrict the radius of the look up for locations of interest. - "polygon" an array of longitude and latitude tuples representing a bounded region|
|location|query|string|false|An object representing geographical information associated with a location of interest. This can be represented by a simple TruFactor place ID or a center point the location or a bounded region or by conventional geo name attributes (e.g city, state).|
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
    "before": [
      {
        "category_id": "44fa7368-1cf4-4c58-999e-400f91e9849c",
        "category_name": "Shopping Malls",
        "users_in_percentage": 23.1
      },
      {
        "category_id": "3953400a-a934-4b4b-8d3c-f8faa5a97bda",
        "category_name": "Restaurants",
        "users_in_percentage": 23.1
      }
    ],
    "at": [
      {
        "category_id": "44fa7368-1cf4-4c58-999e-400f91e9849c",
        "category_name": "Shopping Malls",
        "users_in_percentage": 23.1
      },
      {
        "category_id": "3953400a-a934-4b4b-8d3c-f8faa5a97bda",
        "category_name": "Restaurants",
        "users_in_percentage": 23.1
      }
    ]
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

<h3 id="get__visits_journeys_physical-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|list of insights as specified in the results parameter|[inline_response_200_10](#schemainline_response_200_10)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad input parameter. When the passed place_id is in invalid format (e.g in non UUID format) or when the place_id is not sent at all, the server will respond with HTTP 400 status code. Also, if the query parameters "start", "end" are invalid, the request will be rejected with HTTP status code 400.|[inline_response_400](#schemainline_response_400)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|API key is missing or invalid|None|
|429|[Too Many Requests](https://tools.ietf.org/html/rfc6585#section-4)|Raised when too many requests have been sent.|[inline_response_400](#schemainline_response_400)|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Credits|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|
|400|RequestId|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|
|401|WWW_Authenticate|string||none|
|429|RequestId|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|

<aside class="success">
This operation does not require authentication
</aside>

## get__visits_journeys_digital

> Code samples

```shell
# You can also use wget
curl -X GET /visits/journeys/digital \
  -H 'Accept: application/json' \
  -H 'x-api-key: string'

```

```http
GET /visits/journeys/digital HTTP/1.1

Accept: application/json
x-api-key: string

```

```javascript
var headers = {
  'Accept':'application/json',
  'x-api-key':'string'

};

$.ajax({
  url: '/visits/journeys/digital',
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

fetch('/visits/journeys/digital',
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

result = RestClient.get '/visits/journeys/digital',
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

r = requests.get('/visits/journeys/digital', params={

}, headers = headers)

print r.json()

```

```java
URL obj = new URL("/visits/journeys/digital");
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
    req, err := http.NewRequest("GET", "/visits/journeys/digital", data)
    req.Header = headers

    client := &http.Client{}
    resp, err := client.Do(req)
    // ...
}

```

`GET /visits/journeys/digital`

*Returns the percentage of users split based on the top apps used at the store, X hours before or after the store visit.*

Returns the percentage of users split based on the top apps used at the store, X hours before or after the store visit. Place of interest can be one or more TruFactor place id or a location co-ordinate of the place or a bounded region or a polygon.

<h3 id="get__visits_journeys_digital-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|x-api-key|header|string|true|Pass the API key|
|location_type|query|string|false|Defines how the location information about the place is passed to the server. The API accepts one of - "place_id", an identifier of the place (refer /places/ API for the details) - "point", an array of longitude and latitude representing a point, typically the center point of the location of interest. Specify the query parameter "location.radius" to restrict the radius of the look up for locations of interest. - "polygon" an array of longitude and latitude tuples representing a bounded region|
|location|query|string|false|An object representing geographical information associated with a location of interest. This can be represented by a simple TruFactor place ID or a center point the location or a bounded region or by conventional geo name attributes (e.g city, state).|
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
    "at": [
      {
        "app_id": "7287d23d-a3a5-41e6-84c8-b2eafe5ce9e1",
        "app_category_id": "339192ba-8933-4e87-9157-e2ec58596af7",
        "link": "http://api.trufactor.io/metadata/app/",
        "app_display_name": "TikTok",
        "app_publisher_name": "TikTok Pte Ltd",
        "app_publisher_logo": "https://play.google.com/store/apps/developer?id=TikTok+Pte.+Ltd.",
        "app_icon": "https://lh3.googleusercontent.com/2kdv4gGWKchMkThhxMYlWlkSouhx6BP50X1b7O7_Yl78fFCitAe3t4hLACuCyC9tsJA=s180-rw",
        "ios_link": "string",
        "android_link": "https://play.google.com/store/apps/details?id=com.ss.android.ugc.trill&hl=en_IN",
        "users_in_percentage": 40.9
      },
      {
        "app_id": "90272a48-949e-4614-93ef-0f6b024fa036",
        "link": "http://api.trufactor.io/metadata/app/",
        "app_category_id": "339192ba-8933-4e87-9157-e2ec58596af7",
        "app_display_name": "Google Maps",
        "app_publisher_name": "Google",
        "app_publisher_logo": "https://play.google.com/store/apps/developer?id=TikTok+Pte.+Ltd.",
        "app_icon": "https://lh3.googleusercontent.com/2kdv4gGWKchMkThhxMYlWlkSouhx6BP50X1b7O7_Yl78fFCitAe3t4hLACuCyC9tsJA=s180-rw",
        "ios_link": "string",
        "android_link": "https://play.google.com/store/apps/details?id=com.ss.android.ugc.trill&hl=en_IN",
        "users_in_percentage": 20.9
      }
    ],
    "before": [
      {
        "app_id": "7287d23d-a3a5-41e6-84c8-b2eafe5ce9e1",
        "app_category_id": "339192ba-8933-4e87-9157-e2ec58596af7",
        "link": "http://api.trufactor.io/metadata/app/",
        "app_display_name": "TikTok",
        "app_publisher_name": "TikTok Pte Ltd",
        "app_publisher_logo": "https://play.google.com/store/apps/developer?id=TikTok+Pte.+Ltd.",
        "app_icon": "https://lh3.googleusercontent.com/2kdv4gGWKchMkThhxMYlWlkSouhx6BP50X1b7O7_Yl78fFCitAe3t4hLACuCyC9tsJA=s180-rw",
        "ios_link": "string",
        "android_link": "https://play.google.com/store/apps/details?id=com.ss.android.ugc.trill&hl=en_IN",
        "users_in_percentage": 40.9
      },
      {
        "app_id": "90272a48-949e-4614-93ef-0f6b024fa036",
        "link": "http://api.trufactor.io/metadata/app/",
        "app_category_id": "339192ba-8933-4e87-9157-e2ec58596af7",
        "app_display_name": "Google Maps",
        "app_publisher_name": "Google",
        "app_publisher_logo": "https://play.google.com/store/apps/developer?id=TikTok+Pte.+Ltd.",
        "app_icon": "https://lh3.googleusercontent.com/2kdv4gGWKchMkThhxMYlWlkSouhx6BP50X1b7O7_Yl78fFCitAe3t4hLACuCyC9tsJA=s180-rw",
        "ios_link": "string",
        "android_link": "https://play.google.com/store/apps/details?id=com.ss.android.ugc.trill&hl=en_IN",
        "users_in_percentage": 20.9
      }
    ],
    "after": [
      {
        "app_id": "7287d23d-a3a5-41e6-84c8-b2eafe5ce9e1",
        "app_category_id": "339192ba-8933-4e87-9157-e2ec58596af7",
        "link": "http://api.trufactor.io/metadata/app/",
        "app_display_name": "TikTok",
        "app_publisher_name": "TikTok Pte Ltd",
        "app_publisher_logo": "https://play.google.com/store/apps/developer?id=TikTok+Pte.+Ltd.",
        "app_icon": "https://lh3.googleusercontent.com/2kdv4gGWKchMkThhxMYlWlkSouhx6BP50X1b7O7_Yl78fFCitAe3t4hLACuCyC9tsJA=s180-rw",
        "ios_link": "string",
        "android_link": "https://play.google.com/store/apps/details?id=com.ss.android.ugc.trill&hl=en_IN",
        "users_in_percentage": 40.9
      },
      {
        "app_id": "90272a48-949e-4614-93ef-0f6b024fa036",
        "link": "http://api.trufactor.io/metadata/app/",
        "app_category_id": "339192ba-8933-4e87-9157-e2ec58596af7",
        "app_display_name": "Google Maps",
        "app_publisher_name": "Google",
        "app_publisher_logo": "https://play.google.com/store/apps/developer?id=TikTok+Pte.+Ltd.",
        "app_icon": "https://lh3.googleusercontent.com/2kdv4gGWKchMkThhxMYlWlkSouhx6BP50X1b7O7_Yl78fFCitAe3t4hLACuCyC9tsJA=s180-rw",
        "ios_link": "string",
        "android_link": "https://play.google.com/store/apps/details?id=com.ss.android.ugc.trill&hl=en_IN",
        "users_in_percentage": 20.9
      }
    ]
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

<h3 id="get__visits_journeys_digital-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|list of insights as specified in the results parameter|[inline_response_200_11](#schemainline_response_200_11)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|Bad input parameter. When the passed place_id is in invalid format (e.g in non UUID format) or when the place_id is not sent at all, the server will respond with HTTP 400 status code. Also, if the query parameters "start", "end" are invalid, the request will be rejected with HTTP status code 400.|[inline_response_400](#schemainline_response_400)|
|401|[Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)|API key is missing or invalid|None|
|429|[Too Many Requests](https://tools.ietf.org/html/rfc6585#section-4)|Raised when too many requests have been sent.|[inline_response_400](#schemainline_response_400)|

### Response Headers

|Status|Header|Type|Format|Description|
|---|---|---|---|---|
|200|Credits|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|
|400|RequestId|string||An unique TruFactor request ID per API request. Use this for debugging and tracking credit consumption.|
|401|WWW_Authenticate|string||none|
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

<h2 id="tocSinline_response_200_2_data">inline_response_200_2_data</h2>

<a id="schemainline_response_200_2_data"></a>

```json
{
  "percentile": 25,
  "visits_count": 2933,
  "unique_users_count": 1023
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|percentile|number(int64)|false|none|none|
|visits_count|number|false|none|Total number of users that visited the place falling in to the percentile|
|unique_users_count|number|false|none|Total number of unique users that visited the place falling in to the percentile|

#### Enumerated Values

|Property|Value|
|---|---|
|percentile|25|
|percentile|50|
|percentile|75|
|percentile|90|

<h2 id="tocSinline_response_200_2">inline_response_200_2</h2>

<a id="schemainline_response_200_2"></a>

```json
{
  "data": [
    {
      "percentile": 25,
      "visits_count": 2933,
      "unique_users_count": 1023
    },
    {
      "percentile": 50,
      "visits_count": 3432,
      "unique_users_count": 809
    },
    {
      "percentile": 75,
      "visits_count": 234,
      "unique_users_count": 92
    }
  ]
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|data|[[inline_response_200_2_data](#schemainline_response_200_2_data)]|false|none|none|

<h2 id="tocSinline_response_200_3_data">inline_response_200_3_data</h2>

<a id="schemainline_response_200_3_data"></a>

```json
{
  "store_id": "bfc2c04e-3db7-4f80-9b80-7167746d02a1",
  "store_display_name": "cvs pharmacy",
  "link": "http://api.trufactor.io/store/bfc2c04e-3db7-4f80-9b80-7167746d02a1",
  "visits_count": 9832,
  "unique_users_count": 8904,
  "percentile": 90
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|store_id|string|false|none|none|
|store_display_name|string|false|none|none|
|link|string|false|none|Hypermedia link to fetch the details of the store|
|visits_count|number|false|none|none|
|unique_users_count|number|false|none|none|
|percentile|number|false|none|none|

#### Enumerated Values

|Property|Value|
|---|---|
|percentile|25|
|percentile|50|
|percentile|75|
|percentile|90|

<h2 id="tocSinline_response_200_3">inline_response_200_3</h2>

<a id="schemainline_response_200_3"></a>

```json
{
  "data": [
    {
      "store_id": "bfc2c04e-3db7-4f80-9b80-7167746d02a1",
      "store_display_name": "cvs pharmacy",
      "link": "http://api.trufactor.io/store/bfc2c04e-3db7-4f80-9b80-7167746d02a1",
      "visits_count": 9832,
      "unique_users_count": 8904,
      "percentile": 90
    }
  ],
  "next": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|data|[[inline_response_200_3_data](#schemainline_response_200_3_data)]|false|none|none|
|next|string|false|none|URL to fetch the next set of results. By default, 25 result set is returned per request.|

<h2 id="tocSinline_response_200_4_gender">inline_response_200_4_gender</h2>

<a id="schemainline_response_200_4_gender"></a>

```json
{
  "type": "male",
  "value": 23.1
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|type|string|false|none|none|
|value|number(float)|false|none|the number returned is in percentage|

#### Enumerated Values

|Property|Value|
|---|---|
|type|male|
|type|female|
|type|unknown|
|type|both|

<h2 id="tocSinline_response_200_4_age_group">inline_response_200_4_age_group</h2>

<a id="schemainline_response_200_4_age_group"></a>

```json
{
  "type": "18-25",
  "value": 13.1
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|type|string|false|none|none|
|value|number|false|none|the number returned is in percentage|

#### Enumerated Values

|Property|Value|
|---|---|
|type|18-25|
|type|26-35|
|type|36-45|
|type|46-60|
|type|61-85|

<h2 id="tocSinline_response_200_4_income_group">inline_response_200_4_income_group</h2>

<a id="schemainline_response_200_4_income_group"></a>

```json
{
  "type": "0-25000",
  "value": 13.1
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|type|string|false|none|none|
|value|number|false|none|the number returned is in percentage|

#### Enumerated Values

|Property|Value|
|---|---|
|type|0-25000|
|type|25000-100000|

<h2 id="tocSinline_response_200_4_ethnicity">inline_response_200_4_ethnicity</h2>

<a id="schemainline_response_200_4_ethnicity"></a>

```json
{
  "type": "asian",
  "value": 13.1
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|type|string|false|none|none|
|value|number|false|none|the number returned is in percentage|

#### Enumerated Values

|Property|Value|
|---|---|
|type|asian|
|type|african american|
|type|hispanic|
|type|unknown|

<h2 id="tocSinline_response_200_4_data">inline_response_200_4_data</h2>

<a id="schemainline_response_200_4_data"></a>

```json
{
  "place_id": "string",
  "gender": [
    {
      "type": "male",
      "value": 23.1
    }
  ],
  "age_group": [
    {
      "type": "18-25",
      "value": 13.1
    }
  ],
  "income_group": [
    {
      "type": "0-25000",
      "value": 13.1
    }
  ],
  "ethnicity": [
    {
      "type": "asian",
      "value": 13.1
    }
  ]
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|place_id|string|false|none|none|
|gender|[[inline_response_200_4_gender](#schemainline_response_200_4_gender)]|false|none|none|
|age_group|[[inline_response_200_4_age_group](#schemainline_response_200_4_age_group)]|false|none|none|
|income_group|[[inline_response_200_4_income_group](#schemainline_response_200_4_income_group)]|false|none|none|
|ethnicity|[[inline_response_200_4_ethnicity](#schemainline_response_200_4_ethnicity)]|false|none|none|

<h2 id="tocSinline_response_200_4">inline_response_200_4</h2>

<a id="schemainline_response_200_4"></a>

```json
{
  "data": [
    {
      "place_id": "string",
      "gender": [
        {
          "type": "male",
          "value": 23.1
        }
      ],
      "age_group": [
        {
          "type": "18-25",
          "value": 13.1
        }
      ],
      "income_group": [
        {
          "type": "0-25000",
          "value": 13.1
        }
      ],
      "ethnicity": [
        {
          "type": "asian",
          "value": 13.1
        }
      ]
    }
  ]
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|data|[[inline_response_200_4_data](#schemainline_response_200_4_data)]|false|none|none|

<h2 id="tocSinline_response_200_5_data">inline_response_200_5_data</h2>

<a id="schemainline_response_200_5_data"></a>

```json
{
  "app_id": "string",
  "link": "string",
  "app_category_id": "string",
  "app_display_name": "TikTok",
  "app_publisher_name": "TikTok Pte Ltd",
  "app_publisher_logo": "https://play.google.com/store/apps/developer?id=TikTok+Pte.+Ltd.",
  "app_icon": "https://lh3.googleusercontent.com/2kdv4gGWKchMkThhxMYlWlkSouhx6BP50X1b7O7_Yl78fFCitAe3t4hLACuCyC9tsJA=s180-rw",
  "ios_link": "string",
  "android_link": "https://play.google.com/store/apps/details?id=com.ss.android.ugc.trill&hl=en_IN",
  "users_in_percentage": 40.9
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|app_id|string|false|none|Internal id of the app|
|link|string|false|none|URL to fetch the details of the app|
|app_category_id|string|false|none|ID of the category that theapp belongs to. Look up category metadata API to fetch the category details|
|app_display_name|string|false|none|Display name of the app|
|app_publisher_name|string|false|none|Name of the app publisher|
|app_publisher_logo|string|false|none|none|
|app_icon|string|false|none|none|
|ios_link|string|false|none|none|
|android_link|string|false|none|none|
|users_in_percentage|number|false|none|none|

<h2 id="tocSinline_response_200_5_data_1">inline_response_200_5_data_1</h2>

<a id="schemainline_response_200_5_data_1"></a>

```json
{
  "data": [
    {
      "app_id": "string",
      "link": "string",
      "app_category_id": "string",
      "app_display_name": "TikTok",
      "app_publisher_name": "TikTok Pte Ltd",
      "app_publisher_logo": "https://play.google.com/store/apps/developer?id=TikTok+Pte.+Ltd.",
      "app_icon": "https://lh3.googleusercontent.com/2kdv4gGWKchMkThhxMYlWlkSouhx6BP50X1b7O7_Yl78fFCitAe3t4hLACuCyC9tsJA=s180-rw",
      "ios_link": "string",
      "android_link": "https://play.google.com/store/apps/details?id=com.ss.android.ugc.trill&hl=en_IN",
      "users_in_percentage": 40.9
    }
  ]
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|data|[[inline_response_200_5_data](#schemainline_response_200_5_data)]|false|none|Top apps used by the visitors that visited the place(s)|

<h2 id="tocSinline_response_200_5">inline_response_200_5</h2>

<a id="schemainline_response_200_5"></a>

```json
{
  "data": [
    {
      "data": [
        {
          "app_id": "string",
          "link": "string",
          "app_category_id": "string",
          "app_display_name": "TikTok",
          "app_publisher_name": "TikTok Pte Ltd",
          "app_publisher_logo": "https://play.google.com/store/apps/developer?id=TikTok+Pte.+Ltd.",
          "app_icon": "https://lh3.googleusercontent.com/2kdv4gGWKchMkThhxMYlWlkSouhx6BP50X1b7O7_Yl78fFCitAe3t4hLACuCyC9tsJA=s180-rw",
          "ios_link": "string",
          "android_link": "https://play.google.com/store/apps/details?id=com.ss.android.ugc.trill&hl=en_IN",
          "users_in_percentage": 40.9
        }
      ]
    }
  ]
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|data|[[inline_response_200_5_data_1](#schemainline_response_200_5_data_1)]|false|none|none|

<h2 id="tocSinline_response_200_6_data">inline_response_200_6_data</h2>

<a id="schemainline_response_200_6_data"></a>

```json
{
  "website_category_id": "string",
  "publisher_name": "Google",
  "url": "http://www.maps.google.com",
  "users_in_percentage": 39.1
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|website_category_id|string|false|none|ID of the website category. Look up category metadata API to fetch the category details|
|publisher_name|string|false|none|Display name of web site publisher|
|url|string|false|none|none|
|users_in_percentage|number|false|none|none|

<h2 id="tocSinline_response_200_6">inline_response_200_6</h2>

<a id="schemainline_response_200_6"></a>

```json
{
  "data": [
    {
      "website_category_id": "string",
      "publisher_name": "Google",
      "url": "http://www.maps.google.com",
      "users_in_percentage": 39.1
    }
  ]
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|data|[[inline_response_200_6_data](#schemainline_response_200_6_data)]|false|none|none|

<h2 id="tocSinline_response_200_7_data_by_home_census_block_group">inline_response_200_7_data_by_home_census_block_group</h2>

<a id="schemainline_response_200_7_data_by_home_census_block_group"></a>

```json
{
  "block_group_id": "string",
  "users_in_percentage": 0
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|block_group_id|string|false|none|none|
|users_in_percentage|number|false|none|none|

<h2 id="tocSinline_response_200_7_data_by_distance_between_home_and_place">inline_response_200_7_data_by_distance_between_home_and_place</h2>

<a id="schemainline_response_200_7_data_by_distance_between_home_and_place"></a>

```json
{
  "radius_in_miles": 0,
  "users_in_percentage": 0
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|radius_in_miles|number|false|none|none|
|users_in_percentage|number|false|none|none|

<h2 id="tocSinline_response_200_7_data_by_time_between_home_and_place">inline_response_200_7_data_by_time_between_home_and_place</h2>

<a id="schemainline_response_200_7_data_by_time_between_home_and_place"></a>

```json
{
  "time_range": "string",
  "users_in_percentage": 0
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|time_range|string|false|none|none|
|users_in_percentage|number|false|none|none|

<h2 id="tocSinline_response_200_7_data">inline_response_200_7_data</h2>

<a id="schemainline_response_200_7_data"></a>

```json
{
  "by_home_census_block_group": [
    {
      "block_group_id": "string",
      "users_in_percentage": 0
    }
  ],
  "by_work_census_block_group": [
    {
      "block_group_id": "string",
      "users_in_percentage": 0
    }
  ],
  "by_distance_between_home_and_place": [
    {
      "radius_in_miles": 0,
      "users_in_percentage": 0
    }
  ],
  "by_time_between_home_and_place": [
    {
      "time_range": "string",
      "users_in_percentage": 0
    }
  ]
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|by_home_census_block_group|[[inline_response_200_7_data_by_home_census_block_group](#schemainline_response_200_7_data_by_home_census_block_group)]|false|none|none|
|by_work_census_block_group|[[inline_response_200_7_data_by_home_census_block_group](#schemainline_response_200_7_data_by_home_census_block_group)]|false|none|none|
|by_distance_between_home_and_place|[[inline_response_200_7_data_by_distance_between_home_and_place](#schemainline_response_200_7_data_by_distance_between_home_and_place)]|false|none|none|
|by_time_between_home_and_place|[[inline_response_200_7_data_by_time_between_home_and_place](#schemainline_response_200_7_data_by_time_between_home_and_place)]|false|none|none|

<h2 id="tocSinline_response_200_7">inline_response_200_7</h2>

<a id="schemainline_response_200_7"></a>

```json
"{\"data\":{\"by_home_census_block_group\":[{\"block_group_id\":\"101001\",\"users_in_percentage\":47.3}],\"by_work_census_block_group\":[{\"block_group_id\":\"101002\",\"users_in_percentage\":40.1}],\"by_distance_between_home_and_place\":[{\"radius_in_miles\":5,\"users_in_percentage\":0},{\"radius_in_miles\":15,\"users_in_percentage\":0},{\"radius_in_miles\":25,\"users_in_percentage\":0}],\"by_time_between_home_and_place\":[{\"time_range\":\"5-15\",\"users_in_percentage\":12.4},{\"time_range\":\"15-30\",\"users_in_percentage\":21.4},{\"time_range\":\"30-45\",\"users_in_percentage\":28.1},{\"time_range\":\"45-60\",\"users_in_percentage\":20.4},{\"time_range\":\"> 60\",\"users_in_percentage\":11.4}]}}"

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|data|[inline_response_200_7_data](#schemainline_response_200_7_data)|false|none|none|

<h2 id="tocSinline_response_200_8_data_by_day_of_week">inline_response_200_8_data_by_day_of_week</h2>

<a id="schemainline_response_200_8_data_by_day_of_week"></a>

```json
{
  "day": "string",
  "users_in_percentage": 0
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|day|string|false|none|none|
|users_in_percentage|number|false|none|none|

<h2 id="tocSinline_response_200_8_data_by_hour_of_day">inline_response_200_8_data_by_hour_of_day</h2>

<a id="schemainline_response_200_8_data_by_hour_of_day"></a>

```json
{
  "hour_range": "string",
  "users_in_percentage": 0
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|hour_range|string|false|none|none|
|users_in_percentage|number|false|none|none|

<h2 id="tocSinline_response_200_8_data_by_visit_frequency">inline_response_200_8_data_by_visit_frequency</h2>

<a id="schemainline_response_200_8_data_by_visit_frequency"></a>

```json
{
  "frequency_range": "string",
  "users_in_percentage": 0
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|frequency_range|string|false|none|none|
|users_in_percentage|number|false|none|none|

<h2 id="tocSinline_response_200_8_data_by_dwell_time">inline_response_200_8_data_by_dwell_time</h2>

<a id="schemainline_response_200_8_data_by_dwell_time"></a>

```json
{
  "dwell_time_range": "string",
  "users_in_percentage": 0
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|dwell_time_range|string|false|none|none|
|users_in_percentage|number|false|none|none|

<h2 id="tocSinline_response_200_8_data">inline_response_200_8_data</h2>

<a id="schemainline_response_200_8_data"></a>

```json
{
  "by_day_of_week": [
    {
      "day": "string",
      "users_in_percentage": 0
    }
  ],
  "by_hour_of_day": [
    {
      "hour_range": "string",
      "users_in_percentage": 0
    }
  ],
  "by_visit_frequency": [
    {
      "frequency_range": "string",
      "users_in_percentage": 0
    }
  ],
  "by_dwell_time": [
    {
      "dwell_time_range": "string",
      "users_in_percentage": 0
    }
  ]
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|by_day_of_week|[[inline_response_200_8_data_by_day_of_week](#schemainline_response_200_8_data_by_day_of_week)]|false|none|none|
|by_hour_of_day|[[inline_response_200_8_data_by_hour_of_day](#schemainline_response_200_8_data_by_hour_of_day)]|false|none|none|
|by_visit_frequency|[[inline_response_200_8_data_by_visit_frequency](#schemainline_response_200_8_data_by_visit_frequency)]|false|none|none|
|by_dwell_time|[[inline_response_200_8_data_by_dwell_time](#schemainline_response_200_8_data_by_dwell_time)]|false|none|none|

<h2 id="tocSinline_response_200_8">inline_response_200_8</h2>

<a id="schemainline_response_200_8"></a>

```json
{
  "data": {
    "by_day_of_week": [
      {
        "day": "string",
        "users_in_percentage": 0
      }
    ],
    "by_hour_of_day": [
      {
        "hour_range": "string",
        "users_in_percentage": 0
      }
    ],
    "by_visit_frequency": [
      {
        "frequency_range": "string",
        "users_in_percentage": 0
      }
    ],
    "by_dwell_time": [
      {
        "dwell_time_range": "string",
        "users_in_percentage": 0
      }
    ]
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|data|[inline_response_200_8_data](#schemainline_response_200_8_data)|false|none|none|

<h2 id="tocSinline_response_200_9_data_other_places_visited_by_category">inline_response_200_9_data_other_places_visited_by_category</h2>

<a id="schemainline_response_200_9_data_other_places_visited_by_category"></a>

```json
{
  "place_category_id": "string",
  "place_category_name": "string",
  "users_in_percentage": 0
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|place_category_id|string|false|none|none|
|place_category_name|string|false|none|none|
|users_in_percentage|number|false|none|none|

<h2 id="tocSinline_response_200_9_data_top_visited_pois">inline_response_200_9_data_top_visited_pois</h2>

<a id="schemainline_response_200_9_data_top_visited_pois"></a>

```json
{
  "place_id": "string",
  "place_name": "string",
  "link": "string",
  "users_in_percentage": 0
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|place_id|string|false|none|none|
|place_name|string|false|none|none|
|link|string|false|none|URL to fetch the details of the place|
|users_in_percentage|number|false|none|none|

<h2 id="tocSinline_response_200_9_data">inline_response_200_9_data</h2>

<a id="schemainline_response_200_9_data"></a>

```json
{
  "other_places_visited_by_category": [
    {
      "place_category_id": "string",
      "place_category_name": "string",
      "users_in_percentage": 0
    }
  ],
  "top_visited_pois": [
    {
      "place_id": "string",
      "place_name": "string",
      "link": "string",
      "users_in_percentage": 0
    }
  ]
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|other_places_visited_by_category|[[inline_response_200_9_data_other_places_visited_by_category](#schemainline_response_200_9_data_other_places_visited_by_category)]|false|none|none|
|top_visited_pois|[[inline_response_200_9_data_top_visited_pois](#schemainline_response_200_9_data_top_visited_pois)]|false|none|none|

<h2 id="tocSinline_response_200_9">inline_response_200_9</h2>

<a id="schemainline_response_200_9"></a>

```json
{
  "data": {
    "other_places_visited_by_category": [
      {
        "place_category_id": "string",
        "place_category_name": "string",
        "users_in_percentage": 0
      }
    ],
    "top_visited_pois": [
      {
        "place_id": "string",
        "place_name": "string",
        "link": "string",
        "users_in_percentage": 0
      }
    ]
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|data|[inline_response_200_9_data](#schemainline_response_200_9_data)|false|none|none|

<h2 id="tocSinline_response_200_10_before">inline_response_200_10_before</h2>

<a id="schemainline_response_200_10_before"></a>

```json
{
  "category_id": "string",
  "category_name": "string",
  "users_in_percentage": 0
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|category_id|string|false|none|Category ID|
|category_name|string|false|none|Category name of the place visited before visiting this place|
|users_in_percentage|number|false|none|none|

<h2 id="tocSinline_response_200_10_data">inline_response_200_10_data</h2>

<a id="schemainline_response_200_10_data"></a>

```json
{
  "before": [
    {
      "category_id": "string",
      "category_name": "string",
      "users_in_percentage": 0
    }
  ],
  "after": [
    {
      "category_id": "string",
      "category_name": "string",
      "users_in_percentage": 0
    }
  ]
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|before|[[inline_response_200_10_before](#schemainline_response_200_10_before)]|false|none|none|
|after|[[inline_response_200_10_before](#schemainline_response_200_10_before)]|false|none|none|

<h2 id="tocSinline_response_200_10">inline_response_200_10</h2>

<a id="schemainline_response_200_10"></a>

```json
{
  "data": [
    {
      "before": [
        {
          "category_id": "string",
          "category_name": "string",
          "users_in_percentage": 0
        }
      ],
      "after": [
        {
          "category_id": "string",
          "category_name": "string",
          "users_in_percentage": 0
        }
      ]
    }
  ]
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|data|[[inline_response_200_10_data](#schemainline_response_200_10_data)]|false|none|none|

<h2 id="tocSinline_response_200_11_data_at">inline_response_200_11_data_at</h2>

<a id="schemainline_response_200_11_data_at"></a>

```json
{
  "cateogory_id": "string",
  "app_id": "string",
  "app_display_name": "string",
  "app_publisher_name": "string",
  "ios_link": "string",
  "android_link": "string",
  "link": "string",
  "users_in_percentage": 0
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|cateogory_id|string|false|none|none|
|app_id|string|false|none|none|
|app_display_name|string|false|none|none|
|app_publisher_name|string|false|none|none|
|ios_link|string|false|none|none|
|android_link|string|false|none|none|
|link|string|false|none|none|
|users_in_percentage|number|false|none|none|

<h2 id="tocSinline_response_200_11_data">inline_response_200_11_data</h2>

<a id="schemainline_response_200_11_data"></a>

```json
{
  "at": {
    "cateogory_id": "string",
    "app_id": "string",
    "app_display_name": "string",
    "app_publisher_name": "string",
    "ios_link": "string",
    "android_link": "string",
    "link": "string",
    "users_in_percentage": 0
  },
  "before": {
    "cateogory_id": "string",
    "app_id": "string",
    "app_display_name": "string",
    "app_publisher_name": "string",
    "ios_link": "string",
    "android_link": "string",
    "link": "string",
    "users_in_percentage": 0
  },
  "after": {
    "cateogory_id": "string",
    "app_id": "string",
    "app_display_name": "string",
    "app_publisher_name": "string",
    "ios_link": "string",
    "android_link": "string",
    "link": "string",
    "users_in_percentage": 0
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|at|[inline_response_200_11_data_at](#schemainline_response_200_11_data_at)|false|none|none|
|before|[inline_response_200_11_data_at](#schemainline_response_200_11_data_at)|false|none|none|
|after|[inline_response_200_11_data_at](#schemainline_response_200_11_data_at)|false|none|none|

<h2 id="tocSinline_response_200_11">inline_response_200_11</h2>

<a id="schemainline_response_200_11"></a>

```json
{
  "data": {
    "at": {
      "cateogory_id": "string",
      "app_id": "string",
      "app_display_name": "string",
      "app_publisher_name": "string",
      "ios_link": "string",
      "android_link": "string",
      "link": "string",
      "users_in_percentage": 0
    },
    "before": {
      "cateogory_id": "string",
      "app_id": "string",
      "app_display_name": "string",
      "app_publisher_name": "string",
      "ios_link": "string",
      "android_link": "string",
      "link": "string",
      "users_in_percentage": 0
    },
    "after": {
      "cateogory_id": "string",
      "app_id": "string",
      "app_display_name": "string",
      "app_publisher_name": "string",
      "ios_link": "string",
      "android_link": "string",
      "link": "string",
      "users_in_percentage": 0
    }
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|data|[inline_response_200_11_data](#schemainline_response_200_11_data)|false|none|none|

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

