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