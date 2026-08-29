https://coderslegacy.com/pyjwt-tutorial-token-authentication-in-python/

https://www.youtube.com/watch?v=ZWEIeLiysp0


https://coderslegacy.com/pyjwt-tutorial-token-authentication-in-python/


https://www.youtube.com/watch?v=xrj3zzaqODw

> 🔵 **NOTE:** This material was prepared using ...  :  https://www.youtube.com/watch?v=xrj3zzaqODw 

# JWT — Complete Guide

## English Translation of the Transcript

### 0:00 – Introduction

Hello everyone, how are you? Welcome to Chai aur Code.

If you are new to the channel, quickly subscribe. Our target is 500 comments.

You must have already seen the title and thumbnail. This video is a complete guide to JWT, or JWT tokens.

By the end of this video, you should have complete knowledge of:

* What JWT is
* How JWT is different from sessions
* Which is better: JWT or sessions
* Whether JWT is secure
* Who uses JWT
* How JWT is used
* How JWT works internally

We are going to understand everything in depth.

The video will obviously be a little long, but after watching this video, my promise is that you should not need another video explaining JWT.

I previously covered JWT in my backend series, but there we mainly looked at its implementation and practical usage.

This video will be more theoretical. We will understand whether you should use JWT, how you should implement it, and answer common FAQs related to JWT.

When I recently visited Bangalore, there were many requests to make a detailed video on this topic. That is why I am making this video.

First, let me explain the overall structure of the video.

We have some notes about JWT and common FAQs.

After that, we will discuss:

* Authentication vs. Authorization
* JWT vs. Sessions
* Diagrams explaining the difference between sessions and tokens
* The official JWT website
* JWT documentation
* The RFC standard
* How a complete JWT is created
* Advantages and disadvantages
* `iat` and other JWT fields
* Some implementation details

We will also briefly discuss how JSON Web Tokens are available in NPM, Django, Ruby on Rails, and almost every major framework.

---

# 1. Concepts You Should Know Before JWT

Before understanding what JWT is, why it exists, and how it works, there are two concepts you should understand.

## Public-Key / Private-Key Cryptography

You don't need a very deep understanding of cryptography for this discussion.

You only need to know that public/private-key cryptography is a security mechanism that uses two keys:

1. Public key
2. Private key

The public key can be distributed to other people without much concern.

Data encrypted using the public key can be decrypted using the corresponding private key.

The public key is intended for distribution.

The important part is the private key.

The private key should never be shared. It must always be kept secure.

JWT works with concepts related to this type of cryptography, and we will discuss that further.

---

# 2. Stateless vs. Stateful

Another important concept is:

* Stateless
* Stateful

These concepts are not limited to JWT. They are used in many areas of computer science.

### Stateless

Stateless means that we do not store the state in a database or file.

JWT is generally used as a stateless mechanism.

The objective of stateless implementation is that the server should not have to maintain session state.

With JWT tokens, possession of a valid token indicates that the holder is authorized to access a particular resource.

In simpler language, the token may be used to prove that the user has already logged in and is allowed to access something.

A common question is:

> What if somebody steals the token? Wouldn't that person then be able to log in as the user? How is this secure?

That is a valid question.

JWT is designed to work in this manner, but there are various security mechanisms around it. We will discuss them later.

So, at this point, the two concepts you need to understand are:

* Public key vs. private key
* Stateless vs. stateful

---

# 3. What Is JWT?

JWT stands for **JSON Web Token**.

A JWT is a long string consisting of letters, numbers, and other encoded characters.

When you look at a JWT, you will normally see two dots separating the string into three components.

A JWT generally consists of three parts.

At first, the long string might look meaningless, but there is a defined structure behind it.

The official website is:

`jwt.io`

Formally, JSON Web Token is an open industry standard used for representing claims between parties.

In normal application development, we commonly use JWT for things such as:

* Login
* Authentication
* Authorization
* Resource access

In formal computer-science language, two resources or parties are communicating with each other, and one side needs to provide claims proving that it is allowed to communicate with or access the other resource.

JWT provides a mechanism for carrying those claims.

In simpler terms, the token can communicate something like:

> I am allowed to access this resource.
> I am logged in.
> I am the user you believe I am.

Think about entering your house.

You need a key to unlock the house. If you possess the correct key, you can unlock it.

JWT works somewhat like that concept.

---

# 4. What Is Inside a JWT?

One of the most important questions is:

How is this large JWT string generated, and what information does it contain?

A JWT contains encoded information and is typically divided into three sections.

The three main components are:

1. Header
2. Payload
3. Signature

---

## Part 1 — Header

The first section tells you information such as:

* The type of token
* The algorithm being used

For example:

