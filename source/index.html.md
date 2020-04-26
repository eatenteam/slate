---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  # - ruby
  # - python
  # - javascript

# toc_footers:
#   - <a href='#'>Sign Up for a Developer Key</a>
#   - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors
# search: true
---

# Introduction

Welcome to the EATEN API! You can use our API to access EATEN API endpoints, which can get information on various orders in our database.

We have language bindings in Shell. You can view code examples in the dark area to the right.

# Authentication

> To get JWT token, use this code:

<!--
```ruby
require 'EATEN'

api = EATEN::APIClient.authorize!('meowmeowmeow')
```

```python
import EATEN

api = EATEN.authorize('meowmeowmeow')
``` -->

```shell
# With shell, you can just pass the correct header with each request
curl --location --request POST '<url>/api/v1/login' \
--header 'Content-Type: application/json' \
--data '{
    "username": "test",
    "password": "test"
}'
```

<!-- ```javascript
const EATEN = require("EATEN");

let api = EATEN.authorize("meowmeowmeow");
``` -->

> Make sure to replace `username,password` with yours.

EATEN uses JWT token to allow access to the API. You can register a new JWT token by using a register endpoint below.

EATEN expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: <Token>`

<aside class="notice">
You must replace <code>Token</code> with your personal JWT token.
</aside>

# Endpoints

## Get All Orders

```shell
curl --location --request GET '<url>/api/v1/orders/' \
--header 'Authorization: Bearer <Token>'
```

> The above command returns array structured like this:

```json
[
  {
    "products": [
      {
        "name": "Croissant",
        "productID": "12345"
      }
    ],
    "_id": "abcde1",
    "customerName": "Chris Foo",
    "address": "12345",
    "time": "2020-04-25T08:00:00.000Z",
    "area": "Pathumwan",
    "price": "123"
  },
  {
    "products": [
      {
        "name": "Croissant",
        "productID": "12346"
      }
    ],
    "_id": "abcde2",
    "customerName": "John Doe",
    "address": "11000 St",
    "time": "2020-04-25T09:00:00.000Z",
    "area": "Sukhumvit",
    "price": "456"
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET /api/v1/orders`

### Headers

**Authorization**&nbsp;&nbsp;&nbsp;&nbsp; Bearer \<Token>

<!-- ### Query Parameters

| Parameter    | Default | Description                                                                      |
| ------------ | ------- | -------------------------------------------------------------------------------- |
| include_cats | false   | If set to true, the result will also include cats.                               |
| available    | true    | If set to false, the result will include kittens that have already been adopted. | -->

<!-- <aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside> -->

## Get Today Order

```shell
curl --location --request GET '<url>/api/v1/orders/today' \
--header 'Authorization: Bearer <Token>'
```

> The above command returns array structured like this:

```json
[
  {
    "products": [
      {
        "name": "Croissant",
        "productID": "12345"
      }
    ],
    "_id": "abcde1",
    "customerName": "Chris Foo",
    "address": "12345",
    "time": "2020-04-25T08:00:00.000Z",
    "area": "Pathumwan",
    "price": "123"
  }
]
```

This endpoint retrieves all orders for today.

<aside class="warning">This endpoint will return an array of objects</aside>

### HTTP Request

`GET /api/v1/orders/today`

### Headers

**Authorization**&nbsp;&nbsp;&nbsp;&nbsp; Bearer \<Token>

## Get Order By ID

```shell
curl --location --request GET '<url>/api/v1/orders/<id>' \
--header 'Authorization: Bearer <Token>'
```

> The above command returns JSON structured like this:

```json
{
  "products": [
    {
      "name": "Croissant",
      "productID": "12345"
    }
  ],
  "_id": "abcde1",
  "customerName": "Chris Foo",
  "address": "12345",
  "time": "2020-04-25T08:00:00.000Z",
  "area": "Pathumwan",
  "price": "123"
}
```

This endpoint retrieves all orders for today.

<aside class="warning">This endpoint will return an object</aside>

### HTTP Request

`GET /api/v1/orders/<id>`

### Headers

**Authorization**&nbsp;&nbsp;&nbsp;&nbsp; Bearer \<Token>

### URL Parameters

| Parameter | Description                     |
| --------- | ------------------------------- |
| id        | The ID of the order to retrieve |

## Add Order

```shell
curl --location --request POST 'https://dev.sprawl.team/api/v1/orders' \
--header 'Authorization: Bearer <Token'
--header 'Content-Type: application/json' \
--data '{
    "customerName": "John Foo",
    "address": "Earth",
    "round": 1,
    "area": "Mars",
    "restaurant": "test",
    "products": [
        {
            "name": "Croissant",
            "productID": "1234"
        }
    ],
    "price": "234"
}'
```

> The above command returns a status like this:

```
OK
```

This endpoint is use to add new order.

### HTTP Request

`POST /api/v1/orders`

### Headers

**Authorization**&nbsp;&nbsp;&nbsp;&nbsp; Bearer \<Token>

### Body

`{ "customerName": "John Foo", "address": "Earth", "round": 1, "area": "Mars", "restaurant": "test", "products": [ { "name": "Croissant", "productID": "1234" } ], "price": "234" }`

## Update Order

```shell
curl --location --request PUT '<url>/api/v1/orders' \
--header 'Authorization: Bearer <Token>' \
--header 'Content-Type: application/json' \
--data ' {
        "products": [
        {
            "name": "Croissant",
            "productID": "1234"
        }
        ],
        "_id": "abcde",
        "customerName": "John Foo",
        "address": "North Pole",
        "time": "2020-04-25T08:00:00.000Z",
        "area": "51",
        "price": "1234"
    }'
```

> The above command returns a status like this:

```
OK
```

This endpoint is use to add new order.

### HTTP Request

`PUT /api/v1/orders`

### Headers

**Authorization**&nbsp;&nbsp;&nbsp;&nbsp; Bearer \<Token>

### Body

`{ "products": [ { "name": "Croissant", "productID": "1234" } ], "_id": "abcde", "customerName": "John Foo", "address": "North Pole", "time": "2020-04-25T08:00:00.000Z", "area": "51", "price": "1234" }`

## Delete a Specific Order

```shell
curl --location --request DELETE '<url>/api/v1/orders/<ID>' \
--header 'Authorization: Bearer <Token>'
```

> The above command returns a status like this:

```
OK
```

This endpoint deletes a specific order.

### HTTP Request

`DELETE <url>/api/v1/orders/<ID>`

### URL Parameters

| Parameter | Description                   |
| --------- | ----------------------------- |
| ID        | The ID of the order to delete |
