---
date: 2019-08-09 18:30:00 +0000
title: Slack Bot using Python Flask
image: "/images/blog1.jpg"
tags:
- Slack
- Flask

---
Usually bots perform two operation one to receive the user messages and the other is to provide response to the obtained messages. Dynamically changing response needs backend works to done.

<!-- excerpt -->

**Receiving** **Messages :**

For receiving messages go to [Event Subscription](https://api.slack.com/apps/AM8F6C48G/event-subscriptions?) page and enable it and provide your ngrok redirected link.

![](/images/blog1_1.jpeg)

First verify the payload by getting it in POST method and then returning the same payload.

    from flask import Flask, request, Response
    app = Flask(__name__)
    @app.route(‘/’, methods=[‘POST’])
    def verify():
    data = request.json
    return data
    if __name__ == “__main__”:
    app.run(debug=True)

The same code can be used to get the message payload which gives the information about the message. To check it just print data for reference.

**Sending Response :**

Use the [Incoming Webhook](https://api.slack.com/apps/AM8F6C48G/incoming-webhooks?) page and enable it.

![](/images/blog1_2.jpeg)

Use the below code snippet for responding to the incoming message using python webhook.

    from flask import Flask, request, Response
    import requests
    import json
    app = Flask(__name__)
    @app.route(‘/’, methods=[‘POST’])
    def verify():
    data = request.json
    if data[‘event’][‘type’] == “app_mention”:
    user_text = data[‘event’][‘text’]
    user = data[‘event’][‘user’]
    webhook_url = ‘***********Your webhook url******************’
    slack_data = { “text”: “How can I help you ?” }
    response = requests.post(
    webhook_url, data=json.dumps(slack_data),
    headers={‘Content-Type’: ‘application/json’}
    )
    return(‘’, 204)
    if __name__ == “__main__”:
    app.run(debug=True)

For any queries ping me at [https://twitter.com/vigneshwar1998](https://twitter.com/vigneshwar1998 "https://twitter.com/vigneshwar1998")