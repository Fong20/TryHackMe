# Web Application Basics

## Uniform Resource Locator (URL)
A URL is a web address that guides the browser to the correct online resource.

### Anatomy of a URL
1. **Scheme** - Defines the protocol (e.g., `http`, `https`). HTTPS is secure.
2. **User** - May contain login details (rare due to security risks).
3. **Host/Domain** - The unique website address (beware of typosquatting).
4. **Port** - Directs traffic (e.g., `80` for HTTP, `443` for HTTPS).
5. **Path** - Specifies the resource on the server.
6. **Query String** - Starts with `?`, used for searches or parameters.
7. **Fragment** - Starts with `#`, points to a specific section on a webpage.

## HTTP Messages
HTTP messages are exchanged between clients and servers.

### Types of HTTP Messages
1. **HTTP Requests** - Sent by clients to request data/actions.
2. **HTTP Responses** - Sent by servers with requested data or status messages.

### Structure of HTTP Messages
1. **Start Line** - Defines request/response type.
2. **Headers** - Contain metadata about the message.
3. **Empty Line** - Separates headers from the body.
4. **Body** - Contains data (e.g., form submissions, JSON, files).

## HTTP Requests
### Request Line Format
`METHOD /path HTTP/version`

### HTTP Methods and Security Considerations
- **GET** - Fetches data (avoid exposing sensitive info in URLs).
- **POST** - Sends data (validate inputs to prevent SQL/XSS attacks).
- **PUT** - Updates resources (check authorization before accepting).
- **DELETE** - Removes resources (restrict to authorized users).
- **PATCH** - Partially updates a resource.
- **HEAD** - Retrieves headers only.
- **OPTIONS** - Lists allowed methods.
- **TRACE** - Used for debugging (disable for security reasons).
- **CONNECT** - Establishes secure tunnels (e.g., HTTPS).

### Request Headers
- **Host** - Identifies the web server.
- **User-Agent** - Specifies browser/client details.
- **Referer** - Indicates the request source.
- **Cookie** - Stores session data.
- **Content-Type** - Defines request data format.

### Request Body Formats
1. **URL Encoded (`application/x-www-form-urlencoded`)** - Key-value pairs.
2. **Form Data (`multipart/form-data`)** - For file uploads.
3. **JSON (`application/json`)** - Structured data format.
4. **XML (`application/xml`)** - Hierarchical data format.

## HTTP Responses
### Status Line Components
- **HTTP Version** - Protocol version.
- **Status Code** - Three-digit number indicating request outcome.
- **Reason Phrase** - Human-readable message.

### Status Code Categories
1. **1xx (Informational)** - Request received, continue.
2. **2xx (Success)** - Request processed successfully.
3. **3xx (Redirection)** - Resource moved, follow new URL.
4. **4xx (Client Errors)** - Invalid request (e.g., `404 Not Found`).
5. **5xx (Server Errors)** - Server issues (e.g., `500 Internal Server Error`).

### Common Response Headers
- **Date** - Server response timestamp.
- **Content-Type** - Specifies content format.
- **Server** - Indicates server software (avoid exposing for security).
- **Set-Cookie** - Sends cookies to client.
- **Cache-Control** - Defines caching behavior.
- **Location** - Specifies redirection URL.

### Response Body
Contains requested data (HTML, JSON, etc.). Always sanitize data to prevent XSS.

## Security Headers
### **Content-Security-Policy (CSP)**
Restricts allowed content sources to prevent XSS attacks.
Example: `Content-Security-Policy: default-src 'self'; script-src 'self' https://cdn.example.com; style-src 'self'`

### **Strict-Transport-Security (HSTS)**
Forces HTTPS connections.
Example: `Strict-Transport-Security: max-age=63072000; includeSubDomains; preload`

### **X-Content-Type-Options**
Prevents MIME-type sniffing.
Example: `X-Content-Type-Options: nosniff`

### **Referrer-Policy**
Controls referrer information sharing.
Examples:
- `no-referrer` - No referrer data.
- `same-origin` - Referrer only sent within the same origin.
- `strict-origin` - Referrer sent if protocol matches.
- `strict-origin-when-cross-origin` - Referrer sent in full for same-origin requests, limited for cross-origin.

### Summary
- Understanding URLs and HTTP messages is crucial for web security.
- Implement secure headers to protect applications from common attacks.

