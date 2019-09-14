# Errors

<aside class="notice">
	Standard API error codes
</aside>

The BatchPack API uses the following error codes:

> Gateway Responses:

```json
// message queued for sending 
{
	"gatewayResponse": "message queued"
}

// insufficinet funds to send message
{
	"gatewayResponse": "Insufficient funds"
}

// Resouces not available or have been used
{
	"gatewayResponse": "unavailable"
}

// Invalid resource or have none
{
	"gatewayResponse": "create ID"
}

// downtime from sms servcer
{
	"gatewayResponse": "Unprocessable entity"
}

// phone number not valid
{
	"gatewayResponse": "invalid number"
}

// Using a resource that has already been used
{
	"gatewayResponse": "No user rights"
}
```

Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid.
401 | Unauthorized -- Your API key is wrong.
403 | Forbidden -- The request requested is not available.
404 | Not Found -- The specified request could not be found.
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.