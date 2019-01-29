# Utility

## GET username from token

```go
Golang code here.
```

```python
Python code here.
```

```javascript
let data = new FormData();
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

xhr.open("GET", "https://dev.api.temporal.cloud/v2/account/token/username");
xhr.setRequestHeader("Cache-Control", "no-cache");
xhr.setRequestHeader("Authorization", "Bearer " + Session.get('token'));
xhr.send(data);
```

> Example Response (200)

```
{
  "code": 200,
  "response": "postables"
}
```

`https://dev.api.temporal.cloud/v2/account/token/username`

Returns the username associated with the current token (for validation purposes).


## GET refreshed auth token

```go
Golang code here.
```

```python
Python code here.
```

```javascript
let data = new FormData();
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

xhr.open("GET", "https://dev.api.temporal.cloud/v2/auth/refresh");
xhr.setRequestHeader("Cache-Control", "no-cache");
xhr.setRequestHeader("Authorization", "Bearer " + Session.get('token'));
xhr.send(data);
```

> Example Response (200)

```
{
  // Need example response.
}
```

`https://dev.api.temporal.cloud/v2/auth/refresh`

// Need description.






