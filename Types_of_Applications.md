# **Types of Applications – Native, Web, and Hybrid**

Understanding the different types of applications is important because the way an app is built affects how it can interact with **[APIs](API.md)** and what device features it can use.
Modern applications can be broadly grouped into three main categories: **native apps**, **web apps**, and **hybrid apps**.
Each type interacts with devices and operating systems differently, with trade-offs in performance, cost, and access to device capabilities.

---

## **1. Native Applications**

A **native app** is built to run directly on a specific operating system (OS), such as **iOS**, **Android**, or **Windows**.

### **What is an Operating System?**

An **OS** is the software layer that manages the device’s hardware and provides system-level services. It exposes **[APIs](API.md)** — predefined ways for apps to request and use features of the device.

* **Low-level APIs** – Direct access to hardware capabilities, such as vibration, microphone, camera, GPS location, or phone calls.
* **High-level APIs** – Ready-made services like calendar integration, push notifications, email handling, or contacts management.

When you install a native app, it has direct access to these OS APIs.
For example, **Google Translate** on Android can request location data through the OS API to offer region-specific translations.

![Alt text for accessibility](/images/Native_App.png)

Native apps are **downloaded and installed** through app stores, and because they are built for a specific platform, they typically offer:

* **Better performance** (optimized for the OS)
* **Full access** to device features
* **High-quality user experience**

---

## **2. Web Applications**

A **web app** runs inside a web browser rather than directly on the operating system.
It is limited to the APIs that the browser itself exposes — meaning it cannot directly access OS-level features like vibration or native push notifications (unless supported through browser standards).

![Alt text for accessibility](/images/Web_App.png)

Browser APIs include examples such as:

* **Geolocation API** – Get the user’s location (with permission)
* **Web Storage API** – Store small amounts of data locally in the browser
* **Notifications API** – Display system notifications from a web page

Web apps are usually built with **HTML**, **CSS**, and **JavaScript**, and they run on any device with a compatible browser.

**Advantages:**

* **Platform independence** – Design once, run everywhere
* **No installation required** – Access via a URL
* **Lower development cost** compared to building separate native apps for multiple OSs

**Limitations:**

* **Restricted access** to device hardware and OS services
* **Performance** can be slower than native apps for complex, resource-heavy tasks

---

## **3. Hybrid Applications**

A **hybrid app** combines elements of both native and web apps.

There are two main approaches:

1. **Native shell + embedded web content** – The app is a native container that displays web content inside it, often through a **WebView** component. This allows developers to reuse web code while still accessing some native APIs.
2. **Middleware frameworks** – Tools like Ionic, React Native, or Capacitor act as a bridge between JavaScript code and native APIs, letting developers write in web technologies but still tap into OS features.

Hybrid apps aim to balance development efficiency with access to device capabilities.
Examples include **Uber**, which uses a hybrid model to combine native performance with reusable web components, and many banking apps that embed account pages as web views.

---

## **Quick Comparison**

| Feature               | Native App          | Web App           | Hybrid App                |
| --------------------- | ------------------- | ----------------- | ------------------------- |
| **Runs on**           | Directly on OS      | In a browser      | On OS with web/middleware |
| **Device API Access** | Full                | Limited (browser) | Partial via bridging      |
| **Performance**       | High                | Medium–Low        | Medium–High               |
| **Development Cost**  | High (per platform) | Low (single code) | Medium                    |
| **Installation**      | App store           | URL only          | App store                 |

---
