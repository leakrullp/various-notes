

# Lecture 7: Web APIs (RESTful Web Services)

## What are Web Services?

Web Services are software services exposed on the internet so other applications can consume their functionality. A client sends a request over the internet, the server processes it via the web service, and returns a response — for example, requesting weather data for a zip code and receiving a forecast back.

Key characteristics include loose coupling between clients and servers, platform independence, service evolution (APIs can grow without breaking existing clients), and reliance on web standards like HTTP, XML, and JSON.

---

## SOAP vs REST

There are two main web service standards. **SOAP** (Simple Object Access Protocol) is XML-based, uses WSDL for service description, and underpins Service-Oriented Architecture (SOA). **RESTful services** are based on the REST architectural style, use JSON, and are described with the OpenAPI specification. REST is dominant today — it's easier to develop, less verbose, and scales better in cloud environments. Companies like Amazon, Netflix, and Twitter all use RESTful APIs.

---

## REST Architectural Style

REST is built around the concept of a **resource** — any object, data, or service a client can access. Each resource has a unique URI:

```
https://abc.com/customers/7835
```

When a client calls a RESTful API, the server returns a **representation of the state** of that resource — usually as JSON:

json

```json
{ "customerID": 7835, "customerName": "John Johnson" }
```

REST APIs are **stateless** — each HTTP request is independent and self-contained.

---

### HTTP Protocol

HTTP messages (both requests and responses) share the same structure:

|Element|Description|
|---|---|
|Start-line|The HTTP method + target resource (request), or status code (response)|
|Headers|Meta-information (Content-Type, Accept, cookies, etc.)|
|Blank line|Marks end of headers|
|Body|Optional data payload|

**Common HTTP methods used in REST:**

|Method|Purpose|
|---|---|
|GET|Retrieve a resource|
|POST|Create a new resource|
|PUT|Create or replace a resource|
|PATCH|Partially update a resource|
|DELETE|Remove a resource|

**Common status codes:**

- `200 OK` — success
- `201 Created` — resource created
- `400 Bad Request` — malformed request
- `404 Not Found` — resource doesn't exist
- `500 Internal Server Error` — server-side failure

**Media types** (MIME types) declare the format of the body:

- `application/json` — JSON data
- `application/xml` — XML data
- `text/plain` — plain text

Example request/response with JSON:

http

```http
POST https://adventure-works.com/orders HTTP/1.1
Content-Type: application/json; charset=utf-8

{"Id": 1, "Name": "Gizmo", "Category": "Widgets", "Price": 1.99}
```

http

```http
GET https://adventure-works.com/orders/2 HTTP/1.1
Accept: application/json
```

---

### JSON Format

JSON (JavaScript Object Notation) is the most common data format for REST APIs. It derives from JavaScript object syntax and is less verbose than XML.

**Name/value pair:**

json

```json
"firstName": "John"
```

**Object (curly braces):**

json

```json
{ "firstName": "John", "lastName": "Doe" }
```

**Array (square brackets):**

json

```json
[
  { "firstName": "John", "lastName": "Doe" },
  { "firstName": "Anna", "lastName": "Smith" },
  { "firstName": "Peter", "lastName": "Jones" }
]
```

**Valid JSON value types:** string, number, object, array, boolean, null. Functions, dates, and `undefined` are not valid JSON values.

**Nested example:**

json

```json
{
  "companyName": "ACME ApS",
  "address": {
    "streetAddress": "Forårsvej",
    "city": "Charlottenlund",
    "postalCode": "2920"
  },
  "employees": [
    { "firstName": "John", "lastName": "Doe", "salary": 56000 },
    { "firstName": "Anna", "lastName": "Smith", "salary": 56000 }
  ]
}
```

**Converting between JSON and JavaScript:**

js

````js
// Parse JSON string → JS object
const myObj = JSON.parse('{"name":"John", "age":31}');

