---
title: Flowroute API Reference

language_tabs:
  - shell

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Flowroute API reference documentation. Here you will find specifications for our V1 Number Management Endpoints and our V2 Messages Endpoints. 

# Authentication

> Example Request:

```shell
# With curl, you can use the -u option to include your credentials
curl -u accessKey:secretKey https://api.flowroute.com/v2/messages/mdr1-2b9c5b0551724ad9a3fdeeb30bab3926
```

> Make sure to replace `accessKey:secretKey` with your credentials from the [Flowroute Manager](https://manage.flowroute.com/accounts/preferences/api/).

The V2 Flowroute API utilizes Basic Auth via HTTPS to authenticate API requests. Any requests sent via HTTP will fail. 

<aside class="notice">
You must replace <code>accessKey:secretKey</code> with your personal API credentials from the <a href="https://manage.flowroute.com/accounts/preferences/api/">Flowroute Manager</a>.
</aside>

# Messages

## Send a Message

```shell
curl -u AccessKey:SecretKey \
	-H "Content-Type: application/json" \
	-X POST \
	-d '{"to":"12066418000", "from":"18553569768", "body":"example body"}' \
	https://api.flowroute.com/v2/messages
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "mdr1-e3672cb28a9d422a9671945c9bc4eb9a"
  }
}
```

This API endpoint is used to send a message from one valid phone number to another valid phone number.
All `to` and `from` phone numbers must use an E.164 format, which is an 11-digit _`1NPANXXXXXX`_-formatted number in North America. While you can send an SMS to any valid North American Numbering Plan Administration (NANPA) phone number, Flowroute cannot guarantee delivery to any phone number not enabled for SMS. Additionally, you are only allowed to send an SMS from an SMS-enabled phone number set up on the Direct Inward Dialing <a href="https://manage.flowroute.com/accounts/dids/" target="blank"> (DIDS > Manage) </a> page. You cannot send an SMS from a phone number not on your Flowroute account.

### Body Parameters

| Field | Description                                                                                                                                                                                                                                                                                                                      | Required |
|-------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| to    | **String**: Phone number of the message recipient, using an E.164 format, This must be in an E.164 format, which is a North American, 11-digit 1NPANXXXXXX-formatted number.                                                                                                                                                         | True     |
| from  | **String**: Flowroute phone number to send the message from, using an E.164 format. On the receiver's phone, this is typically referred to as the Caller ID.                                                                                                                                                                         | True     |
| body  | **String**: The content of the message to deliver. If a message is greater than 160 characters, and the carrier sends header information with the message, the message with be reassembled on the receiver's phone as one message. If header information is not sent by the carrier, the message will be received in multiple parts. | True     |

