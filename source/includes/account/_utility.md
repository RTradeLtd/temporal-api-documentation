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

This allows a user to refresh their JWT before the expiration data of 24 hours, preventing them having to generate a new JWT.

## GET usage data

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

```json
{
    "code": 200,
    "response": {
        "ID": 57,
        "CreatedAt": "0001-01-01T00:00:00Z",
        "UpdatedAt": "2019-02-03T02:33:50.796677Z",
        "DeletedAt": null,
        "UserName": "postables",
        "MonthlyDataLimitBytes": 3221225472,
        "CurrentDataUsedBytes": 5169444,
        "IPNSRecordsPublished": 1,
        "IPNSRecordsAllowed": 5,
        "PubSubMessagesSent": 1,
        "PubSubMessagesAllowed": 1000,
        "KeysCreated": 4,
        "KeysAllowed": 5,
        "Tier": "free"
    }
}
```

`https://dev.api.temporal.cloud/v2/account/usage`

This allows returning the users current data usage information