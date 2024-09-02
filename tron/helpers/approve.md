---
description: >-
  This endpoint returns an unsigned transaction to approve an unlimited amount
  of tokens for trading on SunPump.  This should be signed and broadcasted
  locally or on the client side.
icon: hexagon-check
---

# Approve Tokens

### Endpoint

* **URL:** `/sunpump/approve`
* **Method:** `POST`
* **Content-Type:** `application/json`
* **API Key Header:** `api-key: your-api-key`

### Parameters

| Parameter      | Type   | Required | Description                   |
| -------------- | ------ | -------- | ----------------------------- |
| `tokenAddress` | string | Yes      | Token Contract Address        |
| `userAddress`  | string | Yes      | Public Tron Address of sender |

### Example Approve Requests

{% tabs %}
{% tab title="cURL" %}
```sh
curl -X POST https://api.dangeracorn.com/sunpump/approve \
-H "Content-Type: application/json" \
-H "api-key: your-api-key" \
-d '{
  "tokenAddress": "token-contract-address",
  "userAddress": "sender-public-tron-address"
}'

```
{% endtab %}

{% tab title="JavaScript" %}
{% code title="npm install axios" %}
```javascript
const axios = require('axios');

const sellRequest = async () => {
  const response = await axios.post('https://api.dangeracorn.com/sunpump/approve', {
    tokenAddress: 'token-contract-address',
    userAddress: 'sender-public-tron-address'
  }, {
    headers: {
      'Content-Type': 'application/json',
      'api-key': 'your-api-key'
    }
  });

  const { unsignedTx } = await response.data;
};

sellRequest();

```
{% endcode %}
{% endtab %}

{% tab title="Python" %}
{% code title="pip install requests" %}
```python
import requests

url = 'https://api.dangeracorn.com/sunpump/approve'
headers = {
    'Content-Type': 'application/json',
    'api-key': 'your-api-key'
}

data = {
    tokenAddress: 'token-contract-address',
    userAddress: 'sender-public-tron-address'
}

response = requests.post(url, json=data, headers=headers)
print(response.json())

```
{% endcode %}
{% endtab %}

{% tab title="Go" %}
```go
package main

import (
	"bytes"
	"encoding/json"
	"net/http"
	"fmt"
)

func main() {
	data := map[string]interface{}{
	    tokenAddress: 'token-contract-address',
	    userAddress: 'sender-public-tron-address'
	}

	payload, _ := json.Marshal(data)
	req, _ := http.NewRequest("POST", "https://api.dangeracorn.com/sunpump/approve", bytes.NewBuffer(payload))
	req.Header.Set("Content-Type", "application/json")
	req.Header.Set("api-key", "your-api-key")

	client := &http.Client{}
	resp, _ := client.Do(req)
	defer resp.Body.Close()

	fmt.Println("Response Status:", resp.Status)
}

```
{% endtab %}

{% tab title="PHP" %}
```php
<?php

$url = 'https://api.dangeracorn.com/sunpump/approve';

$data = array(
    'tokenAddress' => 'token-contract-address',
    'userAddress' => 'sender-public-tron-address'
);

$options = array(
    'http' => array(
        'header'  => "Content-Type: application/json\r\n" .
                     "api-key: your-api-key\r\n",
        'method'  => 'POST',
        'content' => json_encode($data),
    ),
);

$context  = stream_context_create($options);
$response = file_get_contents($url, false, $context);

echo $response;

```
{% endtab %}
{% endtabs %}

### Example Response JSON

```json
{
  "unsignedTx": {
    "raw_data": { /* transaction data */ },
    "txID": "b69f27c7bfcf54a464294f1df99aaeff1b53714a12a80460709b20923a24486c" // example
  },
  "status": "unsigned",
  "code": "200"
}
```

### Error Responses

#### Invalid Parameters

```json
{
  "error": "Invalid parameters",
  "message": "You must only provide tokenAddress and userAddress",
  "code": "400"
}
```

#### Insufficient Funds

```json
{
  "error": "Insufficient funds",
  "message": "Your account does not have enough funds to perform this transaction.",
  "code": "400"
}
```

### _Notes_

> * **Rate Limiting:** This endpoint is rate-limited according to your plan's API key limits. Ensure that you handle these limits in your application.
> * **Unsigned Transactions**: The API returns unsigned transactions that users must sign before broadcasting.
