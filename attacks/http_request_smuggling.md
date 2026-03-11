# HTTP Request Smuggling

## Introduction

- HTTP request smuggling is a security vulnerability that arises when there are mismatches in different web infrastructure components.
- This includes proxies, load balancers, and servers that interpret the boundaries of HTTP requests.
- This vulnerability mainly includes the headers like `Content-Length` and `Transfer-Encoding`, which indicates the end of the request body.
- When these headers are manipulated or interpreted this may lead to one request being mixed with another.

- Request Splitting or HTTP desync attacks are possible because of the nature of HTTP pipelining's keep-alive nature of connections.

## Importance

- Smuggled requests might evade security mechanisms like WAFs. This potentially leads to unauthorized access or data leaks.
- Attackers can poison web caches by smuggling malicious content, causing users to see incorrect or harmful data.
- Smuggled requests can be chained to exploit other vulnerabilties in the system, amplifying the potential damage.
- Due to intricate nature of this vulnerability, it can often go undetected, making it crutial for security professionals to understand and mitigate it.

## Infrastructure underneath

- Front-end server - This is usually the reverse proxy or load balancer that forwards the request to the back-end.
- Back-end server - This server-side component processes user requests, interacts with databases, and serves data to the front-end.
- Databases
- APIs - Allows communication between front-end and back-end and integrate other services.
- Load balancers - These devices or services distributes the incoming traffic across multiple servers to ensure no single server is overwhelmed with high traffic. This ensures high availability and high reliability.
- Reverse proxy - Sits before one or more web servers and forwards client request to the appropriate web server. While they can also perform as load balancers, but their primary purpose is to provide a single access point for back-end servers.

### Caching Mechanisms

- Content Caching - By storing web content that doesn't change frequently like images, css or js files. caching mechanisms can reduce the load on web servers and speed up content delivery to users.
- Database query caching - Databases cache results of frequent queries, reducing the time and compute needed to fetch the same data repeatedly.
- Full-page caching - Entire web pages are cached, so they don't need to be regenerated for each user. This is especially useful for websites with high traffic.
- Edge caching/CDNs - Content Delivery Networks (CDNs) cache content closer to the end user (at the 'edge' of the network) reducing the latency and speeding up the access for users
- API caching - Caching the responses can significantly reduce back-end processing for APIs that serve similar requests repeatedly.

## 1. HTTP Request Structure

An **HTTP request** consists of three primary components:

### Request Line

Format:

```
<METHOD> <PATH> <HTTP VERSION>
```

Example:

```
POST /admin/login HTTP/1.1
```

Components:

| Component    | Description                                |
| ------------ | ------------------------------------------ |
| Method       | Action to perform (GET, POST, PUT, DELETE) |
| Path         | Resource being requested                   |
| HTTP Version | Protocol version (HTTP/1.1, HTTP/2)        |

---

### Request Headers

Headers provide **metadata about the request**.

Examples:

```
Host: example.com
Content-Type: application/json
Authorization: Bearer token
```

Headers control:

* Content type
* Authentication
* Caching behavior
* Request parsing
* Encoding methods

---

### Message Body

The **body contains the actual request data**.

Examples:

Form data:

```
username=test&password=123
```

JSON:

```
{
 "username": "test"
}
```

Typically present in:

* POST
* PUT
* PATCH requests

---

# Important Headers in Request Smuggling

## Content-Length

Defines the **size of the request body in bytes**.

Example:

```
POST /submit HTTP/1.1
Host: good.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 14

q=smuggledData
```

Meaning:

* Server reads **exactly 14 bytes** of body data.

---

## Transfer-Encoding

Defines **how the body is encoded during transfer**.

Most common value:

```
Transfer-Encoding: chunked
```

### Chunked Encoding Format

Example:

```
POST /submit HTTP/1.1
Host: good.com
Transfer-Encoding: chunked

b
q=smuggledData
0
```

Explanation:

| Part           | Meaning                      |
| -------------- | ---------------------------- |
| b              | Chunk size in hex (11 bytes) |
| q=smuggledData | Actual data                  |
| 0              | End of chunks                |

---

# HTTP Request Smuggling

HTTP Request Smuggling occurs when **front-end and back-end servers interpret request boundaries differently**.

Common scenario:

```
Client → Proxy/Load Balancer → Backend Server
```

If these components **prioritize headers differently**, attackers can inject **hidden requests**.

Main cause:

```
Content-Length vs Transfer-Encoding conflict
```

---

# CL.TE Request Smuggling

## Meaning

```
CL.TE = Content-Length / Transfer-Encoding
```

Behavior:

| Component       | Header Used       |
| --------------- | ----------------- |
| Front-end proxy | Content-Length    |
| Back-end server | Transfer-Encoding |

---

## Example Payload

```
POST /search HTTP/1.1
Host: example.com
Content-Length: 130
Transfer-Encoding: chunked

0

POST /update HTTP/1.1
Host: example.com
Content-Length: 13
Content-Type: application/x-www-form-urlencoded

isadmin=true
```

### How it Works

1. **Front-end server**

   * Uses `Content-Length`
   * Treats entire payload as **single request**

2. **Back-end server**

   * Uses `Transfer-Encoding`
   * Stops reading at `0`
   * Interprets following content as **new request**

Result:

```
POST /update
```

becomes a **smuggled request**.

---

## Incorrect Content-Length

If `Content-Length` is incorrect:

Example body:

```
username=test&query=test
```

Size:

```
24 bytes
```

If header is:

```
Content-Length: 10
```

Server reads only:

```
username=t
```

Remaining data may become **separate request data**.

---

# TE.CL Request Smuggling

## Meaning

```
TE.CL = Transfer-Encoding / Content-Length
```

Behavior:

| Component       | Header Used       |
| --------------- | ----------------- |
| Front-end proxy | Transfer-Encoding |
| Back-end server | Content-Length    |

---

## Example Payload

```
POST / HTTP/1.1
Host: example.com
Content-Length: 4
Transfer-Encoding: chunked

78
POST /update HTTP/1.1
Host: example.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 15

isadmin=true
0
```

---

## How TE.CL Works

### Front-End Server

Uses:

```
Transfer-Encoding: chunked
```

Reads until:

```
0
```

Everything before `0` = body.

---

### Back-End Server

Uses:

```
Content-Length: 4
```

Reads only:

```
78\n
```

Remaining content:

```
POST /update HTTP/1.1
```

becomes a **new backend request**.

---

# Key Differences

| Technique | Front-End Uses    | Back-End Uses     |
| --------- | ----------------- | ----------------- |
| CL.TE     | Content-Length    | Transfer-Encoding |
| TE.CL     | Transfer-Encoding | Content-Length    |

---

# Impact of Request Smuggling

Possible attack outcomes:

* Authentication bypass
* Cache poisoning
* Web cache deception
* Request hijacking
* Session fixation
* Admin privilege escalation
* Backend request manipulation

---

# Key Indicators During Testing

Look for:

* Both headers present

```
Content-Length
Transfer-Encoding
```

* Frontend proxies:

  * Nginx
  * HAProxy
  * Cloudflare
  * AWS ALB

* Backend servers:

  * Apache
  * Tomcat
  * Node.js
  * IIS

---

