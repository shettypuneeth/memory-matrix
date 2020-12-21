# Exceptions to the Same Origin Policy, Cross-Site Script Inclusion

> Lecture 05 https://www.youtube.com/watch?v=ud9cVQDte3A

### DNS hijacking

When you request a `non-existent.example.com` the service provider can respond with some different page where there could be a malicious script which can read cookies from `example.com`

Use the Referrer policy HTTP header to prevent requests from unwanted sites

### How to prevent sites from being embedded

- Frame busting
  - compare window.top.location and window.location.
- Use header as a more robust solution
  - X-Frame-Options
    - deny | sameorigin

### Can we prevent a site from submitting a form to our site

- Why do this?
  - Prevent cross site forgery CSRF
- How?
  - Detect origin header, use an allow list
  - SameSite cookie

### Can we prevent images from being embedded

- Why?
  - Prevent hotlinking.
- How?
  - Look at the Referrer header, and have an allowlist
  - SameSite cookies

### Working out way around making requests to cross site

If site A.com tries make a fetch call to B.com, say

```
// A.com
const response  = await fetch('B.com');
const data = response.json();

// CORS error
```

As a workaround we can use the script tag to make the call to a different origin but we can't access the data that was returned. It is only going to fetch it, parse it and try to execute it.

We can hack it by using JSONP requests

```js
<script>
  function handleData(data)
  {
    // do something with the data
  }
</script>

<script src="https://b.com/enpoint?callback=handleData"></script>

// And the response is gonna look like,
// handleData({ data: ... })
```
