Usage
=====

.. _installation:

Installation
------------

To use Airtime2Pesa API, first get your business registered by contacting njoshsn@gmail.com :


Purchasing Airtime
----------------

To purchase airtime with our apis,
you need to first get an access token by hitting the ``/token`` endpoint:

The content-type should be ``application/x-www-form-urlencoded`` with a payload of:

```
{
    "grant_type": "client_credentials",
    "client_id": "your-client-id",
    "client_secret": "your-client-secret"
}
```
If successful the api responds with the following result:

```
{
   "access_token":"03807cb390319329bdf6c777d4dfae9c0d3b3c35",
   "expires_in":3600,
   "token_type":"bearer",
   "scope":null
}
```

If an error occurs, the api responds with a ``400`` status code with the following payload:

```
{
    "error": "invalid_client",
    "error_description": "The client credentials are invalid"
}
```


With an access token, you can now purchase using the ``/purchase`` endpoint:

The content-type should be ``application/x-www-form-urlencoded``, with the following payload:

```
{
    "access_token": "your-access-token",
    "data": [
       {
          "phone":"07xxxxxxxx",
          "airtime_amount":100
       }
    ]
}
```

The ``phone`` should start with ``07``

A ``200`` status code will be returned for a successful API response will a response data as follows:

```
{
    "message": "Transaction Iniiated Successfully"
}
```

Any API error will respond with a ``500`` status code with a message of the error:

```
{
    "message": "Insufficient Float Balance"
}
```

Checking Float Balance
----------------

To check your business float balance, hit the ``check-balance`` endpoint with the following payload:

```
{
    "access_token": "your-access-token"
}
```

The API responds with the following sample data:

```
{
    "balance": 500
}
```

Topping Up Float Balance
----------------

The ``/topup`` API endpoint initiates an STKPUSH request to the provided phone number which if successful updates your balance. The API expects the folllowing payload:

```
{
    "access_token": "your-access-token",
    "phone": "070000000",
    "amount": 100
}
```

If the request is successful, the API responds with a ``200`` status code with the following data:

```
{
    "message":"Transaction Iniiated Successfully"
}
```

In the event the API fails a  ``500`` status code is returned with the following data:

```
{
    "message":"Transaction Failed"
}
```
