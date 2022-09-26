# How to send SMS with Python and Infobip

![Python](https://img.shields.io/pypi/pyversions/infobip-api-python-sdk)

As an outcome of this guide, you will send a simple text message to your headset with Infobip SMS API.

---

## Prerequisites

• [Infobip account](https://www.infobip.com/signup)

• Working [Python 3](https://www.python.org/downloads/) environment

## Difficulty level

This guide assumes very basic knowledge of Python and basic familiarity with APIs.

## Summary of the steps

• Install the Infobip API Python SDK.\
• Import the SMS Channel and creeate an SMS Channel instance.\
• Add credentials, phone number, and SMS payload to your instance.\
• Send an SMS and print the response to track its progress.

## Install the Infobip API Python SDK

```bash
pip install infobip-api-python-sdk
```

## Create an SMS Channel instance

You'll use the instance to input your credentials and access its methods. In this case, we will use the `send_sms_message` method to add the SMS payload.

__Step 1.__ Import the `SMSChannel`.

```python
from infobip_channels.sms.channel import SMSChannel
```
  
__Step 2.__ Create the `SMSChannel` instance and add your `base_url` and `api_key` that you can access either from your [Infobip account](https://portal.infobip.com/homepage/) or from the [Infobip API landing page](https://www.infobip.com/docs/api), provided you have logged in.

```python
channel = SMSChannel.from_auth_params({
    "base_url": "<your_base_url>",
    "api_key": "<your_api_key>"
})
```
  
__Step 3.__ Use the `send_sms_message` method to add the [SMS payload](https://www.infobip.com/docs/api#channels/sms/send-sms-message). 

Key points:  

• The destination address in the `to` field must be in international format, e.g. `447415774332`.  
• If using a free trial account, the phone number you use must be the same phone number you've registered on signup.  
• We recommend you put the `send_sms_message` method within a variable, so that you can print out the response.  

```python
sms_response = channel.send_sms_message({
    "messages": [{
        "destinations": [{
            "to": "<phone_number>"
            }],
        "from": "InfobipSMS",
        "text": "Hi! I'm your first Infobip message. Have a lovely day!"
            }
        ]
    }
)
```

### Add multiple recipients and multiple messages

Add multiple recipients by adding multipule `to` fields to the `destination` array. Similarily, create multiple `destinations` objects to send multiple messages with one request.

__Step 4.__ Print the response to monitor the progress of your SMS.

```python
print(sms_response)
```

Once you run the code, you should get an SMS on your handset and see the following `200 OK` response.

```bash
{
  "bulkId": "2034072219640523072",
  "messages": [
    {
      "messageId": "41793026727",
      "status": {
        "description": "Message sent to next instance",
        "groupId": 1,
        "groupName": "PENDING",
        "id": 26,
        "name": "MESSAGE_ACCEPTED"
      },
      "to": "2250be2d4219-3af1-78856-aabe-1362af1edfd2"
    }
  ]
}
```

For troubleshooting and analytics, Use the auto-generated `bulkId` to fetch the entire bulk of messages, or the `messageId` to fetch one specific message.
