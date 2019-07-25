---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - Json

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the `croxit.io` API! You can use our API to access croxit API endpoints, which can get payment / invoice on your business or product.

We have language bindings in Json, Ruby, Python, and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

Just enjoy to explore more on this croxit API!

## Learn more about API
If you are not master at APIs, feel free to ask us about our API or you can explore more about API in <a href='https://www.restapitutorial.com/'>here</a>

# Authentication

> `Croxit` use secrete key every you hit our APIs, for example your API key is

```Json
  crx_development_P4qDfOss0OCpl8RtKrROHjaQYNCk9dN5lSfk+R1l9Wbe+rSiCwZ3jw==
```

> First add a colon at the end

```Json
  crx_development_P4qDfOss0OCpl8RtKrROHjaQYNCk9dN5lSfk+R1l9Wbe+rSiCwZ3jw==
```

> Finally, just encode your api key to get this

```Json
  Y3J4X2RldmVsb3BtZW50X1A0cURmT3NzME9DcGw4UnRLclJPSGphUVlOQ2s5ZE41bFNmaytSMWw5V2JlK3JTaUN3WjNqdz09
```

Croxit uses API keys to allow access to the API. You can register a new croxit API key at our [developer portal](http://croxit.io/developers).

Croxit expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: your base64 secrete key`

All the following request must inlcude header json type, so just place this on your header:

`Content-Type: application/json`

<aside class="notice">
You have to register first at <code>croxit.io</code> to get your API secrete key.
</aside>

# Virtual Accounts

<!-- CREATE FIXED VIRTUAL ACCOUNT -->

## Create Fixed Virtual Account


One of the payment method offered by `Croxit` is Virtual Account. By using this payment method, customers will be avaiable to pay everytime with any amount needed.
This Fixed virtual account is open (can be pay every time) and you can set the expired date of your virtual account's customers. And you can set the amount to free or determined.

Croxit will send real time notification to your callback system when the customer complete the payment. You have to register at <code>croxit.io</code> to set your Callback url.

This endpoint is use to create virtual account.

### HTTP Request

`POST https://croxit.io/virtual_accounts/create`

### Request Parameters

> Example create fixed Virtual Account

```json
  {
    "customer_id":"virtual_account_123456789",
    "bank_id":"BNI",
    "name":"Brama Diwangkara"
  }
```

Parameter | Mandatory | Description
--------- | ------- | -----------
customer_id | yes | `string` 
bank_id | yes | `string`
customer_name | yes | `string`
virtual_account_number | no | `string`
is_closed | no | `boolean`
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
  "virtual_account_number":"80008087798381082",
  "virtual_account_id":"5tty4212233uiu",
  "is_closed":false,
  "datetime_expired":"2020-01-01 13:00:00",
  "status":"active",
}
```

Parameter |  Description
--------- |  -----------
company_id | Your user ID
customer_id | Your customer ID based on your request 
bank_id | Bank id for the created virtual account
customer_name | Name of your virtual account 
virtual_account_number | Generated Virtual Account number and virtual account bank, we place <code>random number</code> if this value is not defined
virtual_account_id | Generate id for Virtual Account from <code>croxit.io</code>
is_closed | The transaction amount determined if has true <code>value</code>, default value is <code>false</code>
trx_amount | Amount of transaction if you set `is_closed` equals true
datetime_expired | The time when the virtual account will be expired, default for this value is 1 year from virtual account created
status | status that defines virtual account ACTIVE or INACTIVE



<aside class="notice">
Possible error codes: <code>401</code>, <code>402</code>, <code>406</code> and <code>410</code>. See error tab for detail <code>error</code>.
</aside>


<!-- UPDATE FIXED VIRTUAL ACCOUNT -->

## Update Fixed Virtual Account

### HTTP Request

`PUT https://croxit.io/virtual_accounts/update/{virtual_account_id}`

### Request Parameters

> Example update fixed Virtual Account

```json
  {
    "trx_amount":2000000,
    "datetime_expired":"2020-01-01 13:00:00"
  }
```

Parameter | Description
--------- | ------- | -----------
customer_name | `string`
trx_amount | `number` changeable if your virtual account is set to <code>is_closed</code>
datetime_expired | `ISO_DATE` 

### Response Parameters


> The above command returns response JSON structured like this:


