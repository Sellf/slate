# <a name="deals"></a>Deals

The Deals API allows you to get, create, update and delete your deals.

### Attributes

Parameter | Type | Permission | Description
--------- | ------- | ------- | -----------
id | integer | read | Unique identifier of the deal
code | string | write | Custom identifier of the deal
**name** | string | write | Brief description of the deal
value | float | write | (Estimated) value of the deal, with decimal part if needed
is_hot | boolean | write | To point if the deal is important or not
win_probability | integer | write | Probability of closing the deal successfully
estimated_close_at | datetime | write | Estimated close date of the deal
started_at | datetime | read | Date in which the deal has been opened
stage_changed_at | datetime | write | Last date in which the deal has been moved into a stage
tags | array | write | An array of tags for a deal
person_id | integer | write | Unique identifier of a primary person
company_id | integer | write | Unique identifier of a primary company
**stage_id** | integer | write | Unique identifier of the deal's current stage in the pipeline
source_id | integer | write | Unique identifier of the deal source
loss_reason_id | integer | write | Unique identifier of the deal loss reason
**user_id** | integer | write | Unique identifier of the user that the person is assigned to
created_at | datetime | read | Date of creation
updated_at | datetime | read | Date of last edit

<aside class="notice">
Custom fields are also attributes that can be attached to create or update actions, as explained in the <a href="#custom_fields">requests</a> section. The can be also used as filters following the rules of the <a href="#query_language">query language</a>.
</aside>

<aside class="warning">
<!-- When you want to update the tags of a deal be aware to include any existing tag, otherwise they will be fully replaced by the tags specified in the update request. This behaviour will be applied to all fields that can accept multiple values, custom fields included. -->
When you want to update the tags of a deal be aware to include any existing tag, otherwise they will be fully replaced by the tags specified in the update request. In fact, the <em>tag</em> attributes acts like the <em>rtags</em> (phantom) attribute, which replace any existing tag associated with the deal.<br>
If you want to explicitly add tags to a deal instead of replacing the existing ones, use the <em>atags</em> (phantom) attribute instead of the <em>tags</em> one.
</aside>




## Get All Deals

```shell
curl https://api.sellf.io/v2/deals -H "Api-Key: {YOUR_API_KEY}"
```

> The above command returns JSON structured like this:

```json
{
  "meta": {
    "has_more": true,
    "object": "list"
  },
  "data": [
    {
      "stage_id": 5,
      "stage_changed_at": "2016-01-05T16:02:41.058040",
      "user_id": 1,
      "name": "Rent in London",
      "tags": [
        "duplex",
        "luxury"
      ],
      "created_at": "2015-11-27T14:57:55.461828",
      "updated_at": "2016-07-05T12:21:24",
      "value": 5000,
      "company_id": 4,
      "person_id": 9,
      "win_probability": 100,
      "estimated_close_at": "2015-11-30T11:59:59",
      "source_id": null,
      "loss_reason_id": null,
      "is_hot": true,
      "started_at": "2015-11-27T14:57:55",
      "id": 2,
      "code": null
    },
    {
      "stage_id": 10,
      "stage_changed_at": "2015-11-28T07:34:13",
      "user_id": 1,
      "name": "Venice villa",
      "tags": [],
      "created_at": "2015-11-28T07:34:13.330420",
      "updated_at": "2016-07-05T12:21:24",
      "value": 370000,
      "company_id": 7,
      "person_id": null,
      "win_probability": 100,
      "estimated_close_at": null,
      "source_id": null,
      "loss_reason_id": null,
      "is_hot": false,
      "started_at": "2016-03-30T13:08:49",
      "id": 3,
      "code": null
    }
  ]
}
```

This endpoint retrieves all deals.

### HTTP Request

`GET /deals`

### Query Parameters

Parameter| Description
--------- | -----------
sort_by | Column to sort by <br> (i.e. `id`, `name`, `value`, `estimated_close_at`, `stage_changed_at`, `created_at`, `updated_at`)
user_id | Unique identifier of the user the deal is owned by
stage_id | Unique identifier of the stage in which the deal is placed
person_id | Unique identifier of the main deal with whom the deal is associated
company_id | Unique identifier of the main company with whom the deal is associated
source_id | Unique identifier of the deal source
loss_reason_id | Unique identifier of the deal loss reason
name | A string matching the description of the deal
code | A string matching the custom code of the deal
created_at | A date to be compared with the creation of the deal
updated_at | A date to be compared with the last edit of the deal
tags | One or more tags associated to the deal




