# Best practice of RESTful api

### Rules

1.1 动词 + 宾语， `GET /name` 

````
GET Read
POST Create
PUT Update
PATCH Update, partially
DELETE Delete
````

1.2 动词的覆盖

解决客户端的请求方法受限问题，利用请求头

`X-HTTP-Method-Override`

1.3 宾语必须是名词

宾语就是 API 的 URL

Bad:

 `/getNames`

Good:

 `names` 

1.4 复数 URL

建议使用复数 URL，比如 `GET /names`

1.5 避免多级 URL

Bad:

`GET /names/1/groups/1`

Good:

`GET /nams?group=1`

### Status Code

2.1 HTTP code must be returned.

HTTP Status Code types:

```
1xx: info (not needed)
2xx: ok
3xx: redirection
4xx: client error
5xx: server error
```

### Server Response

3.1 Do not return plain text

API should return a JSON object, so HTTP header should contain 

`Content-Type` `application/json`

Then client's header `ACCEPT` must be `application/json`

3.2 Do not return 2xx when error happened

Bad:

````
HTTP/1.1 200 OK
Content-Type: application/json

{
  "status": "failure",
  "data": {
    "error": "Expected at least two items in list."
  }
}
````

Good:

```
HTTP/1.1 400 Bad Request
Content-Type: application/json
{
  "error": "Invalid payoad.",
  "detail": {
     "surname": "This field is required."
  }
}
```

------

### PUT vs POST

Both PUT & POST can be used for creating.

you do not need to support both method.

- PUT is idempotent, so you PUT an object twice, it has no effect.
- You can update or create a resource with PUT with the same object URL.
- With POST you can have 2 requests coming in at a same time making modifications to  a URL, and they may update different parts of the object.



Bad:

```
/question/show/<whatever>
/question/edit/<whatever>
/question/update/<whatever> (this is the post back url)
/question/list   (lists the questions)
```

Use the URLs to specify your objects, not your actions.

Good:

````
GET /questions HTTP/1.1
Host: xx.com
````

```
POST /questions HTTP/1.1
Host: xx.com
```



