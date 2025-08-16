# 📘 RESTful API

## What is an API?

**API** stands for **Application Programming Interface**.  
In simple words, it is a **bridge** that allows **two different pieces of software** to communicate and understand each other.

---

## How an API Works  

Whenever you interact with an API, the communication follows a **clear structure**:

- **Request Structure** → How you **send data** to the API.  
  This includes:
  - The **HTTP method** (e.g., GET, POST, PUT, DELETE).  
  - The **endpoint (URL)** where the API lives.  
  - The **headers** (such as authentication tokens or content type).  
  - The **body** (if you’re sending extra data, usually in JSON format).  

- **Response Structure** → How the API **sends data back** to you.  
  This usually contains:
  - A **status code** (e.g., `200 OK`, `404 Not Found`, `500 Server Error`).  
  - The **headers** (like response type).  
  - The **response body**, often JSON, which carries either the requested data or an error message.  

---

## 📦 Analogy: The API as a Box  

Think of an **API like a box** that only accepts certain shapes:  
- If the box is designed for a **square, circle, or triangle**, these shapes represent the **API’s accepted standards** (the request format).  
- If you send one of these correct shapes, the box accepts it and gives you a proper result (response).  
- If you send the wrong shape, the box **rejects it** and throws an **error**.  

---

### 🔑 In short:  
An **API defines the rules of communication**.  
It makes sure that **both sides (your application and the server)** use the same “language” so they can understand each other without confusion.


---

## What is REST?

**REST** stands for **Representational State Transfer**.  
It is an **architectural style** used for communication between a **client** (like a web or mobile app) and a **server**.

Key points about REST:
- It is based on the **HTTP protocol** (using methods like `GET`, `POST`, `PUT`, `DELETE`).  
- It is **stateless** → every request from the client must contain all the information the server needs.  
- It defines a set of **constraints** (rules) for building APIs.

