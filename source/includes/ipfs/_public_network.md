# Public Network - Usage

## POST upload file

```go
Golang code here.
```

```python
Python code here.
```

```javascript
handleUpload = (file, holdtime) => {

    let data = new FormData();
    data.append("file", file);
    data.append("hold_time", holdTime);

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

    xhr.open("POST", "https://api.temporal.cloud/v2/ipfs/public/file/add");
    xhr.setRequestHeader("Cache-Control", "no-cache");
    xhr.setRequestHeader("Authorization", "Bearer " + <JWT>);
    xhr.send(data);
};
```

> Example Response (200)

```
{
  "code": "200",
  "response": "QmRiC6GKnKZpG7mZmkok6B1mTPWzHnfuEEQQpNYbuZEuGa"
}
```

`https://api.temporal.cloud/v2/ipfs/public/file/add`

Uploads a file to the public network with optional encryption, and pins it for the specified number of months. When encrypting the file, it is impossible for Temporal to assist with recovery as we do not store the password.

The response is an IPFS hash that is publicly accessible.

<aside class="success">
This API endpoint is used for uploading files to <b>public</b> networks only.
</aside>

<aside class="warning">
For uploading files to private networks, see
<b><a href="#post-upload-file13">POST upload file</a></b> underneath <b>Private Networks - Primary</b>.
</aside>

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>file</b> | File (Blob) | The file you intend to upload.
| <b>hold_time</b> | Int | Number of months to pin the file.

### Optional Parameters

| Field | Type | Description
|-------|------|-------------
| <b>passphrase</b> | String | optional parameter used to encrypt upload.

## POST upload directory

```go
Golang code here.
```

```python
Python code here.
```

```javascript
```

> Example Response (200)

```
> add example respone
```

`https://api.temporal.cloud/v2/ipfs/public/file/add/directory`

Used to upload a directory to IPFS, particularly useful for hosting websites. The directory **must** first be zipped, with a `.zip` extension, and that zip file is what you must upload. The total uncompressed size of the zip file must be no larger than the maximum upload limit, which is currently 1GB

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>file</b> | File (Blob) | The *zipped* file of the directory you want to upload
| <b>hold_time</b> | Int | Number of months to pin the file.


## POST pin hash

```go
Golang code here.
```

```python
Python code here.
```

```javascript
handlePinFile = (ipfsHash, holdTime) => () => {

    let data = new FormData();
    data.append("hold_time", holdTime);

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

    xhr.open("POST", "https://api.temporal.cloud/v2/ipfs/public/pin/" + ipfsHash);
    xhr.setRequestHeader("Cache-Control", "no-cache");
    xhr.setRequestHeader("Authorization", "Bearer " + <JWT>);
    xhr.send(data);
};
```

> Example Response (200)

```
{
  "code": 200,
  "response": "pin request sent to backend"
}
```

`https://api.temporal.cloud/v2/ipfs/public/pin/:hash`

Pin an IPFS hash through Temporal, storing for the specified number of months. This is used when you want content that already exists on IPFS to be persistently stored and guaranteed to be available for the specified duration. 

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>hash</b> | IPFS Hash | The specific hash to pin.
| <b>hold_time</b> | Int | Number of months to pin the hash.


## POST extend pin

```go
Golang code here.
```

```python
Python code here.
```

```javascript
Javascript code here
```

> Example Response (200)

```
{
    "code": 200,
    "response": "pin time successfully extended"
}
```

`https://api.temporal.cloud/v2/ipfs/public/pin/:hash/extend`

Used to extend the hold time of an existing IPFS pin of yours, up to the specified number of months. The total hold time for free accounts must be 1 month (including after extension), while non-free accounts is 2 years (including after extension)

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>hash</b> | IPFS Hash | The specific hash to pin.
| <b>hold_time</b> | Int | Number of months to pin the hash.


## POST pubsub

```go
Golang code here.
```

```python
Python code here.
```

```javascript
handlePubSub = (message, topic) => () => {

    let data = new FormData();
    data.append("message", message);

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

    xhr.open("POST", "https://api.temporal.cloud/v2/ipfs/public/pubsub/publish/" + topic.toString());
    xhr.setRequestHeader("Cache-Control", "no-cache");
    xhr.setRequestHeader("Authorization", "Bearer " + <JWT>);
    xhr.send(data);

};
```

> Example Response (200)

```
{
  "code": 200,
  "response": {
    "message": "bar",
    "topic": "foo"
  }
}
```

`https://api.temporal.cloud/v2/ipfs/public/pubsub/publish/:topic`

Publish a message to the given PubSub topic.

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>message</b> | String | The message to publish.

### Response (200)

| Field | Type | Description
|-----------|------|-------------
| <b>message</b> | String | The message you published.
| <b>topic</b> | String | The topic you published the message to.

## GET object stats

```go
Golang code here.
```

```python
Python code here.
```

