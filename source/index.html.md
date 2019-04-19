---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Actum's API allows developers to manage a variety of powerful tasks, such as creating and updating transacions, managing customer and payment data, and query settlement information. It was initially built for merchants requiring a high level of customization. Its same, customizable architecture now allows simple integration with software partners, as well. Actum uses HTTPS for all transactions to ensure the safety of consumer information.

This guide provides an overview for our merchants and partners of how to start using Actum. If you have any questions throughout the process, please don't hesitate to contact us at [support@actumprocessing.com](support@actumprocessing.com).

# Getting Started

# Getting Started

To get started using Actum's API, you'll want to follow these steps:

## Register for a Test Account

First, you will want to navigate to Actum's [Register for a Test Account](https://www.actumprocessing.com/register-test-account/) page. You will need to enter your First Name, Last Name, Email, Company Name, and Phone Number to sign up. Actum's support team will use this information for verification purposes in order to create your account.

Once your account is created (typically within less than 24 hours on business days), you will receive a welcome email with your new test account credentials.

## Log into your Test Account

To begin testing, you will be able to log into a test portal using the username and password provided by Actum's support team. Actum's portal is available at the following link: [https://join.actumprocessing.com](https://join.actumprocessing.com)

It is recommended that you change your password immediately upon login. There is no need to create a separate API key to complete setup, as your username and password will allow you to authenticate to Actum's test enviroment, securely.

##Create a Call

To create a new API call, you'll first want to join the server at [https://join.actumprocessing.com/cgi-bin/dbs/man_trans.cg](https://join.actumprocessing.com/cgi-bin/dbs/man_trans.cgi). The following parameters are required:

* `username` (your assigned username)
* `password`(the password associated with your username, that can be changed)

(unsure of the following):
* `syspass` (a system password assigned your account, that cannot be changed)
* `action_code` (this uses `D`)
* `order id` (order number of a test transaction

**Note:** All API request methods are `POST` only. In this case, `POST` requests act similarly to `GET` requests, in that the requests function primarily to return information pertaining to a specific resource.

> To join the server, use this code in shell:
```shell
curl "HTTPS://join.actumprocessing.com/cgi-bin/dbs/man_trans.cgi"
  -H "Authorization: meowmeowmeow"
```
> The content type you'll need to use is `application/x---www---form---urlencoded **or** multipart/form--data`.

#### Understanding Responses

Text to explain returns from different objects.

#### Status Codes

Explanation and table of status codes.

#### Understanding Webhooks

Explanation and examples

### Step 4: Test your Calls

Description

In-app consequences of a return
Payment retries and refunds


> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

## Merchants

The `merchant` object represents account information pertaining to the merchant that submits a debit or credit transaction.

Parameter | Description | Type        | Req |
--------- | ----------- | ----------- | --- |
| `parent_id` | Parent ID of merchant. [max Length = 8] | ALPHANUMERIC | Y |
| `sub_id` | Sub ID of merchant. [max Length = 8] | ALPHANUMERIC | Y |
| `pmt_type` | Type of payment being submitted (check, or `chk`, is the default value). | -- | N |
| `response_location` | The `man_trans.cgi` script will respond to this URL with response variables if passed in. | Full path URL | N |


<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Customers and Accounts

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Description | Type        | Req |
--------- | ----------- | ----------- | --- |
| `parent_id` | Parent ID of merchant. [max Length = 8] | ALPHANUMERIC | Y |
| `sub_id` | Sub ID of merchant. [max Length = 8] | ALPHANUMERIC | Y |
| `pmt_type` | Type of payment being submitted (check, or `chk`, is the default value). | -- | N |
| `response_location` | The `man_trans.cgi` script will respond to this URL with response variables if passed in. | Full path URL | N |

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete
