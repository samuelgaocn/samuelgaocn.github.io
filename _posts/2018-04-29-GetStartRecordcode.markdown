---
layout: post
category: "read"
title:  “Python 监测VPS状态"
tags: [Python,VPS]
---
 
    #!/usr/bin/python
    # -*- coding: utf-8 -*-

    import os
    import requests
    from datetime import datetime
    timeout = 10
    time = datetime.now().strftime('%Y-%m-%d %H:%M:%S')
    key = 'SCKEY'
    title = "VPS在线检测"
    hostname = "xx.xx.xx.xx"
    response = os.system("ping -c 1 "+ hostname)
    if response != 0:
        content = "VPS已无法连接" + "\n" + time
        payload = {
            'text': title,
            'desp': content
        }
        url = 'https://sc.ftqq.com/{}.send'.format(key)
        requests.post(url, params=payload, timeout=timeout)
    else:
        content = "VPS正常连接" + "\n" + time