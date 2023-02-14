# API Security Checklist
Checklist of the most important security countermeasures when designing, testing, and releasing your API.


---

## Authentication
- [x] Don't use `Basic Auth`. Use standard authentication instead (e.g., [JWT](https://jwt.io/)).
- [x] Don't reinvent the wheel in `Authentication`, `token generation`, `password storage`. Use the standards.
- [x] Use `Max Retry` and jail features in Login.
- [x] Use encryption on all sensitive data.

## Access
- [ ] Limit requests (Throttling) to avoid DDoS / brute-force attacks. (check in the end)
- [x] Use HTTPS on server side with TLS 1.2+ and secure ciphers to avoid MITM (Man in the Middle Attack).
- [x] Use `HSTS` header with SSL to avoid SSL Strip attacks.
- [x] Turn off directory listings.
- [x] For private APIs, allow access only from whitelisted IPs/hosts.

## Authorization


## Input
- [x] Use the proper HTTP method according to the operation: `GET (read)`, `POST (create)`, `PUT/PATCH (replace/update)`, and `DELETE (to delete a record)`, and respond with `405 Method Not Allowed` if the requested method isn't appropriate for the requested resource.
- [x] Validate `content-type` on request Accept header (Content Negotiation) to allow only your supported format (e.g., `application/xml`, `application/json`, etc.) and respond with `406 Not Acceptable` response if not matched.
- [x] Validate `content-type` of posted data as you accept (e.g., `application/x-www-form-urlencoded`, `multipart/form-data`, `application/json`, etc.).
- [ ] Validate user input to avoid common vulnerabilities (e.g., `XSS`, `SQL-Injection`, `Remote Code Execution`, etc.).
- [x] Don't use any sensitive data (`credentials`, `Passwords`, `security tokens`, or `API keys`) in the URL, but use standard Authorization header.
- [x] Use only server-side encryption.
- [ ] Use an API Gateway service to enable caching, Rate Limit policies (e.g., `Quota`, `Spike Arrest`, or `Concurrent Rate Limit`) and deploy APIs resources dynamically.

## Processing
- [x] Check if all the endpoints are protected behind authentication to avoid broken authentication process.
- [x] User own resource ID should be avoided. Use `/me/orders` instead of `/user/654321/orders`.
- [x] Don't auto-increment IDs. Use `UUID` instead.
- [x] If you are parsing XML data, make sure entity parsing is not enabled to avoid `XXE` (XML external entity attack).
- [x] If you are parsing XML, YAML or any other language with anchors and refs, make sure entity expansion is not enabled to avoid `Billion Laughs/XML bomb` via exponential entity expansion attack.
- [x] Use a CDN for file uploads.
- [x] If you are dealing with huge amount of data, use Workers and Queues to process as much as possible in background and return response fast to avoid HTTP Blocking.
- [x] Do not forget to turn the DEBUG mode OFF.
- [x] Use non-executable stacks when available.

## Output
- [ ] Send `X-Content-Type-Options: nosniff` header.
- [ ] Send `X-Frame-Options: deny` header.
- [ ] Send `Content-Security-Policy: default-src 'none'` header.
- [x] Remove fingerprinting headers - `X-Powered-By`, `Server`, `X-AspNet-Version`, etc.
- [x] Force `content-type` for your response. If you return `application/json`, then your `content-type` response is `application/json`.
- [x] Don't return sensitive data like `credentials`, `passwords`, or `security tokens`.
- [x] Return the proper status code according to the operation completed. (e.g., `200 OK`, `400 Bad Request`, `401 Unauthorized`, `405 Method Not Allowed`, etc.).


