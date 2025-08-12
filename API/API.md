# **What is an API?**

An **Application Programming Interface (API)** is a set of rules that allows different software applications to communicate with each other.
It tells one program **how to ask** another program for something, **what information** needs to be included in the request, and **how the answer** will be delivered back.

You can think of it as a bridge: it connects two separate systems so they can exchange data or trigger actions, even if they were built by different people, in different programming languages, or for different purposes.

---

## **A Simple Analogy – The Restaurant Waiter**

![Alt text for accessibility](/images/API_analogy.png)

Imagine you’re at a restaurant. You, the customer, want a specific meal from the kitchen. Instead of walking into the kitchen and making it yourself, you tell the waiter what you want from the menu.
The waiter takes your order to the kitchen, the chefs prepare it, and the waiter returns with your meal.

In this analogy:

* **You** are the client (the software requesting data or a service).
* **The waiter** is the API, carrying your request to the server and delivering the response.
* **The kitchen** is the application providing the functionality.

You don’t need to know how the kitchen works internally — you only need to know **how to ask for what you want**.

---

## **Breaking Down the Term "API"**

The name itself explains what it is:

* **Application** – The program or service that provides specific functions, such as a weather service, payment gateway, or messaging platform.
* **Programming** – The act of writing code to interact with that application.
* **Interface** – The defined way two systems can interact, whether that’s through functions, methods, or web endpoints.

Together, **Application Programming Interface** simply means:
*A defined way for code to interact with a specific application.*

---

## **When Does an API Exist?**

An API exists when there is a documented and predictable way to tell a program to interact with another application.
If a service provides functions, methods, or endpoints that external code can call, then it has an API.

---

## **Why APIs Matter**

APIs are powerful because they allow you to use existing capabilities without building them yourself.
They can be used across different platforms and programming languages, and a well-designed API remains stable over time, even as the underlying application evolves.

This means developers can:

* Build new apps that integrate existing services.
* Automate tasks that would otherwise require manual work.
* Access data and features from other systems securely and consistently.

---

## **Real-World Examples**

To make this concrete, let’s look at how APIs appear in everyday life.

**Example 1 – Weather App**
When you open a weather app on your phone, it doesn’t generate the forecast itself. Instead, it calls a weather service’s API, asking for the forecast data for your location. The app sends a request, the API retrieves the data from its system, and the result is shown on your screen.

**Example 2 – eBay API**
Suppose you want to build your own shopping app that lists products from eBay. Instead of scraping the website, you can use the official eBay API. By sending a properly formatted request (e.g., for “wireless mouse”), the API might return:

* **Title:** Logitech Wireless Mouse M185
* **Price:** 15.99 USD
* **Availability:** In stock

Your program doesn’t need to know how eBay stores its data — only how to talk to its API.

Other examples include:

* Sending a WhatsApp message through the WhatsApp API.
* Running a Google search through the Google Search API.
* Creating a new order in SAP via the SAP API.

---

Got it — I’ll weave HTTP more explicitly into both **How an API Transaction Works** and **A Practical Example** so it’s clear that HTTP is the core communication protocol in these cases.
Here’s the refined version of those two sections:

---

## **How an API Transaction Works**

Regardless of the application, most web-based API interactions follow the same **HTTP request–response cycle**:

1. **A request is sent** –
   The client (such as a browser, mobile app, or backend service) sends an **HTTP request** to the API’s server. This request includes:

   * The **URL** — the web address of the API endpoint.
   * The **HTTP method** — such as:

     * `GET` – Retrieve data.
     * `POST` – Send data or create something.
     * `PUT` / `PATCH` – Update data.
     * `DELETE` – Remove data.
   * Optional **headers** — metadata like authentication tokens, content type, or caching instructions.
   * Optional **body** — usually in JSON or XML format, containing data to be processed.

2. **The server processes the request** –
   The server-side application receives the HTTP request, executes the necessary operations (e.g., database queries, third-party API calls, business logic), and prepares the output.

3. **A response is returned** –
   The server sends back an **HTTP response** consisting of:

   * An **HTTP status code** — `200 OK` for success, `404 Not Found` if the resource doesn’t exist, `500 Internal Server Error` if something failed, etc.
   * The **response body** — usually JSON or XML containing the requested data or confirmation of the action taken.
   * Optional **response headers** — extra metadata like caching info or content type.

This cycle — **HTTP request → processing → HTTP response** — is the backbone of how most modern APIs operate.

---

## **A Practical Example – Google Search**

Typing into Google’s search bar is essentially making an **HTTP request** to Google’s servers.

* **Base URL (application location):**

  ```
  https://www.google.com
  ```
* **Path (specific function to run):**

  ```
  /search
  ```
* **Query parameter (what you’re searching for):**

  ```
  ?q=elephant
  ```

Full URL:

```
https://www.google.com/search?q=elephant
```

![Alt text for accessibility](/images/Client_server_google.png)

Here’s what happens:

1. Your browser sends an **HTTP GET** request to Google’s `/search` endpoint, including the query parameter `q=elephant`.
2. Google’s server processes the HTTP request by running its search algorithm to find relevant results.
3. Google sends back an **HTTP response** with:

   * Status code: `200 OK` (if successful).
   * Body: HTML content showing your search results.
   * Headers: Information about caching, content type, and more.
4. Your browser renders the HTML from the HTTP response, displaying the results on your screen.

This **HTTP request–response loop** is the same whether you’re fetching weather data from a weather API, retrieving products from an online store, or interacting with a social media platform’s API.

---

If you want, I can now **add a labeled HTTP transaction diagram** that applies to both sections so readers can visually connect the steps. That would make it easier to understand than just text. Would you like me to create it?


---

In short, APIs are the translators of the software world — turning your requests into actions and bringing back the results, without you ever having to see the inner workings of the system.

---
