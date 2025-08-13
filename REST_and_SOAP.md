# **Introduction to REST and SOAP**

When an **[API](API.md)** communicates over **[HTTP](HTTP_intro.md)**, the client sends a request to a server, and the server sends back a response.
How this communication is **structured** depends on the architectural style or protocol the API follows.
Two of the most widely known approaches are **SOAP** and **REST**.

---

## **SOAP – Simple Object Access Protocol**

SOAP is a **protocol** — meaning it has strict rules for how requests and responses must be formatted.
It can operate over various transport protocols ([HTTP](HTTP_intro.md), SMTP, etc.), but in web APIs it most often runs over HTTP.
SOAP services are typically described using a **WSDL** (Web Services Description Language) file, which defines the available operations and message formats.

**Example – Searching “elephant” in SOAP:**

1. The client sends an **HTTP POST** request to the server.
2. The request body contains an **[XML](JSON_and_XML.md) message** following SOAP’s envelope structure.
3. The server processes the request and returns a **SOAP XML response**.

**SOAP Request Structure:**

* **Start line**: Always `POST /endpoint HTTP/1.1`
* **Headers**:

  ```
  Content-Type: text/xml
  ```
* **Blank line**
* **Body**: [XML](JSON_and_XML.md) in SOAP envelope format.

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
RESTful APIs are **stateless** — each request contains all the information needed for the server to process it.

REST makes full use of HTTP methods to describe the action being taken:

| Method   | Purpose                     | Example                                                         |
| -------- | --------------------------- | --------------------------------------------------------------- |
| `GET`    | Retrieve data               | `GET /animals/elephant` – Fetch details about an elephant.      |
| `POST`   | Create new data             | `POST /animals` with a JSON body to add a new animal.           |
| `PUT`    | Update an existing resource | `PUT /animals/27` to replace the elephant record with new data. |
| `DELETE` | Remove a resource           | `DELETE /animals/27` to remove the elephant entry.              |

---

**Example – Searching “elephant” in REST:**

1. Send an HTTP request to a resource URL such as `/search?q=elephant`.
2. The **HTTP method** specifies the action.
3. REST can return data in **[JSON](JSON_and_XML.md)**, **[XML](JSON_and_XML.md)**, HTML, images, or other formats — JSON is most common.
4. The server responds with a status code and the requested data.

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
* **REST** is lightweight, stateless, and has become the dominant style for modern web [API](API.md)s due to its simplicity and flexibility.

