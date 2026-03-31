# DNS in Detail — TryHackMe Writeup

## What is DNS?

DNS stands for Domain Name System. At its core, it's what lets you type something like `google.com` into your browser instead of memorizing a string of numbers. It translates human-readable domain names into IP addresses that machines actually understand.

---

## Domain Structure

Domains are broken up into a hierarchy, and understanding each layer matters.

**TLDs (Top-Level Domains)** sit at the far right of a domain name. They usually hint at the purpose or location of the site. There are two flavors — generic TLDs like `.com` or `.org`, and country-code TLDs like `.co.uk` which represent the United Kingdom.

**Second-level domains** are what most people think of as "the domain name" — the part right before the TLD. These are capped at 63 characters.

**Subdomains** get tacked onto the left side of the domain. So in `shops.myshopify.com`, `shops` is the subdomain. A few rules apply here — subdomains max out at 63 characters, you can't use underscores in them, and the entire domain name as a whole can't exceed 253 characters.

---

## DNS Record Types

Different record types exist for different purposes.

- **A records** resolve a domain to an IPv4 address
- **AAAA records** resolve to an IPv6 address
- **CNAME records** don't point to an IP at all — they point to another domain name, acting as an alias
- **MX records** direct email by pointing to the mail server responsible for a domain
- **TXT records** are a bit of a catch-all — they store text and get used for things like domain verification and email security policies

**TTL** (Time To Live) is attached to every record and tells resolvers how long to cache it before checking again.

---

## How DNS Resolution Works

When you type a domain into your browser, a few things happen behind the scenes.

Your request first hits a **recursive DNS server**, which is typically provided by your ISP. It does the legwork of hunting down the answer for you. If it doesn't have the answer cached already, it goes up the chain — querying root servers, then TLD servers, and finally landing on an **authoritative server**, which is the one that actually holds the records for that domain.

---

## Answers

| Question | Answer |
|----------|--------|
| What does DNS stand for? | Domain Name System |
| What type of TLD is `.co.uk`? | ccTLD |
| What is the max length of a subdomain? | 63 characters |
| What character cannot be used in a subdomain? | Underscore (`_`) |
| What is the max length of a domain name? | 253 characters |
| What record type resolves to IPv4? | A |
| What record type resolves to IPv6? | AAAA |
| What record is an alias for another domain? | CNAME |
| What record handles email routing? | MX |
| What record stores text data? | TXT |
| What specifies how long a record is cached? | TTL |
| Who usually provides your recursive DNS server? | ISP |
| What holds the actual records for a domain? | Authoritative server |
| What is the example subdomain used? | shops.myshopify.com |
| What is the MX record priority? | 30 |
| What IP did the A record resolve to? | 10.10.10.10 |
| Flag | `THM{7012BBA60997F35A9516C2E16D2944FF}` |
