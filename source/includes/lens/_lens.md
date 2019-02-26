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
    data.append("query",  query);

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
        "results": [
            {
                "score": 0.018188993,
                "doc": {
                    "hash": "QmNo18enTNX6hZYtYvB8dEMfKT7YjeSEWgTuAmYBMG8bYG",
                    "mime_type": "application/pdf",
                    "category": "pdf"
                }
            }
        ]
    }
```

`https://dev.api.temporal.cloud/v2/lens/search`

Search for a particular file through Lens by providing a required query string. Example of queries are `blockchain` `data storage`.
There are optional additional search clauses which can effect the results returned.

### Parameters

| Field | Type | Description | Required Parameter  
|-----------|------|----------|------------------------
| <b>query</b> | String | The search clause | Yes
| <b>tags</b> | String Array | *to do* | No  
| <b>categories</b> | String Array | The category to search through (eg, pdf) | No  
| <b>mime_types</b> | String Array | The mime type to search for (eg, pdf) | No  
| <b>hashes</b> | String Array | The ipfs hash of the indexed data that must match this query | No  
| <b>required</b> | String Array | *to do* | No  

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
    // data.append("reindex", reindex); disabled until further notice
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
    "response": {
        "hash": "QmNo18enTNX6hZYtYvB8dEMfKT7YjeSEWgTuAmYBMG8bYG",
        "mime_type": "application/pdf",
        "category": "pdf"
    }
}
```

`https://api.temporal.cloud/v2/lens/index`

Submit a file for indexing to the Lens database.

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>hash</b> | IPFS Hash | The public hash to submit for indexing.
| <b>type</b> | String | The object type, only `ipld` is supported.

### Response (200)

| Field | Type | Description
|-----------|------|-------------
| <b>name</b> | IPFS Hash | The hash submitted.
| <b>mimeType</b> | String | The file type submitted.
| <b>category</b> | String | The category of the file type submitted.