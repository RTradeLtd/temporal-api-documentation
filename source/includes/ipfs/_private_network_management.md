# Private Network - Management

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

    xhr.open("POST", "https://api.temporal.cloud/v2/ipfs/private/network/new");
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

`https://api.temporal.cloud/v2/ipfs/private/network/new`

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

    xhr.open("POST", "https://api.temporal.cloud/v2/ipfs/private/network/start");
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

`https://api.temporal.cloud/v2/ipfs/private/network/start`

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

    xhr.open("POST", "https://api.temporal.cloud/v2/ipfs/private/network/stop");
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

`https://api.temporal.cloud/v2/ipfs/private/network/stop`

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

`https://api.temporal.cloud/v2/ipfs/private/network/remove`

Delete a private network.

<aside class="warning">
Network deletion will not work if your private network is running. Ensure you have stopped it.
</aside>

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>username</b> | String | The username.
| <b>password</b> | String | The associated password.

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

    xhr_stat.open("GET", "https://api.temporal.cloud/v2/ipfs/private/networks");
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

`https://api.temporal.cloud/v2/ipfs/private/networks`

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

    xhr_stat.open("GET", "https://api.temporal.cloud/v2/ipfs/private/network/" + networkName);
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

`https://api.temporal.cloud/v2/ipfs/private/network/:name`

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