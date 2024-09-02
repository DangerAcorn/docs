---
icon: quotes
description: >-
  Gets specific price TOKEN/TRX or TRX/TOKEN base on TRX or Token amount. 
  Subtract slippage % to get accurate minimum expected amount on front end
  applications.
---

# Get Quote

{% hint style="info" %}
This quote automatically takes SunPump's 1% trading fee into account. You do not need to estimate trading fees.
{% endhint %}

### Endpoint

* **URL:** `/sunpump/getQuote`
* **Method:** `GET`
* **Content-Type:** `application/json`
* **API Key Header:** `api-key: your-api-key`
