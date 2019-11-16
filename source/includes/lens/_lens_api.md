# Lens API

The Lens API is used to perform indexing, and searching of files stored on IPFS through Temporal. Lens is *opt-int*, and available without signing up to Temporal.
Anything you index is available to the **public** so do not index anything you don't want easily discoverable. The search engine is facilitated through [bleve](https://github.com/blevesearch/bleve), while indexing is performed using a mix of text based analysis, Tesseract-OCR, and Tensorflow.

To access the development API use the following url:

* https://dev.api.temporal.cloud

Should you wish to access the production API  use the following url:

* https://api.temporal.cloud

## Authentication

Temporal uses JSON Web Tokens for authentication, accessed through the `POST login` call.

Throughout the code examples in this documentation, you will see `<JWT>` which requires a JWT for access.

<aside class="success">
<b>Important:</b>  JWT tokens expire after 24 hours. You will need to call <b><a href="/account.html#post-login">POST login</a></b> to generate another valid JWT after 24 hours, or call <b><a href="/account.html#get-refreshed-auth-token">GET refresh auth token</a></b> in advance.
</aside>


## General Errors

Except for 400 responses unique to an API call, error codes generally conform to the following:

Error Code | Meaning
---------- | -------
<b>400</b> | Error -- Invalid data supplied.
<b>401</b> | Unauthorized -- Invalid authentication token.  Check to make sure you're properly passing the authorization token.
<b>403</b> | Forbidden -- You do not have access to this functionality.
<b>404</b> | Not Found -- Resource not found.
<b>500</b> | Server Error -- We had a problem with our server. Try again later or contact <b>support@rtradetechnologies.com</b>


In some cases, calls will return a `200` code as generally expected, but will not successfully execute the command.
In this case, we will specify the particular conditions this could occur for a given API call.

## Validation (400 Error Code)

```json
{
  "code": "400",
  "response": [
    {
        "message": "Must be one of: RSA, ED25519",
        "field": "key_type"
    }
  ]
}
```

Methods that take input will validate all parameters. Any parameter that fails validation will trigger an error response with status `400`. The response body will be a JSON object that includes a message as well as a list of fields that failed validation.
