---
date: 2019-08-09 18:30:00 +0000
title: Slack Bot using Python Flask
image: "/images/blog1.png"
tags:
- Slack
- Flask

---
Usually bots perform two operation one to receive the user messages and the other is to provide response to the obtained messages. Dynamically changing response needs backend works to done.

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