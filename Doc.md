---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
- shell
- ruby
- javascript
- python

toc_footers:
- <a href='https://app.batchpack.co'>Sign Up for a BatchPack Key</a>
- <a href='https://batchpack.co/contact'>Build a Library for BatchPack</a>

includes:
- Errors

search: true
---

# Introduction

Welcome to the BatchPack API Documentation. Get familiar with our powerful communication APIs and technical resources to help you build your communication solution.

Pick the docs that are right for you. These guides, sample app tutorials, and API reference docs will get you across the deploy line, straight to HTTP 200 OK.

You’ve got an idea in mind. Let’s get it to production.


```ruby
# To use the BatchPack's api seamlessly in ruby, you must use an http service. Httparty, faraday, etc
Add gem 'httparty' to your Gemfile
or
# gem install httparty
```
```python
# To use the BatchPack's api seamlessly in python
 pip install requests
# and import the following
import requests
import json
```

# Authentication

> To authorize, use this code:

```ruby
require "httparty"

    initBatchpPack = HTTParty.post("https://api.batchpack.co/v1/example_endpoint/#{ENV["BTOKEN"]}",
      :headers => { "apikey"=> ENV["API_KEY"], "content-type" => "application/json"})
    puts initBatchpPack
```

```shell
# With shell, you can just pass the correct header with each request
curl "https://api.batchpack.co/v1/example_endpoint/BTOKEN"
-H "apikey: API_KEY"
```

```python
def sendMessage():
    api_endpoint = "https://api.batchpack.co/v1/company/example_endpoint/#BTOKEN"
    data = {'fromPhoneNumber': SENDER_ID,
            'toPhoneNumber': "+145678088", 'message': "The Message Body"}
    
    headers = {'Content-Type': 'application/json',
               'apikey': API_KEY}
sendMessage()

```


Before we get started, sign up to BatchPack for free and collect your live API_KEY from the [Dashboard](http://app.batchpack.co).

Next, enter your BTOKEN key at the end of your the url 

`API_KEY` &
`BTOKEN`

For security reasons, you will need to put this credentials in an .env file and utilize them as an environmental variable `ENV['KEY_NAME']`
<aside class="notice">
  You must replace <code>API_KEY</code> and <code>BTOKEN</code> with your personal Credentials from your profile page
</aside>
> Send Message:

# Programmatic SMS

## Send an SMS

```javascript

// SEND SMS
const sendSms = () => {
const requestBody = {
    fromPhoneNumber: "BATCHPACK",
    toPhoneNumber: "+23481********",
    message: "This is the second JS test text"
  };
  axios
    .post(
      `https://api.batchpack.co/v1/company/send_message/${ENV['BTOKEN']}`,
      requestBody,
      {
        headers: {
          apikey: ENV['API_KEY'],
          Accept: "application/json",
          "Content-Type": "application/json"
        }
      }
    )
    .then(response => {
      // DO WHAT YOU WANT WITH API RESPONSE DATA
      console.log(response);
    })
    .catch(error => {
      // Log response error
      console.log(error);
    });
};

sendSms();
```
```ruby
require "httparty"

    triggerSms = HTTParty.post("https://api.batchpack.co/v1/company/send_message/#{ENV["BTOKEN"]}",
      :body => {"fromPhoneNumber": "BATCHPACK", "toPhoneNumber": +15467876786, "message": "Hi There, Thanks!", "callback": "https://9dcc0399.ngrok.io/v1/post/wehbook"},
      :headers => { "apikey"=> ENV["API_KEY"], "content-type" => "application/json"})
    puts triggerSms
```
```shell
curl "https://api.batchpack.co/v1/company/send_message/BTOKEN" \
-H "apikey: API_KEY" \
-d '{"fromPhoneNumber": "BATCHPACK", "toPhoneNumber": "+15467876786", "message": "Hi There, Thanks!", "callback": "https://9dcc0399.ngrok.io/v1/post/wehbook"}" \
-X POST
```
```python
# Copy your API_KEY, BTOKEN, and SENDER_ID from your dashboard page
def sendMessage():
    api_endpoint = "https://api.batchpack.co/v1/company/send_message/#BTOKEN"
    data = {'fromPhoneNumber': SENDER_ID,
            'toPhoneNumber': "+2348107176019", 'message': "The Message Body"}
    
    headers = {'Content-Type': 'application/json',
               'apikey': API_KEY}
    try:
        response = requests.post(
            api_endpoint, data=json.dumps(data), headers=headers)
        if response.ok:
            print(response.json())
        else:
            print(response.status_code)
    except Exception as e:
        print(e)

