---
date: 2019-08-31 16:02:01 +0000
title: Redis Queue implementation in Python
image: "/images/rq.png"
tags:
- RQ
- Python

---
RQ (_Redis Queue_) is a simple Python library for queueing jobs and processing them in the background with workers.

<!-- excerpt -->

After redis installation, run the redis server with the command,

> ➜  redis-server

![](/images/redis-server.png)

Use the below code in the mentioned files,

app.py

    from redis import Redis
    from rq import Queue
    from my_module import count_words_at_url
    
    q = Queue(connection=Redis())
    
    result = q.enqueue(count_words_at_url, 'http://nvie.com')

my_module.py

    import requests
    
    def count_words_at_url(url):
      resp = requests.get(url)
      return len(resp.text.split())

Pip install the below modules

> ➜  pip install rq
>
> ➜  pip install requests

**The worker:**

To start executing enqueued function calls in the background, start a worker from your project’s directory:

> ➜  rq worker

![](/images/rq_worker1.png)

Run the python file app.py and check the rq worker terminal for the job updation.

![](/images/rq_worker.png)

For any queries ping me at [https://twitter.com/vigneshwar1998](https://twitter.com/vigneshwar1998 "https://twitter.com/vigneshwar1998")