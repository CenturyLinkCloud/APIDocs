{{{
"title": "Cost Centers API",
"date": "12-19-2018",
"author": "Julio Castanar",
"attachments": [],
"contentIsHTML": false,
"keywords": ["cam", "cloud application manager", "api", "cost center"]
}}}

**Manage Cost Centers**

| Resource | Description |
|----------|-------------|
| [POST /services/costcenters](#post-servicescostcenters) | Creates a Cost Center. |
| [GET /services/costcenters/{costcenter_id}](#get-servicescostcenters) |  Fetches an existing Cost Center. |
| [PUT /services/costcenters/{costcenter_id}](#put-servicescostcenters) | Updates an existing Cost Center.|
| [DELETE /services/costcenters/{costcenter_id}](#delete-servicescostcenters) | Deletes an existing Cost Center.|

## POST /services/costcenters

Creates a new Cost Center and gets the created Cost Center

### URL

#### Structure
```
[POST] /services/costcenters
```
#### Example
```
[POST] https://cam.ctl.io/services/costcenters
```
### Request

#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```
#### URI Parameters

* None

#### Request body parameters

| Name | Type |Description | Req. |
|------|------|------------|------|
| name | string | Cost Center name. | Yes  |
| organization | string | Name of the organization with access to the Cost Center. | Yes |
| schema | string | Cost Center schema. Always “http://elasticbox.net/schemas/costcenter” | Yes  |
| members | array | Members' id list of the Cost Center as Administrators. | No |

##### Members list parameters

An item in the list `members` require 3 parameters:

| Parameter | Type |Description | Req. |
|-----------|------|------------|------|
| id | string | can then be a workspace ID or a ldap group DN. | Yes |
| role | string | always is *administrator*. | No |
| type | string | can be *workspace* (default) or *ldap*. | No |


```
{
    "name": "Cost Center example",
    "organization": "camdemo",
    "schema": "http://elasticbox.net/schemas/costcenter",
    "members":[{"id":"camdemo"}]
}
```

### Response

#### Normal Response Codes

- **201** Created

#### Common Error Response Codes

- **400** Bad Request
- **401** Unauthorized

#### Headers

```
Content-Type: application/json
Content-Length: 489
Date: Thu, 27 Dec 2018 09:57:34 GMT
Elasticbox-Release: 4.0.0
```
#### Response Parameters

| Parameter | Type |Description |
|-----------|------|------------|
| clc_alias | string | Costcenter account alias in the organization. |
| created | string | Creation date. Example “2015-07-02 10:23:47.748740” |
| deleted | object | Identifies whether the Cost Center is deleted; *null* for existing objects. |
| id | string | Cost Center unique identifier. |
| members | array | Members' list of a Cost Center. See [Member parameters](#members-list-parameters) |
| name | string | Cost Center name |
| organization | string | Organization which the Cost Center belongs to. |
| schema | string | Schema URI. http://elasticbox.net/schemas/costcenter. |
| updated | string | Date of the last update. Example “2018-10-30 16:03:14.409029” |
| uri | string | Cost Center URI. |

#### Response Body

```
{
    "created": "2018-12-27 10:53:26.389183",
    "deleted": null,
    "id": "1072ca63-d84d-42f2-87a5-f09c72338eb1",
    "members": [{"role": "administrator","id": "camdemo"}],
    "name": "Cost Center example",
    "organization": "camdemo",
    "schema": "http://elasticbox.net/schemas/costcenter",
    "updated": "2018-12-27 10:53:26.389183",
    "uri": "/services/costcenters/1072ca63-d84d-42f2-87a5-f09c72338eb1"
}
```

## GET /services/costcenters

Fetches an existing Cost Center.

### URL

#### Structure
```
[GET] /services/costcenters/{costcenter_id}
```
#### Example
```
[GET] https://cam.ctl.io/services/costcenters/1072ca63-d84d-42f2-87a5-f09c72338eb1
```
### Request

#### Headers

```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```

#### URI Parameters
| Name | Type | Description | Req. |
|------| ---- | ----------- | ---- |
| costcenter_id | string | Cost Center ID | Yes |

#### Request body parameters
* None

### Response

#### Normal Response Codes

- **200** OK

#### Common Error Response Codes
- **400** Bad Request
- **401** Unauthorized
- **404** Not Found

#### Response Parameters

| Parameter | Type |Description |
|-----------|------|------------|
| clc_alias | string | Costcenter account alias in the organization. |
| created | string | Creation date. Example “2015-07-02 10:23:47.748740” |
| deleted | object | Identifies whether the Cost Center is deleted. |
| id | string | Cost Center unique identifier. |
| members | array | Members' list of a Cost Center. See [Member parameters](#members-list-parameters) |
| name | string | Cost Center name |
| organization | string | Organization which the Cost Center belongs to. |
| schema | string | Schema URI. http://elasticbox.net/schemas/costcenter. |
| updated | string | Date of the last update. Example “2018-10-30 16:03:14.409029” |
| uri | string | Cost Center URI. |

#### Response Body

```
{
    "updated": "2018-10-30 16:03:14.409029",
    "name": "Cost Center example",
    "created": "2015-07-02 10:23:47.748740",
    "deleted": null,
    "uri": "/services/costcenters/1072ca63-d84d-42f2-87a5-f09c72338eb1",
    "members": [
        {
            "type": "workspace",
            "role": "administrator",
            "id": "camdemo"
        },
    ],
    "clc_alias": "A73B",
    "organization": "camdemo",
    "id": "1072ca63-d84d-42f2-87a5-f09c72338eb1",
    "schema": "http://elasticbox.net/schemas/costcenter"
}
```

## PUT /services/costcenters

Updates one or several values on an existing Cost Center.

**Note:**
Be careful using this command because you can add or remove some values depending on whether they are included or not as a request parameter. We recommend first obtain this data with GET command and then make changes over them. 

Pay attention to values like *members* which will be added or deleted if they exists or not in the request parameter.  

### URL

#### Structure
```
[PUT] /services/costcenters/{costcenter_id}
```
#### Example
```
[PUT] https://cam.ctl.io/services/costcenters/1072ca63-d84d-42f2-87a5-f09c72338eb1
```
### Request

#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```
#### URI Parameters
| Name | Type | Description | Req. |
|------| ---- | ----------- | ---- |
| costcenter_id | string | Cost Center ID | Yes |

#### Request body parameters

| Name | Type | Description | Req. |
|------| ---- | ----------- | ---- |
| id | string | Cost Center unique identifier. | Yes |
| members | array | Members' list of the Cost Center. See [Member parameters](#members-list-parameters) | Yes |
| name | string | Cost Center name. | Yes |
| organization | string | Organization which the Cost Center belongs to. | Yes |
| schema | string | Schema URI. http://elasticbox.net/schemas/costcenter. | Yes |
| icon_metadata | string | Icon used for the Cost Center account.. | No |

**Note:**
Be careful using this command because some values like *members* will be added or deleted if they exists or not in the request parameter. To not be deleted an existing member, just give its member id.

```
{
    "id":"1072ca63-d84d-42f2-87a5-f09c72338eb1",
    "name":"Cost Center example",
    "organization":"camdemo",
    "schema":"http://elasticbox.net/schemas/costcenter",
    "members":[{"id":"camdemo"}]
}

```

### Response

#### Normal Response Codes

- **200** OK

#### Common Error Response Codes
- **400** Bad Request
- **401** Unauthorized
- **404** Not Found

#### Headers

```
Content-Type: application/json
Content-Length: 489
Date: Thu, 27 Dec 2018 09:57:34 GMT
Elasticbox-Release: 4.0.0
```

#### Response Parameters

* None

#### Response Body

* See response in [GET command](#get-servicescostcenters).



## DELETE /services/costcenters

Deletes an existing Cost Center of the authenticated user.

### URL

#### Structure
```
[DELETE] /services/costcenters/{costcenter_id}
```
#### Example
```
[DELETE] https://cam.ctl.io/services/costcenters/1072ca63-d84d-42f2-87a5-f09c72338eb1
```

### Request

#### Headers
```
Content-Type: application/json
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```

#### URI Parameters
| Name | Type | Description | Req. |
|------| ---- | ----------- | ---- |
| costcenter_id | string | Cost Center ID | Yes |

#### Request body parameters

* None

### Response

#### Normal Response Codes

- **204** OK - No Content

#### Common Error Response Codes
- **401** Unauthorized
- **404** Not Found

#### Response Parameters

* None

#### Response Body

* None
