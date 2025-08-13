# **Introduction to REST and SOAP**

When an **[API](/docs/fundamentals/api.md)** communicates over **[HTTP](/docs/fundamentals/http.md)**, the client sends a request to a server, and the server sends back a response.
How this communication is **structured** depends on the architectural style or protocol the API follows.
Two of the most widely known approaches are **SOAP** and **REST**.

---

## **SOAP – Simple Object Access Protocol**

SOAP is a **protocol** — meaning it has strict rules for how requests and responses must be formatted.
It can operate over various transport protocols ([HTTP](/docs/fundamentals/http.md), SMTP, etc.), but in web APIs it most often runs over HTTP.
SOAP services are typically described using a **WSDL** (Web Services Description Language) file, which defines the available operations and message formats.

**Example – Searching “elephant” in SOAP:**

1. The client sends an **HTTP POST** request to the server.
2. The request body contains an **[XML](/docs/fundamentals/json-xml.md) message** following SOAP’s envelope structure.
3. The server processes the request and returns a **SOAP XML response**.

**SOAP Request Structure:**

* **Start line**: Always `POST /endpoint HTTP/1.1`
* **Headers**:

  ```
  Content-Type: text/xml
  ```
* **Blank line**
* **Body**: [XML](/docs/fundamentals/json-xml.md) in SOAP envelope format.

**Example SOAP HTTP request:**

```http
POST /search HTTP/1.1
Host: api.example.com
Content-Type: text/xml

<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <SearchRequest>
      <Query>elephant</Query>
    </SearchRequest>
  </soap:Body>
</soap:Envelope>
```

---

## **REST – Representational State Transfer**

REST is an **architectural style** rather than a strict protocol.
It was introduced as a simpler, more flexible way to build web APIs using HTTP’s existing features directly.

Unlike SOAP, REST makes full use of HTTP methods to describe the action being taken.

**Core HTTP Methods in REST:**

| Method   | Purpose                     | Example                                                         |
| -------- | --------------------------- | --------------------------------------------------------------- |
| `GET`    | Retrieve data               | `GET /animals/elephant` – Fetch details about an elephant.      |
| `POST`   | Create new data             | `POST /animals` with a JSON body to add a new animal.           |
| `PUT`    | Update an existing resource | `PUT /animals/27` to replace the elephant record with new data. |
| `DELETE` | Remove a resource           | `DELETE /animals/27` to remove the elephant entry.              |

---

### **How REST Works (example)**

Searching “elephant” in a REST API:

1. You send an HTTP request directly to a resource URL.
2. The **HTTP method** in the start line tells the server what action to take.
3. REST can return data in **[JSON](JSON_XML.md)**, XML, images, or other formats — JSON is most common.
4. The server responds with a status code and the requested data.

**REST Request Structure:**

* **Start line**:
  Example:

  ```
  GET /search?q=elephant HTTP/1.1
  ```
* **Headers**:

  ```
  Content-Type: application/json
  ```
* **Blank line**
* **Body**: Optional — used for `POST` and `PUT` requests, often JSON.

**Example REST HTTP request:**

```http
GET /search?q=elephant HTTP/1.1
Host: api.example.com
Content-Type: application/json
```

**Example REST HTTP response:**

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
  "results": [
    {
      "name": "African Elephant",
      "species": "Loxodonta africana",
      "status": "Vulnerable"
    },
    {
      "name": "Asian Elephant",
      "species": "Elephas maximus",
      "status": "Endangered"
    }
  ]
}
```

---

## **SOAP vs REST – Key Differences**

| Feature                  | SOAP                                         | REST                                        |
| ------------------------ | -------------------------------------------- | ------------------------------------------- |
| **Type**                 | Protocol (strict rules)                      | Architectural style (flexible)              |
| **HTTP Method**          | Always `POST`                                | Uses all standard HTTP methods              |
| **Data Format**          | XML only                                     | JSON, XML, HTML, images, etc.               |
| **Verbosity**            | More verbose                                 | More compact                                |
| **Standards Compliance** | Requires strict SOAP envelope and XML schema | Few constraints; follows general HTTP rules |
| **State Management**     | Stateful or stateless                        | Stateless                                   |
| **Ease of Use**          | More complex                                 | Simpler to implement                        |

---

**Summary:**

* **SOAP** is rigid, XML-based, and suited for enterprise systems needing strong contracts and formal standards.
* **REST** is lightweight, stateless, and has become the dominant style for modern web [API](/docs/fundamentals/api.md)s due to its simplicity and flexibility.
