# IPFS Keys

## POST generate ipfs key

```go
Golang code here.
```

```python
Python code here.
```

```javascript
handleKeyGenerate = (keyName, keyType, keySize) => () => {

    let data = new FormData();
    data.append("key_name", keyName);
    data.append("key_type", keyType);
    data.append("key_bits", keySize);

    let xhr = new XMLHttpRequest();
    xhr.withCredentials = false;

    xhr.addEventListener("readystatechange", function () {

        if (xhr.readyState === 4) {

            let result = JSON.parse(xhr.responseText);

            if (result.code === 200) {
                console.log(result);
            }

            else {
                // Error handling.
            }
        }
    }.bind(this));

    xhr.open("POST", "https://dev.api.temporal.cloud/v2/account/key/ipfs/new");
    xhr.setRequestHeader("Cache-Control", "no-cache");
    xhr.setRequestHeader("Authorization", "Bearer " + <JWT>);
    xhr.send(data);

};
```

> Example Response (200)

```
{
  "code": 200,
  "response": "key creation sent to backend"
}
```

`https://dev.api.temporal.cloud/v2/account/key/ipfs/new`

Create an IPFS key with the given parameters.

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>key_type</b> | String | The type of the key, either `RSA` or `ED25519`.
| <b>key_size</b> | Int | The size of the key. `RSA` accepts `2048`, `3072`, or `4096` while `ED25519` only accepts `256`.
| <b>key_name</b> | String | The name of the key.

## GET export ipfs key

```go
Golang code here.
```

```python
Python code here.
```

```javascript
handleKeyExport = (keyName) => () => {

    let data = new FormData();
    let xhr = new XMLHttpRequest();
    xhr.withCredentials = false;

    xhr.addEventListener("readystatechange", function () {

        if (xhr.readyState === 4) {

            let result = JSON.parse(xhr.responseText);

            if (result.code === 200) {
                console.log(result);
            }

            else {
                // Error handling.
            }
        }
    }.bind(this));

    xhr.open("GET", "https://dev.api.temporal.cloud/v2/account/key/export/" + keyName);
    xhr.setRequestHeader("Cache-Control", "no-cache");
    xhr.setRequestHeader("Authorization", "Bearer " + <JWT>);
    xhr.send(data);
};
```

> Example Response (200)

```
{
  "code": "200",
  "response": [
    "road",
    "carwash",
    "ambulance",
    "vehicle",
    "manhole",
    "explosion"
  ]
}
```

`https://dev.api.temporal.cloud/v2/account/key/export/:name`

Exports the mnemonic phrase associated with a given key.

<aside class="warning">Mnemonic phrases for RSA keys are extremely large and can exceed 1,000 words.</aside>

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>name</b> | String | Name of the key to export.

### Response (200)

| Field | Type | Description
|-----------|------|-------------
| <b>response</b> | Array[String] | An array of all words in the mnemonic phrase.

## GET ipfs keys

```go
Golang code here.
```

```python
Python code here.
```

```javascript
let xhr = new XMLHttpRequest();
xhr.withCredentials = false;

xhr.addEventListener("readystatechange", function () {

    if (xhr.readyState === 4) {

        let result = JSON.parse(xhr.responseText);

        if (result.code === 400) {
            // Error handling.
        }

        else if  (result.code === 200) {
            console.log(result);
        }

        else {
            // Error handling.
        }

    }
}.bind(this));

xhr.open("GET", "https://dev.api.temporal.cloud/v2/account/key/ipfs/get");
xhr.setRequestHeader("Cache-Control", "no-cache");
xhr.setRequestHeader("Authorization", "Bearer " + <JWT>);
xhr.send();
```

> Example Response (200)

```
{
  "code": 200,
  "response": {
    "key_ids": [
      "QmRxu16ho4kmak3ZFEwUuSQAHiLQoaanLeYa4R3LG2ozCg",
      "Qme3dCHims67ACrKXNoioP5ftr4tP1n1beaWCcJiTJYL1E",
      "QmNRcEwEmFK1jz6w58LS7TfxHsR42AinVdCbmqReXuAqWM",
      "12D3KooWRtMLutruxkjWkdTdkk96qyMvXtvLJDEUxdjyzQwj8HPS"
    ],
    "key_names": [
      "postables-ke2",
      "postables-muchkeysuchwow",
      "postables-1",
      "postables-key2019ED25519"
    ]
  }
}
```

`https://dev.api.temporal.cloud/v2/account/key/ipfs/get`

Retrieve all IPFS keys generated through Temporal.

<aside class="warning">Note that <b>key_ids</b> and <b>key_names</b> mirror each other; the first element in <b>key_ids</b> corresponds to the first element in <b>key_names</b>.</aside>

### Response (200)

| Field | Type | Description
|-----------|------|-------------
| <b>key_ids</b> | IPFS Hash | The hash of a key.
| <b>key_names</b> | String | The name of a key.