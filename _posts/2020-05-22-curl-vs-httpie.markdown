---
title: "cURL vs HTTPie: Interacting with HTTP servers"
layout: post
date: 2020-05-21 02:24
image: 
headerImage: false
tag:
- cURL
- HTTPie
- CLI
- HTTP
- GET
- POST
- python
star: false
category: blog
author: prashant
hidden: false
description: Making CLI interaction with web services as human-friendly as possible.
---

<p align="center">
   <img src="https://httpie.org/static/img/httpie2.png?v=1f6219a5a07bb6e99aa7afd98d0e67ec" alt="curl-vs-httpie" style="width:60%;">
</p>

For testing and debugging while developing RESTful APIs or HTTP servers or even playing around with APIs, [cURL](https://github.com/curl/curl) used to be my default tool of choice. However, my life literally changed once I found out about [HTTPie](https://github.com/jakubroztocil/httpie). HTTPie is a command line HTTP client written in python that allows for sending arbitrary HTTP requests using a simple and natural syntax, and displays colorized output.

Let's make some GET and POST requests using curl and httpie and see the difference in request syntax as well as responses.

## GET Request

- cURL

  ```bash
  curl 'https://postman-echo.com/get?arg1=value1&key2=value2'
  ```

  Response:
  ![curl get request response](../assets/images/curl-vs-httpie/curl_get.png)

- HTTPie

  ```bash
  https https://postman-echo.com/get arg1==value1 arg2==value2 
  ```

  Response:
  ![httpie get request response](../assets/images/curl-vs-httpie/httpie_get.png)

## POST Request

- cURL

  ```bash
  curl -d '{"key1":"value1", "key2":"value2"}' \
       -H "Content-Type: application/json" \
       -X POST https://postman-echo.com/post
  ```

  Response:
  ![curl post request response](../assets/images/curl-vs-httpie/curl_post.png)

- HTTPie

  ```bash
  https POST https://postman-echo.com/post key1=value1 key2=value2
  ```

  Response:
  ![httpie post request response](../assets/images/curl-vs-httpie/httpie_post.png)

## Installation

Installing HTTPie is pretty simple using pip.

```bash
pip install httpie
```

I really like HTTPie due to its expressive and intuitive syntax, formatted and colorized terminal output and built-in JSON support. I recommend you try it as well.
