# Lens

## POST search request

```go
Golang code here.
```

```python
Python code here.
```

```javascript
handleSearch = (query) => () => {

    let data = new FormData();
    data.append("keywords",  query);

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

    xhr.open("POST", "https://dev.api.temporal.cloud/v2/lens/search");
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
    "keywords": [
      "return",
      "function",
      "case",
      "break",
      "lcb"
    ],
    "lens_id": "15e3fe2f-603a-4af5-b057-6805961568b5"
  }
}
```

`https://dev.api.temporal.cloud/v2/lens/search`

Search for a particular file through Lens by providing a keyword (or keywords).
The response returns an array of keywords, which is publicly searchable through Temporal Lens.

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>keywords</b> | String | The keyword to search for.

## POST index request

```go
Golang code here.
```

```python
Python code here.
```

```javascript
handleIndexing = (hash, reindex, type) => {

    let data = new FormData();
    data.append("object_identifier", hash;
    data.append("reindex", reindex);
    data.append("object_type", type);

    let xhr = new XMLHttpRequest();
    xhr.withCredentials = false;

    xhr.addEventListener("readystatechange", function () {

        if (xhr.readyState === 4) {

            if (result.code === 200) {
                console.log(result);
            }

            else {
                // Error handling.
            }

        }
    }.bind(this));

    xhr.open("POST", "https://dev.api.temporal.cloud/v2/lens/index");
    xhr.setRequestHeader("Cache-Control", "no-cache");
    xhr.setRequestHeader("Authorization", "Bearer " + <JWT>);
    xhr.send(data);

};
```

> Example Response (200)

```
{
  "code": 200,
  "response": [
    {
      "name": "QmYwwdB1X6aivm8me71EwWXFZjGtjkAmUuT9qEDQBZmdSk",
      "mimeType": "text/plain; charset=utf-8",
      "category": "document"
    }
  ]
}
```

`https://api.temporal.cloud/v2/auth/login`

Submit a file for indexing to the Lens database.

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>hash</b> | IPFS Hash | The public hash to submit for indexing.
| <b>reindex</b> | Bool | Description ...
| <b>type</b> | String | The object type, default `ipld`.

### Response (200)

| Field | Type | Description
|-----------|------|-------------
| <b>name</b> | IPFS Hash | The hash submitted.
| <b>mimeType</b> | String | The file type submitted.
| <b>category</b> | String | The category of the file type submitted.