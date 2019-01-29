# Private Networks - Utility

## POST beam

```go
Golang code here.
```

```python
Python code here.
```

```javascript
handleBeam = (sourceNetwork, destinationNetwork, hash, passphrase) => () => {

    let data = new FormData();
    data.append("source_network", sourceNetwork);
    data.append("destination_network", destinationNetwork);
    data.append("content_hash", hash);
    data.append("passphrase", passphrase);

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

    xhr.open("POST", "https://dev.api.temporal.cloud/v2/ipfs/utils/laser/beam");
    xhr.setRequestHeader("Cache-Control", "no-cache");
    xhr.setRequestHeader("Authorization", "Bearer " + <JWT>);
    xhr.send(data);
};
```

> Example Response (200)

```
{
  "expire": "2018-12-21T19:31:42Z",
  "token": "eyJhbG ... "
}
```

`https://dev.api.temporal.cloud/v2/ipfs/utils/laser/beam`

Transfer content between two different IPFS networks.

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>source_network</b> | String | The network to copy content from.
| <b>destination_network</b> | String | The network to copy content to.
| <b>content_hash</b> | IPFS Hash | The content to hash.
| <b>passphrase</b>* | String | Passphrase to encrypt the content with.

<aside class="warning">
*Optional parameter. If you supply a passphrase, the content will be encrypted during transfer.
</aside>

## GET object stats

```go
Golang code here.
```

```python
Python code here.
```

```javascript
handleObject = (hash, networkName) => () => {

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

    xhr_stat.open("GET", "https://dev.api.temporal.cloud/v2/ipfs/private/stat/" + hash + "/" + networkName);
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
    "Hash": "QmejvEPop4D7YUadeGqYWmZxHhLc4JBUCzJJHWMzdcMe2y",
    "BlockSize": 12,
    "CumulativeSize": 12,
    "DataSize": 10,
    "LinksSize": 2,
    "NumLinks": 0
  }
}
```

`https://dev.api.temporal.cloud/v2/ipfs/private/stat/:hash/:networkName`

Retrieve information about an object (hash) on a private network.

### Response (200)

| Field | Type | Description
|-----------|------|-------------
| <b>Hash</b> | IPFS Hash | The hash requested.
| <b>BlockSize</b> | Int | The ...
| <b>CumulativeSize</b> | Int | The ...
| <b>DataSize</b> | Int | The ...
| <b>LinksSize</b> | Int | The ...
| <b>NumLinks</b> | Int | The ...

## GET uploads

```go
Golang code here.
```

```python
Python code here.
```

```javascript
handleUploads = (networkName) => () => {

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

    xhr_stat.open("GET", "https://dev.api.temporal.cloud/v2/ipfs/private/uploads/" + networkName);
    xhr_stat.setRequestHeader("Cache-Control", "no-cache");
    xhr_stat.setRequestHeader("Authorization", "Bearer " + <JWT>);
    xhr_stat.send();
};
```

> Example Response (200)

```
{
  "code": 200,
  "response": [
    {
      "ID": 522,
      "CreatedAt": "2018-12-20T20:19:41.383403Z",
      "UpdatedAt": "2018-12-20T20:20:56.778709Z",
      "DeletedAt": null,
      "Hash": "QmYwwdB1X6aivm8me71EwWXFZjGtjkAmUuT9qEDQBZmdSk",
      "Type": "file",
      "NetworkName": "private_net_12222",
      "HoldTimeInMonths": 2,
      "UserName": "postables",
      "GarbageCollectDate": "2019-02-20T20:19:41.382864Z",
      "UserNames": [
        "postables"
      ],
      "Encrypted": false
    }
  ]
}
```

`https://dev.api.temporal.cloud/v2/ipfs/private/uploads/:networkName`

Retrieve uploads for a private network.

### Response (200)

| Field | Type | Description
|-----------|------|-------------
| <b>CreatedAt</b> | DateTime | Time the file was created.
| <b>DeletedAt</b> | DateTime | Time the file was deleted.
| <b>Encrypted</b> | Bool | Whether the file is encrypted or not.
| <b>GarbageCollectDate</b> | DateTime | When the file will be deleted (or pinning stops).
| <b>Hash</b> | IPFS Hash | The hash associated with your content.
| <b>HoldTimeInMonths</b> | Int | Number of months your content is pinned.
| <b>ID</b> | Int | The unique ID of your upload.
| <b>NetworkName</b> | String | The private network your file was published on.
| <b>Type</b> | String | The type of file you uploaded.
| <b>UpdatedAt</b> | DateTime | Time the file was last updated.
| <b>Username</b> | String | User that uploaded the file (<i>that's you</i>).
| <b>Usernames</b> | Array[String] | Usernames that have access to the file (<i>for private networks</i>).

## GET authorized networks

```go
Golang code here.
```

```python
Python code here.
```

```javascript
handleAuthorizedNetworks = () => {

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

    xhr_stat.open("GET", "https://dev.api.temporal.cloud/v2/ipfs/private/networks");
    xhr_stat.setRequestHeader("Cache-Control", "no-cache");
    xhr_stat.setRequestHeader("Authorization", "Bearer " + <JWT>);
    xhr_stat.send();
};
```

> Example Response (200)

```
{
  "code": 200,
  "response": [
    "private_net_1",
    "myprivatenetwork",
    "thisisnotarealtestnetwork",
    "thisisnotarealtestnetwork-222",
    "private_net_12222"
  ]
}
```

`https://dev.api.temporal.cloud/v2/ipfs/private/networks`

View your authorized networks. The response is an array of strings, each representing a private network name.

## GET information

```go
Golang code here.
```

```python
Python code here.
```

```javascript
handleNetwork = (networkName) => () => {

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

    xhr_stat.open("GET", "https://dev.api.temporal.cloud/v2/ipfs/private/network/" + networkName);
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
    "database": {
      "ID": 55,
      "CreatedAt": "2018-12-20T20:16:31.897258Z",
      "UpdatedAt": "2018-12-20T20:16:43.837002Z",
      "Name": "private_net_12222",
      "APIURL": "192.168.1.243:5299",
      "SwarmKey": "/key/swarm/psk/1.0.0/\n/base16/\nb4afbfa3b9e7903c1a8265dd6336c02339a53597fb19278873dda83d066c5b39",
      "Users": [
        "postables"
      ],
      "LocalNodePeerAddresses": null,
      "LocalNodePeerIDs": null,
      "BootstrapPeerAddresses": null,
      "BootstrapPeerIDs": null,
      "Activated": "2018-12-20T20:16:43.836162Z"
    }
  }
}
```

`https://dev.api.temporal.cloud/v2/ipfs/private/network/:name`

Retrieve network statistics from a single private network.

### Response (200)

| Field | Type | Description
|-----------|------|-------------
| <b>ID</b> | Int | The unique ID of your upload.
| <b>CreatedAt</b> | DateTime | Time the network was created.
| <b>DeletedAt</b> | DateTime | Time the network was deleted.
| <b>Name</b> | String | Name of the private network.
| <b>APIURL</b> | String | The ...
| <b>SwarmKey</b> | String | The private network your file was published on.
| <b>Users</b> | Array[String] | Usernames that have access to the file (<i>for private networks</i>).
| <b>LocalNodePeerAddresses</b> | Array[String] | The ...
| <b>LocalNodePeerIDs</b> | Array[String] | The ...
| <b>BootstrapPeerAddresses</b> | Array[String] | The ...
| <b>BootstrapPeerIDs</b> | Array[String] | The ...
| <b>Activated</b> | DateTime | Time the network was last activated.