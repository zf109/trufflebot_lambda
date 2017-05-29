# Lex IO format for lambda functions

The lambda handle function is as:

```python
def lambda_handler(event, context):
    """
    Route the incoming request based on intent.
    The JSON body of the request is provided in the event slot.
    """
    #... processing
    response = process(event)
    return response
```
the input ```event``` and the response ```response``` are as per
[aws lex io format](http://docs.aws.amazon.com/lex/latest/dg/lambda-input-response-format.html)


## Input jason format
```json
{
  "currentIntent": {
    "name": "intent-name",
    "slots": {
      "slot-name": "value",
      "slot-name": "value",
      "slot-name": "value"
    },
    "confirmationStatus": "None, Confirmed, or Denied (intent confirmation, if configured)",
  },
  "bot": {
    "name": "bot-name",
    "alias": "bot-alias",
    "version": "bot-version"
  },
  "userId": "user-id specified in the POST request to Amazon Lex.",
  "inputTranscript": "Text used to process the request",
  "invocationSource": "FulfillmentCodeHook or DialogCodeHook",
  "outputDialogMode": "Text or Voice, based on ContentType request header in runtime API request",
  "messageVersion": "1.0",
  "sessionAttributes": { 
     "key1": "value1",
     "key2": "value2"
  }
}
```

## Response json format

```json
{
    "sessionAttributes": {
    "key1": "value1",
    "key2": "value2"
  },
  "dialogAction": {
    "type": "ElicitIntent, ElicitSlot, ConfirmIntent, Delegate, or Close",
  }
}
```


## dialogAction format 1

```json
"dialogAction": {
    "type": "Close",
    "fulfillmentState": "Fulfilled or Failed",
    "message": {
      "contentType": "PlainText or SSML",
      "content": "message to convey to the user, i.e. Thanks, your pizza has been ordered."
    },
   "responseCard": {
      "version": "integer-value",
      "contentType": "application/vnd.amazonaws.card.generic",
      "genericAttachments": [
          {
             "title":"card-title",
             "subTitle":"card-sub-title",
             "imageUrl":"URL of the image to be shown",
             "attachmentLinkUrl":"URL of the attachment to be associated with the card",
             "buttons":[ 
                 {
                    "text":"button-text",
                    "value":"value sent to server on button click"
                 }
              ]
           } 
       ] 
     }
  }
```

