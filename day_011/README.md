# Day 11: HTTP Protocol Deep Dive & Socket Programming

<div align="center">
  <img src="https://media.giphy.com/media/3oKIPEqDGUULpEU0aQ/giphy.gif" width="500" alt="HTTP Communication Animation">
  
  <h1>🌐 HTTP Protocol & Socket Programming 🌐</h1>
  
  <p>
    <img src="https://img.shields.io/badge/HTTP-Methods%20%26%20Headers-blue" alt="HTTP Methods">
    <img src="https://img.shields.io/badge/Status%20Codes-Response%20Handling-green" alt="Status Codes">
    <img src="https://img.shields.io/badge/TCP-Connection%20Management-red" alt="TCP">
    <img src="https://img.shields.io/badge/Sockets-Network%20Programming-purple" alt="Sockets">
  </p>
  
  <hr>
</div>

## Table of Contents
- [Introduction to HTTP](#introduction-to-http)
- [HTTP Methods in Depth](#http-methods-in-depth)
- [HTTP Headers Explained](#http-headers-explained)
- [HTTP Status Codes](#http-status-codes)
- [HTTP State Management: Cookies and Sessions](#http-state-management-cookies-and-sessions)
- [HTTP and TCP Relationship](#http-and-tcp-relationship)
- [Introduction to Socket Programming](#introduction-to-socket-programming)
- [Socket vs HTTP](#socket-vs-http)
- [Practical Examples](#practical-examples)
- [HTTP Evolution: HTTP/1.0 to HTTP/3](#http-evolution-http10-to-http3)
- [RESTful API Design](#restful-api-design)
- [Practice Questions](#practice-questions)
- [Additional Resources](#additional-resources)

## Introduction to HTTP

HTTP (Hypertext Transfer Protocol) is an application layer protocol designed for distributed, collaborative, hypermedia information systems. It forms the foundation of data communication for the World Wide Web, enabling the retrieval of interlinked text pages, images, videos, and other multimedia resources.

```mermaid
graph TD
    subgraph "HTTP Communication Model"
        A[Client] -- "1. HTTP Request" --> B[Server]
        B -- "2. HTTP Response" --> A
    end
    
    subgraph "HTTP Layers"
        C[Application Layer] --> D[Transport Layer: TCP]
        D --> E[Internet Layer: IP]
        E --> F[Network Interface Layer]
    end
```

### Key HTTP Characteristics

- **Stateless Protocol**: Each request from a client to server is treated independently
- **Client-Server Model**: Clear separation of responsibilities
- **Media Independence**: Can transfer any type of data if both client and server agree
- **Connectionless**: Although HTTP uses TCP, each request-response cycle is independent
- **Extensible**: Headers and methods can be extended for new features

## HTTP Methods in Depth

HTTP methods (also called "verbs") indicate the desired action to be performed on a resource. Each method has specific semantics and expected behavior.

### Core HTTP Methods

```mermaid
graph TD
    A[HTTP Methods] --> B[GET: Retrieve Resource]
    A --> C[POST: Create Resource]
    A --> D[PUT: Update/Replace Resource]
    A --> E[DELETE: Remove Resource]
    A --> F[HEAD: GET without body]
    A --> G[OPTIONS: Get supported operations]
    A --> H[PATCH: Partial update]
```

#### GET Method

```http
GET /api/users/123 HTTP/1.1
Host: example.com
Accept: application/json
```

- **Purpose**: Retrieve a resource or collection of resources
- **Properties**:
  - Safe (read-only)
  - Idempotent (same result regardless of how many times executed)
  - Cacheable
  - Should not change server state
- **Typical Use Cases**: 
  - Retrieving web pages
  - API data retrieval
  - Search queries (via query parameters)
- **Security Considerations**: 
  - Parameters are visible in URL (don't use for sensitive data)
  - Length limitations on URLs (typically <2048 characters)

#### POST Method

```http
POST /api/users HTTP/1.1
Host: example.com
Content-Type: application/json
Content-Length: 45

{
  "name": "John Doe",
  "email": "john@example.com"
}
```

- **Purpose**: Create new resources or submit data for processing
- **Properties**:
  - Not safe (changes server state)
  - Not idempotent (multiple identical requests may create multiple resources)
  - May be cacheable (uncommon)
- **Typical Use Cases**:
  - Form submissions
  - File uploads
  - Creating new resources
  - Triggering operations with side effects
- **Security Considerations**:
  - Data is in request body (more secure than GET)
  - Should use CSRF protection

#### PUT Method

```http
PUT /api/users/123 HTTP/1.1
Host: example.com
Content-Type: application/json
Content-Length: 76

{
  "id": 123,
  "name": "John Doe",
  "email": "john.updated@example.com"
}
```

- **Purpose**: Update or replace an existing resource completely
- **Properties**:
  - Not safe (changes server state)
  - Idempotent (multiple identical requests produce same result)
  - Not typically cacheable
- **Typical Use Cases**:
  - Updating resources when you know the full resource representation
  - Replacing resources at a specific URI
- **Security Considerations**:
  - Requires authorization to prevent unauthorized updates
  - Complete replacement could cause data loss if partial data is sent

#### DELETE Method

```http
DELETE /api/users/123 HTTP/1.1
Host: example.com
Authorization: Bearer token123
```

- **Purpose**: Remove a resource
- **Properties**:
  - Not safe (changes server state)
  - Idempotent (deleting same resource multiple times has same effect)
  - Not cacheable
- **Typical Use Cases**:
  - Removing resources from the system
- **Security Considerations**:
  - Requires strong authorization controls
  - Should consider soft deletes for recoverable data

#### PATCH Method

```http
PATCH /api/users/123 HTTP/1.1
Host: example.com
Content-Type: application/json-patch+json
Content-Length: 40

[
  { "op": "replace", "path": "/email", "value": "new.email@example.com" }
]
```

- **Purpose**: Partially update a resource
- **Properties**:
  - Not safe (changes server state)
  - Not inherently idempotent (depends on implementation)
  - Not typically cacheable
- **Typical Use Cases**:
  - Updating specific fields without replacing entire resource
  - Optimizing bandwidth by sending only changed data
- **Security Considerations**:
  - Same as PUT (requires authorization)
  - Can use JSON Patch format for describing changes

#### HEAD Method

```http
HEAD /api/users/123 HTTP/1.1
Host: example.com
```

- **Purpose**: Identical to GET but without response body
- **Properties**:
  - Safe
  - Idempotent
  - Cacheable
- **Typical Use Cases**:
  - Checking if resource exists
  - Retrieving metadata (like content-length) without downloading content
  - Testing caching headers
- **Security Considerations**:
  - Same as GET

#### OPTIONS Method

```http
OPTIONS /api/users HTTP/1.1
Host: example.com
```

- **Purpose**: Get information about available communication options
- **Properties**:
  - Safe
  - Idempotent
  - Not typically cached
- **Typical Use Cases**:
  - CORS preflight requests
  - Discovering supported methods for a resource
  - API self-documentation
- **Response Example**:
  ```http
  HTTP/1.1 200 OK
  Allow: GET, POST, PUT, DELETE, OPTIONS
  Access-Control-Allow-Methods: GET, POST, PUT, DELETE
  Access-Control-Allow-Headers: Content-Type, Authorization
  ```

### Method Characteristics Table

| Method  | Safe | Idempotent | Cacheable | Request Body | Response Body |
|---------|------|------------|-----------|--------------|---------------|
| GET     | Yes  | Yes        | Yes       | No           | Yes           |
| POST    | No   | No         | Rarely    | Yes          | Yes           |
| PUT     | No   | Yes        | No        | Yes          | Optional      |
| DELETE  | No   | Yes        | No        | Optional     | Optional      |
| HEAD    | Yes  | Yes        | Yes       | No           | No            |
| OPTIONS | Yes  | Yes        | No        | No           | Yes           |
| PATCH   | No   | No*        | No        | Yes          | Optional      |

*PATCH can be made idempotent depending on implementation

## HTTP Headers Explained

HTTP headers allow the client and server to pass additional information with requests or responses. They define operating parameters and provide metadata.

### Request Headers

```http
GET /index.html HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)
Accept: text/html,application/xhtml+xml
Accept-Language: en-US,en;q=0.9
Accept-Encoding: gzip, deflate
Connection: keep-alive
Cookie: session=123abc; user_pref=dark_mode
Cache-Control: no-cache
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

#### Common Request Headers

| Header | Purpose | Example |
|--------|---------|---------|
| Host | Specifies domain name of the server | `Host: api.example.com` |
| User-Agent | Identifies client application | `User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)` |
| Accept | Media types client can process | `Accept: application/json, text/plain` |
| Accept-Language | Preferred languages | `Accept-Language: en-US,en;q=0.8` |
| Accept-Encoding | Acceptable content encodings | `Accept-Encoding: gzip, deflate` |
| Authorization | Authentication credentials | `Authorization: Bearer token123` |
| Cookie | Client cookies | `Cookie: session=abc123; pref=dark` |
| Content-Type | Format of request body | `Content-Type: application/json` |
| Content-Length | Size of the request body | `Content-Length: 348` |
| Cache-Control | Directives for caching | `Cache-Control: no-cache` |
| If-Modified-Since | Conditional request timestamp | `If-Modified-Since: Wed, 21 Oct 2021 07:28:00 GMT` |

### Response Headers

```http
HTTP/1.1 200 OK
Date: Mon, 23 May 2023 22:38:34 GMT
Server: Apache/2.4.41 (Ubuntu)
Content-Type: text/html; charset=UTF-8
Content-Length: 138
Cache-Control: max-age=3600
ETag: "1a2b3c4d"
Access-Control-Allow-Origin: https://example.org
Set-Cookie: session=xyz789; Path=/; HttpOnly
```

#### Common Response Headers

| Header | Purpose | Example |
|--------|---------|---------|
| Server | Software used by the server | `Server: nginx/1.18.0` |
| Date | Date and time of the response | `Date: Mon, 23 May 2023 22:38:34 GMT` |
| Content-Type | Format of response body | `Content-Type: application/json; charset=utf-8` |
| Content-Length | Size of the response body | `Content-Length: 1024` |
| Cache-Control | Directives for caching | `Cache-Control: max-age=3600, public` |
| ETag | Resource version identifier | `ETag: "1a2b3c4d"` |
| Last-Modified | Last modification timestamp | `Last-Modified: Wed, 21 Oct 2021 07:28:00 GMT` |
| Set-Cookie | Set cookies on the client | `Set-Cookie: session=abc123; Path=/; Secure; HttpOnly` |
| Location | Redirect URL | `Location: https://example.com/new-page` |
| Access-Control-Allow-Origin | CORS permitted origins | `Access-Control-Allow-Origin: *` |
| Strict-Transport-Security | Force HTTPS connections | `Strict-Transport-Security: max-age=31536000; includeSubDomains` |

### Header Categories

```mermaid
graph TD
    A[HTTP Headers] --> B[General Headers]
    A --> C[Request Headers]
    A --> D[Response Headers]
    A --> E[Entity Headers]
    A --> F[Security Headers]
```

- **General Headers**: Apply to both requests and responses (e.g., Date, Connection)
- **Request Headers**: Client to server information (e.g., User-Agent, Accept)
- **Response Headers**: Server to client information (e.g., Server, Set-Cookie)
- **Entity Headers**: Describe the content (e.g., Content-Type, Content-Length)
- **Security Headers**: Enhance web security (e.g., Content-Security-Policy, X-XSS-Protection)

## HTTP Status Codes

HTTP status codes indicate the result of the HTTP request. They are three-digit numbers grouped into five categories.

```mermaid
graph LR
    A[HTTP Status Codes] --> B[1xx: Informational]
    A --> C[2xx: Success]
    A --> D[3xx: Redirection]
    A --> E[4xx: Client Error]
    A --> F[5xx: Server Error]
```

### 1xx: Informational

These status codes indicate that the request was received and the process is continuing.

| Code | Status | Description |
|------|--------|-------------|
| 100 | Continue | Server received headers, client should proceed with request body |
| 101 | Switching Protocols | Server is switching protocols as requested (e.g., WebSocket upgrade) |
| 102 | Processing | Server has received and is processing the request, but no response is available yet |
| 103 | Early Hints | Used to return some response headers before final HTTP message |

### 2xx: Success

These status codes indicate that the request was successfully received, understood, and accepted.

| Code | Status | Description |
|------|--------|-------------|
| 200 | OK | Standard success response for successful HTTP requests |
| 201 | Created | Request succeeded and a new resource was created |
| 202 | Accepted | Request accepted for processing but not yet completed |
| 204 | No Content | Request succeeded but returns no content |
| 206 | Partial Content | Server is delivering only part of the resource due to a range header |

### 3xx: Redirection

These status codes indicate that further action needs to be taken to complete the request.

| Code | Status | Description |
|------|--------|-------------|
| 300 | Multiple Choices | Multiple possible responses; user or user agent should choose one |
| 301 | Moved Permanently | Resource has been permanently moved to a new URL |
| 302 | Found | Resource temporarily located at a different URL |
| 303 | See Other | Response to the request can be found at another URI using GET |
| 304 | Not Modified | Resource has not been modified since the specified version |
| 307 | Temporary Redirect | Resource temporarily moved, but use the same HTTP method |
| 308 | Permanent Redirect | Resource permanently moved, preserve HTTP method and body |

### 4xx: Client Error

These status codes indicate that the client seems to have made an error.

| Code | Status | Description |
|------|--------|-------------|
| 400 | Bad Request | Server cannot process request due to client error (malformed syntax) |
| 401 | Unauthorized | Authentication is required and has failed or not been provided |
| 403 | Forbidden | Server understood request but refuses to authorize it |
| 404 | Not Found | Requested resource could not be found |
| 405 | Method Not Allowed | Request method not supported for the requested resource |
| 406 | Not Acceptable | Resource cannot generate content according to Accept headers |
| 408 | Request Timeout | Server timed out waiting for the request |
| 409 | Conflict | Request conflicts with current state of the server |
| 413 | Payload Too Large | Request entity is larger than limits defined by server |
| 415 | Unsupported Media Type | Request entity has media type which the server does not support |
| 429 | Too Many Requests | User has sent too many requests in a given amount of time (rate limiting) |

### 5xx: Server Error

These status codes indicate that the server failed to fulfill a valid request.

| Code | Status | Description |
|------|--------|-------------|
| 500 | Internal Server Error | Generic server error message |
| 501 | Not Implemented | Server does not recognize the request method or lacks ability to fulfill it |
| 502 | Bad Gateway | Server, while acting as a gateway, received an invalid response |
| 503 | Service Unavailable | Server is not ready to handle the request (overloaded or down for maintenance) |
| 504 | Gateway Timeout | Server, while acting as a gateway, did not receive a timely response |
| 505 | HTTP Version Not Supported | Server does not support the HTTP protocol version used in the request |

### Status Code Decision Flow

```mermaid
flowchart TD
    A[Process HTTP Request] --> B{Request Valid?}
    B -- Yes --> C{Resource Exists?}
    B -- No --> D[400 Bad Request]
    
    C -- Yes --> E{User Authorized?}
    C -- No --> F[404 Not Found]
    
    E -- Yes --> G{Resource Modified?}
    E -- No --> H[401/403 Unauthorized/Forbidden]
    
    G -- Yes --> I{Operation Successful?}
    G -- No --> J[304 Not Modified]
    
    I -- Yes --> K[200 OK / 201 Created / 204 No Content]
    I -- No --> L[500 Internal Server Error]
```

## HTTP State Management: Cookies and Sessions

HTTP is fundamentally a stateless protocol, meaning each request from a client to a server is treated as an independent transaction with no memory of previous interactions. However, many web applications require state management to provide personalized experiences and maintain user context across multiple requests.

```mermaid
graph TD
    A[HTTP Statelessness Challenge] --> B[Solution: State Management]
    B --> C[Client-Side State]
    B --> D[Server-Side State]
    C --> E[Cookies]
    C --> F[Web Storage]
    C --> G[URL Parameters]
    D --> H[Sessions]
    D --> I[Databases]
    E --> J[Connected to Sessions]
```

### Cookies: Client-Side State Tokens

Cookies are small pieces of data stored on the client's browser. They are sent with every HTTP request to the same domain, allowing servers to recognize clients across multiple requests.

#### Cookie Creation and Transmission

```mermaid
sequenceDiagram
    participant Client
    participant Server
    
    Client->>Server: HTTP Request
    Server->>Client: HTTP Response with Set-Cookie header
    Note over Client: Cookie stored in browser
    
    Client->>Server: Subsequent Request with Cookie header
    Server->>Client: Response (server recognizes client)
```

#### Cookie Anatomy

```
Set-Cookie: name=value; Domain=domain.com; Path=/; Expires=Wed, 21 Oct 2025 07:28:00 GMT; Secure; HttpOnly; SameSite=Strict
```

| Attribute | Purpose | Example |
|-----------|---------|---------|
| name=value | The cookie data | `sessionid=abc123` |
| Domain | Specifies domain that can receive the cookie | `Domain=example.com` |
| Path | Specifies URL path that must exist in the requested URL | `Path=/shop/` |
| Expires/Max-Age | Sets cookie lifetime | `Expires=Wed, 21 Oct 2025 07:28:00 GMT` |
| Secure | Cookie only sent over HTTPS | `Secure` |
| HttpOnly | Prevents JavaScript access | `HttpOnly` |
| SameSite | Controls cross-site request behavior | `SameSite=Strict` |

#### Cookie Types

1. **Session Cookies**: Temporary cookies that exist only until the browser is closed
   - No Expires or Max-Age attribute
   - Used for temporary state (shopping carts, form wizard steps)

2. **Persistent Cookies**: Remain on client for extended periods
   - Include Expires or Max-Age attribute
   - Used for long-term preferences, authentication tokens

3. **First-party Cookies**: Set by the domain in the address bar
   - Used for core site functionality

4. **Third-party Cookies**: Set by domains other than the one being visited
   - Often used for tracking and advertising
   - Increasingly restricted by browsers

#### Cookie Implementation Example

**Server Response (Setting a Cookie):**
```http
HTTP/1.1 200 OK
Content-Type: text/html
Set-Cookie: user_id=12345; Path=/; Expires=Wed, 21 Oct 2025 07:28:00 GMT; HttpOnly
Set-Cookie: theme=dark; Path=/

<html>
<body>
  <h1>Welcome to our site!</h1>
</body>
</html>
```

**Subsequent Client Request (Sending Cookies):**
```http
GET /profile HTTP/1.1
Host: example.com
Cookie: user_id=12345; theme=dark
Accept: text/html
```

#### Cookie Limitations

- **Size Limits**: 4KB per cookie, ~50 cookies per domain, ~3000 total per browser
- **Security Concerns**: Vulnerable to XSS and CSRF attacks if not properly secured
- **Privacy Issues**: Can be used for tracking users across sites
- **Regulatory Compliance**: Subject to laws like GDPR and ePrivacy Directive
- **Browser Restrictions**: Increasing limitations on third-party cookies

### Sessions: Server-Side State Management

Sessions provide a way to store user information on the server while using a small identifier on the client side to reference that information.

```mermaid
graph TD
    subgraph "Client"
        A[Browser]
        B[Session Cookie: session_id=abc123]
    end
    
    subgraph "Server"
        C[Session Storage]
        D["Session Data for abc123:
        - user_id: 42
        - cart_items: [...]
        - preferences: {...}"]
    end
    
    A --> B
    B -- "Request with session_id" --> C
    C -- "Lookup" --> D
```

#### How Sessions Work

1. **Session Creation**:
   - User visits site or logs in
   - Server generates unique session ID
   - Server stores session data with this ID as key
   - Server sends session ID to client (typically as a cookie)

2. **Session Identification**:
   - Client sends session ID with each request
   - Server looks up session data using this ID
   - Server processes request in context of session

3. **Session Termination**:
   - User logs out (explicit termination)
   - Session times out (inactivity)
   - Browser closes (if using session cookies)

#### Session Storage Methods

| Method | Description | Pros | Cons |
|--------|-------------|------|------|
| Memory | Stored in server's RAM | Fast access | Lost on server restart, doesn't scale |
| File System | Stored as files | Persistent | Slower than memory, cleanup issues |
| Database | Stored in database tables | Persistent, scalable | Higher latency than memory |
| Distributed Cache | Stored in Redis, Memcached, etc. | Fast, scalable, persistent | Additional infrastructure |

#### Session Implementation Example (Express.js)

```javascript
const express = require('express');
const session = require('express-session');
const app = express();

// Session middleware configuration
app.use(session({
  secret: 'keyboard cat',
  resave: false,
  saveUninitialized: true,
  cookie: { 
    secure: true,    // HTTPS only
    httpOnly: true,  // Not accessible via JavaScript
    maxAge: 3600000  // 1 hour in milliseconds
  }
}));

// Using session to store data
app.get('/view', (req, res) => {
  // Increment the views count
  req.session.views = (req.session.views || 0) + 1;
  
  res.send(`You have viewed this page ${req.session.views} times`);
});

// Using session for user authentication
app.post('/login', (req, res) => {
  // Validate user credentials (simplified)
  const user = authenticateUser(req.body.username, req.body.password);
  
  if (user) {
    // Store user info in session
    req.session.userId = user.id;
    req.session.username = user.username;
    req.session.isAuthenticated = true;
    
    res.redirect('/dashboard');
  } else {
    res.redirect('/login?error=invalid');
  }
});

app.get('/dashboard', (req, res) => {
  // Check if user is authenticated
  if (!req.session.isAuthenticated) {
    return res.redirect('/login');
  }
  
  // User is authenticated, show dashboard
  res.send(`Welcome to your dashboard, ${req.session.username}!`);
});

app.get('/logout', (req, res) => {
  // Destroy the session
  req.session.destroy(err => {
    res.redirect('/');
  });
});

app.listen(3000);
```

### Cookies vs. JWT for Authentication

Modern web applications often use JSON Web Tokens (JWT) as an alternative to traditional cookie-session authentication.

```mermaid
graph TD
    subgraph "Cookie-Session Authentication"
        A1[User Logs In]
        B1[Server Creates Session]
        C1[Server Sends Session ID Cookie]
        D1[Client Stores Cookie]
        E1[Client Sends Cookie with Requests]
        F1[Server Validates Session ID]
    end
    
    subgraph "JWT Authentication"
        A2[User Logs In]
        B2[Server Creates JWT with Claims]
        C2[Server Sends JWT to Client]
        D2[Client Stores JWT]
        E2[Client Sends JWT in Authorization Header]
        F2[Server Validates JWT Signature]
    end
    
    A1 --> B1 --> C1 --> D1 --> E1 --> F1
    A2 --> B2 --> C2 --> D2 --> E2 --> F2
```

| Feature | Cookie-Session | JWT |
|---------|----------------|-----|
| Storage | Server-side state | Stateless (client-side) |
| Scalability | Requires shared session store for multiple servers | No server storage needed |
| Size | Small cookie, data on server | Larger token with all data |
| Revocation | Easy (delete server-side session) | Difficult (requires blacklist) |
| Security | HttpOnly cookies prevent XSS | Must be stored securely |
| Cross-Domain | Restricted by SameSite | Works across domains |

### Best Practices for Cookie and Session Security

1. **Set Proper Cookie Attributes**:
   - `Secure` flag to ensure HTTPS-only
   - `HttpOnly` to prevent JavaScript access
   - `SameSite=Lax` or `SameSite=Strict` to prevent CSRF
   - Appropriate `Domain` and `Path` restrictions

2. **Session Management**:
   - Generate cryptographically strong session IDs
   - Regenerate session IDs after authentication
   - Implement absolute and idle timeouts
   - Provide logout functionality

3. **Protection Against Attacks**:
   - Implement CSRF tokens for state-changing operations
   - Validate and sanitize all user inputs
   - Use Content-Security-Policy headers
   - Rotate session IDs periodically

4. **Data Minimization**:
   - Store only necessary data in cookies
   - Avoid storing sensitive data in client-accessible storage

### State Management in Modern Web Applications

Modern web applications often use a combination of state management techniques:

1. **Cookies**: Still used for authentication tokens and session IDs
2. **Local Storage**: For persistent client-side data (with XSS risk)
3. **Session Storage**: For temporary client-side data (cleared on browser close)
4. **Server Sessions**: For sensitive user data and server state
5. **JWTs**: For stateless authentication and authorization
6. **IndexedDB**: For client-side structured data storage
7. **URL Parameters**: For shareable state and deep linking

## HTTP and TCP Relationship

HTTP relies on the Transmission Control Protocol (TCP) for reliable communication. Understanding this relationship is key to mastering HTTP.

### TCP Connection for HTTP

```mermaid
sequenceDiagram
    participant Client
    participant Server
    
    note over Client,Server: TCP 3-Way Handshake
    Client->>Server: SYN (Sequence = x)
    Server->>Client: SYN-ACK (Sequence = y, ACK = x+1)
    Client->>Server: ACK (ACK = y+1)
    
    note over Client,Server: HTTP Transaction
    Client->>Server: HTTP Request
    Server->>Client: HTTP Response
    
    note over Client,Server: TCP Connection Close (HTTP/1.0)
    Client->>Server: FIN
    Server->>Client: ACK
    Server->>Client: FIN
    Client->>Server: ACK
    
    note over Client,Server: OR Keep-Alive (HTTP/1.1+)
    Client->>Server: HTTP Request 2
    Server->>Client: HTTP Response 2
```

### Connection Lifecycle

1. **Connection Establishment**:
   - TCP three-way handshake establishes connection
   - Client and server agree on initial sequence numbers
   - Connection parameters are negotiated

2. **HTTP Request/Response Exchange**:
   - Client sends HTTP request over established TCP connection
   - Server processes request and sends response
   - Multiple request/response pairs may occur on the same connection (Keep-Alive)

3. **Connection Termination**:
   - Either party can initiate connection close
   - TCP four-way handshake ensures clean termination
   - All in-flight data is delivered before connection closes

### HTTP/1.0 vs HTTP/1.1 Connection Handling

#### HTTP/1.0
- Default: One TCP connection per request/response pair
- Connection closed after each response
- `Connection: keep-alive` header needed for persistent connections
- Inefficient for modern web pages with many resources

#### HTTP/1.1
- Default: Persistent connections (keep-alive)
- Multiple requests can be sent on a single TCP connection
- `Connection: close` header needed to close after response
- Reduced latency and improved performance
- Still limited by head-of-line blocking

### HTTP/2 Connection Handling

- Single TCP connection with multiple bidirectional streams
- Binary framing layer for multiplexing
- Concurrent requests and responses on single connection
- Eliminates head-of-line blocking at HTTP layer
- Server push capability for predicted resources

### How HTTP Uses TCP

1. **Reliability**: TCP ensures all data packets arrive in order without errors
2. **Flow Control**: Prevents overwhelming receiver with too much data
3. **Congestion Control**: Adapts to network conditions
4. **Connection-Oriented**: Establishes dedicated communication channel
5. **Full-Duplex**: Allows simultaneous bidirectional data flow

### TCP Socket States in HTTP Communication

```mermaid
stateDiagram-v2
    [*] --> CLOSED
    CLOSED --> SYN_SENT: Client initiates connection
    SYN_SENT --> ESTABLISHED: SYN-ACK received, ACK sent
    ESTABLISHED --> CLOSE_WAIT: Server initiates close
    CLOSE_WAIT --> LAST_ACK: Application closes
    LAST_ACK --> CLOSED: ACK received
    ESTABLISHED --> FIN_WAIT_1: Client initiates close
    FIN_WAIT_1 --> FIN_WAIT_2: ACK received
    FIN_WAIT_2 --> TIME_WAIT: FIN received, ACK sent
    TIME_WAIT --> CLOSED: Timeout (2MSL)
```

### HTTP Performance Considerations with TCP

- **TCP Slow Start**: New connections start with small congestion window
- **TCP Handshake Overhead**: Each new connection requires handshake (RTT delay)
- **Head-of-Line Blocking**: TCP must deliver packets in order, blocking on packet loss
- **Nagle's Algorithm**: Small packets combined for efficiency (can delay transmissions)
- **TCP Connection Reuse**: Persistent connections reduce overhead
- **TLS Handshakes**: Additional roundtrips for secure connections

## Introduction to Socket Programming

Socket programming provides the foundation for network communication, including HTTP. Sockets are endpoints for sending and receiving data across a network.

### What are Sockets?

```mermaid
graph LR
    subgraph "Process A"
        A[Application] --> B[Socket]
    end
    
    subgraph "Network"
        C[Protocol Stack]
    end
    
    subgraph "Process B"
        D[Socket] --> E[Application]
    end
    
    B <--> C
    C <--> D
```

A socket is an endpoint for communication between two machines. It's a combination of:
- IP address (identifies the machine)
- Port number (identifies the process)
- Protocol (TCP or UDP)

### Socket Types

1. **Stream Sockets (SOCK_STREAM)**:
   - Use TCP for reliable, connection-oriented communication
   - Guarantee order and delivery of data
   - Used for HTTP, FTP, SMTP, etc.

2. **Datagram Sockets (SOCK_DGRAM)**:
   - Use UDP for connectionless communication
   - No guarantees on order or delivery
   - Used for DNS, DHCP, video streaming, etc.

3. **Raw Sockets**:
   - Direct access to lower-level protocols
   - Used for custom protocols or packet analysis
   - Typically requires administrative privileges

### Socket Programming Model

```mermaid
sequenceDiagram
    participant Server
    participant Client
    
    Note over Server: socket()
    Note over Server: bind()
    Note over Server: listen()
    Note over Server: accept() [blocking]
    
    Note over Client: socket()
    Client->>Server: connect()
    Note over Server: accept() returns
    
    loop Communication
        Client->>Server: write()/send()
        Server->>Client: read()/recv()
        Server->>Client: write()/send()
        Client->>Server: read()/recv()
    end
    
    Client->>Server: close()
    Server->>Client: close()
```

### Basic Socket Operations

1. **Server Side**:
   - Create socket with `socket()`
   - Bind to address and port with `bind()`
   - Listen for connections with `listen()`
   - Accept client connection with `accept()`
   - Receive/send data with `recv()`/`send()`
   - Close connection with `close()`

2. **Client Side**:
   - Create socket with `socket()`
   - Connect to server with `connect()`
   - Send/receive data with `send()`/`recv()`
   - Close connection with `close()`

### Python Socket Programming Example

#### TCP Server

```python
import socket

# Create a socket object
server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# Define host and port
host = '127.0.0.1'
port = 12345

# Bind the socket to the address
server_socket.bind((host, port))

# Listen for incoming connections
server_socket.listen(5)
print(f"Server listening on {host}:{port}")

while True:
    # Accept a connection
    client_socket, addr = server_socket.accept()
    print(f"Connection from {addr}")
    
    # Receive data
    data = client_socket.recv(1024).decode('utf-8')
    print(f"Received: {data}")
    
    # Send a response
    message = "Hello from server!"
    client_socket.send(message.encode('utf-8'))
    
    # Close the connection
    client_socket.close()
```

#### TCP Client

```python
import socket

# Create a socket object
client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# Define host and port
host = '127.0.0.1'
port = 12345

# Connect to the server
client_socket.connect((host, port))

# Send data
message = "Hello from client!"
client_socket.send(message.encode('utf-8'))

# Receive response
data = client_socket.recv(1024).decode('utf-8')
print(f"Received: {data}")

# Close the connection
client_socket.close()
```

### Simple HTTP Server with Sockets

```python
import socket

def handle_request(request):
    # Parse HTTP request
    headers = request.split('\n')
    request_line = headers[0].split()
    
    if len(request_line) >= 2:
        method = request_line[0]
        path = request_line[1]
        
        # Generate a simple response
        if path == '/':
            return create_response(200, "Hello, World!")
        else:
            return create_response(404, "Not Found")
    else:
        return create_response(400, "Bad Request")

def create_response(status, body):
    status_messages = {
        200: 'OK',
        400: 'Bad Request',
        404: 'Not Found'
    }
    
    response = f"HTTP/1.1 {status} {status_messages.get(status)}\r\n"
    response += "Content-Type: text/html\r\n"
    response += f"Content-Length: {len(body)}\r\n"
    response += "\r\n"
    response += body
    
    return response

# Create server socket
server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server_socket.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)

# Bind and listen
host = '127.0.0.1'
port = 8080
server_socket.bind((host, port))
server_socket.listen(5)
print(f"HTTP Server running on http://{host}:{port}")

while True:
    # Accept connection
    client_connection, client_address = server_socket.accept()
    
    # Receive data
    request = client_connection.recv(1024).decode('utf-8')
    
    # Handle request and send response
    response = handle_request(request)
    client_connection.sendall(response.encode('utf-8'))
    
    # Close connection
    client_connection.close()
```

### Socket Options and Parameters

| Option | Description | Example |
|--------|-------------|---------|
| SO_REUSEADDR | Allow reuse of local addresses | `socket.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)` |
| SO_KEEPALIVE | Send keepalive messages | `socket.setsockopt(socket.SOL_SOCKET, socket.SO_KEEPALIVE, 1)` |
| TCP_NODELAY | Disable Nagle's algorithm | `socket.setsockopt(socket.IPPROTO_TCP, socket.TCP_NODELAY, 1)` |
| SO_RCVBUF | Receive buffer size | `socket.setsockopt(socket.SOL_SOCKET, socket.SO_RCVBUF, 8192)` |
| SO_SNDBUF | Send buffer size | `socket.setsockopt(socket.SOL_SOCKET, socket.SO_SNDBUF, 8192)` |
| SO_TIMEOUT | Set timeout | `socket.settimeout(10)` |

## Socket vs HTTP

While HTTP operates on top of sockets, they offer different levels of abstraction and are used for different purposes.

### Comparison Table

| Feature | Sockets | HTTP |
|---------|---------|------|
| Abstraction Level | Low-level (transport layer) | High-level (application layer) |
| Connection Type | Persistent until closed | Traditionally request/response (HTTP/1.x), persistent with multiplexing (HTTP/2+) |
| Communication Model | Bidirectional, full-duplex | Request-response pattern |
| Protocol | Raw TCP/UDP | Structured protocol with headers, methods, status codes |
| Use Cases | Real-time applications, custom protocols | Web browsing, API communication, document retrieval |
| Data Format | Raw bytes (application-defined) | Formatted headers and payloads (HTML, JSON, etc.) |
| State Management | Stateful (connection maintained) | Stateless (though cookies/sessions add state) |
| Implementation Complexity | Higher (manual framing, parsing) | Lower (libraries handle protocol details) |

### When to Use Sockets vs HTTP

```mermaid
graph TD
    A[Choose Communication Method] --> B{Need Real-time Communication?}
    B -- Yes --> C{Need Bidirectional Communication?}
    B -- No --> D{Standard Web Communication?}
    
    C -- Yes --> E[WebSockets or Raw Sockets]
    C -- No --> F{Need Low Latency?}
    
    D -- Yes --> G[HTTP]
    D -- No --> H{Custom Protocol Needed?}
    
    F -- Yes --> I[UDP Sockets]
    F -- No --> J[TCP Sockets]
    
    H -- Yes --> K[Custom Sockets]
    H -- No --> G
```

#### Use Sockets When:

- Building real-time applications (chat, gaming, live data)
- Implementing custom protocols
- Need for bidirectional, persistent communication
- Performance is critical (lower overhead)
- Developing low-level networking components
- Implementing non-HTTP protocols

#### Use HTTP When:

- Building web applications and services
- RESTful API design
- Document/resource retrieval
- Integration with existing web infrastructure
- Need for caching, proxying, and other web features
- Simplicity and standardization are priorities
- Cross-domain communication (with CORS)

### WebSockets: Bridging the Gap

WebSockets provide a persistent connection for two-way communication while starting with an HTTP handshake.

```mermaid
sequenceDiagram
    participant Client
    participant Server
    
    Client->>Server: HTTP Request with Upgrade Header
    Server->>Client: HTTP 101 Switching Protocols
    
    note over Client,Server: Connection upgraded to WebSocket
    
    Client->>Server: WebSocket Frame (binary/text)
    Server->>Client: WebSocket Frame (binary/text)
    Client->>Server: WebSocket Frame (binary/text)
    Server->>Client: WebSocket Frame (binary/text)
    
    note over Client,Server: Bidirectional communication continues
    
    Client->>Server: WebSocket Close Frame
    Server->>Client: WebSocket Close Frame
```

#### WebSocket Characteristics:

- Starts with HTTP handshake but switches to WebSocket protocol
- Full-duplex communication channel
- Low overhead for sending messages
- Operates over TCP (like HTTP)
- Standardized in RFC 6455
- Support for text and binary messages
- Built-in ping/pong mechanism for keep-alive

## Practical Examples

### Manual HTTP Request with Telnet

```bash
$ telnet example.com 80
Trying 93.184.216.34...
Connected to example.com.
Escape character is '^]'.

GET / HTTP/1.1
Host: example.com
Connection: close

HTTP/1.1 200 OK
Accept-Ranges: bytes
Age: 429546
Cache-Control: max-age=604800
Content-Type: text/html; charset=UTF-8
Date: Thu, 02 Sep 2021 19:15:52 GMT
Etag: "3147526947+ident"
Expires: Thu, 09 Sep 2021 19:15:52 GMT
Last-Modified: Thu, 17 Oct 2019 07:18:26 GMT
Server: ECS (nyb/1D07)
Vary: Accept-Encoding
X-Cache: HIT
Content-Length: 1256
Connection: close

<!doctype html>
<html>
<head>
    <title>Example Domain</title>
    ...
</html>
```

### Simple HTTP Request with curl

```bash
$ curl -v http://example.com
*   Trying 93.184.216.34:80...
* Connected to example.com (93.184.216.34) port 80 (#0)
> GET / HTTP/1.1
> Host: example.com
> User-Agent: curl/7.68.0
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< Accept-Ranges: bytes
< Age: 558699
< Cache-Control: max-age=604800
< Content-Type: text/html; charset=UTF-8
< Date: Thu, 02 Sep 2021 19:16:42 GMT
< Etag: "3147526947+ident"
< Expires: Thu, 09 Sep 2021 19:16:42 GMT
< Last-Modified: Thu, 17 Oct 2019 07:18:26 GMT
< Server: ECS (nyb/1D10)
< Vary: Accept-Encoding
< X-Cache: HIT
< Content-Length: 1256
< 
<!doctype html>
<html>
<head>
    <title>Example Domain</title>
    ...
</html>
```

### HTTP Request with Python Requests Library

```python
import requests

# Simple GET request
response = requests.get('https://api.github.com/users/github')
print(f"Status Code: {response.status_code}")
print(f"Headers: {response.headers}")
print(f"Content Type: {response.headers['content-type']}")
print(f"JSON Response: {response.json()}")

# POST request with JSON data
data = {'name': 'John Doe', 'email': 'john@example.com'}
post_response = requests.post('https://httpbin.org/post', json=data)
print(f"POST Response: {post_response.json()}")
```

### WebSocket Example with JavaScript

```javascript
// Client-side WebSocket
const socket = new WebSocket('wss://echo.websocket.org');

// Connection opened
socket.addEventListener('open', (event) => {
    console.log('Connected to WebSocket server');
    socket.send('Hello Server!');
});

// Listen for messages
socket.addEventListener('message', (event) => {
    console.log('Message from server:', event.data);
});

// Connection closed
socket.addEventListener('close', (event) => {
    console.log('Disconnected from WebSocket server');
});

// Connection error
socket.addEventListener('error', (event) => {
    console.error('WebSocket error:', event);
});
```

## HTTP Evolution: HTTP/1.0 to HTTP/3

HTTP has evolved significantly over the years to meet the demands of the modern web.

```mermaid
timeline
    title HTTP Protocol Evolution
    1991 : HTTP/0.9 : Simple one-line protocol<br>GET only, no headers
    1996 : HTTP/1.0 : Headers, status codes<br>Multiple methods
    1997 : HTTP/1.1 : Persistent connections<br>Host header, chunked encoding
    2015 : HTTP/2 : Multiplexing, header compression<br>Server push, binary format
    2022 : HTTP/3 : QUIC protocol (UDP)<br>Improved performance
```

### HTTP/1.0 (1996)

- First widely used version
- Request/response headers introduced
- Methods: GET, HEAD, POST
- Status codes introduced
- Content-Type for multiple document types
- One request per connection (inefficient)

```http
GET /index.html HTTP/1.0
User-Agent: Mozilla/5.0
Accept: text/html

HTTP/1.0 200 OK
Content-Type: text/html
Content-Length: 137

<html>
...
</html>
```

### HTTP/1.1 (1997)

- Persistent connections (keep-alive)
- Pipelining (limited parallelization)
- Host header (virtual hosting)
- Additional methods: PUT, DELETE, OPTIONS, etc.
- Chunked transfer encoding
- Cache control mechanisms
- 100 Continue status
- Still limited by head-of-line blocking

```http
GET /index.html HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0
Accept: text/html
Connection: keep-alive

HTTP/1.1 200 OK
Content-Type: text/html
Content-Length: 137
Connection: keep-alive

<html>
...
</html>
```

### HTTP/2 (2015)

- Binary protocol (not text-based)
- Multiplexing (multiple requests/responses over single connection)
- Header compression with HPACK
- Server push (server can send resources before client requests)
- Stream prioritization
- Still uses TCP (head-of-line blocking at transport layer)
- Requires TLS in most implementations

```
[Binary Frame Format]
HEADERS frame (stream 1) →
DATA frame (stream 1) →
← HEADERS frame (stream 1)
HEADERS frame (stream 3) →
← PUSH_PROMISE frame (stream 2)
← DATA frame (stream 1)
DATA frame (stream 3) →
← HEADERS frame (stream 2)
← DATA frame (stream 2)
```

### HTTP/3 (2022)

- Uses QUIC protocol (based on UDP) instead of TCP
- Improved connection establishment (0-RTT handshakes)
- Built-in TLS 1.3
- Independent streams (no head-of-line blocking at transport layer)
- Better handling of network changes (connection migration)
- Improved congestion control
- Inherits HTTP/2 features (multiplexing, header compression)

```
[QUIC Packet Format]
UDP Datagram →
  QUIC Header
  CRYPTO Frame (TLS handshake) →
UDP Datagram ←
  QUIC Header
  CRYPTO Frame (TLS response)
UDP Datagram →
  QUIC Header
  HTTP/3 HEADERS Frame (stream 0)
UDP Datagram ←
  QUIC Header
  HTTP/3 HEADERS Frame (stream 0)
  HTTP/3 DATA Frame (stream 0)
```

### HTTP Version Comparison

| Feature | HTTP/1.0 | HTTP/1.1 | HTTP/2 | HTTP/3 |
|---------|----------|----------|--------|--------|
| Year | 1996 | 1997 | 2015 | 2022 |
| Protocol | Text | Text | Binary | Binary |
| Transport | TCP | TCP | TCP | QUIC (UDP) |
| Connections | One per request | Persistent | Multiplexed | Multiplexed |
| Header Compression | No | No | Yes (HPACK) | Yes (QPACK) |
| Server Push | No | No | Yes | Yes |
| Prioritization | No | No | Yes | Yes |
| HOL Blocking | Yes | Yes | Transport layer only | No |
| TLS Required | No | No | De facto yes | Yes |
| Browser Support | All | All | Modern browsers | Chrome, Firefox, Safari |
| Deployment Complexity | Low | Low | Medium | High |

## RESTful API Design

REST (Representational State Transfer) is an architectural style for designing networked applications, typically using HTTP.

### REST Principles

1. **Stateless**: Server doesn't store client state between requests
2. **Client-Server**: Separation of concerns between UI and data storage
3. **Cacheable**: Responses must define themselves as cacheable or non-cacheable
4. **Uniform Interface**: Consistent resource identification and manipulation
5. **Layered System**: Client can't tell if connected directly to server
6. **Code on Demand** (optional): Server can extend client functionality

### RESTful Resource Design

```mermaid
graph TD
    A[RESTful API Design] --> B[Use Nouns for Resources]
    A --> C[Use HTTP Methods for Actions]
    A --> D[Structure Collections & Items]
    A --> E[Use HATEOAS for Navigation]
    A --> F[Return Appropriate Status Codes]
    A --> G[Use Proper HTTP Headers]
```

#### Resource Naming Examples

| Resource | URL | Description |
|----------|-----|-------------|
| Collection | `/users` | List of users |
| Specific Item | `/users/123` | User with ID 123 |
| Sub-collection | `/users/123/orders` | Orders belonging to user 123 |
| Specific Sub-item | `/users/123/orders/456` | Order 456 of user 123 |
| Filtering | `/users?status=active` | Active users only |
| Sorting | `/users?sort=name` | Users sorted by name |
| Pagination | `/users?page=2&limit=10` | Second page, 10 users per page |

#### HTTP Methods for CRUD Operations

| Operation | HTTP Method | URL | Status Code |
|-----------|-------------|-----|-------------|
| Create | POST | `/users` | 201 Created |
| Read (List) | GET | `/users` | 200 OK |
| Read (Single) | GET | `/users/123` | 200 OK |
| Update (Full) | PUT | `/users/123` | 200 OK |
| Update (Partial) | PATCH | `/users/123` | 200 OK |
| Delete | DELETE | `/users/123` | 204 No Content |

### RESTful API Example

#### Request: Create a User

```http
POST /api/users HTTP/1.1
Host: example.com
Content-Type: application/json
Authorization: Bearer token123

{
  "name": "John Doe",
  "email": "john@example.com",
  "role": "user"
}
```

#### Response: User Created

```http
HTTP/1.1 201 Created
Content-Type: application/json
Location: /api/users/456

{
  "id": 456,
  "name": "John Doe",
  "email": "john@example.com",
  "role": "user",
  "created_at": "2023-09-02T10:30:00Z",
  "_links": {
    "self": { "href": "/api/users/456" },
    "orders": { "href": "/api/users/456/orders" }
  }
}
```

#### Request: Get User Details

```http
GET /api/users/456 HTTP/1.1
Host: example.com
Accept: application/json
```

#### Response: User Details

```http
HTTP/1.1 200 OK
Content-Type: application/json
ETag: "abc123"
Cache-Control: max-age=3600

{
  "id": 456,
  "name": "John Doe",
  "email": "john@example.com",
  "role": "user",
  "created_at": "2023-09-02T10:30:00Z",
  "_links": {
    "self": { "href": "/api/users/456" },
    "orders": { "href": "/api/users/456/orders" }
  }
}
```

### API Versioning Strategies

1. **URI Path**: `/api/v1/users`
2. **Query Parameter**: `/api/users?version=1`
3. **Header**: `Accept: application/vnd.example.v1+json`
4. **Content Negotiation**: `Accept: application/json; version=1`

### HATEOAS (Hypermedia as the Engine of Application State)

HATEOAS provides dynamic navigation through resources by including links in responses.

```json
{
  "id": 456,
  "name": "John Doe",
  "_links": {
    "self": { "href": "/api/users/456" },
    "update": { "href": "/api/users/456", "method": "PUT" },
    "delete": { "href": "/api/users/456", "method": "DELETE" },
    "orders": { "href": "/api/users/456/orders" }
  }
}
```

## Practice Questions

1. How does the TCP three-way handshake contribute to HTTP's reliability? Explain the steps involved and what would happen if one step failed.

2. Compare and contrast the HTTP methods PUT, PATCH, and POST. When would you use each one in a RESTful API?

3. Explain the difference between a 301 and a 302 redirect status code. How would each affect search engine optimization and browser behavior?

4. A user reports that they received a 403 status code when trying to access a resource. What does this mean, and what troubleshooting steps would you take?

5. How does HTTP/2 multiplexing improve performance compared to HTTP/1.1? Provide specific examples of scenarios where the improvement would be most noticeable.

6. Write pseudocode for a simple socket server that accepts connections and echoes back any messages it receives. Include error handling and proper socket closure.

7. Explain how WebSockets differ from traditional HTTP communication and why they're better suited for real-time applications.

8. Design a RESTful API for a library management system with resources for books, members, and loans. Include the appropriate endpoints, HTTP methods, and status codes.

9. Compare the header compression techniques used in HTTP/2 (HPACK) and HTTP/3 (QPACK). Why was a new compression scheme needed for HTTP/3?

10. Explain the concept of head-of-line blocking in HTTP and how it's addressed differently in HTTP/1.1, HTTP/2, and HTTP/3.

## Additional Resources

- [RFC 9110: HTTP Semantics](https://datatracker.ietf.org/doc/html/rfc9110)
- [RFC 9113: HTTP/2](https://datatracker.ietf.org/doc/html/rfc9113)
- [RFC 9114: HTTP/3](https://datatracker.ietf.org/doc/html/rfc9114)
- [Mozilla Developer Network: HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP)
- [RESTful API Design Best Practices](https://restfulapi.net/)
- [Socket Programming in Python](https://realpython.com/python-sockets/)
- [HTTP Status Codes Reference](https://httpstatuses.com/)
- [Wireshark for HTTP Analysis](https://www.wireshark.org/docs/wsug_html_chunked/ChUseDisplayFilterSection.html)

---

<div align="center">
  <p>
    <a href="../day_010/README.md">⬅️ Previous Day</a> | 
    <a href="../README.md">🏠 Home</a> |
    <a href="../day_012/README.md">➡️ Next Day</a>
  </p>
</div>
