# Uploads

## GET uploads

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

xhr.open("GET", "https://dev.api.temporal.cloud/v2/database/uploads");
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
        "CreatedAt": "2018-09-03T21:23:40.886121Z",
        "DeletedAt": null,
        "Encrypted": false,
        "GarbageCollectDate": "2018-10-03T21:23:40.885741Z",
        "Hash": "QmVzyrQByv4KQ9qknwo5v3wKR8wCjMwwfX282NxhYZdi2f",
        "HoldTimeInMonths": 1,
        "ID": 30,
        "NetworkName": "public",
        "Type": "file",
        "UpdatedAt": "2018-09-03T23:47:04.771439Z",
        "UserName": "pseudonaut_two",
        "UserNames": ["pseudonaut_two"]
    },
    {
        "CreatedAt": "2018-09-03T02:21:33.065631Z",
        "DeletedAt": null,
        "Encrypted": false,
        "GarbageCollectDate": "2018-10-03T02:21:33.065291Z",
        "Hash": "QmeuMb3ToBWtCp5xduNxcuozxawha3eikhCHNgLYJEvBMG",
        "HoldTimeInMonths": 1,
        "ID": 24,
        "NetworkName": "public",
        "Type": "file",
        "UpdatedAt": "2018-09-03T03:16:16.592957Z",
        "UserName": "pseudonaut_two",
        "UserNames": ["pseudonaut_two"]
    }
  ]
}
```

`https://dev.api.temporal.cloud/v2/database/uploads`

Returns a list of all uploads to the Temporal database. The response is an array which conforms to the following data structure:

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
| <b>NetworkName</b> | String | The network your file was published on ("public" = Public Network).
| <b>Type</b> | String | The type of file you uploaded.
| <b>UpdatedAt</b> | DateTime | Time the file was last updated.
| <b>Username</b> | String | User that uploaded the file (<i>that's you</i>).
| <b>Usernames</b> | Array[String] | Usernames that have access to the file (<i>for private networks</i>).

## GET encrypted uploads

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

xhr.open("GET", "https://dev.api.temporal.cloud/v2/database/uploads/encrypted");
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
        "CreatedAt": "2018-09-03T21:23:40.886121Z",
        "DeletedAt": null,
        "Encrypted": true,
        "GarbageCollectDate": "2018-10-03T21:23:40.885741Z",
        "Hash": "QmVzyrQByv4KQ9qknwo5v3wKR8wCjMwwfX282NxhYZdi2f",
        "HoldTimeInMonths": 1,
        "ID": 30,
        "NetworkName": "public",
        "Type": "file",
        "UpdatedAt": "2018-09-03T23:47:04.771439Z",
        "UserName": "pseudonaut_two",
        "UserNames": ["pseudonaut_two"]
    },
    {
        "CreatedAt": "2018-09-03T02:21:33.065631Z",
        "DeletedAt": null,
        "Encrypted": true,
        "GarbageCollectDate": "2018-10-03T02:21:33.065291Z",
        "Hash": "QmeuMb3ToBWtCp5xduNxcuozxawha3eikhCHNgLYJEvBMG",
        "HoldTimeInMonths": 1,
        "ID": 24,
        "NetworkName": "public",
        "Type": "file",
        "UpdatedAt": "2018-09-03T03:16:16.592957Z",
        "UserName": "pseudonaut_two",
        "UserNames": ["pseudonaut_two"]
    }
  ]
}
```

`https://dev.api.temporal.cloud/v2/database/uploads/encrypted`

Returns a list of all encrypted uploads to the Temporal database.

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
| <b>NetworkName</b> | String | The network your file was published on ("public" = Public Network).
| <b>Type</b> | String | The type of file you uploaded.
| <b>UpdatedAt</b> | DateTime | Time the file was last updated.
| <b>Username</b> | String | User that uploaded the file (<i>that's you</i>).
| <b>Usernames</b> | Array[String] | Usernames that have access to the file (<i>for private networks</i>).