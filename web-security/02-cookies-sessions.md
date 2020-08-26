# HTTP, Cookies, Sessions

### How DNS resolution works

1. Client reach out to recursive DNS resolver. Called recursive cause it can multiple calls to `Name servers` to get the IP address. Say client makes a call with `stanford.edu`
2. DNS resolver then makes a call to the Root Nameserver. But this server may not have the IP address simply because of the issues of scale. But it sends back the address of the Nameserver `edu NS` that has IPs of edu servers
3. DNS resolver makes a call to `edu NS` which doesn't have it either but responds with address of `stanford NS`
4. `stanford NS` is the authoritative NS and returns the IP

### DNS Hijacking

- Malware can change the local DNS resolution file. http.hosts file
- DNS resolver itself could be hacked
- Router could be hacked

### HTTP codes

1. 1xx - Informational (Hold on)
2. 2xx - Success
3. 3xx - Redirection
4. 4xx - Client error
5. 5xx - Server error

### Common codes

- 200
- 206 Partial content: Used in range request. When doing streaming content like Music or podcasts
- 301 - Won't bother checking with server
- 302 - Redirect and call server asking for redirection value
- 304 - Using last cached value

### Cookies

Sample usage

> Set-cookie: theme=dark;
