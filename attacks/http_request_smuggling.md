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
