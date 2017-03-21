# SMS 

Sending and querying SMS Messages.

- messages 
  - send
  - list / search / sort 
- numbers
  - create
  - list / search / sort 
- logs 
  - list / search / sort 
- products 

## Overview ##

### Resource CRUD ###

| Resource | <b>POST</b><br><i>Create</i> | <b>GET</b><br><i>Read</i> | <b>PUT</b><br><i>Update</i> | <b>DELETE</b><br><i>Delete</i> |
|----------|--------|------|--------|--------|
| {messages}    | NA - Use [Send SMS](#send-sms-message) | We do not really create a message so use logs to get details | Error | Error |
| /numbers | - Create if null<br>- Update otherwise | List all `tn` data | Error | Error |
| /numbers/{`tn`} | Error | List data for `tn` | - If `tn` exists, update it.<br> - If not - Error | Delete a `tn` |
| /logs | Error | List Sdr details with search and sort features | Error | Error |
| /products | Error <br> Managed by the system (Armand)| List Sdr details with search and sort features | Error | Error |


To send an SMS, use [Send SMS](#send-sms-message)


 <br>Link to [Delete all dogs](#delete-all-dogs)
 <br>Link to [List all dogs](#list-dogs)
 <br>Link to [Dogs - Error Codes](#dogs-error-codes)
 <br>Link to [James](#james)


## Send Messages

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-post">POST</i>
		<h6>/sms/v1/send     [Verb]</h6>
	</div>
</div>

```http
POST /sms/v1/send HTTP/1.1
Content-Type: application/json

{
    "text":"Test 3 for 2 numbers :) ",
    "from": "12149979912",
    "to": [ "15022692525", "16788523301" ],
    "referenceId" : "myRefId",
    "_log": {
        "app": "textland",
        "serverId": "docker-11445fgh",
        "gmsId": "wek23h42kkjhwk2jhkreuobuob",        
    }
}
```

```shell
curl -X POST https://api.sipstorm.com/sms/v1/send \
    -H "Content-Type: application/json" \
    -d '{
    "text":"Test 3 for 2 numbers :) ",
    "from": "12149979912",
    "to": [ "15022692525", "16788523301"],
    "referenceId" : "myRefId"
}'
```

> Example OK Response

```json
{
  "status": 200,
  "statusCode": "Queued",
  "message": "The messages have been queued to send.",
  "requestBody": {
    "text": "Test 3 for 2 numbers :) ",
    "from": "12149979912",
    "to": [ "15022692525", "16788523301"],
    "referenceId" : "myRefId"
  }
}
```

> Example Error Response

```json
{
  "status": 400,
  "statusCode": "MissingFromNumber",
  "message": "The required `from` telephone number was not provided. You MUST provide a valid from TN.",
  "moreInfo": "http://api.sipstorm.com/sms/v1/sms-errors",
  "requestBody": {
    "text": "Test 3 for 2 numbers :) ",
    "from": "12149979912",
    "to": [ "15022692525", "16788523301"],
    "referenceId" : "myRefId"
  }  
}
```

### SMS Messages - Attributes ###
SMS Attributes go here.

| Attribute | Type | Description |
|-----------|------|-------------|
|`text`         | string |The message to be sent <i class="label label-info">required</i>|
|`from`         | string |The originating telephone number (TN) <i class="label label-info">required</i>|
|`to`        | [ string ] | An `array` of terminating Telephone Number <i class="label label-info">required</i>|
|`referenceId`        | string |This is a user defined tracking string. <br>Length Limit = 40.  Alphanumeric [no special characters or white space]. <br>If left blank the server will create a default value. <i class="label label-info">optional</i>|
|`_log.app`         | string |The app you are sending from.<br>Example: `textland` <i class="label label-info">recommended</i>|
|`_log.serverId`         | string |The ID of the server you are sending from.<br>Example: `docker-11445fgh` <i class="label label-info">recommended</i>|
|`_log.gmsId`         | string |The Global Matched Session Id that can be used to match this tranaction with other transactions from other services <i class="label label-info">recommended</i>|



### SMS Messages - Response Codes ###
Sending an SMS can create errors.

| Status    | Status Code | Message | Notes |
|-----------|------|-------------|------|
|200         | Queued | The messages have been queued to send. | Messages get queued to make sure only 1 text per second is sent by any given originating (`to`) number.|
|400         | MissingFromNumber |The required `from` telephone number was not provided. You MUST provide a valid from TN. | |
|400         | InvalidToField |The `to` field is either not an array or has bad data in it.	Make sure it is an array of telephone numbers. | See example.|
|404         | InvalidFromNumber |The `from` telephone number has not been provisioned so may not send texts.  Please make sure the number is provisioned via the SMS number provisioning system.| This would usually be done at the time the account is set up by Perry's services. |
|500         | Redis Error | Redis server had an error {Plus the Error}.| Example: redis communication failure connection refused. |
|500         | ElasticSearch Error | ElasticSearch had an error {Plus the Error}.| |




## Paging ##

This is a paging area





## <a name="sms-get-logs-errors"></a>James ##

This is the James Section



## Get Log Messages

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-get">GET</i>
		<h6>/sms/v1/logs{?uri-Parameters}</h6>
	</div>
</div>

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-get">GET</i>
		<h6>/sms/v1/logs/{messageId}{?uri-Parameters}</h6>
	</div>
</div>

```http
GET /sms/v1/messages HTTP/1.1
Content-Type: application/json
```

```http
GET /sms/v1/messages?timestampStart=2016-01-01 HTTP/1.1
Content-Type: application/json
```

```http
GET /sms/v1/messages?referenceId=My_Brown_Fox HTTP/1.1
Content-Type: application/json
```

```http
GET /sms/v1/messages?message=Where%20are%20you&to=18135791001 HTTP/1.1
Content-Type: application/json
```

```shell
curl -X GET https://api.sipstorm.com/sms/v1/messages \
    -H "Content-Type: application/json"
```

> Example OK Response

```json
{
  "status": 200,
  "_data": [
      {
        "stuff": "here"
      },
      {
        "stuff": "here"
      }
  ]
}
```

> Example Error Response

```json
{
  "status": 404,
  "statusCode": "NotFound",
  "message": "Was not able to find a record for the criteria.",
  "_data" : []
}
```

### URI  ###


| Attribute | Type | Choices | Default | Description |
|-----------|------|---------|---------|-------------|
|`messageId`         | string | | | The unique message Id. |
|`message`         | string | | | Text message contains this phrase.  |
|`from`         | string | | | A `from` telephone number. |
|`to`         | string | | | A `to` telephone number. |
|`timestampStart`  | ISO-8601 | | Beginning of time | Examples:<br> '2017-03-21T15:51:34Z' <br>'2017-03-21' |
|`timestampEnd`  | ISO-8601 | | End of time | Examples:<br> '2017-03-21T15:51:34Z' <br>'2017-03-21' |
|`referenceId`         | string | | | A `referenceId` use in sending messages. |
|`app`         | string | `textland`, etc.| | The data entered as `_log.app` when sending the message. Leave the value empty to find those with no `app` data. |
|`serverId`         | string | | | The data entered as `_log.serverId` when sending the message. Leave the value empty to find those with no `serverId` data. |
|`gmsId`         | string | | | The data entered as `_log.gmsId` when sending the message. Leave the value empty to find those with no `gmsId` data. |
|`limit`         | int | | 50 | The quantity to return. |
|`offset`         | int | | 0 | The beginning number. |
|`sortBy`        | string | `from`<br> `to`<br> `referenceId`<br> `timestamp` | | Sort by ascending or descending order. |
|`sortDirection`        | string | `asc`<br> `desc` | asc | Sort by ascending or descending order. |


### Response Codes ###
Sending an SMS can create errors.

| Status    | Status Code | Message | Notes |
|-----------|------|-------------|------|
|200         |  | | This is an OK request.  See "_data" for response.|
|400         | InvalidOffset |The `offset` was not an integer, was less than zero (0) or greater than the number of records.| |
|400         | InvalidSortBy | The `sortBy` field was not a valid field.  Use  `to`, `from`, or `referenceId` | |
|400         | InvalidSortDirection | The `sortDirection` field was not as sting or a valid value.  Use  `asc` or `desc` | |
|404         | NotFound |Was not able to find a record for the criteria. | |




[//]: # (===================================================================)
[//]: # ( Number Create Section  )
[//]: # (===================================================================)


## Number - Create ##

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-post">POST</i>
		<h6>/sms/v1/numbers</h6>
	</div>
</div>

```http
POST /sms/v1/numbers HTTP/1.1
Content-Type: application/json

{
    "number": "12149979912",
    "product" : "textland",
    "_log": {
        "app": "textland",
        "serverId": "docker-11445fgh",
        "gmsId": "wek23h42kkjhwk2jhkreuobuob",        
    }
}
```

> Example OK Response

```json
{
  "status": 200,
  "_data": [
      {
        "stuff": "here"
      },
      {
        "stuff": "here"
      }
  ]
}
```

> Example Error Response

```json
{
  "status": 404,
  "statusCode": "NotFound",
  "message": "Was not able to find a record for the criteria.",
  "_data" : []
}
```

| Attribute | Type | Description |
|-----------|------|-------------|
|`number`         | string | E164 (without plus sign) for the subscriber telephone number <i class="label label-info">required</i>|
|`product`         | string | A valid product.  XXXX  See Get/List Products XXXX <i class="label label-info">required</i>|
|`_log.app`         | string |The app you are sending from.<br>Example: `textland` <i class="label label-info">recommended</i>|
|`_log.serverId`         | string |The ID of the server you are sending from.<br>Example: `docker-11445fgh` <i class="label label-info">recommended</i>|
|`_log.gmsId`         | string |The Global Matched Session Id that can be used to match this tranaction with other transactions from other services <i class="label label-info">recommended</i>|




[//]: # (===================================================================)
[//]: # ( Number UPDATE  )
[//]: # (===================================================================)




## Number - Update ##

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-put">PUT</i>
		<h6>/sms/v1/numbers/{tn}</h6>
	</div>
</div>


```http
POST /sms/v1/numbers/{tn} HTTP/1.1
Content-Type: application/json

{
    "product" : "textland",
    "_log": {
        "app": "textland",
        "serverId": "docker-11445fgh",
        "gmsId": "wek23h42kkjhwk2jhkreuobuob",        
    }
}
```

> Example OK Response

```json
{
  "status": 200,
  "_data": [
      {
        "stuff": "here"
      },
      {
        "stuff": "here"
      }
  ]
}
```

> Example Error Response

```json
{
  "status": 404,
  "statusCode": "NotFound",
  "message": "Was not able to find a record for the criteria.",
  "_data" : []
}
```

| Attribute | Type | Description |
|-----------|------|-------------|
|`product`         | string | A valid product.  XXXX  See Get/List Products XXXX <i class="label label-info">required</i>|
|`_log.app`         | string |The app you are sending from.<br>Example: `textland` <i class="label label-info">recommended</i>|
|`_log.serverId`         | string |The ID of the server you are sending from.<br>Example: `docker-11445fgh` <i class="label label-info">recommended</i>|
|`_log.gmsId`         | string |The Global Matched Session Id that can be used to match this tranaction with other transactions from other services <i class="label label-info">recommended</i>|





[//]: # (===================================================================)
[//]: # ( Number GET LIST  )
[//]: # (===================================================================)



## Number - Get/List ##

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-get">GET</i>
		<h6>/sms/v1/numbers{?uri-Parameters}</h6>
	</div>
</div>

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-get">GET</i>
		<h6>/sms/v1/numbers/{tn}</h6>
	</div>
</div>


```http
GET /sms/v1/numbers HTTP/1.1
Content-Type: application/json
```

```http
GET /sms/v1/numbers?product=textland&limit=100&offset=500&sortDirection=asc HTTP/1.1
Content-Type: application/json
```

```http
GET /sms/v1/numbers/18135791001 HTTP/1.1
Content-Type: application/json
```

> Example OK Response

```json
{
  "status": 200,
  "_data": [
      {
        "stuff": "here"
      },
      {
        "stuff": "here"
      }
  ]
}
```

> Example Error Response

```json
{
  "status": 404,
  "statusCode": "NotFound",
  "message": "Was not able to find a record for the criteria.",
  "_data" : []
}
```

### URI Parameters ###


| Attribute | Type | Choices | Default | Description |
|-----------|------|---------|---------|-------------|
|`number`         | string | | | The telephone number. |
|`product`         | string | `textland`<br>others| | A valid product code.  |
|`limit`         | int | | 50 | The quantity to return. |
|`offset`         | int | | 0 | The beginning number. |
|`sortDirection`        | string | `asc`<br> `desc` | asc | Sort by ascending or descending order. |


### Response Codes ###
Sending an SMS can create errors.

| Status    | Status Code | Message | Notes |
|-----------|------|-------------|------|
|200         |  | | This is an OK request.  See "_data" for response.|
|400         | CrapForData |You entered data that was not valid.| |
|500         | ServerError | Any server errors. | |




[//]: # (===================================================================)
[//]: # ( Number DELETE  )
[//]: # (===================================================================)



## Number - Delete ##

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-delete">DELETE</i>
		<h6>/sms/v1/numbers{?uri-Parameters}</h6>
	</div>
</div>

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-delete">DELETE</i>
		<h6>/sms/v1/numbers/{tn}</h6>
	</div>
</div>


```http
DELETE /sms/v1/numbers?product=textland HTTP/1.1
Content-Type: application/json
```

```http
DELETE /sms/v1/numbers/18135791001 HTTP/1.1
Content-Type: application/json
```

> Example OK Response

```json
{
  "status": 200,
  "_data": [
      {
        "stuff": "here"
      },
      {
        "stuff": "here"
      }
  ]
}
```

> Example Error Response

```json
{
  "status": 404,
  "statusCode": "NotFound",
  "message": "Was not able to find a record for the criteria.",
  "_data" : []
}
```

### URI Parameters ###


| Attribute | Type | Choices | Default | Description |
|-----------|------|---------|---------|-------------|
|`number`         | string | | | The telephone number. |
|`product`         | string | `textland`<br>others| | A valid product code.  |


### Response Codes ###
Sending an SMS can create errors.

| Status    | Status Code | Message | Notes |
|-----------|------|-------------|------|
|200         |  | | This is an OK request.  See "_data" for response.|
|400         | CrapForData |You entered data that was not valid.| |
|500         | ServerError | Any server errors. | |

















[//]: # (===================================================================)
[//]: # ( Number GET LIST  )
[//]: # (===================================================================)



## Products - Get/List ##

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-get">GET</i>
		<h6>/sms/v1/products</h6>
	</div>
</div>


```http
GET /sms/v1/products HTTP/1.1
Content-Type: application/json
```

> Example OK Response

```json
{
  "status": 200,
  "_data": [
      {
        "stuff": "here"
      },
      {
        "stuff": "here"
      }
  ]
}
```

> Example Error Response

```json
{
  "status": 404,
  "statusCode": "NotFound",
  "message": "Was not able to find a record for the criteria.",
  "_data" : []
}
```

### URI Parameters ###


| Attribute | Type | Choices | Default | Description |
|-----------|------|---------|---------|-------------|
| none        | | | | |


### Response Codes ###
Sending an SMS can create errors.

| Status    | Status Code | Message | Notes |
|-----------|------|-------------|------|
|200         |  | | This is an OK request.  See "_data" for response.|
|400         | CrapForData |You entered data that was not valid.| |
|500         | ServerError | Any server errors. | |


## Received Message (From Layered ) ##

Tell all about it here, in story form or however you want



