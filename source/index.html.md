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
  crx_development_R3tJfOss0OC8HjjtKrROHjgkTNCk9dN5lSfk-R1l9Wbe+rSiCwZ3jw==
```

> First add a exclamation mark at the end of your token

```Json
  crx_development_P4qDfOss0OCpl8RtKrROHjaQYNCk9dN5lSfk+R1l9Wbe+rSiCwZ3jw==!
```

> Finally, just encode your api key with <a href='https://www.base64encode.org/'>base64</a> to get this

```Json
  Y3J4X2RldmVsb3BtZW50X1IzdEpmT3NzME9DOEhqanRLclJPSGpna1ROQ2s5ZE41bFNmay1SMWw5V2JlK3JTaUN3WjNqdz09IQ==
```

Croxit uses API keys to allow access to the API. You can register a new croxit API key at our [developer portal](http://croxit.io/developers).

Croxit expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: your base64 secrete key`

All the following request must inlcude header json type, so just place this on your header:

`Content-Type: application/json`

And you all the reponse and request body should be:

`Camel case variable`

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
    "customerId":"virtual_account_123456789",
    "bankId":"BNI",
    "name":"Adhi Santosa"
  }
```

Parameter | Mandatory | Description
--------- | ------- | -----------
customerId | yes | `string` Your customer id (depend on your set) with maximum character is 1000
bankId | yes | `string` Bank ID of your virtual account you want to create
customerName | yes | `string` Your customer name (contain letter and space only) to display on the bank's interface (like ATM or mobile banking)
virtualAccountNumber | no | `string` Virtual Account number, contain 8 character of number
isClosed | no | `boolean` if this parameter set to true, then the payment of your customer based on your set amount (trxAmount)
trxAmount | optional | `number` if virtual_account set to closed, you have to determine the trxAmount
datetimeExpired | no | `ISO_DATE` the time when virtual account will be expired

### Response Parameters


> The above command returns response JSON structured like this:


```json
{
  "businessPartnerId":"128971hjkiie",
  "customerId":"virtual_account_123456789",
  "bankId":"BNI",
  "customerName":"Adhi Santosa",
  "virtualAccountNumber":"80008087798381082",
  "virtualAccountId":"5tty4212233uiu",
  "isClosed":false,
  "datetimeExpired":"2020-01-01 13:00:00",
  "status":"active",
}
```

Parameter |  Description
--------- |  -----------
businessPartnerId | Your user ID
customerId | Your customer ID based on your request 
bankId | Bank id for the created virtual account
customerName | Name of your virtual account 
virtualAccountNumber | Generated Virtual Account number and virtual account bank, we place <code>random number</code> if this value is not defined
virtualAccountId | Generate id for Virtual Account from <code>croxit.io</code>
isClosed | The transaction amount determined if has true <code>value</code>, default value is <code>false</code>
trxAmount | Amount of transaction if you set `isClosed` equals true
datetimeExpired | The time when the virtual account will be expired, default for this value is 1 year from virtual account created
status | status that defines virtual account ACTIVE or INACTIVE



<aside class="notice">
Possible error codes: <code>401</code>, <code>402</code>, <code>406</code> and <code>410</code>. See error tab for detail <code>error</code>.
</aside>


<!-- UPDATE FIXED VIRTUAL ACCOUNT -->

## Update Fixed Virtual Account

### HTTP Request

`PUT https://croxit.io/virtual_accounts/update/{virtualAccountId}`

### Request Parameters

> Example update fixed Virtual Account

```json
  {
    "trxAmount":2000000,
    "datetimeExpired":"2020-01-01 13:00:00"
  }
```

Parameter | Description
--------- | ------- | -----------
customerName | `string` Your customer name (contain letter and space only) to display on the bank's interface (like ATM or mobile banking)
trxAmount | `number` changeable if your virtual account is set to <code>isClosed</code>
datetimeExpired | `ISO_DATE` the time when virtual account will be expired

### Response Parameters


> The above command returns response JSON structured like this:


```json
{
  "businessPartnerId":"128971hjkiie",
  "customerId":"virtual_account_123456789",
  "bankId":"BNI",
  "customerName":"Adhi Santosa",
  "virtualAccountNumber":"80008087798381082",
  "virtualAccountId":"5tty4212233uiu",
  "isClosed":true,
  "trxAmount":2000000,
  "datetimeExpired":"2020-01-01 13:00:00",
  "status":"active",
}
```

