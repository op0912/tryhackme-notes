# HTTP — TryHackMe Notes (Integrated)

## HTTP — Structure & Behavior

All concepts described here are further detailed in the corresponding sub-blocks of my Payloab_Fx repository:

- [B2 — Transport Layer](https://github.com/op0912/Payloab_Fx/blob/main/B/B2_transport.md)
- [B3 — Services](https://github.com/op0912/Payloab_Fx/blob/main/B/B3_Services.md)
- [B4 — Web Services (Ports)](https://github.com/op0912/Payloab_Fx/blob/main/B/B4_ports/Web%20Services.md)

## Core Concept (B3)

HTTP = communication protocol between client and server

- client sends request  
- server sends response  
- stateless → no memory between requests  

---

## Request / Response Structure (B2, B3)

HTTP communication is structured:

[START LINE]  
[HEADERS]

[BODY]

→ empty line separates headers and body

---

## HTTP Request Example (B2)

POST /login HTTP/1.1
Host: site.com
User-Agent: Mozilla/5.0
Content-Type: application/json
Content-Length: 48
Cookie: session=abc123

{"username":"admin","password":"test123"}

---

## HTTP Response Example (B2)

HTTP/1.1 200 OK
Content-Type: text/html
Set-Cookie: session=xyz789

<html>...</html>

---

## HTTP Methods (B3)

- GET → retrieve data  
- POST → send / create  
- PUT → update  
- DELETE → remove  

→ method defines the action requested to the server

---

## HTTP Status Codes (B3)

### Categories

- 1xx → informational  
- 2xx → success  
- 3xx → redirection  
- 4xx → client error  
- 5xx → server error  

### Important Codes

- 200 → OK  
- 201 → Created  
- 301 / 302 → Redirect  
- 400 → Bad Request  
- 401 → Unauthorized  
- 403 → Forbidden  
- 404 → Not Found  
- 500 → Internal Error  
- 503 → Service Unavailable  

→ server response behavior indicator

---

## Headers (B2, B3)

Headers = metadata sent with requests and responses

Format:
key: value

---

### Request Headers (B2)

- Host → target domain  
- User-Agent → client identity  
- Content-Type → data format  
- Content-Length → body size  
- Accept-Encoding → compression support  
- Cookie → session / identity  

---

### Response Headers (B2)

- Set-Cookie → assigns session  
- Content-Type → response format  
- Content-Encoding → compression used  
- Cache-Control → caching rules  
- Server → server info  

---

## Body (B2)

Body = actual data

- used mainly in POST / PUT  
- contains payload (JSON, form data, etc.)

Example:

{"username":"admin","password":"test123"}

---

## Cookies (B2, B3)

HTTP is stateless → needs a way to remember user

Cookies provide session persistence

---

### Cookie Flow

1. Server sends:
Set-Cookie: session=abc123  

2. Browser stores  

3. Client sends:
Cookie: session=abc123  

---

### Key Understanding

Cookie = user identity proof

→ server does not remember you  
→ you re-identify yourself every request  

---

## Real Behavior (THM Insight) (B2, B4)

A single webpage triggers multiple HTTP requests:

- HTML  
- CSS  
- JavaScript  
- images  
- API calls  

Each uses:

- HTTP/HTTPS  
- specific ports (80 / 443 / 8080)  
- separate connections  

---

## HTTP vs HTTPS (B3, B4)

HTTP:
- unencrypted  
- readable / modifiable  

HTTPS:
- encrypted via TLS  
- authenticated  
- integrity protected  

→ HTTPS = HTTP over TLS (port 443)

---

## Key Insight (B2, B3, B4)

A website is not a single request

It is:

- multiple HTTP requests  
- each independent  
- linked by cookies  
- secured by TLS  
- exposed via ports  

---

## Final Understanding

HTTP =

- method → action  
- URL → target  
- headers → context  
- body → data  
- cookies → identity  
- status code → result  

→ everything in web communication follows this model
