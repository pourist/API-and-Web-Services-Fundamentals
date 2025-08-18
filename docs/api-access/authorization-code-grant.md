# **Authorization Code Grant**

The **Authorization Code Grant** is the most widely used [OAuth](./oauth.md) 2.0 flow, designed primarily for web and native applications that can securely handle client secrets and redirect URIs. It is defined in [RFC 6749 §4.1](https://www.rfc-editor.org/rfc/rfc6749.html).

This flow is preferred because it allows a client application to obtain an **access token** (and optionally a **refresh token**) through a secure server-to-server exchange, reducing exposure of sensitive credentials to the user agent.

---

## **Key Actors**

* **Resource Owner (RO)** – The user granting access to their resources.
* **User Agent** – Typically the user’s browser, which mediates between the client and the authorization server.
* **Client** – The application requesting access on behalf of the user.
* **Authorization Server** – The system that authenticates the user and issues tokens.
* **Resource Server** – The [API](/docs/fundamenals/api.md) that serves the protected resources.

---

## **Prerequisite: Client Registration (RFC 6749 §2)**

Before the flow begins, the client must be registered with the authorization server.

The client submits (via [HTTP](/docs/fundamentals/http.md) request to the authorization server):

* Application type (public or confidential)
* Redirect URIs (one or more)
* Client name and optional metadata

The authorization server responds with:

* **Client Identifier** (`client_id`)
* **Client Secret** (for confidential clients)

---

## **Flow Overview**

```
     +----------+                                  +---------------+
     | Resource |                                  | Authorization |
     |   Owner  |                                  |     Server    |
     +----------+                                  +---------------+
          ^                                              ^      v
          |                                              |      |
         (B)                                             |      |
     +----|-----+          Client Identifier      +-------|-------+
     |  User-   +----(A)-- & Redirection URI ---->| Authorization |
     |  Agent   |                                 |   Endpoint    |
     |          +----(B)-- User authenticates --->|               |
     |          |                                 |               |
     |          +----(C)-- Authorization Code ---<|               |
     +----|-----+                                  +---------------+
          |                                             ^      v
         (A)                                           (D)    (E)
          |                                             |      |
          v                                             |      |
     +---------+                                        |      |
     |  Client |----------------------------------------'      |
     |         |<------------------- Access Token -------------'
     +---------+       (and optionally Refresh Token)
```

**Steps (RFC 6749 §4.1):**

1. **Authorization Request (A)** – The client directs the user agent to the authorization server’s authorization endpoint.
2. **User Authentication & Consent (B)** – The resource owner authenticates and approves the request.
3. **Authorization Code Grant (C)** – The authorization server redirects the user agent back to the client’s redirect URI with an **authorization code**.
4. **Token Request (D)** – The client exchanges the authorization code for an access token via a direct request to the authorization server’s token endpoint.
5. **Token Response (E)** – The authorization server responds with an access token (and optional refresh token).

---

## **Authorization Request (RFC 6749 §4.1.1)**

The client constructs an [HTTP](/docs/fundamentals/http.md) request to the **authorization endpoint**, typically triggered by a user clicking a login or connect button.

**Example:**

```
GET /authorize?response_type=code&client_id=CLIENT_ID
    &redirect_uri=https://client.example.com/callback
    &scope=read%20write
    &state=xyz123 HTTP/1.1
Host: auth.example.com
```

* `response_type=code` – Indicates Authorization Code flow.
* `client_id` – Issued during registration.
* `redirect_uri` – Must exactly match a registered URI.
* `scope` – Permissions requested.
* `state` – Random string to prevent CSRF.

---

## **Authorization Response (RFC 6749 §4.1.2)**

If the user approves, the authorization server redirects the user agent to the client’s redirect URI with an **authorization code**.

**Example:**

```
HTTP/1.1 302 Found
Location: https://client.example.com/callback?code=AUTH_CODE&state=xyz123
```

* `code` – Short-lived authorization code.
* `state` – Returned unchanged for CSRF protection.

Notes:

* The code is one-time use.
* Codes expire quickly (typically 1–10 minutes).

---

## **Access Token Request (RFC 6749 §4.1.3)**

The client exchanges the authorization code for an access token. This request is made **server-to-server** and requires client authentication.

**Example (HTTP POST):**

```
POST /token HTTP/1.1
Host: auth.example.com
Content-Type: application/x-www-form-urlencoded

 grant_type=authorization_code
 &code=AUTH_CODE
 &redirect_uri=https://client.example.com/callback
 &client_id=CLIENT_ID
 &client_secret=CLIENT_SECRET
```

---

## **Access Token Response (RFC 6749 §4.1.4)**

If valid, the authorization server issues an **access token**, and optionally a **refresh token**.

**Example:**

```json
{
  "access_token": "ACCESS_TOKEN_VALUE",
  "token_type": "Bearer",
  "expires_in": 3600,
  "refresh_token": "REFRESH_TOKEN_VALUE",
  "scope": "read write"
}
```

* `access_token` – Used to access protected resources.
* `token_type` – Typically `Bearer`.
* `expires_in` – Lifetime in seconds.
* `refresh_token` – Used to obtain new access tokens.
* `scope` – Granted permissions (may differ from requested scope).

---

## **Security Considerations**

* **State parameter** – Prevents CSRF by binding requests and responses.
* **PKCE (Proof Key for Code Exchange)** – Recommended for public clients (native/mobile apps) to protect against code interception.
* **Redirect URI validation** – Must match exactly what is registered.
* **One-time codes** – Authorization codes must be used once and expire quickly.
* **Confidential clients** – Must protect `client_secret`.

---

## **Common Errors**

* `invalid_request` – Missing or malformed parameter.
* `unauthorized_client` – Client not authorized to use this grant.
* `access_denied` – Resource owner denied request.
* `unsupported_response_type` – Wrong or unsupported `response_type`.
* `invalid_grant` – Code expired, already used, or mismatched `redirect_uri`.
* `invalid_client` – Client authentication failed.

---

## **Example Walkthrough**

1. User clicks **Login with Example**.
2. Browser redirects to `https://auth.example.com/authorize?...`.
3. User logs in and approves access.
4. Authorization server redirects back:

   ```
   https://client.example.com/callback?code=abc123&state=xyz123
   ```
5. Client exchanges code:

   ```
   POST /token
   grant_type=authorization_code&code=abc123&redirect_uri=...
   ```
6. Server responds with tokens:

   ```json
   {
     "access_token": "abcd1234",
     "token_type": "Bearer",
     "expires_in": 3600,
     "refresh_token": "r12345"
   }
   ```

The client can now call the resource server with the access token in the `Authorization: Bearer` header.

---

## **Summary**

The Authorization Code Grant is the most secure and commonly used [OAuth](./oauth.md) 2.0 flow. It separates the user-facing authentication step from the secure token exchange, ensures client authentication, and enables refresh tokens for long-term access. For public clients, PKCE adds essential protection against code interception attacks.