```text
typ: JWT
alg: HS256
```

HS256 is one commonly used algorithm.

Other algorithms can also be used.

---

## Part 2 — Payload

The second part is the payload.

The payload can contain information about the user or the request.

For example, it may contain:

```text
subject
user ID
name
email
issued-at time
expiration time
```

A common field is the **subject**.

In practical application development, instead of `subject`, you may often see something like:

```text
id
_id
user_id
```

Developers frequently store the user's ID because if you know the ID or primary key, you can query the database and retrieve additional information about that user.

JWTs are intended to remain relatively lightweight, although names and email addresses may sometimes also be included.

Generally, highly sensitive information should not be stored there.

---

## `iat` — Issued At

Another field you may see is:

```text
iat
```

`iat` means:

**Issued At**

It represents when the token was issued.

---

## Token Expiration

You may also see an expiration field such as:

```text
exp
```

Expiration is extremely important.

Just as it is important to know when a JWT was issued, it is also important to know when the JWT expires.

JWT access tokens are often configured with relatively short expiration periods.

Most JWT implementations in JavaScript or other languages allow you to define an expiration time.

---

# 5. Signature

The third component of a JWT is the signature.

The signature helps determine whether the token has been modified.

Even a small change in the data affects the generated signature.

The signature is created based on the token's contents and a secret/key.

For example, suppose the secret is something simple like:

```text
chai-aur-code
```

That would obviously be a weak secret.

In actual applications, you should generate a strong secret using appropriate utilities.

The secret must be securely stored on the server and should never be distributed publicly.

The server uses the secret to generate and validate the signature.

When the user presents a JWT, the server validates the token before allowing access to a resource.

That gives you a basic idea of what JWT is and how it works.

---

# 6. Authentication vs. Authorization

Before moving further, we need to understand another important topic:

**Authentication vs. Authorization**

These are two different things.

## Authentication

Authentication means verifying:

> Are you really the person you claim to be?

When you registered for a service, you may have provided things such as:

* Username
* Password
* Email

When you later log in using those credentials, the system verifies your identity.

That is authentication.

It means:

> I am proving that I am the user who originally registered.

Authentication by itself does not necessarily mean that you are allowed to access every resource.

---

## Authorization

Authorization determines:

> What are you allowed to access?

For example, suppose you successfully authenticate.

You may be authorized to access:

```text
User Dashboard
```

but not:

```text
Admin Dashboard
```

Or perhaps your account is authorized to access both.

Those permissions are part of **authorization**.

So:

### Authentication

**Who are you?**

### Authorization

**What are you allowed to do?**

JWT was originally useful for communicating claims that can help determine which resources a user is authorized to access.

It also became widely used in authentication workflows.

---

# 7. JWT Across Multiple Services

Consider a system with several services.

For example:

```text
Service 1 → Documentation
Service 2 → Main Website
Service 3 → Application
```

A user logs into one service.

With a traditional session-based approach, session information may be maintained by the server.

With a JWT-based architecture, the token can be passed to multiple services.

If those services can validate the token using the appropriate shared secret or key mechanism, the user can access multiple resources without creating independent login sessions everywhere.

This is one of the useful scenarios for JWT.

At this point, you should understand the difference between authentication and authorization.

JWT is particularly useful for authorization between services and resources.

---

# 8. JWT Structure Summary

A JSON Web Token is a long string divided into three parts:

```text
HEADER.PAYLOAD.SIGNATURE
```

### Header

Contains information about the token and algorithm.

### Payload

Contains claims or information.

### Signature

Used to verify the integrity of the token.

You can also add an expiration time indicating when the token will become invalid.

---

# 9. How Do You Securely Store JWT on the Client?

This is an important question.

We now have a JWT, but how do we keep it secure?

JWT commonly acts as a short-lived token.

Whoever possesses a valid token can potentially use it to access the resource, so the token must be protected.

There are several client-side storage options.

---

## Option 1 — Local Storage

You can store JWT tokens in:

```text
localStorage
```

However, there is a potential problem.

JavaScript-based attacks such as Cross-Site Scripting, or XSS, may allow malicious JavaScript to access local storage and potentially steal a token.

---

## Option 2 — Session Storage

You can also store tokens in:

```text
sessionStorage
```

Session storage works similarly to local storage but has different lifetime behavior.

---

## Option 3 — Cookies

JWTs can also be stored in cookies.

Cookies can be configured with security-related flags to provide additional protection.

---

# 10. Keep Access Tokens Short-Lived

One of the strongest protections discussed here is keeping access tokens short-lived.

For example, a JWT access token might expire after:

```text
10 minutes
15 minutes
20 minutes
```

Once the token expires, the client requests another token.

This leads to the concept of a:

