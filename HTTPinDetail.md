# HTTP in Detail — TryHackMe Writeup

---

## Task 1 — What is HTTP(S)?

HTTP stands for **HyperText Transfer Protocol**. It's the foundation of how your browser communicates with web servers — every time you load a webpage, HTTP is doing the heavy lifting under the hood.

HTTPS is just the secure version. The **S** stands for **Secure**, and the difference is that HTTPS encrypts all the data being sent back and forth. This means nobody snooping on the network can read your traffic, and it also confirms you're actually talking to the right server and not an imposter.

To find the flag for this task, you click **View Site** and look at the mock webpage. You'll notice the padlock in the URL bar has a red line through it — that's the issue. Click it.

> **Flag:** `THM{INVALID_HTTP_CERT}`

---

## Task 2 — Requests & Responses

This task breaks down what an actual HTTP request and response look like.

A basic request looks something like this:
```
GET / HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0 Firefox/87.0
Referer: https://tryhackme.com/
```

And a response comes back like:
```
HTTP/1.1 200 OK
Server: nginx/1.15.8
Content-Type: text/html
Content-Length: 98
```

The protocol version in use here is **HTTP/1.1**, and the header that tells the browser how much data to expect is **Content-Length**.

---

## Task 3 — HTTP Methods

HTTP methods define what action you're trying to perform. The main ones you need to know:

- **GET** — retrieve data (e.g., viewing a web article)
- **POST** — send data to create something new (e.g., creating a new user account)
- **PUT** — update existing data (e.g., changing your email address)
- **DELETE** — remove something (e.g., deleting an uploaded picture)

---

## Task 4 — HTTP Status Codes

Status codes tell you how the server handled your request. A few key ones:

| Code | Meaning |
|------|---------|
| 201 | Created — used when something new is successfully made, like a blog post |
| 401 | Unauthorised — you need to log in first |
| 404 | Not Found — the page doesn't exist |
| 503 | Service Unavailable — server-side failure, like a database crash |

---

## Task 5 — Headers

Headers pass extra information along with requests and responses. Some important ones:

- **Host** — tells the server which website you're requesting
- **User-Agent** — tells the server what browser you're using
- **Content-Type** — describes the format of the data being sent
- **Set-Cookie** — used by the server to save a cookie to your machine

---

## Task 6 — Cookies

Cookies are small pieces of data that the server saves to your browser via the **Set-Cookie** header. They're how sites remember who you are between visits — things like keeping you logged in or tracking session state.

You can inspect them in your browser's developer tools under the **Network** tab, then clicking on a request and checking the **Cookies** tab.

---

## Task 7 — Making Requests (Practical)

This is the hands-on section using the built-in HTTP request emulator.

**GET /room**
Make a GET request to `/room`. The flag shows up in the response.
> **Flag:** `THM{YOU'RE_IN_THE_ROOM}`

**GET /blog?id=1**
Switch the URL to `/blog` and add the query parameter `id=1` using the gear icon.
> **Flag:** `THM{YOU_FOUND_THE_BLOG}`

**DELETE /user/1**
Change the method to DELETE and the URL to `/user/1`.
> **Flag:** `THM{USER_IS_DELETED}` *(not provided but standard answer)*

**PUT /user/2**
Switch to PUT, set the URL to `/user/2`, and add the parameter `username=admin`.
> **Flag:** `THM{USER_HAS_UPDATED}`

**POST /login**
Change method to POST, URL to `/login`, and set two parameters: `username=thm` and `password=letmein`.
> **Flag:** `THM{HTTP_REQUEST_MASTER}`
