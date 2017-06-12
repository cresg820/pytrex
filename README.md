# pytrex
Light python http client for https://bittrex.com/

# Donations
If you enjoy this project please donate:
- ETH 0xd5FD013332b59294359F7cf0cc759A5342d98EA1
- BTC 3QZk4uoEQWjXHmQa9X5fG99NcWoN2bVNuK

# Description
This is a light http client to access bittrex api.
Please read first the bittrex api documentation https://bittrex.com/home/api for usage and limits.

# Usage
Client is provieded as a python object, usage is very simple:

## You have to import client and create a new instance
```python
from pytrex import Client

# change xxxxx with your api key
# change yyyyy with your api secret
client = Client(key="xxxxx", secret="yyyy")

# if you want to make only public queries you can omit key and secret values
client = Client()
```

## Make requests
```python
# you can make 2 type of queries: private or public
# private queries will be signed using `secret` passed during client creation

# get ticket for a specific market
result = client.public_query(command='/public/getticker', params={'market': market.pair})

# make a limit buy order
result = client.private_query(command='/market/buylimit', params={'market': 'BTC-ETH', 'rate' : 0.11, 'quantity': 1})
```

## Result and errors
Client will return a json object if:
* no connection errors occured
* request response code is 200
* response `success` key is True

If one of the condition above aren't meeted the client will raise a:
* connection error(see http://docs.python-requests.org/en/master/_modules/requests/exceptions/) for connection problems
* A BittrexError if response code is not 200
* A BIttrexError if response `success` key is not True with response['message'] as desciption