**Refresh Token**

---

# 11. Common JWT Use Cases

JWT has many use cases.

The most common ones are:

### Authentication

JWT can be used as part of the login/authentication process.

### Authorization

JWT can communicate what resources the user is permitted to access.

### Information Exchange

JWT can also be useful for exchanging information between systems.

Because information can be carried in the payload, JWT communication doesn't necessarily have to be only between a browser client and a server.

It can also be used for:

```text
Server → Server
```

communication.

---

# 12. How Do You Invalidate a JWT?

Whenever you create a JWT, you generally configure an expiration time.

Different JWT implementations, whether in NPM, Django, or other ecosystems, give you options for controlling expiration.

You must decide what is appropriate for your application.

For example:

```text
15 minutes
1 hour
1 day
```

The duration depends on your application's requirements.

Another mechanism commonly used with access tokens is:

**Refresh Tokens**

---

# 13. Refresh Token Workflow

Suppose we have:

```text
CLIENT → SERVER
```

### Step 1 — Client Logs In

The client sends information such as:

```text
username
password
```

or other credentials.

### Step 2 — Server Validates Credentials

The server checks the credentials.

If they are valid, the server returns an access token.

For example:

```text
JWT Access Token
```

---

### Step 3 — Client Sends JWT with Requests

Whenever the client sends another request to the server, it attaches the JWT.

Conceptually:

```text
Client
   |
   | Request + JWT
   ↓
Server
```

The server validates the token.

If it is valid, the server allows access to the requested resources.

---

# 14. What Happens When the Access Token Expires?

Suppose the access token is valid for only 15 minutes.

The user remains idle for 15 minutes.

When the next request is made, the token may already have expired.

The server will then reject the expired token.

An unauthorized response such as an HTTP authentication-related error may be returned.

But instead of forcing the user to log in again every time an access token expires, applications commonly use a refresh token.

---

# 15. Access Token + Refresh Token

During the original login process, the server can issue:

```text
Access Token
+
Refresh Token
```

The access token has a relatively short lifetime.

The refresh token generally has a longer lifetime.

The system may also maintain information about refresh tokens in the database.

Conceptually:

```text
CLIENT
   |
   | Login
   ↓
SERVER
   |
   |---- Access Token
   |
   |---- Refresh Token
   ↓
CLIENT
```

The refresh token can also have server-side state associated with it.

---

# 16. Refreshing the Access Token

Suppose the access token expires.

Instead of asking the user to log in again, the client sends the refresh token.

Conceptually:

```text
Access Token
     ↓
  EXPIRED

Client
   |
   | Refresh Token
   ↓
Server
   |
   | New Access Token
   ↓
Client
```

If the refresh token is still valid, the server creates a new access token.

Therefore, the user does not have to continuously enter their username and password again.

The speaker describes this as introducing some stateful behavior because information about refresh tokens can be maintained in a database.

---

# 17. Why Refresh Tokens Are Useful

An access token may expire after:

```text
15 minutes
1 hour
```

But the user should not necessarily have to log in again every 15 minutes.

The refresh token solves this problem.

When the access token expires:

```text
Client → sends Refresh Token
Server → validates Refresh Token
Server → issues new Access Token
```

This process allows the session-like experience to continue while keeping access tokens short-lived.

Refresh-token implementations require their own workflow and can be covered as a separate topic in greater detail.

---

# 18. Other Token Invalidation Mechanisms

There are several possible mechanisms for managing tokens.

You can:

* Let tokens expire naturally
* Maintain allowlists/whitelists
* Maintain blocklists/blacklists
* Invalidate refresh tokens
* Generate new access tokens using refresh tokens

So now you should have a basic understanding of:

* What JWT is
* How JWT is created
* Token expiration
* Refresh tokens
* Authentication
* Authorization

---

# 19. JWT vs. Sessions

Now let's compare JWT and traditional sessions.

Consider a typical three-tier setup:

```text
CLIENT
   ↓
SERVER
   ↓
DATABASE
```

One thing to remember is that every time the server needs to query the database, resources are consumed.

There is also network and I/O overhead.

The database performs read/write operations, which can increase processing time.

This distinction helps explain one of the differences between stateless token-based authentication and stateful session-based authentication.

---

# 20. JWT — Stateless Workflow

Let's first understand the token-based, stateless mechanism.

### Login Request

The client sends:

```text
username
password
```

or:

```text
email
password
```

to the server.

### Credential Validation

The server checks the database to confirm:

```text
Is the user registered?
Are the credentials valid?
```

If the credentials are valid, the server processes the information and issues a JWT.

The required secret/key information is maintained on the server.

---

## Subsequent API Requests