![REST Model](https://idempiere.org/wp-content/uploads/2025/03/restAPI.png)


---

## REST Constraints

For an API to be considered **RESTful**, it needs to follow these key rules:

1. **Client-Server** → The client (like a website or mobile app) only handles the **UI**, and the server only handles **data and logic**. This separation makes both easier to develop and scale.  

2. **Stateless** → Every request must include all the information needed (like authentication tokens, parameters, etc.). The server does **not** remember anything about the client between requests.  

3. **Cacheable** → The server should say if the response can be cached or not. This helps improve speed and performance by avoiding unnecessary repeated requests.  

4. **Uniform Interface** → A standard way to interact with the API:
   - Use **URIs** to identify resources (e.g., `/users/1`).  
   - Use **HTTP methods** (GET, POST, PUT, DELETE) to perform actions.  
   - Use common formats like **JSON** or **XML** for the data.  

5. **Layered System** → The API can work in layers (server, proxy, load balancer, etc.). The client does not need to know what happens in the background.  

👉 In short: A **RESTful API** is just an API that follows all these rules to stay consistent, scalable, and easy to use.  


---

## REST Endpoints & Methods

👉 An **endpoint** is simply the **URL** you use to make a specific request to the server.  
For example, `/products/1` is an endpoint that points to the product with ID = 1.  

Here is the standard format for REST methods and endpoints:

| HTTP Method | Endpoint Example    | Description                              |
|-------------|---------------------|------------------------------------------|
| **GET**     | `/products`         | Retrieve a list of all products.         |
| **GET**     | `/products/1`       | Retrieve a single product by ID.         |
| **POST**    | `/products`         | Create a new product.                    |
| **PUT**     | `/products/1`       | Update an existing product completely.   |
| **PATCH**   | `/products/1`       | Update part of an existing product.      |
| **DELETE**  | `/products/1`       | Delete a product by ID.                  |

---

## Resources in REST

In REST, **everything is treated as a Resource**.  
- A **Resource** can be a user, a product, an order, or any piece of data.  
- Each resource is identified by a unique **endpoint (URL)**.  
- Actions on resources are done using **HTTP methods**.

Example with **Product** as a resource:
- `GET /products` → Get all products.  
- `GET /products/1` → Get product with ID = 1.  
- `POST /products` → Create a new product.  
- `PUT /products/1` → Update product with ID = 1.  
- `DELETE /products/1` → Delete product with ID = 1.  

👉 In REST, the **resource is the main focus**, and endpoints represent resources.

---

## REST Responses

In REST, the server can return data in **JSON** or **XML** format.  

- **JSON (JavaScript Object Notation):** Most commonly used, lightweight, and easier to read and parse.  
- **XML (Extensible Markup Language):** Still supported in some cases, but less popular in modern APIs.  

### Example Response for `GET /products/1`  

**JSON format:**
```json
{
  "id": 1,
  "name": "Laptop",
  "price": 1200,
  "status": "available"
}
```

**XML format:**
```xml
<product>
  <id>1</id>
  <name>Laptop</name>
  <price>1200</price>
  <status>available</status>
</product>
```

**HTTP Header Example:**
```http
Accept: application/json
Accept: application/xml
```


---

## Common HTTP Status Codes

When you call an endpoint, the server also returns a **status code** to describe the result:

### Status Code Ranges
- **1xx → Informational** → Request received, processing continues.  
- **2xx → Success** → Request was successful.  
- **3xx → Redirection** → Client must follow a new URL.  
- **4xx → Client Errors** → Problem with the request.  
- **5xx → Server Errors** → Problem with the server.  

### Common Status Codes in REST APIs

### ✅ Success (2xx)
- **200 OK** → Request successful.  
  _Example_: `GET /api/products` returns a list of products.  

- **201 Created** → Resource created successfully.  
  _Example_: `POST /api/products` returns the created product details.  

- **204 No Content** → Request successful but no content to return.  
  _Example_: `DELETE /api/products/10` deletes the product and returns no content.  


### 🔁 Redirection (3xx)
- **301 Moved Permanently** → Resource moved permanently to a new URL.  
  ⚠️ Browsers change the HTTP method to **GET** even if the original request was **POST**.  
  _Example_: `POST /old-endpoint` will be redirected to `GET /new-endpoint`.  

- **307 Temporary Redirect** → Resource temporarily moved, **method stays the same**.  
  _Example_: `POST /checkout` → redirect to `POST /new-checkout`.  

- **308 Permanent Redirect** → Resource permanently moved, **method stays the same**.  
  _Example_: `POST /api/v1/login` → redirect to `POST /api/v2/login`.  


### ⚠️ Client Errors (4xx)
- **400 Bad Request** → Invalid request format or missing data.  
  _Example_: `POST /api/users` without required `email` field.  

- **401 Unauthorized** → Authentication required or failed.  
  _Example_: `GET /api/orders` without a valid token.  

- **403 Forbidden** → Client is authenticated but not allowed to access.  
  _Example_: `DELETE /api/admin/users/1` by a non-admin user.  

- **404 Not Found** → The resource does not exist.  
  _Example_: `GET /api/products/9999`.  

- **405 Method Not Allowed** → Method not supported for this resource.  
  _Example_: `PUT /api/login`.  

- **422 Unprocessable Entity** → Validation failed (correct format, invalid logic).  
  _Example_: `POST /api/products` with a negative price.  


### 🚨 Server Errors (5xx)
- **500 Internal Server Error** → General server error.  
  _Example_: Database connection failure.  

- **501 Not Implemented** → The server does not support the requested functionality.  
  _Example_: `PATCH /api/products/1` when PATCH is not implemented.  

- **502 Bad Gateway** → Invalid response from an upstream server.  
  _Example_: API Gateway cannot reach the backend service.  

- **503 Service Unavailable** → Server is temporarily overloaded or down.  
  _Example_: High traffic causes downtime.  

- **504 Gateway Timeout** → Server did not get a response in time.  
  _Example_: Request to a slow external payment provider.  


---

## RESTful is a Principle, Not a Language

RESTful is not a programming language or a framework.  
It is an **architectural style** (a set of principles) that you can apply to build APIs in **any language**.

For example:  
- You can build a RESTful API in **PHP (Laravel, Symfony)**.  
- Or in **JavaScript (Node.js, Express)**.  
- Or in **Python (Django, Flask, FastAPI)**.  
- Or in **Java, Go, Ruby, etc.**

👉 In short: RESTful is a **universal principle** for designing APIs, independent of the language or technology you use.
