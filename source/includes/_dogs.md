# Dogs

Hello World

## Create a product attribute ##

This API helps you to manage `dogs` resources.

## Dogs Overview ##

| Resource | <b>POST</b><br><i>create</i> | <b>GET</b><br><i>read</i> | <b>PUT</b><br><i>update</i> | <b>DELETE</b><br><i>delete</i> |
|----------|--------|------|--------|--------|
| /dogs    | Create a new dog | List all dogs | Bulk update all dogs | Delete all dogs |
| /dogs/1234 | Error | Show "Bo" | - If exists, Update "Bo" <BR> - If not, Error | Delete "Bo" |

 Link to [Delete all dogs](#delete-all-dogs)
 Link to [List all dogs](#list-dogs)
 Link to [Dogs - Error Codes](#dogs-error-codes)

 <br>Link to [James](#james)


### Attributes ###

| Attribute | Type | Description |
|-----------|------|-------------|
|id         | integer |Unique Id |
|foo         | string |something here |
|bar        | string |MORE here |
|name        | string |Name stuff |



### Dogs - Error Codes ###

| Status Code | Error Code | Message | Notes |
|-----------|------|-------------|------|
|200         | OK |Everything was OK | |
|400         | InvalidRequest |Invalid request. Check the request body format and verify the right Content-Type header value is being sent.	 | |
|400         | FolderIdNotProvided |Folder Id was not provided.	 | Either the folders to be moved or the target folder was not provided.|
|400	         | FolderNotFound |Folder not found. | Target folder was not found.|




## Dogs attribute properties ##

|   Attribute    |   Type  |                           Description                                       |
|----------------|---------|-----------------------------------------------------------------------------|
| `id`           | integer | Unique identifier for the resource. <i class="label label-info">read-only</i>                             |
| `name`         | string  | Attribute name. <i class="label label-info">required</i>                                                  |
| `slug`         | string  | An alphanumeric identifier for the resource unique to its type.                                           |
| `type`         | string  | Type of attribute. Default is `select`. Options: `select` and `text` (some plugins can include new types) |
| `order_by`     | string  | Default sort order. Default is `menu_order`. Options: `menu_order`, `name`, `name_num` and `id`.          |
| `has_archives` | boolean | Enable/Disable attribute archives. Default is `false`.                                                    |

## List Dogs ##

This is some more stuff

Hi there 

### List all dogs ###

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-post">POST</i>
		<h6>/wp-json/wc/v1/products/attributes</h6>
	</div>
</div>

```http
GET /repos/rails/rails/branches HTTP/1.1
User-Agent: MyClient/1.0.0
Accept: application/vnd.travis-ci.2+json
Host: api.travis-ci.org
HTTP/1.1 200 OK
Content-Type: application/json

{
  "branches": [
    {
      "id": 22554234,
      "repository_id": 891,
      "commit_id": 6534402,
      "number": "15184",
      "config": {},
      "state": "created",
      "started_at": "2014-04-08T00:17:34Z",
      "finished_at": "2014-04-08T00:48:59Z",
      "duration": 30546,
      "job_ids": [],
      "pull_request": false
    }
  ]
}

```

```http
POST /repos/rails/rails/branches HTTP/1.1
User-Agent: MyClient/1.0.0
Accept: application/vnd.travis-ci.2+json
Host: api.travis-ci.org
HTTP/1.1 200 OK
Content-Type: application/json
```

```http
PUT /repos/rails/rails/branches HTTP/1.1
User-Agent: MyClient/1.0.0
Accept: application/vnd.travis-ci.2+json
Host: api.travis-ci.org
HTTP/1.1 200 OK
Content-Type: application/json
```

```http
DELETE /repos/rails/rails/branches HTTP/1.1
User-Agent: MyClient/1.0.0
Accept: application/vnd.travis-ci.2+json
Host: api.travis-ci.org
HTTP/1.1 200 OK
Content-Type: application/json
```

```shell
curl -X POST https://example.com/wp-json/wc/v1/products/attributes \
    -u consumer_key:consumer_secret \
    -H "Content-Type: application/json" \
    -d '{
  "name": "Color",
  "slug": "pa_color",
  "type": "select",
  "order_by": "menu_order",
  "has_archives": true
}'
```

### List one dog ###

<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-post">POST</i>
		<h6>/wp-json/wc/v1/products/attributes</h6>
	</div>
</div>

```shell
curl -X POST https://example.com/wp-json/wc/v1/products/attributes \
    -u consumer_key:consumer_secret \
    -H "Content-Type: application/json" \
    -d '{
  "name": "Color",
  "slug": "pa_color",
  "type": "select",
  "order_by": "menu_order",
  "has_archives": true
}'
```

> JSON response example:

This is more text here

```json
{
  "id": 1,
  "name": "Color",
  "slug": "pa_color",
  "type": "select",
  "order_by": "menu_order",
  "has_archives": true,
  "_links": {
    "self": [
      {
        "href": "https://example.com/wp-json/wc/v1/products/attributes/6"
      }
    ],
    "collection": [
      {
        "href": "https://example.com/wp-json/wc/v1/products/attributes"
      }
    ]
  }
}
```

## List Dogs Get ##


<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-get">GET</i>
		<h6>/wp-json/wc/v1/products/attributes</h6>
	</div>
</div>

This is some more stuff








## Update Dogs ##


<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-put">PUT</i>
		<h6>/wp-json/wc/v1/products/attributes</h6>
	</div>
</div>

This is the details to update Dogs




## Delete All Dogs ##


<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-delete">DELETE</i>
		<h6>/wp-json/wc/v1/products/attributes</h6>
	</div>
</div>

This is how you delete all Dogs

## Delete a specific dog ##


<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-delete">DELETE</i>
		<h6>/wp-json/wc/v1/products/attributes</h6>
	</div>
</div>

This is how you delete on dog





## James ##

This is the James Section


## James ##

This is the James Section


## <a name="james-33"></a>James ##

This is the James Section




## Paging ##

This is a paging area



## Update Dogs ##


<div class="api-endpoint">
	<div class="endpoint-data">
		<i class="label label-put">PUT</i>
		<h6>/wp-json/wc/v1/products/attributes</h6>
	</div>
</div>

This is the details to update Dogs


