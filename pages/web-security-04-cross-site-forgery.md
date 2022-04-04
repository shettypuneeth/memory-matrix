# Cross-Site Request Forgery, Same Origin Policy

> Lecture #4 https://www.youtube.com/watch?v=0-q69vAYSwo

### Can cookie paths be made more secure?

- Cookies can only be accessed by equal or more specific domains, so use a sub-domain.
- a.stanford.com and b.stanford.com are equal.
  - Mutually exclusive
- a.stanford.com and stanford.com
  - Former can access later and not other way around

### What to set cookie path to?

- Set to `/`
- `Set-Cookie: key=value; Secure; HttpOnly; (JS can't access) Path=/`

## Problem with ambient authority (attaching cookies to HTTP requests)

- Can circumvent using embedding below in attacker.com
  - `<img src="https://bank.com/withdraw?=..." />`
    - This could have been avoided if the withdraw is a post request.
  - If user has an active session on bank.com on another tab, cookies get attached
  - This is basically CSRF
    - these attacks force people to transfer funds, change emails
    - if you're an admin, then attacker can create an admin user (the attacker needs to know the system (get/post path))

### Quick example of a CSRF hack

- We have the user logged into bank.com and have an active session
- On another site attacker.com, we do the following
  - We have the knowledge of the how the URL and header look like for a transfer POST call
  - We embed a hidden iFrame with a submit form on POST of which we make a call to bank.coom/transfer
  - Because of ambient authority, the bank.com session and cookies get attached to the POST call made from attacker.com and we are able to exploit the system

### Fix for this

- SameSite cookies to avoid exploitation of ambient authority
  - Lax, Lax(with hold on sublevel routes, but attach cookies for top level route), Strict

## Same Origin Policy

> Fundamental security model of the web.
> Given two javascript execution contexts, one should be able to access the other only if they are on the same protocol of hostname and port.

But there are some specific cases when 2 diff domains would want to communicate with each other based on mutual understanding. In that case, can try one of the below.

- Both parties should set document.domain to the same value. Say, document.domain = 'stanford.edu' on both login.stanford.edu and stanford.edu
- Or, the 2 sites can communicate using the URL fragment. Parent would create and iFrame and embed the child URL. Then would update the iFrame.src to include the new #. The child has to periodically poll to look for changes in the # and perform it's operations.
- use postMessage to communicate.
  - Parent would have `iFrame.contentWindow.postMessage('value', 'target_origin');`
  - Child would have `window.addEventListener('message', (event) => {})`