```javascript
handleObject = (hash) => () => {

    let xhr_stat = new XMLHttpRequest();
    xhr_stat.withCredentials = false;

    xhr_stat.addEventListener("readystatechange", function () {

        if (xhr_stat.readyState === 4) {

            let result = JSON.parse(xhr_stat.responseText);

            if (result.code === 200) {
                console.log(result);
            }

            else {
                // Error handling.
            }
        }
    }.bind(this));

    xhr_stat.open("GET", "https://api.temporal.cloud/v2/ipfs/public/stat/" + hash);
    xhr_stat.setRequestHeader("Cache-Control", "no-cache");
    xhr_stat.setRequestHeader("Authorization", "Bearer " + <JWT>);
    xhr_stat.send();
};
```

> Example Response (200)

```
{
  "code": 200,
  "response": {
    "Hash": "QmZpTc2UXsDeiD4Fb6j1kHqMeBngrN6V4myWR28i1YfuYA",
    "BlockSize": 498,
    "CumulativeSize": 13673755,
    "DataSize": 2,
    "LinksSize": 496,
    "NumLinks": 10
  }
}
```

`https://api.temporal.cloud/v2/ipfs/public/stat/:hash`

Retrieve information about an IPFS hash.

### Response (200)

| Field | Type | Description
|-----------|------|-------------
| <b>Hash</b> | IPFS Hash | The hash requested.
| <b>BlockSize</b> | Int | The ...
| <b>CumulativeSize</b> | Int | The ...
| <b>DataSize</b> | Int | The ...
| <b>LinksSize</b> | Int | The ...
| <b>NumLinks</b> | Int | The ...

## GET dag

```go
Golang code here.
```

```python
Python code here.
```

```javascript
handleDAG = (hash) => () => {

    let xhr_stat = new XMLHttpRequest();
    xhr_stat.withCredentials = false;

    xhr_stat.addEventListener("readystatechange", function () {

        if (xhr_stat.readyState === 4) {

            let result = JSON.parse(xhr_stat.responseText);

            if (result.code === 200) {
                console.log(result);
            }

            else {
                // Error handling.
            }
        }
    }.bind(this));

    xhr_stat.open("GET", "https://api.temporal.cloud/v2/ipfs/public/dag/" + hash);
    xhr_stat.setRequestHeader("Cache-Control", "no-cache");
    xhr_stat.setRequestHeader("Authorization", "Bearer " + <JWT>);
    xhr_stat.send();
};
```

> Example Response (200)

```
{
  "code": 200,
  "response": {
    "data": "CAE=",
    "links": [
      {
        "Cid": {
          "/": "QmSMMHB9QVEC37ie7G2FcekKLn5wFySie9XoMwEWkDwJBS"
        },
        "Name": "404.html",
        "Size": 4561
      },
      {
        "Cid": {
          "/": "QmXwJmxebQTZYiXL5ijojH8SsCkCSycLdF1GP31yt8NJcS"
        },
        "Name": "GCWeb",
        "Size": 2591746
      },
      {
        "Cid": {
          "/": "QmU1by7iZd1vEixJZUosFdw1vyMDBq9hL1Yc7D7Mqn3qCt"
        },
        "Name": "dist",
        "Size": 1152391
      },
      {
        "Cid": {
          "/": "QmUt97qU2VyfV5iQNyHhLG4kYBm4qTctQXEmJd46RtLj8x"
        },
        "Name": "en",
        "Size": 24103
      },
      {
        "Cid": {
          "/": "QmXYdLB7WGkpSajMxgpxkcWDqrdb1vAHyD3V9fMK4JUyR9"
        },
        "Name": "favicon",
        "Size": 66666
      },
      {
        "Cid": {
          "/": "Qmb3fJpXVGvUnNeRLC3P5sTXMzjpf5zq4tKt9XjhtYFf1k"
        },
        "Name": "fonts",
        "Size": 216178
      },
      {
        "Cid": {
          "/": "QmSCVZL3Yj4RxfMcTPyGAvBmDiKDpKdmUMXYxbtJQVtUqU"
        },
        "Name": "fr",
        "Size": 25015
      },
      {
        "Cid": {
          "/": "QmZ4BDukLtAUZj3EB1v6JTUpphjq3mt2rdU3dgMN7s47b3"
        },
        "Name": "img",
        "Size": 323474
      },
      {
        "Cid": {
          "/": "QmSrTNwejyMRyviN2G6xJTCscjNSMhy1fu1METPQZi3wH6"
        },
        "Name": "index.html",
        "Size": 6798
      },
      {
        "Cid": {
          "/": "QmXzfNvwRZcuDZNhtRJ64ADRcz7vxYwD6YJTy9JRzvMH7S"
        },
        "Name": "wet-boew",
        "Size": 9262325
      }
    ]
  }
}
```

`https://api.temporal.cloud/v2/ipfs/public/dag/:hash`

Retrieves the associated IPLD object for a given CID.

### Response (200)

| Field | Type | Description
|-----------|------|-------------
| <b>data</b> | String | The ...
| <b>Cid</b> | String | The ...
| <b>Name</b> | String | The ...
| <b>Size</b> | Int | Size of the file in (kilobytes/bytes?).