// Stringify JS object → JSON string
const myJSON = JSON.stringify({ name: "John", age: 31 });
```

Known caveats: dates become strings, cyclic object graphs aren't supported, and class instances lose their constructor.

Related standards: **JSON Schema** for validating structure, **JSON Patch** for describing partial updates (used with HTTP PATCH).

---

### Designing RESTful APIs

**Step 1 — Identify resources and URIs**

Focus on business entities. URIs should be nouns, not verbs:
```
✓ /customers
✗ /create-customer
```

Organise into a hierarchy (max 2–3 levels deep):
```
/customers
/customers/{customerId}
/customers/{customerId}/orders
/orders/{orderId}
/orders/{orderId}/items
```

URI templates use curly braces for variables:
```
/customers/{customerId}/orders/{orderId}
→ /customers/7835/orders/8765
```

**Step 2 — Map operations to HTTP methods**

| Resource | POST | GET | PUT | DELETE |
|---|---|---|---|---|
| `/customers` | Create customer | Get all customers | Bulk update | Remove all |
| `/customers/{id}` | Error | Get customer | Update customer | Remove customer |
| `/customers/{id}/orders` | Create order | Get all orders | Bulk update orders | Remove all orders |

**Step 3 — Define operation details**

Document parameters, status codes, and request/response bodies. Example template:
```
Path:    /customers/{customerId}
Method:  GET
Summary: Retrieve details for a customer.

URL Params:
  customerId: number, required in path

Success Response:
  Code: 200 OK
  Body: { "customerId": 12, "customerName": "John Johnson" }

Error Response:
  Code: 404 NOT FOUND
  Body: { "error": "Customer doesn't exist" }
````

---

### OpenAPI Specification

OpenAPI (formerly Swagger) is a standard for formally describing RESTful APIs in YAML or JSON. It captures endpoints, operations, parameters, authentication, and more. Tools like Postman and the Swagger VS Code extension support it, and some can auto-generate client code.

---

### Consuming RESTful APIs (Fetch API)

The **Fetch API** is a promise-based browser API for calling web services, introduced in 2017. For Node.js, use the `node-fetch` package.

**Generic GET:**

js

```js
async function getData(url = '') {
  const response = await fetch(url, {
    method: 'GET',
    headers: { 'Accept': 'application/json' }
  });
  return response.json(); // parses JSON response body
}

getData('https://example.com/customers/12')
  .then(data => console.log(data));
```

**Generic POST:**

js

```js
async function postData(url = '', data = {}) {
  const response = await fetch(url, {
    method: 'POST',
    headers: {
      'Accept': 'application/json',
      'Content-Type': 'application/json;charset=UTF-8'
    },
    body: JSON.stringify(data) // must explicitly stringify
  });
  return response;
}

postData('https://example.com/customers', { customerId: 12, customerName: 'John Johnson' })
  .then(response => console.log(response.status));
```

**Client API wrapper pattern** — hide fetch details behind named functions:

js

```js
const websiteURL = 'https://example.com';

async function getCustomer(id) {
  return await getData(`${websiteURL}/customers/${id}`);
}

async function createCustomer(customer) {
  return await postData(`${websiteURL}/customers`, customer);
}
```

Key `Response` object properties: `.status` (HTTP code), `.headers`, `.body`. Call `.json()` to parse a JSON body.

---

---

## Lecture 8: Implementing RESTful Web Services in Node.js and Express

### Node.js

Node.js is an open-source, cross-platform JavaScript runtime built on Chrome's V8 engine. Its key characteristics:

- **Asynchronous and non-blocking** — all APIs are async, so the server never waits idle
- **Single-threaded with an event loop** — incoming requests queue up; I/O is offloaded to a thread pool; completions are handled back on the main thread
- **Highly scalable** — unlike traditional thread-per-request servers

It is well suited for I/O-bound apps, real-time apps, RESTful APIs, and SPAs. It is **not** suitable for CPU-intensive work. It is used in production by LinkedIn, Netflix, PayPal, Uber, and NASA among others.

---

### Node.js Project Structure (npm and package.json)

Every Node.js project is a **package** described by `package.json`:

json

```json
{
  "name": "customer-api",
  "version": "1.0.0",
  "main": "customerAPI.js",
  "type": "module",
  "scripts": {
    "start": "node customerAPI.js"
  },
  "dependencies": {
    "express": "^4.17.1"
  }
}
```

**npm** manages packages:

bash

```bash
npm init                        # create package.json
npm install express             # install runtime dependency
npm install jest --save-dev     # install dev-only dependency
npm install                     # install all dependencies listed in package.json
npm update                      # update packages
npm uninstall express           # remove a package
```

Versions follow **semantic versioning**: `^1.2.3` means "latest where major = 1".

---

### Node.js Module System

**CommonJS (old):**

js

```js
const fs = require('fs');
fs.readFile('file1.js', (error, data) => {
  if (error) throw error;
  console.log(data);
});
```

**ESM / ES6 (new — requires `"type": "module"` in package.json):**

js

```js
import * as fs from 'fs';
// or for specific named exports:
import { readFile } from 'fs/promises';
```