Parameter |  Description
--------- |  -----------
businessPartnerId | Your user ID
customerId | Your customer ID based on your request 
bankId | Bank id for the created virtual account
customerName | Name of your virtual account 
virtualAccountNumber | Generated Virtual Account number and virtual account bank, we place <code>random number</code> if this value is not defined
virtualAccountId | Generate id for Virtual Account from <code>croxit.io</code>
isClosed | The transaction amount determined if has <code>true</code> value, default value is <code>false</code>
trxAmount | Amount of transaction if you set `isClosed` equals true
datetimeExpired | The time when the virtual account will be expired 
status | status that defines virtual account ACTIVE or INACTIVE



<aside class="notice">
Possible error codes: <code>401</code>, <code>402</code>, <code>406</code> and <code>410</code>. See error tab for detail <code>error</code>.
</aside>


<!-- GET DETAIL FIXED VIRTUAL ACCOUNT -->

## Get Detail Fixed Virtual Account

### HTTP Request

`GET https://croxit.io/virtual_accounts/get/{virtualAccountId}`

### Request Parameters

Parameter | Description
--------- | ------- | -----------
virtualAccountId | Generate id for Virtual Account from <code>croxit.io</code>

### Response Parameters

> The above command returns response JSON structured like this:


```json
{
  "businessPartnerId":"128971hjkiie",
  "customerId":"virtual_account_123456789",
  "bankId":"BNI",
  "customerName":"Adhi Santosa",
  "virtualAccountNumber":"80008087798381082",
  "virtualAccountId":"5tty4212233uiu",
  "isClosed":true,
  "trxAmount":2000000,
  "datetimeExpired":"2020-01-01 13:00:00",
  "status":"active",
}
```

Parameter |  Description
--------- |  -----------
businessPartnerId | Your user ID
customerId | Your customer ID based on your request 
bankId | Bank id for the created virtual account
customerName | Name of your virtual account 
virtualAccountNumber | Generated Virtual Account number and virtual account bank, we place <code>random number</code> if this value is not defined
virtualAccountId | Generate id for Virtual Account from <code>croxit.io</code>
isClosed | The transaction amount determined if has <code>true</code> value, default value is <code>false</code>
trxAmount | Amount of transaction if you set `isClosed` equals true
datetimeExpired | The time when the virtual account will be expired 
status | status that defines virtual account ACTIVE or INACTIVE



<aside class="notice">
Possible error codes: <code>401</code>, <code>402</code>, <code>406</code> and <code>410</code>. See error tab for detail <code>error</code>.
</aside>


<!-- GET PAYMENT FIXED VIRTUAL ACCOUNT -->

## Get Payment Fixed Virtual Account

### HTTP Request

`GET https://croxit.io/virtual_accounts/payment/{paymentId}`

### Request Parameters

Parameter | Description
--------- | ------- | -----------
paymentId | Get the <code>paymentId</code> after your server got callback payment from <code>croxit.io</code>. See callback tab for detail.

### Response Parameters

> The above command returns response JSON structured like this:


```json
{
  "paymentId":"pay_9283_99132",
  "paymentAmount":2000000,
  "paymentTimestamp":"2017-08-11 13:21:29",
  "businessPartnerId":"128971hjkiie",
  "customerId":"virtual_account_123456789",
  "bankId":"BNI",
  "customerName":"Adhi Santosa",
  "virtualAccountNumber":"80008087798381082",
  "virtualAccountId":"5tty4212233uiu"
}
```

Parameter |  Description
--------- |  -----------
paymentId | Id for payment Virtual Account
paymentAmount | Amount that was paid to this virtual account
paymentTimestamp | Date time when payment virtual account happened
businessPartnerId | Your user ID
customerId | Your customer ID based on your request 
bankId | Bank id for the created virtual account
customerName | Name of your virtual account 
virtualAccountNumber | Generated Virtual Account number and virtual account bank, we place <code>random number</code> if this value is not defined
virtualAccountId | Generate id for Virtual Account from <code>croxit.io</code>



<aside class="notice">
Possible error codes: <code>401</code>, <code>402</code>, <code>406</code> and <code>410</code>. See error tab for detail <code>error</code>.
</aside>