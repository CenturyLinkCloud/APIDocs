{{{
"title": "Blobs API",
"date": "09-01-2016",
"author": "",
"attachments": [],
"contentIsHTML": false
}}}

**Manage Blobs**

### URL
Uploads a file using multi-part form data.

#### Structure
```
[POST] /services/blobs/upload
```
#### Example
```
[POST] https://cam.ctl.io/services/blobs/upload
```
### Request

#### Headers
```
Content-Type: multipart/form-data
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```
#### URI Parameters
* None
#### Request body parameters
* Form data: blob (binary)

### Response
#### Normal Response Codes

- **200** OK

#### Common Error Response Codes

* Bad Request (**400**)

#### Response Parameters

| Parameter | Type |Description |
|-----------|------|------------|
| content-type | string | File content type |
| length | number | File size in bytes |
| upload_date | string | Date when file was uploaded |
| url | string | Url to download the file |

#### Response Body

```
{
    "url": "/services/blobs/download/5be2de281862a32389a50d81/Screen-Shot-2018-11-07-at-13.44.12.png",
    "upload_date": "2018-11-07 12:44:24.254860",
    "length": 12715,
    "content_type": "image/png"
}
```

### URL
Uploads a file using multi-part form data with the ability of giving file any name when saving in the system.

#### Structure
```
[POST] /services/blobs/upload/{file_name}
```
#### Example
```
[POST] https://cam.ctl.io/services/blobs/upload/another-file-name.png
```
### Request

#### Headers
```
Content-Type: multipart/form-data
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```
#### URI Parameters
* None
#### Request body parameters
* Form data: blob (binary)

### Response
#### Normal Response Codes

- **200** OK

#### Common Error Response Codes

* Bad Request (**400**)

#### Response Parameters

| Parameter | Type |Description |
|-----------|------|------------|
| content-type | string | File content type |
| length | number | File size in bytes |
| upload_date | string | Date when file was uploaded |
| url | string | Url to download the file |

#### Response Body

```
{
    "url": "/services/blobs/download/5be30e001862a32389a50d8f/another-file-name.png",
    "upload_date": "2018-11-07 16:08:32.178537",
    "length": 7264,
    "content_type": "multipart/form-data; boundary=--------------------------077273512344925050592348"
}
```
### URL
Downloads a file uploaded previously when you give the file_id and the file_name. You can get the full download URL from the response body of the file upload request.
#### Structure
```
[GET] /services/blobs/download/{file_id}/{file_name}
```
#### Example
```
[GET] https://cam.ctl.io/services/blobs/download/5be2de281862a32389a50d81/Screen-Shot-2018-11-07-at-13.44.12.png
```
### Request

#### Headers
```
Authorization: Bearer your_json_web_token
ElasticBox-Release: 4.0
```
#### URI Parameters
| NAME | TYPE | DESCRIPTION | REQ. |
|------| ---- | ----------- | ---- |
| file_id | string | File id | Yes |
| file_name | string | File name | Yes |

#### Request body parameters
* None

### Response
#### Normal Response Codes

- **200** OK

#### Common Error Response Codes

* Bad Request (**400**)

#### Response Parameters

| Parameter | Type |Description |
|-----------|------|------------|
| content-type | string | File content type |
| length | number | File size in bytes |
| upload_date | string | Date when file was uploaded |
| url | string | Url to download the file |

#### Response Body

```
The file
```


### Contacting Cloud Application Manager Support

We’re sorry you’re having an issue in [Cloud Application Manager](https://www.ctl.io/cloud-application-manager/). Please review the [troubleshooting tips](https://www.ctl.io/knowledge-base/cloud-application-manager/troubleshooting/troubleshooting-tips/), or contact [Cloud Application Manager support](mailto:incident@CenturyLink.com) with details and screenshots where possible.

For issues related to API calls, send the request body along with details related to the issue.

In the case of a box error, share the box in the workspace that your organization and Cloud Application Manager can access and attach the logs.
* Linux: SSH and locate the log at /var/log/elasticbox/elasticbox-agent.log
* Windows: RDP into the instance to locate the log at ProgramDataElasticBoxLogselasticbox-agent.log