---

### Node.js File System

The promise-based `fs/promises` module is the modern approach:

```js
import * as fs from 'fs/promises';

// Reading a file
try {
  const data = await fs.readFile('file1.js');
  console.log(data.toString());
} catch (err) {
  console.error(err);
}

// Writing a file
try {
  await fs.writeFile('file1.js', 'some text to write');
  console.log('successful write to file');
} catch (err) {
  console.error(err);
}
```

Other operations available: `appendFile`, `copyFile`, `mkdir`, `readdir`, and more.

---

### Creating a Basic Web Server in Node.js

Node.js has a built-in `http` module:

```js
import http from 'http';

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
  res.end('Hello World!');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```

Run with: `node app.js`

---

### Express Framework

Express builds on Node's http module with much better support for routing, middleware, and request/response handling. Its core concepts are: **Application**, **Middleware**, **Request**, **Response**, and **Router**.

**Minimal Express app:**

```js
import * as express from 'express';

const app = express();

app.use(express.json()); // parse JSON request bodies

app.get('/', (req, res) => {
  res.send('hello world');
});

app.listen(3000);
```

---

### Middleware

Each incoming request passes through a **middleware stack** — an ordered chain of functions. Each middleware has the signature `(req, res, next)` and must call `next()` to pass control forward, or send a response to end the chain.

```js
// Logger middleware
app.use(function(req, res, next) {
  console.log('Request URL: ' + req.url);
  console.log('Request date: ' + new Date());
  next(); // critical — pass to next middleware
});
```

Commonly used built-in and third-party middleware:

- `express.json()` — parse JSON bodies
- `express.static()` — serve static files
- `helmet` — security headers
- `passport` — authentication
- `compression` — compress responses

---

### Routing

Routing maps an HTTP method + path to a handler function:

js

```js
app.METHOD(PATH, HANDLER)
```

**Examples:**

js

````js
app.get('/', (req, res) => res.send('Hello World!'));

app.get('/customers/:id', (req, res) => {
  res.send(req.params); // { id: '12' }
});

app.get('/customers/:customerID/orders/:orderID', (req, res) => {
  res.send(req.params); // { customerID: '7', orderID: '42' }
});
```

Hyphens and dots in paths are literal, enabling patterns like:
```
/flights/:from-:to   →  /flights/LAX-SFO  →  req.params = { from: 'LAX', to: 'SFO' }
````

---

### Modular Routing with express.Router

For larger apps, routes can be split into separate modules:

js

```js
// customers/customer.route.js
export const customerRouter = express.Router();

customerRouter.use(express.json());

customerRouter.get('/customers', getAllCustomers);
customerRouter.post('/customers', postCustomer);
customerRouter.get('/customers/:id', getCustomer);
customerRouter.put('/customers/:id', putCustomer);
customerRouter.delete('/customers/:id', deleteCustomer);
```

js

```js
// app.js (main entry)
import express from 'express';
import { customerRouter } from './customers/customer.route.js';

const app = express();
const PORT = 3000;

app.use(customerRouter);

app.get('*', (req, res) => {
  res.send('404! This is an invalid URL.');
});

app.listen(PORT, (err) => {
  if (err) console.log('Error in server setup');
  console.log('Server listening on port', PORT);
});
```

---

### Request and Response Objects

**Request (`req`):**

- `req.params` — path parameters (`/customers/:id` → `req.params.id`)
- `req.body` — parsed request body (requires `express.json()` middleware)
- `req.query` — query string parameters

**Response (`res`):**

js

````js
res.status(403).end()               // status only, no body
res.status(400).send('Bad Request') // status with text body
res.sendStatus(404)                 // shorthand: sets status + sends status string

res.type('json')                    // sets Content-Type header
res.send({ some: 'json' })          // send any body; default 200
res.json({ user: 'tobi' })          // send JSON with correct content-type
res.status(500).json({ error: 'message' })
res.status(404).end()               // end with no body
```

---

### Application Architecture of a RESTful API

The recommended structure is a variant of MVC combined with the **Chain of Responsibility** pattern:
```
HTTP Request
    ↓
 Routes  (express.Router — maps URLs to handler chains)
    ↓
 Middleware stack  (validation, authentication, logging…)
    ↓
 Controllers  (orchestrate the response; call services)
    ↓
 Services / Models  (business logic; database access; JSON conversion)
    ↓
 Database
    ↑
 HTTP Response (JSON)  ← sent back from Controllers
