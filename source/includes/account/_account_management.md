# Account Management

## POST login

```go
Golang code here.
```

```python
Python code here.
```

```javascript
handleLogin = (username, password) => () => {

        fetch('https://dev.api.temporal.cloud/v2/auth/login', {
            method: 'POST',
            headers: {
                'Content-Type': 'text/plain'
            },
            body: JSON.stringify({
                "username": username.toString(),
                "password": password.toString()
            })
        }).then(res => res.json()).catch(error => {
            console.error(error);
            if (error) {
                throw error;
            }
        })
            .then(response => {
                if (response.expire) {
                    console.log(response.token.toString());
                }
                // Error handling here.
            })
            .catch(error => console.error('#' + error));

    };
```

> Example Response (200)

```
{
  "expire": "2018-12-21T19:31:42Z",
  "token": "eyJhbG ... "
}
```

`https://dev.api.temporal.cloud/v2/auth/login`

Validates the provided username and password to generate a JSON Web Token (JWT) used for authentication.
This token is valid for exactly 24 hours, at which point you will need to generate a new token.

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>username</b> | String | The username.
| <b>password</b> | String | The associated password.

### Response (200)

| Field | Type | Description
|-----------|------|-------------
| <b>expire</b> | DateTime | Time at which the token expires (24 hours).
| <b>token</b> | String | Value of the JWT.

## POST register

```go
Golang code here.
```

```python
Python code here.
```

```javascript
handleRegister = (username, password, email) => () => {

        var data = new FormData();
        data.append("username", username);
        data.append("password", password);
        data.append("email_address", email);

        var xhr = new XMLHttpRequest();
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

        xhr.open("POST", "https://dev.api.temporal.cloud/v2/auth/register");
        xhr.setRequestHeader("Cache-Control", "no-cache");
        xhr.send(data);

    };
```

> Example Response (200)

```
{
  "code": 200,
  "response": {
    "ID": 225,
    "CreatedAt": "2018-12-20T19:33:52.003315586Z",
    "UpdatedAt": "2018-12-20T19:33:52.003315586Z",
    "DeletedAt": null,
    "UserName": "postables+test2019",
    "EmailAddress": "postables+test2019@rtradetechnologies.com",
    "EnterpriseEnabled": false,
    "AccountEnabled": true,
    "APIAccess": true,
    "EmailEnabled": false,
    "EmailVerificationToken": "",
    "AdminAccess": false,
    "HashedPassword": "scrubbed",
    "Credits": 99999999,
    "IPFSKeyNames": null,
    "IPFSKeyIDs": null,
    "IPFSNetworkNames": null
  }
}
```

`https://dev.api.temporal.cloud/v2/auth/register`

Registers your information for the `POST login` call, which is used to generate authenticated JSON Web Tokens (JWT).

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>username</b> | String | Your desired username.
| <b>password</b> | String | Your desired password.
| <b>email_address</b> | String | An associated e-mail address.

### Response (200)

| Field | Type | Description
|-----------|------|-------------
| <b>ID</b> | Int | The unique ID of your registration.
| <b>CreatedAt</b> | DateTime | Time the account was created.
| <b>UpdatedAt</b> | DateTime | Time the account was last updated.
| <b>DeletedAt</b> | DateTime | Time the account was deleted.
| <b>Username</b> | String | Your username.
| <b>EmailAddress</b> | String | Your e-mail address.
| <b>EnterpriseEnabled</b> | Bool | Your account's enterprise status.
| <b>AccountEnabled</b> | Bool | Your account status.
| <b>APIAccess</b> | Bool | Your API access.
| <b>EmailEnabled</b> | Bool | Your e-mail notification status.
| <b>EmailVerificationToken</b> | String | Sent via e-mail to confirm association.
| <b>AdminAccess</b> | Bool | Your admin status.
| <b>HashedPassword</b> | String | The handling of your password.
| <b>Credits</b> | Int | Your starting credits.
| <b>IPFSKeyNames</b> | Array[String] | IPFS key names associated with your account.
| <b>IPFSKeyIDs</b> | Array[String] | IPFS key values associated with your account.
| <b>IPFSNetworkNames</b> | Array[String] | Private IPFS networks associated with your account.

## POST password change

```go
Golang code here.
```

```python
Python code here.
```

```javascript
handleChangePassword = (oldPassword, newPassword) => () => {

    let data = new FormData();
    data.append("old_password", oldPassword);
    data.append("new_password", newPassword);

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

    xhr.open("POST", "https://dev.api.temporal.cloud/v2/account/password/change");
    xhr.setRequestHeader("Cache-Control", "no-cache");
    xhr.setRequestHeader("Authorization", "Bearer " + <JWT>);
    xhr.send(data);

};
```

> Example Response (200)

```
{
  "code": 200,
  "response": "password changed"
}
```

`https://dev.api.temporal.cloud/v2/account/password/change`

Change the password associated with your account.

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>old_password</b> | String | Your old password.
| <b>new_password</b> | String | Your desired, new password.

## GET credits

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

xhr.open("GET", "https://dev.api.temporal.cloud/v2/account/credits/available");
xhr.setRequestHeader("Cache-Control", "no-cache");
xhr.setRequestHeader("Authorization", "Bearer " + <JWT>);
xhr.send();
```

> Example Response (200)

```
{
  "code": 200,
  "response": 10000464.996296696
}
```

`https://dev.api.temporal.cloud/v2/account/credits/available`

View the amount of credits your account has.

The response is of type <b>double</b>.

## Upgrade Account

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

```
{
    // add example response
}
```

`https://dev.api.temporal.cloud/v2/account/upgrade`

Used to upgrade your account from free tier to the first non-free tier known as `Light`. When upgrading from a free account you are not eligible to downgrade your account. When upgrading your account, we allocate free $0.115USD worth of your credits, enough to pay for 0.5GB of storage for 1 month.