#### Security
#### CSRF
1. Tricks the user and browser to issue protected resource requests to the target site. Browser adds session cookies in the request to the target server thinking that it's a legitimate request and server assumes that it's a legitimate request as the auth info is present in session cookie.
   1. Conditions for the attack
       1. Site depends on session cookie based authentication solely.
       2. No CSRF token, same site cookie policy, referrer checks.
       3. No unpredictable request params.
2. Examples: Change email address of account, change password etc.. See [CSRF](https://portswigger.net/web-security/csrf) for example URLs crafted.
3. Distributes the link through email, popular post comments on social media or attacker's own website.
4. Mitigate using
   1. CSRF tokens
   2. Referrer checks
   3. Same site cookies policy - chrome introduced feature to restrict sharing session cookies.

#### [XSS](https://portswigger.net/web-security/cross-site-scripting)
1. Tricks the website into executing javascript on the client side.
2. Distribute the link through email, popular post comments on social media.
   1. Reflective XSS: Website sends the request param value in the response without sanitization/encoding. Attacker injects script in the response through the field.
   2. Stored XSS: Website stores the user posts without sanitization/encoding. Attacker comments with script on the post and sends the user to the page containing the post.
   3. DOM-based XSS: Website uses input field response without encoding/sanitization to set inner HTML. Attacker inserts script in the input field to execute script on the client side.
   4. Dangling markup injection: Use input field to inject an non-closed image tag html that would send the data to the remote server until the next closing quote.
3. Mitigation
   1. Input validation and filtering
   2. Encoding the data on the output.
   3. Set content-type headers to stop browser from interpreting data as JS/HTML.
   4. [Content security policy](https://portswigger.net/web-security/cross-site-scripting/content-security-policy) headers specifies what content can run on the current site. It specifies the allowed origins to load JS, images and other assets. It can also specify that the inner JS is not allowed.

#### [Cross site tracing attack](https://en.wikipedia.org/wiki/Cross-site_tracing)
XST scripts exploit ActiveX, Flash, or any other controls that allow executing an HTTP TRACE request. The HTTP TRACE response includes all the HTTP headers including authentication data and HTTP cookie contents, which are then available to the script.

#### Single origin policy
The same-origin policy is a critical security mechanism that restricts how a document or script loaded by one origin can interact with a resource from another origin.
By default, web browsers disallow [certain types](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy#cross-origin_network_access) of cross-origin (A origin other than the current site origin) requests. Origin is a unique combination of schema, host and port.

#### [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS#preflighted_requests)
CORS provides a way for legitimate cross-origin request/resource access. A website can indicate whether a HTTP request can be accessed by the cross-origin or not through response headers. CORS also relies on a mechanism by which browsers make a "preflight" request to the server hosting the cross-origin resource, in order to check that the server will permit the actual request. In that preflight, the browser sends headers that indicate the HTTP method and headers that will be used in the actual request.

#### [Content security policy](https://portswigger.net/web-security/cross-site-scripting/content-security-policy) 
CSP headers specifies what content can run on the current site. It specifies the allowed origins to load JS, images and other assets. It can also specify that the inner JS is not allowed.

#### [Permissions policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/Permissions_Policy)
Permissions Policy is similar to Content Security Policy but controls features instead of security behavior.

#### [Cross origin opener policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cross-Origin-Opener-Policy)
The HTTP Cross-Origin-Opener-Policy (COOP) response header allows you to ensure a top-level document does not share a browsing context group with cross-origin documents.

##### Links
1. [Difference between CSRF and XSS](https://security.stackexchange.com/questions/138987/difference-between-xss-and-csrf)
2. [Labs for practicing attacks](https://portswigger.net/web-security/all-labs#cross-site-request-forgery-csrf)
3. [CSRF](https://portswigger.net/web-security/csrf)
4. [CORS vs CSPs](https://stackoverflow.com/questions/39488241/what-is-the-difference-between-cors-and-csps)
