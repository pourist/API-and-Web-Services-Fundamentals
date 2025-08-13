Here’s your **updated Introduction to JSON and XML** with all the improvements applied:

---

# **Introduction to JSON and XML**

When **[APIs](/docs/fundamentals/api.md)** exchange data over **[HTTP](/docs/fundamentals/http.md)** or **[HTTPS](/docs/fundamentals/https.md)**, the **body** of the request or response often contains information in a structured format.
Two of the most common formats are **JSON** and **XML**.

---

## **What is JSON?**

**JSON** stands for **JavaScript Object Notation** — a **lightweight, text-based format** for storing and transferring data.
It is easy for humans to read, efficient for machines to parse, and supported by virtually all modern programming languages.

While JSON’s syntax comes from JavaScript object literals, it is **language-independent**.

**Content-Type header for JSON:**

```
Content-Type: application/json
```

---

### **Structure of JSON**

JSON represents data as **key–value pairs**:

* **Keys**: Always strings enclosed in double quotes (`" "`).
* **Values**: Can be strings, numbers, booleans, arrays, objects, or `null`.

**Core elements:**

* **Object** – Unordered key–value pairs, inside `{ }`.
* **Array** – Ordered list of values, inside `[ ]`.

**Example – Pizza Order (JSON):**

```json
{
  "pizza": [
    {
      "size": "small",
      "toppings": ["onions", "mushrooms"]
    }
  ]
}
```

Here:

* `"pizza"` → key, value is an array.
* Array contains an object with:

  * `"size"` → `"small"`
  * `"toppings"` → array of strings.

[Full JSON specification](https://www.json.org/json-en.html)

---

## **What is XML?**

**XML** stands for **Extensible Markup Language** — a **markup language** for storing and transporting data using custom-defined tags.
Unlike HTML, XML has no predefined tags and is purely focused on representing structured information.

**Content-Type header for XML:**

```
Content-Type: application/xml
```

---

### **Structure of XML**

* Data enclosed in **start** and **end** tags: `<tag> ... </tag>`
* Tags are **case-sensitive**.
* XML must be **well-formed** — correct nesting, one root element, proper attribute use.

**Example – Pizza Order (XML):**

```xml
<pizza>
  <order>
    <size>small</size>
    <toppings>
      <topping>onions</topping>
      <topping>mushrooms</topping>
    </toppings>
  </order>
</pizza>
```

Here:

* `<pizza>` → root element.
* `<order>` → contains `<size>` and `<toppings>`.
* `<toppings>` → contains multiple `<topping>` elements.

---

## **JSON vs XML**

| Feature           | JSON                                              | XML                                          |
| ----------------- | ------------------------------------------------- | -------------------------------------------- |
| **Full Name**     | JavaScript Object Notation                        | Extensible Markup Language                   |
| **Introduced**    | 2001                                              | 1997                                         |
| **Syntax Style**  | Key–value pairs, arrays, objects                  | Nested tags with attributes                  |
| **Verbosity**     | Compact                                           | More verbose                                 |
| **Data Types**    | Strings, numbers, booleans, null, arrays, objects | All text; type parsing required              |
| **Readability**   | Simple, human-friendly                            | More structured but heavier                  |
| **Extensibility** | Limited (fixed structure)                         | Highly extensible (custom tags, attributes)  |
| **Usage Trend**   | Increasing                                        | Stable in enterprise, decreasing in web APIs |
| **Best For**      | Lightweight web APIs                              | Complex documents, metadata-rich data        |

---

**Summary:**

* **JSON** dominates modern API design due to its compactness and ease of use.
* **XML** remains important in enterprise, finance, government, and cases requiring complex metadata or strict validation.

---
