---
title: ContentHub API specification v1.0.0
language_tabs:
  - shell: Shell
  - http: HTTP
  - javascript: JavaScript
  - ruby: Ruby
  - python: Python
  - php: PHP
  - java: Java
  - go: Go
toc_footers: []
includes: []
search: true
highlight_theme: darkula
headingLevel: 2

---

<!-- Generator: Widdershins v4.0.1 -->

<h1 id="contenthub-api-specification">ContentHub API specification v1.0.0</h1>

> Scroll down for code samples, example requests and responses. Select a language for code samples from the tabs above or the mobile navigation menu.

# Authentication

- HTTP Authentication, scheme: bearer 

<h1 id="contenthub-api-specification-camunda">Camunda</h1>

## fetchNextTask

<a id="opIdfetchNextTask"></a>

`GET /Camunda/nextTask/{userId}`

*fetch a next unAssignTask from tasklist of job*

<h3 id="fetchnexttask-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|userId|path|string|true|user Id|

> Example responses

> 200 Response

```json
{
  "taskId": "string",
  "jobId": "string",
  "payloadId": "string",
  "storageUri": "string",
  "extractedUri": "string"
}
```

<h3 id="fetchnexttask-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved task|[TaskResponse](#schemataskresponse)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Unexpected processing error. The request can be re-submitted to the processing|[errorMessage](#schemaerrormessage)|

<aside class="success">
This operation does not require authentication
</aside>

## CompleteTask

<a id="opIdCompleteTask"></a>

`POST /Camunda/completeTask`

*Complete a task after content engineer reviewed.*

> Body parameter

```json
{
  "taskId": "string",
  "userId": "string",
  "isApproved": true
}
```

<h3 id="completetask-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[TaskRequest](#schemataskrequest)|true|Optional description in *Markdown*|

> Example responses

> 500 Response

```json
{
  "errorText": "string"
}
```

<h3 id="completetask-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Ok|None|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Unexpected processing error. The request can be re-submitted to the processing|[errorMessage](#schemaerrormessage)|

<aside class="success">
This operation does not require authentication
</aside>

## unAssignTask

<a id="opIdunAssignTask"></a>

`POST /Camunda/unassignTask`

*UnAssign task If Content engineer is not interested to review.*

> Body parameter

```json
{
  "taskId": "string",
  "userId": "string"
}
```

<h3 id="unassigntask-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[TaskUnAssignedRequest](#schemataskunassignedrequest)|true|Optional description in *Markdown*|

> Example responses

> 500 Response

```json
{
  "errorText": "string"
}
```

<h3 id="unassigntask-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Ok|None|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Unexpected processing error. The request can be re-submitted to the processing|[errorMessage](#schemaerrormessage)|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="contenthub-api-specification-workflow">Workflow</h1>

## getworkflows

<a id="opIdgetworkflows"></a>

`GET /workflow`

*Get a list of camunda workflow definitions*

> Example responses

> 200 Response

```json
[
  {
    "id": "string",
    "name": "string",
    "description": "string",
    "ispublished": true,
    "path": "string",
    "fileObject": "string"
  }
]
```

<h3 id="getworkflows-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved list of workflows|Inline|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Unexpected processing error. The request can be re-submitted to the processing|[errorMessage](#schemaerrormessage)|

<h3 id="getworkflows-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[[Workflow](#schemaworkflow)]|false|none|none|
|» id|string|false|none|none|
|» name|string|false|none|none|
|» description|string|false|none|none|
|» ispublished|boolean|false|none|none|
|» path|string|false|none|none|
|» fileObject|string(binary)|false|none|none|

<aside class="success">
This operation does not require authentication
</aside>

## uploadworkflow

<a id="opIduploadworkflow"></a>

`POST /workflow`

*Upload camunda workflow definitions*

> Body parameter

```yaml
- id: string
  name: string
  description: string
  ispublished: true
  path: string
  fileObject: string

```

<h3 id="uploadworkflow-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[Workflow](#schemaworkflow)|true|Optional description in *Markdown*|

> Example responses

> 200 Response

```json
[
  {
    "id": "string",
    "name": "string",
    "description": "string",
    "ispublished": true,
    "path": "string",
    "fileObject": "string"
  }
]
```

<h3 id="uploadworkflow-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully saved camunda workflow|Inline|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Unexpected processing error. The request can be re-submitted to the processing|[errorMessage](#schemaerrormessage)|

<h3 id="uploadworkflow-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[[Workflow](#schemaworkflow)]|false|none|none|
|» id|string|false|none|none|
|» name|string|false|none|none|
|» description|string|false|none|none|
|» ispublished|boolean|false|none|none|
|» path|string|false|none|none|
|» fileObject|string(binary)|false|none|none|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="contenthub-api-specification-metadata">Metadata</h1>

