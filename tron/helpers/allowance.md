---
description: >-
  This SunPump endpoint checks if, and how many, Tokens are currently Approved
  for trading (selling).
icon: magnifying-glass-arrow-right
---

# Check Allowance

### Endpoint

* **URL:** `/sunpump/allowance`
* **Method:** `GET`
* **Content-Type:** `application/json`
* **API Key Header:** `api-key: your-api-key`

### Parameters

| Parameter      | Type   | Required | Description                   |
| -------------- | ------ | -------- | ----------------------------- |
| `tokenAddress` | string | Yes      | Token Contract Address        |
| `userAddress`  | string | Yes      | Public Tron Address of sender |

### Example Allowance Requests

{% tabs %}
{% tab title="cURL" %}
```sh
curl -X POST https://api.dangeracorn.com/sunpump/allowance\
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

const buyRequest = async () => {
  const response = await axios.post('https://api.dangeracorn.com/sunpump/allowance', {
    tokenAddress: 'token-contract-address',
    userAddress: 'sender-public-tron-address'
  }, {
    headers: {
      'Content-Type': 'application/json',
      'api-key': 'your-api-key'
    }
  });

  console.log(response.json());
};

buyRequest();

```
{% endcode %}
{% endtab %}

{% tab title="Python" %}
{% code title="pip install requests" %}
```python
import requests

url = 'https://api.dangeracorn.com/sunpump/allowance'
headers = {
    'Content-Type': 'application/json',
    'api-key': 'your-api-key'
}

data = {
    "tokenAddress": "token-contract-address",
    "userAddress": "sender-public-tron-address"
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
		"tokenAddress": "token-contract-address",
		"userAddress": "sender-public-tron-address",
	}

	payload, _ := json.Marshal(data)
	req, _ := http.NewRequest("POST", "https://api.dangeracorn.com/sunpump/allowance", bytes.NewBuffer(payload))
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

$url = 'https://api.dangeracorn.com/sunpump/allowance';

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
  "amount": "999999999000000000000000000000",
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

### _Notes_

> * **Rate Limiting:** This endpoint is rate-limited according to your plan's API key limits. Ensure that you handle these limits in your application.