## Create a Deal

```shell
# Create a new deal
curl https://api.sellf.io/v2/deals \
  -H "Api-Key: {YOUR_API_KEY}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -X POST -d "{"name": "Apartment in Berlin",
               "value": 265789,
               "is_hot": true,
               "estimated_close_at": "2016-12-05T12:00:23",
               "tags": ["Germany"],
               "stage_id": 10,
               "user_id": 1}"
```

> The above command returns JSON structured like this:

```json
{
  "stage_id": 10,
  "stage_changed_at": "2016-09-08T18:14:06",
  "user_id": 1,
  "name": "Apartment in Berlin",
  "tags": [
    "Germany"
  ],
  "created_at": "2016-09-08T18:14:06",
  "updated_at": "2016-09-08T18:14:06",
  "value": 265789,
  "company_id": null,
  "person_id": null,
  "win_probability": 100,
  "estimated_close_at": "2016-12-05T12:00:23",
  "source_id": null,
  "loss_reason_id": null,
  "is_hot": true,
  "started_at": "2016-09-08T18:14:06",
  "id": 12,
  "code": null
}
```

This endpoint allows to create a deal.

### HTTP Request

`POST /deals`




## Get a Specific Deal

```shell
# Retrieve a deal with ID 12
curl https://api.sellf.io/v2/deals/12 -H "Api-Key: {YOUR_API_KEY}"
```

> The above command returns JSON structured like this:

```json
{
  "stage_id": 10,
  "stage_changed_at": "2016-09-08T18:14:06",
  "user_id": 1,
  "name": "Apartment in Berlin",
  "tags": [
    "Germany"
  ],
  "created_at": "2016-09-08T18:14:06",
  "updated_at": "2016-09-08T18:14:06",
  "value": 265789,
  "company_id": null,
  "person_id": null,
  "win_probability": 100,
  "estimated_close_at": "2016-12-05T12:00:23",
  "source_id": null,
  "loss_reason_id": null,
  "is_hot": true,
  "started_at": "2016-09-08T18:14:06",
  "id": 12,
  "code": null
}
```

This endpoint retrieves a specific deal.

### HTTP Request

`GET /deals/:id`

### URL Parameters

Parameter | Description
--------- | -----------
id | The unique identifier of the deal to retrieve




## Update a Specific Deal

```shell
# Update the deal with ID 12
curl https://api.sellf.io/v2/deals/12 \
  -H "Api-Key: {YOUR_API_KEY}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -X PUT -d "{"value": 470000,
              "win_probability": 95,
              "estimated_close_at": "2016-12-23T01:45:00"}"
```

> The above command returns JSON structured like this:

```json
{
  "stage_id": 10,
  "stage_changed_at": "2016-09-08T18:14:06",
  "user_id": 1,
  "name": "Apartment in Berlin",
  "tags": [
    "Germany"
  ],
  "created_at": "2016-09-08T18:14:06",
  "updated_at": "2016-09-08T18:14:06",
  "value": 470000,
  "company_id": null,
  "person_id": null,
  "win_probability": 95,
  "estimated_close_at": "2016-12-23T01:45:00",
  "source_id": null,
  "loss_reason_id": null,
  "is_hot": true,
  "started_at": "2016-09-08T18:14:06",
  "id": 12,
  "code": null
}
```

This endpoint allows to update a specific deal.

### HTTP Request

`PUT /deals/:id`

### URL Parameters

Parameter | Description
--------- | -----------
id | The unique identifier of the deal to retrieve

<aside class="warning">
When you want to update the tags of a deal be aware to include any existing tag, otherwise they will be fully replaced by the tags specified in the update request. In fact, the <em>tag</em> attributes acts like the <em>rtags</em> (phantom) attribute, which replace any existing tag associated with the deal.<br>
If you want to explicitly add tags to a deal instead of replacing the existing ones, use the <em>atags</em> (phantom) attribute instead of the <em>tags</em> one.
</aside>




## Delete a Specific Deal

```shell
# Delete the deal with ID 3
curl https://api.sellf.io/v2/deals/3 \
  -H "Api-Key: {YOUR_API_KEY}" \
  -X DELETE
```

> The above command returns 200 with no content.

This endpoint deletes a specific deal. Deleting a deal implies that even all the associated entities are deleted, except for people and companies.


### HTTP Request

`DELETE /deals/:id`

### URL Parameters

Parameter | Description
--------- | -----------
id | The unique identifier of the deal to be deleted