sendMessage()
```

> Response:

```json
{
  "data": {
  "id": 20,
  "message_body": "TESTINGL",
  "receiver_number": "+1598151010",
  "sent_at": "28 August 2019",
  "message_refernce": "SMBTP29365527724837165981",
  "status": "sending",
  "unit": "USD",
  "send_id": "BATCHPACK",
  "countryCode": "US"
},
"gatewayResponse": "message queued"
}
```

Using BatchPack's REST API, you can send outgoing SMS messages from your BatchPack senderId to any phone number across the globe. At fisrt registration, you will be assigned a default senderId as BATCHPACK until your senderId application is approved.

### HTTP Request

`POST https://api.batchpack.co/v1/company/send_message/BTOKEN`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
fromPhoneNumber | true | Your BatchPack senderID
toPhoneNumber | true | The recipient number to receive the sms.
message | true | The body of the sms.

<aside class="success">
  Signup — BatchPack give you 15 free SMS on trail
</aside>
> Get all Messages:

## List All SMS

```ruby
require "httparty"

    viewMessage = HTTParty.get("https://api.batchpack.co/v1/company/view_messages/#{ENV["BTOKEN"]}",
      :headers => { "apikey"=> ENV["API_KEY"], "content-type" => "application/json"})
    puts viewMessage
```
```shell
curl "https://api.batchpack.co/v1/company/view_messages/BTOKEN" \
-H "apikey: API_KEY" \
```

> Response:

```json
{
  "data": [
  {
        {
      "id": 122,
      "message_body": "Lorem ipsum dolor sit amet adipiscing elits",
      "receiver_number": "+1598151010",
      "user_id": 17,
      "created_at": "2019-08-28T00:48:02.942Z",
      "updated_at": "2019-08-28T00:48:10.492Z",
      "mesage_refernce": "SMBTP69814227010589869943",
      "status": "delivered",
      "cost": "0.0082",
      "send_id": "BATCHPACK",
      "gatewayKey": "SM3d67f33020d14870aa2f8ab89876d57e",
      "version": "v1",
      "timesent": null,
      "messageSegment": "2",
      "webhook_url": null
    }
  ],
}
}
```

You can use BatchPack's SMS API to retrieve information of an existing outbound SMS message.

You only need to supply the unique client id that was returned upon creation.

### HTTP Request

`GET https://api.batchpack.co/v1/company/view_messages/BTOKEN`
> Available Number:

# Phone Number & SenderID

## Check Available Number

```ruby
require "httparty"

    searchNumber = HTTParty.get("https://api.batchpack.co/v1/company/searchNumber/#{ENV["BTOKEN"]}",
      :headers => { "apikey"=> ENV["API_KEY"], "content-type" => "application/json"})
    puts searchNumber
```
    
```shell
curl "https://api.batchpack.co/v1/company/searchNumber/BTOKEN" \
-H "apikey: API_KEY" \
```

> Response:

```json

"available_phone_numbers": [
{
  "friendly_name": "(510) 726-9549",
  "phone_number": "+15107269549",
  "lata": "722",
  "rate_center": "OKLD MN-PD",
  "latitude": "37.800000",
  "longitude": "-122.260000",
  "locality": "OAKLAND",
  "region": "CA",
  "postal_code": "94615",
  "iso_country": "US",
  "address_requirements": "none",
  "beta": false,
    "capabilities": {
      "voice": true,
      "SMS": true,
      "MMS": true,
      "fax": false
    }
  }
]
```

On BatchPack V1, we currently offer only US numbers. BatchPack phone numbers are immediately purchased when bought, but senderID is not.


### HTTP Request

`POST https://api.batchpack.co/v1/company/searchNumber/BTOKEN`
> Buy Phone Number:

