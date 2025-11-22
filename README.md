The Simplo API
==================

Welcome to the Simplo API! If you're looking to integrate your application with Simplo, you're in the right place. We're happy to have you!

Making a request
----------------

All URLs start with **`https://simplo.works/api/v1/999999999/`**. URLs are HTTPS only.

Throughout the Simplo API docs, we include "Copy as cURL" examples. Then you should be able to copy/paste any example from the docs.

Authentication
--------------

To authenticate you must use an API Key. The API key must be sent in the `Authorization` header.

Example: `Authorization: ApiKey my-secure-key`

You can get your API Key from your Simplo account.

JSON only
---------

We use JSON for all API data. The style is no root element and snake\_case for object keys. This means that you have to send the `Content-Type` header `Content-Type: application/json; charset=utf-8` when you're POSTing or PUTing data into Simplo.

Handling errors
---------------

API clients must expect and gracefully handle transient server errors and rate limits. We recommend baking graceful 5xx and 429 retries into your integration from the beginning so errors are handled automatically.

### [5xx server errors](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes#5xx_Server_errors)

If Simplo is having trouble, you will get a response with a 5xx status code indicating a server error. 500 (Internal Server Error), 502 (Bad Gateway), 503 (Service Unavailable), and 504 (Gateway Timeout) may be retried with [exponential backoff](https://en.wikipedia.org/wiki/Exponential_backoff).

### 404 Not Found

API requests may 404 due to deleted content, an inactive account, missing user permissions, etc. Detect these conditions to give your users a clear explanation about why they can't connect to Simplo. Do not automatically retry these requests.

* Inactive account. 404 Not Found response due to an expired trial or account suspension. All API requests to an inactive account will fail, so we recommend detecting and disabling the account in your integration as well.
* Inaccessible items. 404 Not Found response. Due to a deleted item or insufficient permissions.

```json
{
  "type": "about:blank",
  "status": 404,
  "title": "Not Found"
}
```

### 422 Unprocessable Entity
If a validation fails (e.g., a required field is missing or the email is already taken), the API will return a `422 Unprocessable Entity` status with details about the validation errors.

``` json
{
  "type": "https://problems-registry.smartbear.com/validation-error/",
  "status": 422,
  "title": "Validation Error",
  "detail": "The request payload contains validation errors",
  "errors": [
    {
      "detail": "Email has already been taken",
      "pointer": "/customer/email"
    },
    {
      "detail": "Name can't be blank",
      "pointer": "/customer/name"
    }
  ]
}
```

API endpoints
-------------
<!-- START API ENDPOINTS -->
- [Customers](https://github.com/whysimplicity/simplo-api/blob/master/sections/customers.md#customers)
<!-- END API ENDPOINTS -->

Getting Help
------------

If you have a question about the API, please [open a issue](https://github.com/whysimplicity/simplo-api/issues).


License
-------

These API docs are licensed under [Creative Commons (CC BY-SA 4.0)](http://creativecommons.org/licenses/by-sa/4.0/). Please share, remix, and distribute as you see fit.