```json
{
  "company_id":"128971hjkiie",
  "customer_id":"virtual_account_123456789",
  "bank_id":"BNI",
  "customer_name":"Brama Diwangkara",
  "virtual_account_number":"80008087798381082",
  "virtual_account_id":"5tty4212233uiu",
  "is_closed":true,
  "trx_amount":2000000,
  "datetime_expired":"2020-01-01 13:00:00",
  "status":"active",
}
```

Parameter |  Description
--------- |  -----------
company_id | Your user ID
customer_id | Your customer ID based on your request 
bank_id | Bank id for the created virtual account
customer_name | Name of your virtual account 
virtual_account_number | Generated Virtual Account number and virtual account bank, we place <code>random number</code> if this value is not defined
virtual_account_id | Generate id for Virtual Account from <code>croxit.io</code>
is_closed | The transaction amount determined if has <code>true</code> value, default value is <code>false</code>
trx_amount | Amount of transaction if you set `is_closed` equals true
datetime_expired | The time when the virtual account will be expired 
status | status that defines virtual account ACTIVE or INACTIVE



<aside class="notice">
Possible error codes: <code>401</code>, <code>402</code>, <code>406</code> and <code>410</code>. See error tab for detail <code>error</code>.
</aside>


<!-- GET DETAIL FIXED VIRTUAL ACCOUNT -->

## Get Detail Fixed Virtual Account

### HTTP Request

`GET https://croxit.io/virtual_accounts/get/{virtual_account_id}`

### Request Parameters

Parameter | Description
--------- | ------- | -----------
virtual_account_id | Generate id for Virtual Account from <code>croxit.io</code>

### Response Parameters

> The above command returns response JSON structured like this:


```json
{
  "company_id":"128971hjkiie",
  "customer_id":"virtual_account_123456789",
  "bank_id":"BNI",
  "customer_name":"Brama Diwangkara",
  "virtual_account_number":"80008087798381082",
  "virtual_account_id":"5tty4212233uiu",
  "is_closed":true,
  "trx_amount":2000000,
  "datetime_expired":"2020-01-01 13:00:00",
  "status":"active",
}
```

Parameter |  Description
--------- |  -----------
company_id | Your user ID
customer_id | Your customer ID based on your request 
bank_id | Bank id for the created virtual account
customer_name | Name of your virtual account 
virtual_account_number | Generated Virtual Account number and virtual account bank, we place <code>random number</code> if this value is not defined
virtual_account_id | Generate id for Virtual Account from <code>croxit.io</code>
is_closed | The transaction amount determined if has <code>true</code> value, default value is <code>false</code>
trx_amount | Amount of transaction if you set `is_closed` equals true
datetime_expired | The time when the virtual account will be expired 
status | status that defines virtual account ACTIVE or INACTIVE



<aside class="notice">
Possible error codes: <code>401</code>, <code>402</code>, <code>406</code> and <code>410</code>. See error tab for detail <code>error</code>.
</aside>


<!-- GET PAYMENT FIXED VIRTUAL ACCOUNT -->

## Get Payment Fixed Virtual Account

### HTTP Request

`GET https://croxit.io/virtual_accounts/payment/{payment_id}`

### Request Parameters

Parameter | Description
--------- | ------- | -----------
payment_id | Get the <code>payment_id</code> after your server got callback payment from <code>croxit.io</code>. See callback tab for detail.

### Response Parameters

> The above command returns response JSON structured like this:


```json
{
  "callback_payment_id":"188982ff8f918",
  "payment_amount":2000000,
  "payment_id":"pay_9283_99132",
  "payment_timestamp":"2017-08-11 13:21:29",
  "company_id":"128971hjkiie",
  "customer_id":"virtual_account_123456789",
  "bank_id":"BNI",
  "customer_name":"Brama Diwangkara",
  "virtual_account_number":"80008087798381082",
  "virtual_account_id":"5tty4212233uiu"
}
```

Parameter |  Description
--------- |  -----------
callback_payment_id | Callback id created when <code>croxit</code> send your server about callback virtual account payment
payment_amount | Amount that was paid to this virtual account
payment_id | Id for payment Virtual Account
payment_timestamp | Date time when payment virtual account happened
company_id | Your user ID
customer_id | Your customer ID based on your request 
bank_id | Bank id for the created virtual account
customer_name | Name of your virtual account 
virtual_account_number | Generated Virtual Account number and virtual account bank, we place <code>random number</code> if this value is not defined
virtual_account_id | Generate id for Virtual Account from <code>croxit.io</code>



<aside class="notice">
Possible error codes: <code>401</code>, <code>402</code>, <code>406</code> and <code>410</code>. See error tab for detail <code>error</code>.
</aside>