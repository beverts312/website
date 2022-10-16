---
title: Dynamic Route 53 Tool
type: docs
---

This is a simple tool which allows you to dynamically update a Route 53 record set with the current public IP address of the machine it is running on. It can configure it self as a cron job if specified. A hobbyist use case could be to have a dynamic DNS service for being able to access things you are hosting from your home network.

Install: `pip install bails-aws-utils`

```bash
usage: dynamic-dns [-h] -p PREFIX -d DOMAIN [-c CRON] [-i INTERVAL] [-s]

Creates an A record for the current public IP.

optional arguments:
  -h, --help            show this help message and exit
  -p PREFIX, --prefix PREFIX
                        The prefix of the A record to create
  -d DOMAIN, --domain DOMAIN
                        The domain of the A record to create
  -c CRON, --cron CRON  Cron schedule, overrides interval if set, if save is not passed this will be ignored
  -i INTERVAL, --interval INTERVAL
                        Interval in minutes to run the cron job, if save is not passed this will be ignored
  -s, --save            Save the cron job to the crontab
```

Links:
* [PyPi](https://pypi.org/project/bails-aws-utils/)
* [Github](https://github.com/beverts312/bails-aws-utils)
