# Public IPFS and Private IPFS Utility

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
    data.append("network_name");

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

    xhr.open("POST", "https://api.temporal.cloud/v2/ipfs/utils/download/" + ipfsHash);
    xhr.setRequestHeader("Cache-Control", "no-cache");
    xhr.setRequestHeader("Authorization", "Bearer " + <JWT>);
    // Use xhr.send() if not supplying a private networkName.
    xhr.send(data); 
};
```

`https://api.temporal.cloud/v2/ipfs/utils/download/:hash`

Downloads content from the public IPFS network through temporal. Can also be used to download from a private network that the user has access to.

<aside class="warning">
When downloading a file from a private network, please ensure the network is running.
</aside>

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>network_name</b> | String | The private network to download a file from (optional)
| <b>decrypt_key</b> | String | the passphrase used to decrypt an encrypted file before Temporal sends it to you (optional)

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

    xhr.open("POST", "https://api.temporal.cloud/v2/ipfs/utils/laser/beam");
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

`https://api.temporal.cloud/v2/ipfs/utils/laser/beam`

Transfer content between two different IPFS networks.

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>source_network</b> | String | The network to copy content from.
| <b>destination_network</b> | String | The network to copy content to.
| <b>content_hash</b> | IPFS Hash | The content to hash.
| <b>passphrase</b>* | String | Passphrase to encrypt the content with.

<aside class="warning">
*Optional parameter. If you supply a passphrase, the content will be encrypted during transfer before uploading to the destination network
</aside>
