# Public Network

## POST download file

```go
Golang code here.
```

```python
Python code here.
```

```javascript
handleDownload = (ipfsHash, networkName) => () => {

    let xhr = new XMLHttpRequest();
    xhr.withCredentials = false;
    xhr.responseType = 'blob';

    // Optional two lines, used if supplying a private networkName.
    let data = new FormData();
    data.append("networkName");

    let json_reader = new FileReader();

    xhr.addEventListener("readystatechange", function () {

        if (xhr.readyState === 4) {
            if (xhr.response.type === "application/json") {
                // Error handling. (i.e. 400 Response)
            }

            else {
                let blob = new Blob([xhr.response], {type: 'application/octet-stream'});

                // The following code enables automatic downloading through a web app!
                let a = document.createElement("a");
                a.style = "display: none";
                document.body.appendChild(a);
                let url = window.URL.createObjectURL(blob);
                a.href = url;
                a.download = fileName;
                a.click();
                window.URL.revokeObjectURL(url);
            }
        }
    }.bind(this));

    xhr.open("POST", "https://dev.api.temporal.cloud:6767/v2/ipfs/utils/download/" + ipfsHash);
    xhr.setRequestHeader("Cache-Control", "no-cache");
    xhr.setRequestHeader("Authorization", "Bearer " + <JWT>);
    xhr.send(data); // Use xhr.send() if not supplying a private networkName.
};
```

`https://dev.api.temporal.cloud/v2/ipfs/utils/download/:hash`

Downloads a specific hash that was previously uploaded through the Temporal <b><a href="#post-upload-file">POST upload file</a></b> call.

There is an optional parameter, `networkName` that you can pass for downloading files from private IPFS networks created
through Temporal (see <b><a href="#post-create-network">POST create network</a></b>).

<aside class="success">
This API endpoint is used for downloading files from public <b>and</b> private networks.
</aside>

<aside class="warning">
When downloading a file from a private network, please ensure the network is running.
Call <b><a href="#post-start-network">POST start network</a></b> if the network is stopped.
</aside>

### Optional Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>networkName</b> | String | The private network to download a file from.


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

    xhr.open("POST", "https://dev.api.temporal.cloud/v2/ipfs/public/file/add");
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

`https://dev.api.temporal.cloud/v2/ipfs/public/file/add`

Uploads a file to the public network, and pins it for the specified number of months.
The response is an IPFS hash that is publicly accessible (unless uploaded to a private network).

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
| <b>holdtime</b> | Int | Number of months to pin the file.

## POST upload file advanced

```go
Golang code here.
```

```python
Python code here.
```

```javascript
Javascript code here.
```

> Example Response (200)

```
{
  "expire": "2018-12-21T19:31:42Z",
  "token": "eyJhbG ... "
}
```

`https://api.temporal.cloud/v2/auth/login`

Validates the provided username and password to generate a JSON Web Token (JWT) used for authentication.
This token is valid for exactly 24 hours, at which point you will need to generate a new token.

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>username</b> | String | The username.
| <b>password</b> | String | The associated password.

## POST pin file

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

    xhr.open("POST", "https://dev.api.temporal.cloud/v2/ipfs/public/pin/" + ipfsHash);
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

`https://dev.api.temporal.cloud/v2/ipfs/private/pin/:hash`

Pin an IPFS hash through Temporal.

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>ipfsHash</b> | IPFS Hash | The specific hash to pin.
| <b>holdTime</b> | Int | Number of months to pin the hash.

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

    xhr.open("POST", "https://dev.api.temporal.cloud/v2/ipfs/public/pubsub/publish/" + topic.toString());
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

`https://dev.api.temporal.cloud/v2/ipfs/public/pubsub/publish/:topic`

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

    xhr_stat.open("GET", "https://dev.api.temporal.cloud/v2/ipfs/public/stat/" + hash);
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

`https://dev.api.temporal.cloud/v2/ipfs/public/stat/:hash`

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

    xhr_stat.open("GET", "https://dev.api.temporal.cloud/v2/ipfs/public/dag/" + hash);
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

`https://dev.api.temporal.cloud/v2/ipfs/public/dag/:hash`

Retrieves the associated IPLD object for a given CID.

### Response (200)

| Field | Type | Description
|-----------|------|-------------
| <b>data</b> | String | The ...
| <b>Cid</b> | String | The ...
| <b>Name</b> | String | The ...
| <b>Size</b> | Int | Size of the file in (kilobytes/bytes?).