# IPNS

## POST public publish

```go
Golang code here.
```

```python
Python code here.
```

```javascript
handlePublicIPNS = (hash, lifetime, ttl, key, resolve) => () => {

    let data = new FormData();
    data.append("hash", hash);
    data.append("life_time", lifetime);
    data.append("ttl", ttl);
    data.append("key", key);
    data.append("resolve", resolve);

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

    xhr.open("POST", "https://dev.api.temporal.cloud/v2/ipns/public/publish/details");
    xhr.setRequestHeader("Cache-Control", "no-cache");
    xhr.setRequestHeader("Authorization", "Bearer " + <JWT>);
    xhr.send(data);
};
```

> Example Response (200)

```
{
  // Need a response.
}
```

`https://dev.api.temporal.cloud/v2/ipns/public/publish/details`

Publish IPNS records to the public network.

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>hash</b> | IPFS Hash | The hash to publish.
| <b>life_time</b> | String | The lifetime.
| <b>ttl</b> | String | The time-to-live.
| <b>key</b> | String | Name of the IPFS key.
| <b>resolve</b> | Bool | Whether to resolve the IPNS record or not.

## POST private publish

```go
Golang code here.
```

```python
Python code here.
```

```javascript
handlePrivateIPNS = (hash, lifetime, ttl, key, resolve, networkName) => () => {

    let data = new FormData();
    data.append("hash", hash);
    data.append("life_time", lifetime);
    data.append("ttl", ttl);
    data.append("key", key);
    data.append("resolve", resolve);
    data.append("network_name", networkName);

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

    xhr.open("POST", "https://dev.api.temporal.cloud/v2/ipns/private/publish/details");
    xhr.setRequestHeader("Cache-Control", "no-cache");
    xhr.setRequestHeader("Authorization", "Bearer " + <JWT>);
    xhr.send(data);
};
```

> Example Response (200)

```
{
  // Need a response.
}
```

`https://dev.api.temporal.cloud/v2/ipns/private/publish/details`

Publish IPNS records to a private network.

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>hash</b> | IPFS Hash | The hash to publish.
| <b>life_time</b> | String | The lifetime.
| <b>ttl</b> | String | The time-to-live.
| <b>key</b> | String | Name of the IPFS key.
| <b>resolve</b> | Bool | Whether to resolve the IPNS record or not.
| <b>network_name</b> | String | Name of the network you are publishing to.

## GET records

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

        if (result.code === 200) {
            console.log(result);
        }

        else {
            // Error handling.
        }
    }
}.bind(this));

xhr.open("GET", "https://dev.api.temporal.cloud/v2/ipns/records");
xhr.setRequestHeader("Cache-Control", "no-cache");
xhr.setRequestHeader("Authorization", "Bearer " + <JWT>);
xhr.send();
```

> Example Response (200)

```
{
  "code": 200,
  "response": [
    {
        "CreatedAt": "2018-10-11T02:41:09.241844Z",
        "CurrentIPFSHash": "QmWmLpZLUA1cHZGyYATUUHg99EHfSvTyttNZFQkEpCVbwd",
        "DeletedAt": null,
        "ID": 2,
        "IPFSHashes": ["QmWmLpZLUA1cHZGyYATUUHg99EHfSvTyttNZFQkEpCVbwd"],
        "IPNSHash": "QmcPHXmqRCsd6zSDJdQmM7pWhaC8cXK8f27YLpTdZkpGz4",
        "Key": "pseudonaut_two-4096_test",
        "LifeTime": "4h0m0s",
        "NetworkName": "public",
        "Sequence": 1,
        "TTL": "24h0m0s",
        "UpdatedAt": "2018-10-11T02:41:09.241844Z",
        "UserName": "pseudonaut_two"
    },
    {
        "CreatedAt": "2018-12-24T22:27:54.151338Z",
        "CurrentIPFSHash": "QmSKpt2AvPM5QGfRiWLs2esj9PKTcz1GBbpdWJ41vTn8we",
        "DeletedAt": null,
        "ID": 12,
        "IPFSHashes": [
            "QmWmLpZLUA1cHZGyYATUUHg99EHfSvTyttNZFQkEpCVbwd",
            "QmSKpt2AvPM5QGfRiWLs2esj9PKTcz1GBbpdWJ41vTn8we"
        ],
        "IPNSHash": "QmNopw5FsuBSvgG5DYrd4oYXSYt6186bwRfHpwkK6gPwhv",
        "Key": "pseudonaut_two-55",
        "LifeTime": "24h0m0s",
        "NetworkName": "public",
        "Sequence": 2,
        "TTL": "24h0m0s",
        "UpdatedAt": "2019-01-06T06:07:07.999384Z",
        "UserName": "pseudonaut_two"
    }
  ]
}
```

`https://dev.api.temporal.cloud/api/v2/ipns/records`

Lists all IPNS records you've published to public and private networks.

### Response (200)

| Field | Type | Description
|-----------|------|-------------
| <b>CreatedAt</b> | DateTime | Time the record was published.
| <b>CurrentIPFSHash</b> | Bool | <i>Need a description!</i>
| <b>DeletedAt</b> | DateTime | Time the file was deleted.
| <b>ID</b> | Int | The unique ID of your upload.
| <b>IPFSHashes</b> | Array[IPFS Hash] | <i>Need a description!</i>
| <b>IPNSHash</b> | IPFS Hash | <i>Need a description!</i>
| <b>Key</b> | String | Name of the IPFS key used.
| <b>LifeTime</b> | String | Number of months your content is pinned.
| <b>NetworkName</b> | String | Network the record was published on (`public` = Public Network).
| <b>Sequence</b> | Int | <i>Need a description!</i>
| <b>TTL</b> | String | The time to live.
| <b>UpdatedAt</b> | DateTime | Time the file was last updated.
| <b>Username</b> | String | User that published the record (<i>that's you</i>).