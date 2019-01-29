# Lens

## POST search request

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

## POST index request

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