---
title: Security
type: docs
---

Notes from **Node.js Security: Pentesting and Exploitation** course on StackSkills.  

## Vulnerabilities  
[Full code examples on github](https://github.com/ajinabraham/Node.Js-Security-Course)  

### Global Namespace Pollution  
Be very careful with global variables.  

### HTTP Parameter Polution (express)  
If you pass the same url parameter multiple times in request they will all be read as comma seperated values.  
For example consider this code:  
```javascript
app.get('/hpp', (req, res) => {
    res.send(req.query.id);
});
```  
And we sent this request `url/hpp?id=123&id=456` the response would be `123,456`, be aware of the implications of this.  

### eval() is Evil  
Be careful with eval.  
For example consider this code:  
```javascript
app.get('/eval', (req, res) => {
    let resp=eval("("+req,query.name+")");
    res.send(resp);
});
```  
We could pass something like `process.exit(1)` using the `name` parameter and this would kill the web server. 
We could leverage an exploit like this to allow a remote connection to the web server.  

### Remote OS Command Execution  
Be careful with child_process.  
For example consider this code:  
```javascript
var exe = require('child_process');  
app.get('/os', (req, res) => {
    exe.exec('ping -c 2 ' + req.query.ping, (err, data) => {
        res.send(data);
    });
});
```  
We could pass something like `127.0.0.1; whoami`, and get the `whoami` response back from the host. 
Obviously we could do much more malicious things than determine the user.  

### Untrusted User Input  
For example consider this code:  
```javascript
app.get('/hello', (req, res) => {
    res.send('hello ' + req.query.name);
});
```  
We could pass someting like `<img src=x onerror=alert('haha')>` and that html would be rendered allowing us to do things like XSS.  

### Regex DoS  
Ensure you are using safe regex, if you use unsafe regex, it will be easy for attackers to induce load on your server.  

## Information Disclosure  
Ideally we want to hide things like our techstack/frameworks from the users (and attackers), this info can come up in headers, error pages, and cookies.  
[Helmet](https://github.com/helmetjs/helmet) can be used to help make this easier.  

To disable the `x-powered-by` header you can either do `app.disable('x-powered-b')` or if you are using helmet, `app.use(helmet.hidePoweredBy())`  

## Secure Code Tips  
Use strict mode.  
Use helmet (if you are using express) or obfuscate the same info yourself.  

## Things to check in a code review  
* File & DB Operations  
* Insecure Crypto  
* Insecure SSL  
* Insecure Server to Server SSL  
* Logical Flaws  
* Untrusted user input