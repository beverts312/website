---
title: tcpdump
type: docs
---

`tcpdump` is simple but powerful tool for analyzing network traffic.

1. Start capturing `tcpdump -i any -w /tmp/http.log &`
2. Do your thing
3. Stop Capturing `killall tcpdump`
4. Check it out `tcpdump -A -r /tmp/http.log | less`

## Filtering
To make your data easier to view you can scope the traffic tcpdump is capturing to only get what you are interested in.
Filter traffic going to a specific port `tcpdump dst port $PORT`.
Filter traffic going to a specific ip `tcpdump dst $IP`.
Filter traffic going to a specific interface `tcpdump -i $INTERFACE`.