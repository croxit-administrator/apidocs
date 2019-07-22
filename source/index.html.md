---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the `croxit.io` API! You can use our API to access croxit API endpoints, which can get payment / invoice on your business or product.

We have language bindings in Shell, Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

Just enjoy to explore more on this croxit API!

## Learn more about API
If you are not master at APIs, feel free to ask us about our API or you can explore more about API in <a href='https://www.restapitutorial.com/'>here</a>

# Authentication

> `Croxit` use secrete key every you hit our APIs, for example your API key is

```shell
  crx_development_P4qDfOss0OCpl8RtKrROHjaQYNCk9dN5lSfk+R1l9Wbe+rSiCwZ3jw==
```

> First add a colon at the end

```shell
  crx_development_P4qDfOss0OCpl8RtKrROHjaQYNCk9dN5lSfk+R1l9Wbe+rSiCwZ3jw==
```

> Finally, just encode your api key to get this

```shell
  Y3J4X2RldmVsb3BtZW50X1A0cURmT3NzME9DcGw4UnRLclJPSGphUVlOQ2s5ZE41bFNmaytSMWw5V2JlK3JTaUN3WjNqdz09
```

Croxit uses API keys to allow access to the API. You can register a new croxit API key at our [developer portal](http://croxit.io/developers).

Croxit expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: your base64 secrete key`

<aside class="notice">
You have to register first at <code>croxit.io</code> to get your API secrete key.
</aside>

# Virtual Accounts

## Create Fixed Virtual Account


One of the payment method offered by `Croxit` is Virtual Account. By using this payment method, customers will be avaiable to pay everytime with any amount needed.
This Fixed virtual account is open (can be pay every time) and you can set the expired date of your virtual account's customers. And you can set the amount to free or determined.

Croxit will send real time notification to your callback system when the customer complete the payment. You have to register at <code>croxit.io</code> to set your Callback url.

This endpoint is use to create virtual account.

### HTTP Request

`POST https://croxit.io/virtual_accounts/create`

### Request Parameters

> Example create fixed Virtual Account

```shell
curl "https://croxit.io/virtual_accounts/create" -X POST \
  -H "Authorization: Y3J4X2RldmVsb3BtZW50X1A0cURmT3NzME9DcGw4UnRLclJPSGphUVlOQ2s5ZE41bFNmaytSMWw5V2JlK3JTaUN3WjNqdz09" \
  -d customer_id=virtual_account_123456789 \
  -d bank_id=BNI \
  -d name='Brama Diwangkara'
```

Parameter | Mandatory | Description
--------- | ------- | -----------
customer_id | yes | `string` 
bank_id | yes | `string`
customer_name | yes | `string`
virtual_account | no | `string`
is_closed | no | `boolean`
is_single_use | no | `boolean`
trx_amount | optional | `number` if virtual_account set to closed, you have to determine the trx_amount
datetime_expired | no | `ISO_DATE` 

### Response Parameters


> The above command returns response JSON structured like this:


```json
{
  "company_id":"128971hjkiie",
  "customer_id":"virtual_account_123456789",
  "bank_id":"BNI",
  "customer_name":"Brama Diwangkara",
  "virtual_account":"80008087798381082",
  "is_closed":false,
  "is_single_use":false,
  "id":"523frfhhto098",
  "status":"active",
}
```

Parameter |  Description
--------- |  -----------
company_id | Your user ID
customer_id | Your customer ID based on your request 
bank_id | Bank id for the created virtual account
customer_name | Name of your virtual account 
virtual_account | Generated Virtual Account number and virtual account bank
is_closed | The transaction amount determined if has true value
is_single_use | The virtual account can be use only once if has true value 
trx_amount | Amount of transaction if you set `is_closed` equals true
datetime_expired | The time when the virtual account will be expired 



<aside class="notice">
Possible error codes: <code>401</code>, <code>402</code>, <code>406</code> and <code>410</code>. See error tab for detail <code>error</code>.
</aside>

## Update Fixed Virtual Account

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