Whenever the user wants to call an API or access another resource, the token is attached to the request.

Conceptually:

```text
Client
   |
   | API Request + JWT
   ↓
Server
```

The server validates the JWT.

According to the explanation in the video, the important point is that the server can perform token validation without having to look up traditional session state in the database for every request.

That is why it is called stateless.

This approach can help with scalability because the server does not have to maintain a conventional server-side session entry for every authenticated request.

The token also contains expiration information.

If you need token renewal or invalidation, you can introduce mechanisms such as refresh tokens.

---

# 21. Token Validation

The main idea of the diagram is:

```text
If Token Is Valid
        ↓
Allow Resource Access
```

Once the token is validated, the application can perform whatever operation the user is authorized to perform.

For example:

```text
READ
WRITE
CREATE
UPDATE
DELETE
```

No matter how large an application becomes, many of its database operations ultimately involve these basic CRUD operations.

---

# 22. Session-Based Authentication — Stateful

Now let's discuss sessions.

Whenever you hear the word:

**Session**

you should generally think:

**Stateful**

because some session-related state must be maintained on the server side, often in a database or another session store.

Let's look at the workflow.

---

# 23. Session Login Workflow

The client sends:

```text
username
password
```

The server validates the credentials against the database.

Once the credentials are validated, the server creates a:

```text
Session ID
```

The session ID may be stored in the browser, commonly using a cookie.

Conceptually:

```text
Browser Cookie
      ↓
 Session ID
```

A corresponding session record is also maintained on the server side.

For example:

```text
Browser
Session ID: ABC123
```

and:

```text
Database / Session Store
Session ID: ABC123
User: ...
Permissions: ...
```

---

# 24. Validating the Session

Whenever the user requests a resource, the server receives the session ID.

The server then needs to determine whether that session is valid and whether the user is authorized to access the requested resource.

The server can look up the session ID in its session store/database.

Once the session is validated, the application performs the requested resource operation.

The speaker's main comparison is that session-based authentication requires maintaining server-side state, while JWT access tokens can be validated without maintaining the same type of server-side session state.

---

# 25. Database Calls and Session State

The video emphasizes that session-based systems may require an additional lookup against the session store/database to validate the user's session.

For example:

```text
Request
   ↓
Read Session ID
   ↓
Check Session Store
   ↓
Validate User
   ↓
Perform Requested Operation
```

This introduces additional I/O compared with a purely stateless token-validation mechanism.

In computer science, developers often try to minimize unnecessary I/O operations because disk, network, and database read/write operations can be relatively expensive compared with in-memory computation.

Whether you are using:

```text
MySQL
MongoDB
SQLite
```

or another database, data must ultimately be read from some storage system.

That is the general idea being explained.

---

# 26. Example of a Refresh Token API

The speaker then refers to an open-source project's documentation as an example.

The application has authentication functionality such as:

```text
Register User
Login User
Logout User
Refresh Token
```

The documentation describes a refresh-token endpoint.

The idea is approximately:

> The refresh token API is responsible for refreshing the access token when it expires. It allows the client to send the refresh token to an endpoint and obtain a new access token.

The refresh token may be maintained by both the client and the server/database.

Therefore, when the client sends the refresh token, the server can validate or match it.

---

# 27. Refresh Token Expiration

A refresh token generally has a longer expiration time than an access token.

Its purpose is to obtain a new access token.

Conceptually:

```text
Access Token
Short Expiration
       ↓
Expires

Refresh Token
Longer Expiration
       ↓
Send to Refresh Endpoint

Server
       ↓
New Access Token
```

The application may then place the new access token in the appropriate client-side storage or cookie for future authentication requests.

When tokens are refreshed, the server may also rotate or replace refresh tokens depending on the implementation.

---

# 28. Final Summary

Hopefully, you now have much more clarity about:

### What JWT is

JWT stands for:

**JSON Web Token**

It is commonly represented as:

```text
HEADER.PAYLOAD.SIGNATURE
```

### How JWT works

A user authenticates, the server issues a token, and the client sends that token with subsequent requests.

### Authentication

Answers:

> Who are you?

### Authorization

Answers:

> What are you allowed to access?

### Stateless JWT Access Tokens

The server can validate the token without maintaining a traditional server-side session record for every request.

### Stateful Sessions

The server maintains session information, such as a session ID mapped to user/session information.

### Token Expiration

Access tokens should normally have an expiration time.

### Refresh Tokens

A refresh token can be used to obtain a new access token after the previous access token expires.

### Client-Side Storage

JWTs may be stored using mechanisms such as:

```text
Local Storage
Session Storage
Cookies
```

Each option has security considerations.

### JWT Common Use Cases

JWT can be used for:

