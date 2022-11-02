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

The content-type should be either ``application/json`` or ``application/x-www-form-urlencoded``,


For example:

{
    "grant_type": "client_credentials",
    "client_id": "your-client-id",
    "client_secret": "your-client-secret"
}


If successful the api responds with the following result:

{
   "access_token":"03807cb390319329bdf6c777d4dfae9c0d3b3c35",
   "expires_in":3600,
   "token_type":"bearer",
   "scope":null
}


With an access token, you can now purchase using the ``/purchase`` endpoint:

The content-type should be ``application/x-www-form-urlencoded``, with the following payload:

{
    "access_token": "your-access-token",
    "data": [
       {
          "phone":"070000000",
          "airtime_amount":100
       }
    ]
}
