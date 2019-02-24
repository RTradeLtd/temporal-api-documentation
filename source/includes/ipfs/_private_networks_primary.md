# Private Networks - Primary

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
handleUpload = (file, holdtime, networkName) => {

    let data = new FormData();
    data.append("file", file);
    data.append("hold_time", holdTime);
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

    xhr.open("POST", "https://dev.api.temporal.cloud/v2/ipfs/private/file/add");
    xhr.setRequestHeader("Cache-Control", "no-cache");
    xhr.setRequestHeader("Authorization", "Bearer " + <JWT>);
    xhr.send(data);
};
```

> Example Response (200)

```
{
  "code": 200,
  "response": "QmYwwdB1X6aivm8me71EwWXFZjGtjkAmUuT9qEDQBZmdSk"
}
```

`https://dev.api.temporal.cloud/v2/ipfs/private/file/add`

Uploads a file to the specified private network with optional encryption, and pins it for the specified number of months. When encrypting the file, it is impossible for Temporal to assist with recovery as we do not store the password.

The response is an IPFS hash that is not publicly accessible.

<aside class="warning">
File uploads will not work if your private network is stopped.
</aside>

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>file</b> | File (Blob) | The file you intend to upload.
| <b>hold_time</b> | Int | Number of months to pin the file.
| <b>privateNetwork</b> | String | Name of the private network to upload to.

### Optional Parameters

| Field | Type | Description
|-------|------|-------------
| <b>passphrase</b> | String | optional parameter used to encrypt upload.

## POST pin hash

```go
Golang code here.
```

```python
Python code here.
```

```javascript
handlePinFile = (ipfsHash, holdTime, networkName) => () => {

    let data = new FormData();
    data.append("hold_time", holdTime);
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

    xhr.open("POST", "https://dev.api.temporal.cloud/v2/ipfs/private/pin/" + ipfsHash);
    xhr.setRequestHeader("Cache-Control", "no-cache");
    xhr.setRequestHeader("Authorization", "Bearer " + <JWT>);
    xhr.send(data);
};
```

> Example Response (200)

```
{
  "code": 200,
  "response": "content pin request sent to backend"
}
```

`https://dev.api.temporal.cloud/v2/ipfs/private/pin/:hash`

Pin a hash to a private network. This hash *must* be discoverable by the private network node.

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>hash</b> | IPFS Hash | The specific hash to pin.
| <b>hold_time</b> | Int | Number of months to pin the hash.
| <b>network_name</b> | String | Number of months to pin the hash.

## GET check pin

```go
Golang code here.
```

```python
Python code here.
```

```javascript
handleCheckPin = (hash, networkName) => () => {

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

    xhr.open("POST", "https://dev.api.temporal.cloud/v2/ipfs/private/pin/check/" + hash + "/" + networkName);
    xhr.setRequestHeader("Cache-Control", "no-cache");
    xhr.setRequestHeader("Authorization", "Bearer " + <JWT>);
    xhr.send(data);
};
```

> Example Response (200)

```
{
  "code": 200,
  "response": true
}
```

`https://dev.api.temporal.cloud/v2/ipfs/private/pin/check/:hash/:networkName`

Check if a network is pinning the given hash.

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>hash</b> | String | The hash to check.
| <b>networkName</b> | String | The network to check.

## POST pubsub

```go
Golang code here.
```

```python
Python code here.
```

```javascript
handlePubSub = (message, topic, networkName) => () => {

    let data = new FormData();
    data.append("message", message);
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

`https://dev.api.temporal.cloud/v2/ipfs/private/pubsub/publish/:topic`

Publish a message on a private network to the given topic.

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>message</b> | String | The message to publish.
| <b>network_name</b> | String | The private network to publish the message to.

### Response (200)

| Field | Type | Description
|-----------|------|-------------
| <b>message</b> | String | The message you published.
| <b>topic</b> | String | The topic you published the message to.

## POST create network

```go
Golang code here.
```

```python
Python code here.
```

```javascript
handleCreateNetwork = (networkName, swarmKey, bootstrapPeers, users) => () => {

    let data = new FormData();
    data.append("network_name", networkName);

    // If optional paramaters are supplied.
    data.append("swarm_key", swarmKey);
    data.append("bootstrapPeers", bootstrapPeers);
    data.append("users", users.split(','));

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

    xhr.open("POST", "https://dev.api.temporal.cloud/v2/ipfs/private/network/new");
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
    "api_url": "192.168.1.243:5981",
    "id": 51,
    "network_name": "thisisnotarealtestnetwork",
    "swarm_key": "/key/swarm/psk/1.0.0/\n/base16/\n0a1bb9d5a949484f19d84104981c94827bff62268b82d7a36d3358aa629465ba",
    "users": [
      "postables"
    ]
  }
}
```

`https://dev.api.temporal.cloud/v2/ipfs/private/network/new`

Create a private network through Temporal.

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>network_name</b> | String | The name of your network.
| <b>swarm_key</b>* | String | The swarm key.
| <b>bootstrap_peers</b>* | String | The bootstrap peers.
| <b>users</b>* | Array[String] | A list of usernames which have access to the private network.

<aside class="warning">
*Optional parameters. Note that if one optional parameter is supplied, all three must be supplied.
</aside>

### Response (200)

| Field | Type | Description
|-----------|------|-------------
| <b>api_url</b> | String | The API endpoint for your network.
| <b>id</b> | Int | The unique ID of your network.
| <b>network_names</b> | String | The name of your network.
| <b>swarm_key</b> | String | The swarm key generated (or provided) for the network.
| <b>users</b> | Array[String] | A list of usernames which have access to the private network.

## POST start network

```go
Golang code here.
```

```python
Python code here.
```

```javascript
handleStart = (networkName) => () => {

    let data = new FormData();
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

    xhr.open("POST", "https://dev.api.temporal.cloud/v2/ipfs/private/network/start");
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
    "network_name": "thisisnotarealtestnetwork",
    "state": "started"
  }
}
```

`https://dev.api.temporal.cloud/v2/ipfs/private/network/start`

Start a private network, enabling uploads and downloads.

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>network_name</b> | String | The network to start.

### Response (200)

| Field | Type | Description
|-----------|------|-------------
| <b>network_name</b> | String | The network that was started.
| <b>state</b> | String | The new state of the network ("started").

## POST stop network

```go
Golang code here.
```

```python
Python code here.
```

```javascript
handleStart = (networkName) => () => {

    let data = new FormData();
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

    xhr.open("POST", "https://dev.api.temporal.cloud/v2/ipfs/private/network/stop");
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
    "network_name": "thisisnotarealtestnetwork",
    "state": "stopped"
  }
}
```

`https://dev.api.temporal.cloud/v2/ipfs/private/network/stop`

Stop a private network, preventing uploads and downloads.

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>network_name</b> | String | The network to stop.

### Response (200)

| Field | Type | Description
|-----------|------|-------------
| <b>network_name</b> | String | The network that was started.
| <b>state</b> | String | The new state of the network ("stopped").

## DEL remove network

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

`https://dev.api.temporal.cloud/v2/ipfs/private/network/remove`

Delete a private network.

<aside class="warning">
Network deletion will not work if your private network is running. Ensure you have stopped it.
</aside>

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>username</b> | String | The username.
| <b>password</b> | String | The associated password.