```text
Authentication
Authorization
Information Exchange
API Access
Server-to-Server Communication
```

That completes the overview of JSON Web Tokens, how they work, their relationship with authentication and authorization, refresh tokens, and the difference between JWT-based authentication and traditional session-based authentication.


# JWT — Complete Notes (Theory + Analogies + Code)

Simple, beginner-friendly notes covering **all** the JWT theory: what it is,
how it's built, JWT vs Sessions, storage, refresh tokens, and invalidation —
each concept explained with a real-world analogy and a small code example.

---

## 0. Two ideas you need before JWT makes sense

### Idea 1 — Public key vs Private key

> **Analogy:** Think of a **mailbox with a slot**. Anyone walking by can drop
> a letter into the slot (that's the **public key** — safe to hand out to
> everyone). But only the owner has the **key that opens the mailbox** to
> read what's inside (that's the **private key** — never share it).

- **Public key** → can be given to anyone, used to *verify* or *encrypt*.
- **Private key** → must stay secret, used to *sign* or *decrypt*.
- Data locked with a public key can only be opened with its matching
  private key (and vice versa, depending on the use case).

JWT later uses this exact idea when we sign tokens with `RS256` (see §4).

### Idea 2 — Stateless vs Stateful

> **Analogy — Stateful:** A **coat-check counter** at a theater. You hand
> over your coat, they give you a numbered tag, and they keep your actual
> coat on a rack (the "state") until you come back with the tag. The
> counter has to *remember* something about you.
>
> **Analogy — Stateless:** A **concert wristband**. The wristband itself
> proves you paid for entry. The staff at any door don't need to look you
> up in a book — they just check the wristband. No one has to "remember"
> you; the proof travels with you.

- **Stateful** = server stores information about you (a session) and looks
  it up on every request.
- **Stateless** = the server stores nothing; the token you carry *is* the
  proof. Whoever holds a valid token is treated as authorized.

This raises an obvious worry: *"What if someone steals my wristband/token?"*
That's a real concern, and it's exactly why short expiry times, HTTPS,
secure storage, and refresh-token strategies exist (covered in §6–§8).

JWT is the **stateless** approach. Sessions (cookies + server-side session
store) are the **stateful** approach. We compare them properly in §9.

---

## 1. What is a JWT?

**JWT = JSON Web Token.**