## getMetadata

<a id="opIdgetMetadata"></a>

`GET /metadata`

*Get a list of distinct metadata*

> Example responses

> 200 Response

```json
[
  {
    "id": "string",
    "tag": "string",
    "description": "string",
    "componentSource": "string",
    "isOptional": true
  }
]
```

<h3 id="getmetadata-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved list of Metadata Tags|Inline|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Unexpected processing error. The request can be re-submitted to the processing|[errorMessage](#schemaerrormessage)|

<h3 id="getmetadata-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[[MetadataInfo](#schemametadatainfo)]|false|none|none|
|» id|string|false|none|none|
|» tag|string|false|none|none|
|» description|string|false|none|none|
|» componentSource|string|false|none|none|
|» isOptional|boolean|false|none|none|

<aside class="success">
This operation does not require authentication
</aside>

## getTags

<a id="opIdgetTags"></a>

`GET /metadata/tags`

*Get a list of distinct tags*

> Example responses

> 200 Response

```json
[
  "string"
]
```

<h3 id="gettags-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Successfully retrieved list of tags|Inline|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Unexpected processing error. The request can be re-submitted to the processing|[errorMessage](#schemaerrormessage)|

<h3 id="gettags-responseschema">Response Schema</h3>

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="contenthub-api-specification-jobs">Jobs</h1>

## getJob

<a id="opIdgetJob"></a>

`GET /jobs/{jobId}`

*Get job by Id*

<h3 id="getjob-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|jobId|path|string|true|Job ID|

> Example responses

> 200 Response

```json
{
  "jobId": "string",
  "jobStartDate": "2019-08-24",
  "jobEndDate": "2019-08-24",
  "totalDetectedPayloads": 0,
  "totalProcessedPayloads": 0,
  "dataSource": {
    "type": "string",
    "location": "string",
    "principle": "string"
  }
}
```

<h3 id="getjob-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A collection of job objects|[Job](#schemajob)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|The request cannot be processed due to the format or request data value|[errorMessage](#schemaerrormessage)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Unexpected processing error. The request can be re-submitted to the processing|[errorMessage](#schemaerrormessage)|

<aside class="success">
This operation does not require authentication
</aside>

## updateJobById

<a id="opIdupdateJobById"></a>

`PUT /jobs/{jobId}`

*update job by Id*

> Body parameter

```json
{
  "jobId": "string",
  "jobStartDate": "2019-08-24",
  "jobEndDate": "2019-08-24",
  "totalDetectedPayloads": 0,
  "totalProcessedPayloads": 0,
  "dataSource": {
    "type": "string",
    "location": "string",
    "principle": "string"
  }
}
```

<h3 id="updatejobbyid-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[Job](#schemajob)|false|none|

> Example responses

> 200 Response

```json
{
  "jobId": "string",
  "jobStartDate": "2019-08-24",
  "jobEndDate": "2019-08-24",
  "totalDetectedPayloads": 0,
  "totalProcessedPayloads": 0,
  "dataSource": {
    "type": "string",
    "location": "string",
    "principle": "string"
  }
}
```

<h3 id="updatejobbyid-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A collection of job objects|[Job](#schemajob)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|The request cannot be processed due to the format or request data value|[errorMessage](#schemaerrormessage)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Unexpected processing error. The request can be re-submitted to the processing|[errorMessage](#schemaerrormessage)|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="contenthub-api-specification-payloads">Payloads</h1>

## getPayloads

<a id="opIdgetPayloads"></a>

`GET /jobs/{jobId}/payloads`

*Get all Payloads by JobID*

<h3 id="getpayloads-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|jobId|path|string|true|Job ID|
|includeMetadata|query|boolean|false|If true, returns metadata information for each payload|
|startPosition|query|number(integer)|false|Page Start Position|
|elementCount|query|number(integer)|false|Page Element Count. If not specified returns all elements|

> Example responses

> 200 Response

```json
[
  {
    "jobId": "string",
    "Id": "string",
    "Size": 0,
    "InternalReference": "string",
    "OriginalURI": "string",
    "Checksum": "string",
    "ExtractedURI": "string",
    "metadata": {
      "name": "string"
    },
    "securityClaims": {
      "name": "string"
    }
  }
]
```

<h3 id="getpayloads-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|A collection of Payload objects|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|The request cannot be processed due to the format or request data value|[errorMessage](#schemaerrormessage)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Unexpected processing error. The request can be re-submitted to the processing|[errorMessage](#schemaerrormessage)|

