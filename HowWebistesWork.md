# How Websites Work — TryHackMe Writeup

**Room:** How Websites Work
**Difficulty:** Easy
**Path:** Web Fundamentals

---

## Task 1 — How Websites Work

Before you can even think about hacking a website, you need to understand how one actually functions. The basic idea is straightforward — when you type a URL into your browser, it sends a request to a web server somewhere in the world, and that server sends back the data your browser uses to render the page.

There are two sides to every website:

- **Front End (Client-Side)** — what your browser renders and what you actually see
- **Back End (Server-Side)** — the server handling your request behind the scenes

> **Q: What term best describes the component of a web application rendered by your browser?**
> **A: Front End**

---

## Task 2 — HTML

This task drops you into an HTML editor with a simple cat website. HTML is the skeleton of every webpage — it defines the structure and content using tags like `<h1>`, `<p>`, and `<img>`.

The first challenge has a broken image tag. If you look at the source, one of the cat images is missing its file extension. Fixing `img/cat-2` to `img/cat-2.jpg` loads the image and reveals the answer.

> **Q: One of the images on the cat website is broken — fix it, and the image will reveal the hidden text answer.**
> **A: HTMLHERO**

The second part asks you to add a dog image on line 11. All you need is:
```html
<img src='img/dog-1.png'>
```

> **Q: Add a dog image to the page by adding another img tag on line 11.**
> **A: DOGHTML**

---

## Task 3 — JavaScript

JavaScript is what makes websites interactive. Without it, everything is static — just text and images with no dynamic behavior. JS can be loaded directly in `<script>` tags or pulled in from an external file.

This task has you write a JS snippet that changes the content of a `div` element. You add the following inside the `<script>` tags:
```javascript
document.getElementById("demo").innerHTML = "Hack the Planet";
```

After that, you add the button from the example and click it to confirm it works. Once you hit **Render HTML+JS Code** and interact with the page, the flag pops up.

> **Q: What is the flag from the JavaScript challenge?**
> **A: JSISFUN**

---

## Task 4 — Sensitive Data Exposure

This one is a great real-world lesson. Developers sometimes forget to strip sensitive info from frontend code before pushing to production — things like passwords, API keys, or hidden links sitting in plain HTML comments or JS variables that anyone can read by hitting **Ctrl+U** (view source).

For this task, just open the page source and look around. The password is sitting right there in the clear.

> **Q: What is the password hidden in the source code?**
> **A: testpasswd**

---

## Task 5 — HTML Injection

HTML Injection happens when a site takes user input and dumps it directly onto the page without sanitizing it first. If there's no filtering, you can type raw HTML into an input field and the browser will render it as actual markup — not just display it as text.

For this task, the goal is to inject a malicious link pointing to `http://hacker.com`. The payload is just a basic anchor tag:
```html
<a href="http://hacker.com">Click Me</a>
```

Paste that into the input field and submit. The page renders it as a real clickable hyperlink, which is exactly the problem — an attacker could use this to redirect unsuspecting users to phishing pages or malicious sites.

> **Q: What is the flag from the HTML Injection challenge?**
> **A: HTML_INJ3CTI0N**
