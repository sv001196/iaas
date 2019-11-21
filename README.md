--- 

title: Places API 

language_tabs: 
   - shell 

toc_footers: 
   - <a href='#'>Sign Up for a Developer Key</a> 
   - <a href='https://github.com/lavkumarv'>Documentation Powered by lav</a> 

includes: 
   - errors 

search: true 

--- 

# Introduction 

Places API returns information about a place(s) of interest. 

**Version:** 1.0.0 

# /PLACES
## ***GET*** 

**Summary:** returns the details of one or more places

**Description:** Pass one or more comma separated place ids to fetch the details of the places. A single request can return details up to 50 places.


### HTTP Request 
`***GET*** /places` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| ids | query | comma separated list of place ids. Up to 50 place ids can be passed. If this parameter is not specified, all the places available in the system shall be returned in a paginated manner. To limit the number of places returned per request, specify limit and offset in the query parameters. | Yes | string |
| limit | query | Limits the number of place objects returned per request. This parameter is used only when ids parameter is not specified in the request. If limit is not specified, the API will return 50 place objects | No | number |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | list of place objects |
| 400 | bad input parameter |

## ***POST*** 

**Summary:** adds an inventory item

**Description:** Adds an item to the system

### HTTP Request 
`***POST*** /places` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| inventoryItem | body | Inventory item to add | No |  |

**Responses**

| Code | Description |
| ---- | ----------- |
| 201 | item created |
| 400 | invalid input, object invalid |
| 409 | an existing item already exists |

# /PLACES/SEARCH
## ***GET*** 

**Summary:** returns the details of one or more places

**Description:** Pass one or more comma separated place ids to fetch the details of the places. A single request can return details up to 50 places.


### HTTP Request 
`***GET*** /places/search` 

**Parameters**

| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| ids | query | comma separated list of place ids. Up to 50 place ids can be passed. If this parameter is not specified, all the places available in the system shall be returned in a paginated manner. To limit the number of places returned per request, specify limit and offset in the query parameters. | Yes | string |
| limit | query | Limits the number of place objects returned per request. This parameter is used only when ids parameter is not specified in the request. If this parameter is not specified, the API will return 50 place objects | No | number |

**Responses**

| Code | Description |
| ---- | ----------- |
| 200 | list of place objects |
| 400 | bad input parameter |

<!-- Converted with the swagger-to-slate https://github.com/lavkumarv/swagger-to-slate -->
