# **Introduction to HTTPS**

If you haven’t yet reviewed [Introduction to APIs](/docs/fundamentals/api.md) and [Introduction to HTTP](HTTP.md), it’s worth starting there.
APIs often rely on HTTP for communication, and HTTPS builds directly on those concepts.

When you access an API, your client sends a request and receives a response from a program or service.
For most modern web-based APIs, this exchange happens over [HTTP](/docs/fundamentals/http.md) — but in its standard form, HTTP sends data in **plain text**. That means URLs, parameters, and even sensitive information can be read by anyone monitoring the network between client and server.

---

## **Why HTTPS Matters**

Plain HTTP is not safe for transmitting credentials, personal details, or business-critical information.
To protect this data, HTTP is combined with encryption — resulting in **HTTPS**, the secure version of HTTP.

The “S” stands for **Secure**, meaning that the connection uses **TLS (Transport Layer Security)** to encrypt all traffic. Encryption ensures that even if the data is intercepted, it cannot be read or altered without the correct cryptographic keys.

**In practice:**

* **HTTP** – Data travels in plain text. Anyone with access to the network can read it.
* **HTTPS** – Data is encrypted before leaving the client and decrypted by the server, making it unreadable to third parties.

---

## **How HTTPS Works in API Communication**

When you connect to an API using HTTPS, a handshake process occurs before any actual request or response is sent:

1. **Connection Request**
   The client (browser, app, or script) contacts the server over port `443` to request a secure connection.

2. **Server Certificate**
   The server sends a **digital certificate** issued by a trusted Certificate Authority (CA).
   The certificate includes:

   * The server’s public key

   * The server’s domain name (to prevent impersonation)

   * The CA’s digital signature verifying authenticity

   > **Example:** You can see a working setup in my [Inception project](https://github.com/pourist/Inception/tree/main/srcs/requirements/nginx) — the `.cert` and `.key` files in that configuration enable Nginx to serve traffic over HTTPS.

3. **Certificate Verification**
   The client checks whether:

   * The certificate is from a trusted CA
   * The domain matches the certificate
   * The certificate is valid and not expired

   If verification fails, the connection is stopped and a security warning is shown.

4. **Key Exchange**
   The client and server securely agree on a **session key**, which will be used to encrypt all subsequent communication.

5. **Encrypted Communication**
   All [HTTP](/docs/fundamentals/http.md) requests and responses are now sent through the TLS channel, ensuring confidentiality, integrity, and authenticity.

---

## **Example – API Login**

**Without HTTPS (Insecure)**

```
POST /login HTTP/1.1
Host: api.example.com
Content-Type: application/json

{
  "username": "Alice",
  "password": "mypassword123"
}
```

Anyone intercepting this could read the username and password.

**With HTTPS (Secure)**

```
POST /login HTTP/1.1
Host: api.example.com
Content-Type: application/json
```

The request body is encrypted during transit. Intercepted data appears as unreadable ciphertext.

---

## **HTTPS vs HTTP – Performance and Trust**

While HTTPS adds encryption and authentication, it does come with a small performance cost due to the TLS handshake and encryption process.
However, this overhead is minimal with modern hardware and protocols such as TLS 1.3, and is far outweighed by the benefits:

* **Confidentiality** – Prevents eavesdropping on sensitive data.
* **Integrity** – Protects against data being altered in transit.
* **Authentication** – Verifies that you are communicating with the intended server.
* **Trust** – Browsers display a secure padlock icon and warn users if a site is not secure.

For public APIs, HTTPS is now considered the default and is expected by users, browsers, and security standards.

---
