---
title: Using Docker with Node
type: docs
---

### Dockerfile
This is an example of a Dockerfile for a node application.
```Dockerfile
FROM alpine:3.4  

RUN apk add --no-cache --update nodejs &&\
    mkdir /app

ENTRYPOINT /app

ADD . /app

EXPOSE 3000 4300

CMD npm start
```  

Here is a line by line breakdown:
- We start with [alpine](https://hub.docker.com/_/alpine/), this will help us keep only the things we absolutely need in the image
- In the first line of the run statement we install nodejs (this includes npm)
- In the second line we make a directory to add our app to
- We set our working directory to the newly created app directory
- Expose the ports your app listens only
- Use `npm start` to start the app on container startup

### Building
Coming soon

### Running
Coming soon

### Managing App Configuration
Coming soon