> **Analogy:** A JWT is like a **sealed, tamper-evident envelope** that
> says "the person carrying this envelope is who they claim to be, and
> here's some info about them." Anyone can look at what's written on the
> envelope (it's not secret), but no one can quietly reopen and reseal it
> without the wax seal breaking (the signature).

Formally: JWT is an **open industry standard (RFC 7519)** for representing
**claims** between two parties. A "claim" is just a statement like *"I am
user #42"* or *"I am allowed to access the admin panel."*

A JWT is a single long string made of **3 parts separated by dots**:

```
HEADER.PAYLOAD.SIGNATURE
```

Example:
```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIn0.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```

The official reference site is **jwt.io** — you can paste any JWT there
and it decodes the header/payload for you visually.

---

## 2. What's inside a JWT? (The 3 parts)

### Part 1 — Header

Tells you **what kind of token this is** and **which algorithm signed it**.

```json
{ "typ": "JWT", "alg": "HS256" }
```

- `typ` → "this is a JWT"
- `alg` → the signing algorithm (e.g. `HS256`, `RS256` — see §4)

### Part 2 — Payload

The actual **claims** — data about the user or the request.

```json
{
  "sub": "12345",
  "username": "ada",
  "iat": 1735689600,
  "exp": 1735690500
}
```

Common fields:

| Field | Meaning | Analogy |
|---|---|---|
| `sub` | "subject" — usually the user's ID | The name printed on your ID card |
| `iat` | "issued at" — when the token was created | The date stamped on a ticket |
| `exp` | "expires at" — when the token stops being valid | The ticket's expiry date |

> Developers usually store just the **user ID** here (not the full user
> record), because if you know the ID, you can look up everything else
> in the database. Keep the payload lightweight, and **never put
> passwords or secrets in it** — anyone can decode and read this part,
> it is NOT encrypted, just Base64-encoded.

### Part 3 — Signature

> **Analogy:** This is the **wax seal** on the envelope. It's generated
> from the header + payload + a secret key that only the server knows.
> If even **one character** of the header or payload changes, the seal
> breaks — the server immediately knows the letter was tampered with.

```python
import jwt

token = jwt.encode(
    {"sub": "12345", "username": "ada"},
    "my-secret-key",     # kept only on the server
    algorithm="HS256"
)
```

If someone edits the payload (e.g. changes `"role": "user"` to
`"role": "admin"`) without knowing the secret, the signature check will
fail and the server rejects the token.

---

## 3. Authentication vs Authorization

These sound similar but answer **two completely different questions**.

> **Analogy — an airport:**
> - **Authentication** = showing your passport at the counter to prove
>   *"I am really the person named on this ticket."*
> - **Authorization** = your **boarding pass** deciding *"you may enter
>   Gate 12, Business Lounge — but not the cockpit."*

| | Authentication | Authorization |
|---|---|---|
| Question | **Who are you?** | **What are you allowed to do?** |
| Based on | Username/password, email, biometrics | Roles, permissions, claims |
| Example | Logging in successfully | Being allowed into `/admin` but not `/superadmin` |

JWT is useful for **both**: it's commonly issued right after successful
**authentication** (login), and its payload (claims like `role: "admin"`)
is then used to make **authorization** decisions on every request.

```python
def is_admin(token: str) -> bool:
    payload = jwt.decode(token, SECRET_KEY, algorithms=["HS256"])
    return payload.get("role") == "admin"   # authorization check
```

---

## 4. Symmetric vs Asymmetric signing (HS256 vs RS256)

Remember the mailbox analogy from §0? JWT can be signed two ways:

| | HS256 (Symmetric) | RS256 (Asymmetric) |
|---|---|---|
| Keys used | **One shared secret** signs AND verifies | **Private key** signs, **public key** verifies |
| Who can verify a token? | Only whoever has the secret | Anyone with the public key |
| Who can forge a token? | Anyone with the secret | Only whoever has the private key |
| Best for | A single backend service | Multiple services / third parties that only need to check tokens, not create them |

> **Analogy:** HS256 is like a **shared house key** — anyone with a copy
> can lock or unlock the door (sign or verify). RS256 is like a
> **notary's stamp** — only the notary (private key holder) can stamp
> new documents, but anyone can hold a sample stamp image (public key)
> to check whether a document is genuine.

```python
# HS256 - one secret does both
token = jwt.encode(payload, "shared-secret", algorithm="HS256")
data = jwt.decode(token, "shared-secret", algorithms=["HS256"])

# RS256 - private key signs, public key verifies
token = jwt.encode(payload, private_key_pem, algorithm="RS256")
data = jwt.decode(token, public_key_pem, algorithms=["RS256"])
```

### ⚠️ The `"alg": "none"` trap

Some early libraries blindly trusted the `alg` field written **inside the
token itself**. An attacker could set `alg: "none"`, strip the signature
entirely, and some servers would accept it as valid! **Always** tell
`jwt.decode()` explicitly which algorithms you accept — never let the
token itself decide:

```python
# SAFE
jwt.decode(token, SECRET_KEY, algorithms=["HS256"])

# UNSAFE — never derive algorithm from the token/header
# jwt.decode(token, SECRET_KEY, algorithms=[decoded_header["alg"]])
```

---

## 5. JWT across multiple services

> **Analogy:** A **theme park wristband** that works at every ride,
> restaurant, and gift shop inside the park — you don't need a new ticket
> at each stop, because every checkpoint can independently verify the same
> wristband.

If you have several services —

```
Service 1 → Docs site
Service 2 → Main website
Service 3 → Mobile app backend
```

— a user can log in **once**, get a JWT, and as long as every service
can verify that token (shares the secret, or has the public key for
RS256), the user is authenticated everywhere **without a separate login
per service** and without those services needing to share a central
session database.

---

## 6. Where should the client store a JWT?

Once the client (browser/app) receives a JWT, it needs somewhere to keep
it for future requests. Each option has trade-offs:

| Storage | How it works | Risk |
|---|---|---|
| **`localStorage`** | JS reads/writes it directly | Vulnerable to **XSS** — malicious injected JS can read it and steal the token |
| **`sessionStorage`** | Same as localStorage, but cleared when the tab closes | Same XSS risk, shorter lifetime |
| **Cookies** (with `httpOnly`, `Secure`, `SameSite` flags) | Browser sends it automatically; JS *cannot* read `httpOnly` cookies | Safer against XSS, but needs CSRF protection |

> **Analogy:** Storing a token in `localStorage` is like leaving your house
> key **under the doormat** — convenient, but anyone who finds their way
> onto your porch (an XSS bug) can grab it. An `httpOnly` cookie is like
> handing the key to a **trusted doorman** who uses it for you but never
> lets a stranger (JavaScript) touch it directly.

```python
# Example: setting a JWT in a secure, httpOnly cookie (FastAPI)
from fastapi import Response

@app.post("/token")
def login(response: Response):
    token = create_token(user_id=1, username="ada")
    response.set_cookie(
        key="access_token",
        value=token,
        httponly=True,   # JS can't read this
        secure=True,      # only sent over HTTPS
        samesite="strict" # CSRF mitigation
    )
    return {"message": "logged in"}
```

---

## 7. Keep access tokens short-lived

Because possessing a valid JWT is enough to access a resource
(stateless!), the best defense is making tokens **expire quickly**.

Typical access token lifetimes: **10–20 minutes.**

> **Analogy:** A **parking garage ticket** that's only valid for the next
> hour. Even if someone finds a dropped ticket, it's useless once the hour
> is up.

```python
import datetime as dt
import jwt

def create_access_token(user_id: int, username: str, minutes_valid: int = 15) -> str:
    now = dt.datetime.now(dt.timezone.utc)
    payload = {
        "sub": str(user_id),
        "username": username,
        "iat": now,
        "exp": now + dt.timedelta(minutes=minutes_valid),
    }
    return jwt.encode(payload, SECRET_KEY, algorithm="HS256")
```

But short-lived tokens create a UX problem: should the user really have
to log in again every 15 minutes? That's what refresh tokens solve.

---

## 8. Refresh Tokens

> **Analogy:** Think of a **hotel key card system**.
> - Your **room key card** (access token) only works for 1 day and gets
>   you into your room.
> - At the front desk, you also have a **reservation on file** (refresh
>   token) that's valid for your whole stay (e.g. 7 days).
> - Each morning, you don't need to show your passport again — you just
>   tap your reservation info at the desk, and they hand you a **fresh
>   key card** for the next day.

### The full flow

```
1) LOGIN
   Client --(username, password)--> Server
   Server validates credentials against the DB
   Server --(Access Token + Refresh Token)--> Client

2) NORMAL REQUESTS
   Client --(API request + Access Token)--> Server
   Server validates the Access Token (fast, no DB lookup needed)
   Server --(requested data)--> Client

3) ACCESS TOKEN EXPIRES (e.g. after 15 min)
   Client --(API request + expired Access Token)--> Server
   Server --(401 Unauthorized)--> Client

4) REFRESH FLOW (instead of forcing a full re-login)
   Client --(Refresh Token)--> Server
   Server validates the Refresh Token (may check a DB/store)
   Server --(new Access Token)--> Client
```

Notice step 4 introduces **some statefulness back** — the server may keep
a record of issued refresh tokens so it can invalidate them if needed
(e.g. "log out of all devices").

### Code

```python
import datetime as dt
import jwt

SECRET_KEY = "super-secret-dev-key"

def create_refresh_token(user_id: int, expires_in_days: int = 7) -> str:
    now = dt.datetime.now(dt.timezone.utc)
    payload = {
        "sub": str(user_id),
        "type": "refresh",              # tags this as a refresh token
        "iat": now,
        "exp": now + dt.timedelta(days=expires_in_days),
    }
    return jwt.encode(payload, SECRET_KEY, algorithm="HS256")


def refresh_access_token(refresh_token: str, username: str) -> str:
    """Exchange a valid refresh token for a brand-new access token."""
    payload = jwt.decode(refresh_token, SECRET_KEY, algorithms=["HS256"])  # raises if expired/invalid

    if payload.get("type") != "refresh":
        raise jwt.InvalidTokenError("This is not a refresh token")

    user_id = int(payload["sub"])
    return create_access_token(user_id=user_id, username=username)
```

Why tag it with `"type": "refresh"`? So a refresh token can never be
accidentally (or maliciously) used directly as an access token.

---

## 9. How do you invalidate a JWT?

JWTs are stateless, so unlike a session row in a database, you **can't
just "delete" one** — its signature stays mathematically valid until
`exp` passes. Common strategies:

| Strategy | How it works | Analogy |
|---|---|---|
| **Let it expire naturally** | Just wait out the short `exp` window | The parking ticket simply runs out |
| **Allowlist (whitelist)** | Server keeps a list of *currently valid* tokens; anything not on the list is rejected | Bouncer with a guest list — only listed names get in |
| **Blocklist (blacklist / revocation list)** | Server keeps a list of tokens to *reject* even if still unexpired (e.g. on logout) | A "banned" list at the door — even valid-looking tickets get turned away if they're on this list |
| **Invalidate the refresh token** | Even if an access token is still valid for a few more minutes, deleting the refresh token stops any *future* renewals | Cancelling your hotel reservation — your current key card still opens the door today, but you won't get a new one tomorrow |

```python
# Simple blocklist example (use Redis with a TTL in production)
_REVOKED_TOKENS: set[str] = set()

def revoke_token(token: str) -> None:
    _REVOKED_TOKENS.add(token)

def is_token_valid(token: str) -> bool:
    try:
        jwt.decode(token, SECRET_KEY, algorithms=["HS256"])
    except jwt.InvalidTokenError:
        return False
    return token not in _REVOKED_TOKENS   # still check the blocklist!
```

---

## 10. JWT vs Sessions (the full comparison)

This is the core theoretical comparison from the transcript. Let's walk
through **both workflows** side by side.

### 10a. Session-based authentication (Stateful)

> **Analogy:** The **coat-check counter** again. You get a numbered tag
> (Session ID); your actual coat (your data/permissions) stays on a rack
> at the counter (the server's session store).

```
1) LOGIN
   Client --(username, password)--> Server
   Server checks credentials against the DB
   Server creates a Session ID and stores session data server-side
   Server --(Set-Cookie: session_id=ABC123)--> Client

2) EVERY SUBSEQUENT REQUEST
   Client --(request + cookie: session_id=ABC123)--> Server
   Server looks up "ABC123" in the session store/DB   <-- extra I/O here!
   Server confirms the session is valid & fetches user/permissions
   Server --(response)--> Client
```

**Key cost:** every request requires a **round trip to the session
store** (database, Redis, etc.) to check if the session is still valid.
Database/network I/O is relatively expensive compared to in-memory
computation, so this adds a small amount of latency and load to every
single request, at scale.

### 10b. JWT-based authentication (Stateless)

```
1) LOGIN
   Client --(username, password)--> Server
   Server checks credentials against the DB (this DB call is unavoidable, happens once at login)
   Server creates + signs a JWT
   Server --(Access Token)--> Client

2) EVERY SUBSEQUENT REQUEST
   Client --(request + Authorization: Bearer <JWT>)--> Server
   Server verifies the SIGNATURE + EXPIRY locally (pure computation, no DB call!)
   Server --(response)--> Client
```

**Key benefit:** the server can validate the token **without a database
lookup for every request** — it just recomputes the signature and checks
`exp`. This is what makes JWT easier to scale horizontally across many
servers without a shared session store.

### 10c. Side-by-side table

| | Sessions (Stateful) | JWT (Stateless) |
|---|---|---|
| Where is "logged in" info stored? | Server (DB/Redis), keyed by Session ID | Nowhere — it's inside the signed token itself |
| Per-request cost | DB/store lookup on every request | Just a signature check (fast, no DB call) |
| Scaling across many servers | Needs a shared session store | Any server with the secret/public key can verify independently |
| Instant logout / revocation | Trivial — delete the session row | Hard — needs an allowlist/blocklist (§9) |
| What the client holds | An opaque Session ID (meaningless on its own) | A JWT — anyone can decode and read the payload (not encrypted) |
| Typical transport | Cookie | `Authorization: Bearer <token>` header (or `httpOnly` cookie) |

> **There's no universally "better" option** — it's a trade-off. Sessions
> give you easy revocation at the cost of a server-side lookup per
> request. JWTs give you fast, stateless verification at the cost of
> harder revocation. Many production systems even use **both**: JWT
> access tokens for speed + a stateful refresh-token record for control.

---

## 11. Common JWT use cases

- **Authentication** — proving login identity.
- **Authorization** — carrying roles/permissions for access control.
- **Information exchange** — safely passing claims/data between systems,
  including **server-to-server** communication (not just browser ↔ server).
- **API access** — third-party apps calling your API on a user's behalf.

---

## 12. Quick recap / cheat sheet

```
JWT  =  HEADER . PAYLOAD . SIGNATURE

HEADER    -> algorithm + token type
PAYLOAD   -> claims (sub, iat, exp, custom fields) — readable by anyone, NOT encrypted
SIGNATURE -> proves the header+payload weren't tampered with

Authentication -> "Who are you?"
Authorization  -> "What are you allowed to do?"

Stateless (JWT)     -> server verifies locally, no DB lookup per request
Stateful (Sessions) -> server looks up session info per request

Access Token  -> short-lived (minutes), sent on every request
Refresh Token -> long-lived (days), used ONLY to get a new access token

Revocation options -> let it expire / allowlist / blocklist / kill the refresh token

HS256 -> one shared secret signs & verifies (single backend)
RS256 -> private key signs, public key verifies (multi-service systems)

NEVER trust the "alg" field from inside the token when decoding.
NEVER store passwords/secrets inside the JWT payload.
```

```python
import jwt

# Create
token = jwt.encode({"sub": "1", "exp": ...}, SECRET, algorithm="HS256")

# Verify
payload = jwt.decode(token, SECRET, algorithms=["HS256"])

# Common exceptions
jwt.ExpiredSignatureError   # exp has passed
jwt.InvalidSignatureError   # signature doesn't match
jwt.InvalidTokenError       # catch-all for malformed/invalid tokens
```
