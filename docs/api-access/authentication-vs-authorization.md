# **Authentication vs Authorization**

When interacting with [API](/docs/fundamentals/api.md)s or web services, two important concepts often appear together but serve very different purposes: **authentication** and **authorization**.

---

## **Authentication – Proving Identity**

**Authentication** is the process of confirming **who you are**.
It ensures that the client making a request is a real and valid user or system.

Common methods include:

* **Username and password**
* **API keys**
* **[OAuth](./oauth.md) tokens**
* **Biometrics** (fingerprints, face ID, etc.)

**Example:**

* You log in to an API using your email and password.
* The system verifies your credentials.
* If correct, you are **authenticated** , your identity has been proven.

---

## **Authorization – Defining Access**

**Authorization** determines **what you are allowed to do** after your identity is known.
It controls access to specific resources, data, or actions.

Authorization often depends on roles, permissions, or scopes assigned to the authenticated user.

**Example:**

* After logging in (authenticated), you can access your profile.
* But you may not be allowed to delete another user’s account, that requires higher authorization.

---

## **Authentication vs Authorization**

| Aspect         | Authentication              | Authorization                                      |
| -------------- | --------------------------- | -------------------------------------------------- |
| **Definition** | Proves identity             | Grants or restricts access                         |
| **Answers**    | “Who are you?”              | “What are you allowed to do?”                      |
| **Process**    | Happens first               | Happens after authentication                       |
| **Example**    | Logging in with a password  | Checking if the logged-in user can edit a resource |
| **Techniques** | Passwords, API keys, tokens | Roles, permissions, access control lists           |


---
