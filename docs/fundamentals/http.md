# **Introduction to HTTP**

If an **[API](/docs/fundamentals/api.md)** is the bridge that allows different software systems to communicate, then **HTTP** is one of the most common languages spoken across that bridge — especially for APIs used on the web.

HTTP stands for **Hypertext Transfer Protocol**, and it defines the rules for how clients (such as browsers or apps) and servers exchange information.

---

## **What Does "HTTP" Mean?**

* **Hypertext** – Text that contains embedded links (hyperlinks) to other documents or resources, allowing navigation between them. The term comes from systems like HTML, where documents can reference and connect to each other.
* **Transfer Protocol** – A formal set of rules for exchanging data between two systems. In HTTP, this exchange happens between a client and a server.

In short, **HTTP is a protocol that specifies how requests and responses are formatted and transmitted over the web**.

---

## **How HTTP Works**

HTTP is a request–response protocol.
A client sends a request to a server, the server processes it, and the server replies with a response.

Each HTTP message — whether it’s a request or a response — follows the same basic structure:

1. **Start line** – States the type and purpose of the message.
2. **Headers** – Provide metadata about the message.
3. **Blank line** – Separates headers from the body.
4. **Body** – Contains the main content (optional).

---

## **The Start Line**

The start line is always the first line of the message, but its format differs between requests and responses.

![Alt text for accessibility](/assets/images/HTTP_start_line.png)


### **In a Request**

Called the **request line**, it contains:

* **Method** – The action to perform (`GET`, `POST`, `PUT`, `DELETE`, etc.). *See the full list here: [HTTP methods](https://en.wikipedia.org/wiki/HTTP)*
* **Request target** – The resource path, optionally with a query string (e.g., `/search?q=Elephant`).
* **HTTP version** – Such as `HTTP/1.1`.

Example:

```
GET /search?q=Elephant HTTP/1.1
```

### **In a Response**

Called the **status line**, it contains:

* **HTTP version** – Such as `HTTP/1.1`.
* **Status code** – Numeric result code (`200`, `404`, etc.). *See the full list here: [HTTP status codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)*
* **Reason phrase** – Short text describing the status code.

Example:

```
HTTP/1.1 200 OK
```

---

## **HTTP Headers**

Headers follow the start line and provide metadata about the message. They are written as **field name: value** pairs.

Examples:

```
Authorization: Bearer abc123
Cache-Control: no-cache
Date: Tue, 12 Aug 2025 10:23:00 GMT
Host: www.example.com
```

Headers can describe content type, length, encoding, caching rules, authentication, and more. They do not contain the main content — only information about it.

---

## **The Body**

The body carries the main content of the message. It is optional:

* Many `GET` requests omit it.
* Methods like `POST` or `PUT` usually include one.
* Responses typically include one unless the status code specifies otherwise (e.g., `204 No Content`).

The body can contain various formats, such as [JSON](/docs/fundamentals/json-xml.md), [XML](/docs/fundamentals/json-xml.md), HTML, plain text, or binary data.

Example ([JSON](/docs/fundamentals/json-xml.md)):

```json
{
  "name": "Elephant",
  "type": "Animal"
}
```

---

## **Example HTTP Exchange**

### Request (Client → Server)

```
POST /api/animals HTTP/1.1
Host: www.example.com
Date: Tue, 12 Aug 2025 10:23:00 GMT
Authorization: Bearer abc123
Content-Type: application/json
Content-Length: 48

{
  "name": "Elephant",
  "type": "Animal"
}
```

### Response (Server → Client)

```
HTTP/1.1 201 Created
Date: Tue, 12 Aug 2025 10:23:01 GMT
Content-Type: application/json
Content-Length: 53

{
  "id": 27,
  "name": "Elephant",
  "type": "Animal"
}
```

In both directions, the same structure applies: **start line → headers → blank line → body**.
The difference is that requests describe what the client wants to do, while responses describe what happened.

---

## **[SOAP](/docs/fundamentals/rest-soap.md) vs [REST](/docs/fundamentals/rest-soap.md)**

APIs that use HTTP can follow different architectural styles. Two of the most well-known are **[SOAP](/docs/fundamentals/rest-soap.md)** and **[REST](/docs/fundamentals/rest-soap.md)**.

* **[SOAP](/docs/fundamentals/rest-soap.md) (Simple Object Access Protocol)** – A protocol with strict rules, typically using [XML](/docs/fundamentals/json-xml.md) for its messages. It supports advanced features like built-in error handling and security standards but is more complex and heavier in structure.

* **REST (Representational State Transfer)** – An architectural style that uses the standard HTTP methods (`GET`, `POST`, etc.) directly, often with lightweight formats like JSON. REST focuses on simplicity, statelessness, and clear resource-based URLs.

While both are still in use, **REST has become the more common choice** for web-based APIs because it is **simpler, lighter, and easier to integrate** with modern applications.

---
