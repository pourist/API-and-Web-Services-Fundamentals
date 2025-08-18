# **OpenID Connect (OIDC)**

**OpenID Connect (OIDC)** is an identity layer built on top of the [OAuth](./oauth.md) 2.0 framework. While OAuth 2.0 provides a way for applications to obtain access tokens for delegated authorization, OIDC extends it to support **authentication** verifying the identity of the end user.

---

## **Key Concepts**

* **[Authentication vs Authorization](./authentication-vs-authorization.md)** – OAuth handles authorization (what an app can do), while OIDC adds authentication (who the user is).
* **ID Token** – A [JSON](/docs/fundamentals/json-xml.md) Web Token (JWT) issued by the authorization server that contains information about the authenticated user.
* **UserInfo Endpoint** – An API endpoint defined by OIDC that returns additional claims about the user, such as name or email.

---

## **How OIDC Works**

OIDC reuses the standard OAuth 2.0 flows (e.g., Authorization Code Grant) and adds:

1. **ID Token** – Returned alongside the access token, allowing the client to authenticate the user.
2. **Standard Claims** – Predefined attributes (e.g., `sub`, `name`, `email`) that describe the user.
3. **Discovery & Metadata** – A discovery document (`.well-known/openid-configuration`) provides endpoints and configuration details.

---

## **Example Response**

After a successful login via the Authorization Code flow with OIDC:

```json
{
  "access_token": "ACCESS_TOKEN_VALUE",
  "id_token": "eyJhbGciOi...",
  "token_type": "Bearer",
  "expires_in": 3600,
  "scope": "openid profile email"
}
```

* `id_token` – A signed JWT containing the user’s identity claims.
* `access_token` – Used to access protected APIs (as in OAuth).
* `scope` – Must include `openid` to indicate OIDC is in use.

---

## **Why OIDC Matters**

* Provides a **standard way to authenticate users** across applications.
* Works seamlessly with OAuth 2.0, avoiding the need for separate authentication systems.
* Widely used by providers such as Google, Microsoft, and Okta for single sign-on (SSO).

---

## **Summary**

OpenID Connect extends OAuth 2.0 by adding an identity layer. By introducing the **ID Token** and standard user claims, it enables both **authentication** and **authorization** in a single, unified framework. This makes it the foundation of modern single sign-on and identity federation systems.
