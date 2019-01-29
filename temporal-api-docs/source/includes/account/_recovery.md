# Recovery

## POST forgot username

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
  // Need an example response.
}
```

`https://dev.api.temporal.cloud/v2/forgot/username`

Sends a reminder to the associated e-mail address with the given username. Your account must have an activated e-mail address for this call to execute.

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>email_address</b> | String | The e-mail address associated with your account.

## POST forgot password

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
  // Need an example response.
}
```

`https://dev.api.temporal.cloud/v2/forgot/password`

Resets the password for the account with the associated email, sending it via email.

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>email_address</b> | String | The e-mail address associated with your account.

## POST forgot email

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
  // Need example response.
}
```

`https://dev.api.temporal.cloud/v2/forgot/email`

Returns the e-mail address associated with the JWT supplied.
