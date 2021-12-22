---
title: Snippets
type: docs
---

## Encoding/decoding  
To base64 encode a string: `new Buffer(str).toString('base64')`  
To decode a base64 string: ` new Buffer(str, 'base64').toString('ascii')`  