<h3 id="getpayloads-responseschema">Response Schema</h3>

Status Code **200**

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|*anonymous*|[[Payload](#schemapayload)]|false|none|none|
|» jobId|string|false|none|none|
|» Id|string|false|none|none|
|» Size|integer|false|none|none|
|» InternalReference|string|false|none|none|
|» OriginalURI|string|false|none|none|
|» Checksum|string|false|none|none|
|» ExtractedURI|string|false|none|none|
|» metadata|[Element](#schemaelement)|false|none|none|
|»» name|string|false|none|none|
|» securityClaims|[Element](#schemaelement)|false|none|none|

<aside class="success">
This operation does not require authentication
</aside>

## getPayload

<a id="opIdgetPayload"></a>

`GET /jobs/{jobId}/payloads/{payloadId}`

*Download payload by ID*

<h3 id="getpayload-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|jobId|path|string|true|Job ID|
|payloadId|path|string|true|Payload ID|

> Example responses

> 200 Response

```json
{
  "jobId": "string",
  "Id": "string",
  "Size": 0,
  "InternalReference": "string",
  "OriginalURI": "string",
  "Checksum": "string",
  "ExtractedURI": "string",
  "metadata": {
    "name": "string"
  },
  "securityClaims": {
    "name": "string"
  }
}
```

<h3 id="getpayload-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Payload data|[Payload](#schemapayload)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|The request cannot be processed due to the format or request data value|[errorMessage](#schemaerrormessage)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Unexpected processing error. The request can be re-submitted to the processing|[errorMessage](#schemaerrormessage)|

<aside class="success">
This operation does not require authentication
</aside>

## update payload by Id

<a id="opIdupdate payload by Id"></a>

`PUT /jobs/{jobId}/payloads/{payloadId}`

*Update payload by ID*

> Body parameter

```json
{
  "jobId": "string",
  "Id": "string",
  "Size": 0,
  "InternalReference": "string",
  "OriginalURI": "string",
  "Checksum": "string",
  "ExtractedURI": "string",
  "metadata": {
    "name": "string"
  },
  "securityClaims": {
    "name": "string"
  }
}
```

<h3 id="update-payload-by-id-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|body|body|[Payload](#schemapayload)|false|none|

> Example responses

> 200 Response

```json
{
  "jobId": "string",
  "Id": "string",
  "Size": 0,
  "InternalReference": "string",
  "OriginalURI": "string",
  "Checksum": "string",
  "ExtractedURI": "string",
  "metadata": {
    "name": "string"
  },
  "securityClaims": {
    "name": "string"
  }
}
```

<h3 id="update-payload-by-id-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Payload data|[Payload](#schemapayload)|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|The request cannot be processed due to the format or request data value|[errorMessage](#schemaerrormessage)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Unexpected processing error. The request can be re-submitted to the processing|[errorMessage](#schemaerrormessage)|

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="contenthub-api-specification-payload-metadata">Payload Metadata</h1>

## getMegadata groups

<a id="opIdgetMegadata groups"></a>

`GET /jobs/{jobId}/payloads/{payloadId}/metadata`

*Get Payload Metadata by payloadID*

<h3 id="getmegadata-groups-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|jobId|path|string|true|Job ID|
|payloadId|path|string|true|Payload ID|
|includeElements|query|boolean|false|If true, returns metadata elements for each metadata group|
|startPosition|query|number(integer)|false|Page Start Position|
|elementCount|query|number(integer)|false|Page Element Count. If not specified returns all elements|

> Example responses

> 200 Response

```json
{
  "classificationKind": "Brochure",
  "dataSource": "Hitachi Energy",
  "displayTitle.languageCode": "en",
  "displayTitle.title": "EconiQ - Eco-efficient high-voltage portfolio",
  "documentType": "Public",
  "fileExtension": "pdf",
  "fileSize": 3,
  "fileUnit": "MB",
  "identification.contentLanguages": "en",
  "identification.documentNumber": "9AKK107992A1307",
  "identification.partId": "",
  "identification.revision": "AJ",
  "revisionDate": "2024-02-21T07:35:26+00:00",
  "summary": "4-pages technology brochure"
}
```

<h3 id="getmegadata-groups-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|Metadata information of the payload|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|The request cannot be processed due to the format or request data value|[errorMessage](#schemaerrormessage)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Unexpected processing error. The request can be re-submitted to the processing|[errorMessage](#schemaerrormessage)|

<h3 id="getmegadata-groups-responseschema">Response Schema</h3>

<aside class="success">
This operation does not require authentication
</aside>

<h1 id="contenthub-api-specification-payloads-security-cliams">Payloads Security Cliams</h1>

## getPayloadSecurityClaims

<a id="opIdgetPayloadSecurityClaims"></a>

`GET /jobs/{jobId}/payloads/{payloadId}/security`

*Get Payload securty claims by payloadID*

<h3 id="getpayloadsecurityclaims-parameters">Parameters</h3>

|Name|In|Type|Required|Description|
|---|---|---|---|---|
|jobId|path|string|true|Job ID|
|payloadId|path|string|true|Payload ID|
|startPosition|query|number(integer)|false|Page Start Position|
|elementCount|query|number(integer)|false|Page Element Count. If not specified returns all elements|

> Example responses

> 200 Response

```json
{
  "principle": "",
  "principleType": "PUBLIC"
}
```

<h3 id="getpayloadsecurityclaims-responses">Responses</h3>

|Status|Meaning|Description|Schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|security claims of the payload|Inline|
|400|[Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)|The request cannot be processed due to the format or request data value|[errorMessage](#schemaerrormessage)|
|500|[Internal Server Error](https://tools.ietf.org/html/rfc7231#section-6.6.1)|Unexpected processing error. The request can be re-submitted to the processing|[errorMessage](#schemaerrormessage)|

<h3 id="getpayloadsecurityclaims-responseschema">Response Schema</h3>

<aside class="success">
This operation does not require authentication
</aside>

# Schemas

<h2 id="tocS_errorMessage">errorMessage</h2>
<!-- backwards compatibility -->
<a id="schemaerrormessage"></a>
<a id="schema_errorMessage"></a>
<a id="tocSerrormessage"></a>
<a id="tocserrormessage"></a>

```json
{
  "errorText": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|errorText|string|false|none|none|

<h2 id="tocS_Job">Job</h2>
<!-- backwards compatibility -->
<a id="schemajob"></a>
<a id="schema_Job"></a>
<a id="tocSjob"></a>
<a id="tocsjob"></a>

```json
{
  "jobId": "string",
  "jobStartDate": "2019-08-24",
  "jobEndDate": "2019-08-24",
  "totalDetectedPayloads": 0,
  "totalProcessedPayloads": 0,
  "dataSource": {
    "type": "string",
    "location": "string",
    "principle": "string"
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|jobId|string|false|none|none|
|jobStartDate|string(date)|false|none|Job Start Date (GMT) in Epoch Unix timestamp format|
|jobEndDate|string(date)|false|none|Job Start Date (GMT) in Epoch Unix timestamp format|
|totalDetectedPayloads|integer|false|none|none|
|totalProcessedPayloads|integer|false|none|none|
|dataSource|[DataSource](#schemadatasource)|false|none|none|

<h2 id="tocS_Payload">Payload</h2>
<!-- backwards compatibility -->
<a id="schemapayload"></a>
<a id="schema_Payload"></a>
<a id="tocSpayload"></a>
<a id="tocspayload"></a>

```json
{
  "jobId": "string",
  "Id": "string",
  "Size": 0,
  "InternalReference": "string",
  "OriginalURI": "string",
  "Checksum": "string",
  "ExtractedURI": "string",
  "metadata": {
    "name": "string"
  },
  "securityClaims": {
    "name": "string"
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|jobId|string|false|none|none|
|Id|string|false|none|none|
|Size|integer|false|none|none|
|InternalReference|string|false|none|none|
|OriginalURI|string|false|none|none|
|Checksum|string|false|none|none|
|ExtractedURI|string|false|none|none|
|metadata|[Element](#schemaelement)|false|none|none|
|securityClaims|[Element](#schemaelement)|false|none|none|

<h2 id="tocS_Element">Element</h2>
<!-- backwards compatibility -->
<a id="schemaelement"></a>
<a id="schema_Element"></a>
<a id="tocSelement"></a>
<a id="tocselement"></a>

```json
{
  "name": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|name|string|false|none|none|

<h2 id="tocS_ElementGroup">ElementGroup</h2>
<!-- backwards compatibility -->
<a id="schemaelementgroup"></a>
<a id="schema_ElementGroup"></a>
<a id="tocSelementgroup"></a>
<a id="tocselementgroup"></a>

```json
{
  "elements": [
    {
      "name": "string"
    }
  ]
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|elements|[[Element](#schemaelement)]|false|none|none|

<h2 id="tocS_DataSource">DataSource</h2>
<!-- backwards compatibility -->
<a id="schemadatasource"></a>
<a id="schema_DataSource"></a>
<a id="tocSdatasource"></a>
<a id="tocsdatasource"></a>

```json
{
  "type": "string",
  "location": "string",
  "principle": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|type|string|false|none|none|
|location|string|false|none|none|
|principle|string|false|none|none|

<h2 id="tocS_PaginationInfo">PaginationInfo</h2>
<!-- backwards compatibility -->
<a id="schemapaginationinfo"></a>
<a id="schema_PaginationInfo"></a>
<a id="tocSpaginationinfo"></a>
<a id="tocspaginationinfo"></a>

```json
{
  "pageNumber": 0,
  "pageSize": 0
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|pageNumber|integer|false|none|none|
|pageSize|integer|false|none|none|

<h2 id="tocS_Notification">Notification</h2>
<!-- backwards compatibility -->
<a id="schemanotification"></a>
<a id="schema_Notification"></a>
<a id="tocSnotification"></a>
<a id="tocsnotification"></a>

```json
{
  "id": "string",
  "name": "string",
  "description": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string|false|none|Unique identifier of the notification.|
|name|string|false|none|Name of the notification.|
|description|string|false|none|The notification message|

<h2 id="tocS_MetadataInfo">MetadataInfo</h2>
<!-- backwards compatibility -->
<a id="schemametadatainfo"></a>
<a id="schema_MetadataInfo"></a>
<a id="tocSmetadatainfo"></a>
<a id="tocsmetadatainfo"></a>

```json
{
  "id": "string",
  "tag": "string",
  "description": "string",
  "componentSource": "string",
  "isOptional": true
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string|false|none|none|
|tag|string|false|none|none|
|description|string|false|none|none|
|componentSource|string|false|none|none|
|isOptional|boolean|false|none|none|

<h2 id="tocS_Workflow">Workflow</h2>
<!-- backwards compatibility -->
<a id="schemaworkflow"></a>
<a id="schema_Workflow"></a>
<a id="tocSworkflow"></a>
<a id="tocsworkflow"></a>

```json
{
  "id": "string",
  "name": "string",
  "description": "string",
  "ispublished": true,
  "path": "string",
  "fileObject": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string|false|none|none|
|name|string|false|none|none|
|description|string|false|none|none|
|ispublished|boolean|false|none|none|
|path|string|false|none|none|
|fileObject|string(binary)|false|none|none|

<h2 id="tocS_WorkflowRouter">WorkflowRouter</h2>
<!-- backwards compatibility -->
<a id="schemaworkflowrouter"></a>
<a id="schema_WorkflowRouter"></a>
<a id="tocSworkflowrouter"></a>
<a id="tocsworkflowrouter"></a>

```json
{
  "id": "string",
  "name": "string",
  "taxonomy": "string",
  "workflow": {
    "id": "string",
    "name": "string",
    "description": "string",
    "ispublished": true,
    "path": "string",
    "fileObject": "string"
  }
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|id|string|false|none|none|
|name|string|false|none|none|
|taxonomy|string|false|none|none|
|workflow|[Workflow](#schemaworkflow)|false|none|none|

<h2 id="tocS_TaskRequest">TaskRequest</h2>
<!-- backwards compatibility -->
<a id="schemataskrequest"></a>
<a id="schema_TaskRequest"></a>
<a id="tocStaskrequest"></a>
<a id="tocstaskrequest"></a>

```json
{
  "taskId": "string",
  "userId": "string",
  "isApproved": true
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|taskId|string|false|none|none|
|userId|string|false|none|none|
|isApproved|boolean|false|none|none|

<h2 id="tocS_TaskUnAssignedRequest">TaskUnAssignedRequest</h2>
<!-- backwards compatibility -->
<a id="schemataskunassignedrequest"></a>
<a id="schema_TaskUnAssignedRequest"></a>
<a id="tocStaskunassignedrequest"></a>
<a id="tocstaskunassignedrequest"></a>

```json
{
  "taskId": "string",
  "userId": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|taskId|string|false|none|none|
|userId|string|false|none|none|

<h2 id="tocS_TaskResponse">TaskResponse</h2>
<!-- backwards compatibility -->
<a id="schemataskresponse"></a>
<a id="schema_TaskResponse"></a>
<a id="tocStaskresponse"></a>
<a id="tocstaskresponse"></a>

```json
{
  "taskId": "string",
  "jobId": "string",
  "payloadId": "string",
  "storageUri": "string",
  "extractedUri": "string"
}

```

### Properties

|Name|Type|Required|Restrictions|Description|
|---|---|---|---|---|
|taskId|string|false|none|none|
|jobId|string|false|none|none|
|payloadId|string|false|none|none|
|storageUri|string|false|none|none|
|extractedUri|string|false|none|none|