## Phone Number & Sender ID
```ruby
require "httparty"

    buyNumber = HTTParty.post("https://api.batchpack.co/v1/company/buy_sender_id/#{ENV["BTOKEN"]}",
      :body => {"senderId": "COCACOLA", "comments": "My new sms id for promotional messages", "category": "Marketing", "phone": "+15106942131", "rateCenter": "", "region": "LA", "postalCode": "45673"},
      :headers => { "apikey"=> ENV["API_KEY"], "content-type" => "application/json"})
    puts buyNumber
```
```shell
curl "https://api.batchpack.co/v1/company/buy_sender_id/BTOKEN" \
-H "apikey: API_KEY" \
-d '{"senderId": "COCACOLA", "comments": "My new sms id for promotional messages", "category": "Marketing", "phone": "+15106942131", "rateCenter": "", "region": "LA", "postalCode": "45673"}' \
-X POST
```

> Response:

```json
{
  "status": 200,
  "senderId": "MMMMM",
  "phoneNumber": "+15106942131",
  "senderidStatus": "Pending Verification",
  "region": "AL",
  "country": "US",
  "smsUsage": null,
  "amount": "1.5",
  "renewaldate": "2019-10-05",
  "phoneNumberStatus": "Active",
  "numberCenter": "BELLEFONTN",
  "category": "Marketing",
  "commens": "This is my first sender id"
}
```

Alphanumeric sender IDs are used for branded one-way messaging. Alphanumeric sender IDs and a custom phone number cost $1.50. Without a verified senderID you may not be able to send a message using your custom senderID but you can continue sending with you already purchased phone number. If you do not have any of the sender number or Alphanumeric ID, you will only be able to send a message using "BATCHPACK" as senderID


### HTTP Request

`POST https://api.batchpack.co/v1/company/buy_sender_id/BTOKEN`

### URL Parameters

Parameter | Description
--------- | -----------
senderId | The Alphanumeric sender ID
comments | Any thing random

> List Sender ID:

## List Sender ID
```ruby
require "httparty"

    listID = HTTParty.get("https://api.batchpack.co/v1/company/list_sender_id/#{ENV["BTOKEN"]}",
      :headers => { "apikey"=> ENV["API_KEY"], "content-type" => "application/json"})
    puts listID
```
```shell
curl "https://api.batchpack.co/v1/company/list_sender_id/BTOKEN" \
-H "apikey: API_KEY" \
```

> Response:

```json
[
[
  {
    "id": 16,
    "sender_id": "MMMM",
    "comment": "This is my first sender id",
    "senderid_status": "Pending Verification",
    "user_id": 17,
    "created_at": "2019-09-05T08:59:22.691Z",
    "updated_at": "2019-09-05T08:59:22.691Z",
    "category": "Marketing",
    "phone": "+15106620133",
    "rate_center": "BELLEFONTN",
    "region": "AL",
    "postal_code": "456789",
    "country": "US",
    "address_requirements": "none",
    "voice": null,
    "sms": null,
    "mms": null,
    "fax": null,
    "amount": "1.5",
    "lata": "480",
    "renewDate": "2019-10-05 09:59:22 +0100",
    "numberSid": null,
    "phone_status": "Active"
  }
]
```

Use this endpoint to get all available sender ID


### HTTP Request

`POST https://api.batchpack.co/v1/company/list_sender_id/BTOKEN`

This endpoint retruns an array of all the sms sent 
> Check Balance:

# Billing

## Check Balance

```ruby
require "httparty"

    checkBalance = HTTParty.get("https://api.batchpack.co/v1/company/get_balances/#{ENV["BTOKEN"]}",
      :headers => { "apikey"=> ENV["API_KEY"], "content-type" => "application/json"})
    puts checkBalance
```
```shell
curl "https://api.batchpack.co/v1/company/get_balances/BTOKEN" \
-H "apikey: API_KEY" \
```

> Response:

```json
{
  "accountBalance": "300.0",
  "totalDeposit": "300.0",
  "currency": "USD"
}
```

Check available Balance on your BatchPack's account

### HTTP Request

`GET https://api.batchpack.co/v1/company/get_balances/BTOKEN`


<aside class="success">
  BatchPack Help You do anything Message
</aside>





