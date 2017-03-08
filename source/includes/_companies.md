# <a name="companies"></a>Companies

The Companies API allows you to get, create, update and delete your companies. Each company can be associated to a [Company](#companies) and one or more [Deals](#deals).

### Attributes

Parameter | Type | Permission | Required | Description
--------- | ------- | ------- | ------- | -----------
id | integer | read | | Unique identifier of the company
name | string | write | yes | Name of the company
industry | string | write | |  Industry sector of the company
website | string | write | |  writeebsite
email | string | write | | Primary email
email_secondary | string | write | | Secondary email
phone | string | write | | Office or home number
fax | string | write | | Fax number
address | string | write | | Office or home address of the company
latitude | float | write | | Geographic coordinate of the company
longitude | float | write | | Geographic coordinate of the company
description | string | write | | A description of the company
tags | array | write | | An array of tags for a company
user_id | integer | write | yes | Unique identifier of the user that the company is assigned to
created_at | datetime | read | | Date of creation
updated_at | datetime | read | | Date of last edit


## Get All Companies

```shell
curl https://api.sellf.io/v1/companies?sort_by=-name -H "Api-Key: {YOUR_API_KEY}"
```

> The above command returns JSON structured like this:

```json
{
  "meta": {
    "has_more": false,
    "object": "list"
  },
  "data": [
    {
      "website": "http://www.sellfapp.com",
      "fax": null,
      "user_id": 2869,
      "description": null,
      "tags": [],
      "industry": "Mobile CRM",
      "created_at": "2015-11-26T15:25:30.940731",
      "updated_at": "2016-07-05T12:17:47",
      "longitude": 12.4274592,
      "id": 20991,
      "phone": "+39 0422 789611",
      "address": "Via Sile, 41, 31056 Roncade TV, Italia",
      "latitude": 45.5648361,
      "email_secondary": null,
      "email": "hello@sellfapp.com",
      "name": "Sellf s.r.l."
    }
  ]
}
```

This endpoint retrieves all companies.

### HTTP Request

`GET /companies`

### Query Parameters

Parameter | Description
--------- | -----------
sort_by | Column to sort by <br> (i.e. `id`, `name`, `created_at`, `updated_at`)
user_id | Unique identifier of the user the company is owned by
name | A string containing or matching the name of the company




## Create a Company

```shell
# Create a new company
curl https://api.sellf.io/v1/companies \
  -H "Api-Key: {YOUR_API_KEY}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -X POST -d "{"name": "Acme Inc.",
               "industry": "Semiconductor",
               "email": "hey@acme.com",
               "address": "Via Thomas Alva Edison, Padova, PD",
               "user_id": 4}"
```

> The above command returns JSON structured like this:

```json
{
  "website": null,
  "fax": null,
  "user_id": 4,
  "description": null,
  "tags": [],
  "industry": "Semiconductor",
  "created_at": "2016-09-08T16:54:37",
  "updated_at": "2016-09-08T16:54:37",
  "longitude": null,
  "id": 3,
  "phone": null,
  "address": "Via Thomas Alva Edison, Padova, PD",
  "latitude": null,
  "email_secondary": null,
  "email": "hey@acme.com",
  "name": "Acme Inc."
}
```

This endpoint allows to create a company.

### HTTP Request

`POST /companies`




## Get a Specific Company

```shell
# Retrieve a company with ID 3
curl https://api.sellf.io/v1/companies/3 -H "Api-Key: {YOUR_API_KEY}"
```

> The above command returns JSON structured like this:

```json
{
  "website": null,
  "fax": null,
  "user_id": 4,
  "description": null,
  "tags": [],
  "industry": "Semiconductor",
  "created_at": "2016-09-08T16:54:37",
  "updated_at": "2016-09-08T16:54:37",
  "longitude": null,
  "id": 3,
  "phone": null,
  "address": "Via Thomas Alva Edison, Padova, PD",
  "latitude": null,
  "email_secondary": null,
  "email": "hey@acme.com",
  "name": "Acme Inc."
}
```

This endpoint retrieves a specific company.

### HTTP Request

`GET /companies/:id`

### URL Parameters

Parameter | Description
--------- | -----------
id | The unique identifier of the company to retrieve




## Update a Specific Company

```shell
# Update the company with ID 3
curl https://api.sellf.io/v1/companies/3 \
  -H "Api-Key: {YOUR_API_KEY}" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -X PUT -d "{"name": "Acme Holding",
              "industry": "Semiconductor & Devices",
              "email": "sales@acme.com"}"
```

> The above command returns JSON structured like this:

```json
{
  "website": null,
  "fax": null,
  "user_id": 4,
  "description": null,
  "tags": [],
  "industry": "Semiconductor & Devices",
  "created_at": "2016-09-08T16:54:37",
  "updated_at": "2016-09-08T17:02:18",
  "longitude": null,
  "id": 3,
  "phone": null,
  "address": "Via Thomas Alva Edison, Padova, PD",
  "latitude": null,
  "email_secondary": null,
  "email": "sales@acme.com",
  "name": "Acme Holding"
}
```

This endpoint allows to update a specific company.

### HTTP Request

`PUT /companies/:id`

### URL Parameters

Parameter | Description
--------- | -----------
id | The unique identifier of the company to retrieve




## Delete a Specific Company

```shell
# Delete the company with ID 3
curl https://api.sellf.io/v1/companies/3 \
  -H "Api-Key: {YOUR_API_KEY}" \
  -X DELETE
```

> The above command returns 200 with no content.

This endpoint deletes a specific company. Deleting a company implies that even all the associated entities are deleted, except for the associated company.


### HTTP Request

`DELETE /companies/:id`

### URL Parameters

Parameter | Description
--------- | -----------
id | The unique identifier of the company to be deleted