````

Each layer has a single responsibility: routes dispatch, middleware pre-processes, controllers coordinate, and services contain business logic and data access. This keeps the code modular, testable, and maintainable.

# Lecture 9: TypeScript

## TypeScript vs JavaScript

TypeScript is an open-source language maintained by Microsoft, designed by Anders Hejlsberg (also creator of C# and Turbo Pascal). It is a **superset of JavaScript** that adds static typing and compiles (transpiles) down to JavaScript, supporting everything from ES3 to ESNext.

JavaScript is dynamically typed — variables can hold any type and errors only appear at runtime. TypeScript adds compile-time error detection, type inference, and better tooling, making it especially useful for large-scale development.

---

## Basic Types

`string`, `number`, and `boolean` map directly to their JavaScript equivalents. Once declared with a type, a variable cannot change to a different type.
**Type inference** means you don't always need to write the type explicitly — the compiler figures it out from the assigned value:

```typescript
let i = 3;           // inferred as number
let message = "Hi";  // inferred as string
```

---

## Special Types

- **`any`** — disables type checking for that variable. Useful when migrating from JS, but avoid it otherwise.
- **`undefined`** — variable declared but not assigned.
- **`null`** — explicitly empty value.
- **`void`** — used as a return type for functions that return nothing.

---

## Enums

A group of named constant values:

```typescript
enum Season { Spring, Summer, Autumn, Winter }
```

---

## Arrays

Two equivalent syntaxes:

```typescript
let numbers1: number[];
let numbers2: Array<number>;
```

---

## Functions

```typescript
function sumToString(i: number, j: number): string {
  return `${i} + ${j} = ${i + j}`;
}
```

- **Optional parameters** — add `?` after the parameter name. Must come after required parameters.
- **Default parameters** — assign a fallback value if the argument is omitted or `undefined`.
- **Rest parameters** — use `...` prefix, must be last, typed as an array:

```typescript
function getTotal(...numbers: number[]): number {
  return numbers.reduce((total, num) => total + num, 0);
}
```

---

## Interfaces

Describe the shape of an object — which properties exist and what types they are:

```typescript
interface Person {
  firstName: string;
  middleName?: string;        // optional
  readonly dateOfBirth: Date; // read-only
  fullName: () => string;     // method
}
```

Interfaces support inheritance via `extends`. TypeScript uses **structural typing** — if two types have the same shape, they are compatible (unlike Java/C# which use nominal typing).

---

## Union & Intersection Types

**Union** — a value can be one of several types:

```typescript
let result: number | string;
```

**Intersection** — combines multiple types into one:

```typescript
type Customer = Identity & Contact;
```

**Type aliases** give a reusable name to any type:


```typescript
type NumberOrString = number | string;
```

---

## Tuples

A fixed-length array where each position has a known type:


```typescript
let x: [string, number] = ["hello", 10];
```

---

## Destructuring

Unpacking values from arrays, tuples, or objects into variables:


```typescript
let [first, second] = [1, 2];             // array
let { a, b } = { a: "foo", b: 12 };       // object
let [a, b, c] = tuple;                    // tuple
```

---

## Spread Operator

Spreads an array or object into another:

```typescript
let bothPlus = [0, ...first, ...second, 5];
let search = { ...defaults, food: "rich" };
```

---

## Classes

Same syntax as ES6 but with type annotations. Supports constructors, methods, inheritance (`extends`), interface implementation (`implements`), and method overriding.

**Member visibility:**

- `public` (default) — accessible everywhere
- `protected` — accessible within the class and subclasses
- `private` — accessible only within the class

Note: visibility is enforced at compile time only — JavaScript runtime can still access private members.

**Static members** belong to the class itself, not to instances.

---

## Generics

Allow functions, classes, and interfaces to work with any type while preserving type information:


```typescript
function identity<Type>(arg: Type): Type {
  return arg;
}
```

The compiler can infer the type argument automatically. Generic constraints restrict which types are allowed:


```typescript
function displayID<T extends { id: number }>(something: T) {
  console.log(something.id);
}
```

---

## Advanced Types (overview)

TypeScript has a powerful advanced type system including mapped types, conditional types, and utility types such as `Partial<Type>`, `Readonly<Type>`, `ReturnType<Type>`, and `Pick<Type, Keys>`. See the full docs at: [https://www.typescriptlang.org/docs/handbook/2/types-from-types.html](https://www.typescriptlang.org/docs/handbook/2/types-from-types.html)