# Purchase Credits

## POST request signed payment message

```go
Golang code here.
```

```python
Python code here.
```

```javascript
handlePurchase = (type, credits, address) => () => {

    let data = new FormData();
    data.append("payment_type", type);
    data.append("credit_value", creditValue);
    data.append("sender_address", address);

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

    xhr.open("POST", "https://dev.api.temporal.cloud/v2/payments/eth/request");
    xhr.setRequestHeader("Cache-Control", "no-cache");
    xhr.setRequestHeader("Authorization", "Bearer " + <JWT>);
    xhr.send(data);
}
```

> Example Response (200)

```
{
  "code": 200,
  "response": {
    "charge_amount_big": 44529147669208980,
    "formatted": {
      "h": "0xad8ed50340f920c837313062a9950f3847dceec23a86034d7909daae5d847a6a",
      "r": "0x6aea0b08e837b38a5d33c0baafc10f7eb50198fed55c864648ab96ada40608f9",
      "s": "0x3e2cd4b934a72c2bc66068f1277b1dafb3162f0bbd22e8f51f6696480217d108"
    },
    "h": [
      173,
      106
    ],
    "method": 1,
    "payment_number": 6,
    "prefixed": true,
    "r": [
      106,
      "...",
      249
    ],
    "s": [
      62,
      "...",
      8
    ],
    "v": 28
  }
}
```

`https://dev.api.temporal.cloud/v2/payments/eth/request`

Request a signed message that can subsequently be used to purchase credits with RTC or ETH, validated through a smart contract.

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>type</b> | Int | The digital asset you intend to pay with: Ethereum = `1` and RTC  = `0`.
| <b>sender_address</b> | String | Ethereum address you will use for payment (`0x7E4A2359c745A982a54653128085eAC69E446DE1`).
| <b>credit_value</b> | Int | The number of credits you want to purchase.

### Response (200)

| Field | Type | Description
|-----------|------|-------------
| <b>charge_amount_big</b> | Int | The unique ID of your registration.
| <b>formatted</b> | Array[txSig:txVal] | Formatted version of the tx signature.
| <b>h</b> | DateTime | Portion of tx signature.
| <b>method</b> | Int | The digital asset you will pay with (Ethereum = `1`, RTC  = `0`).
| <b>payment_number</b> | Int | A unique number for your payment.
| <b>prefixed</b> | Bool | Tx signature prefixed status.
| <b>r</b> | Array[Int] | Portion of tx signature.
| <b>s</b> | Array[Int] | Portion of tx signature.
| <b>v</b> | Int | Portion of tx signature.

## POST confirm payment

```go
Golang code here.
```

```python
Python code here.
```

```javascript
submitPayment = (paymentNumber, txHash) => {

    let data = new FormData();
    data.append("payment_number", paymentNumber);
    data.append("tx_hash", txHash);

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

    xhr.open("POST", "https://dev.api.temporal.cloud/v2/payments/eth/confirm");
    xhr.setRequestHeader("Cache-Control", "no-cache");
    xhr.setRequestHeader("Authorization", "Bearer " + <JWT>);
    xhr.send(data);

};
```

> Example Response (200)

```
{
  // Need example response.
}
```

`https://dev.api.temporal.cloud/v2/payments/eth/confirm`

Confirm your eth or rtc payment after sending a transaction on the blockchain.

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>payment_number</b> | String | The unique number associated with your payment.
| <b>tx_hash</b> | String | The transaction hash associated with the transaction you sent through Ethereum.

## POST create dash payment

```go
Golang code here.
```

```python
Python code here.
```

```javascript
handleDashPayment = (credits) => () => {

    let data = new FormData();
    data.append("credit_value", sourceNetwork);

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

    xhr.open("POST", "https://dev.api.temporal.cloud/v2/payments/dash/create");
    xhr.setRequestHeader("Cache-Control", "no-cache");
    xhr.setRequestHeader("Authorization", "Bearer " + <JWT>);
    xhr.send(data);
};
```

> Example Response (200)

```
{
  // Need example response.
}
```

`https://dev.api.temporal.cloud/v2/payments/dash/create`

Create a payment request to purchase credits with DASH.

<aside class="success">
<b>Note:</b> We utilize <b><a href="https://chainrider.io" target="_blank">ChainRider</a></b> for all DASH payments.
</aside>

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>credit_value</b> | String | The amount of credits you want to purchase.

## GET deposit address

```go
Golang code here.
```

```python
Python code here.
```

```javascript
handleDepositAddress = (type) => () => {

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

    xhr_stat.open("GET", "https://dev.api.temporal.cloud/v2/payments/deposit/address/" + type);
    xhr_stat.setRequestHeader("Cache-Control", "no-cache");
    xhr_stat.setRequestHeader("Authorization", "Bearer " + <JWT>);
    xhr_stat.send();
};
```

> Example Response (200)

```
{
  "code": 200,
  "response": "0xc7459562777DDf3A1A7afefBE515E8479Bd3FDBD"
}
```

`https://dev.api.temporal.cloud/v2/payments/deposit/address/:type`

Returns the deposit address for RTC or ETH payments.

### Parameters

| Field | Type | Description
|-----------|------|-------------
| <b>type</b> | String | The digital asset you are sending, either `RTC` or `ETH`.





