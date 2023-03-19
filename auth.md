1. Basic Auth
   1. Server responds with 401 status code and www-Authenticate: Basic header if no auth info provided as part of the request. Client prompts the user for username and password.
   2. Client sends "Authorization: Basic <username:password base64 encoded string>" header with subsequent request to the server.
      1. Encoding of the binary "username:password" string is needed as the password might not contain only ASCII chars and HTTP is a character protocol. Cannot distinguish between start of the new header and password containing newline binary value.
      2. Base64 encodes every 6 bit binary string to a printable 7 or 8 bit ASCII char.
   3. Browser sends username:password in every subsequent request header to not prompt for password everytime.
2. Session ID auth
   1. Session-cookie authentication addresses HTTP basic access authentication's inability to track user login status.
   2. Server generates, stores and returns session ID when authenticated using username:password. Server returns session ID in set-cookie header.
   3. Client stores the session ID cookie and sends the session ID cookie to the server with subsequent requests until the cookie expires.
   4. Drawbacks
      1. Session hijacking(i.e steal session cookie), cross site scripting(XSS), CSRF attacks compromise security.
      2. Server has to store and maintain the session IDs generated.
      3. Special type of cookies called session cookies prevent XSS attacks from stealing the cookie since browsers don't allow read of session cookie from Javascript.
3. Token based auth
   1. Server generates and returns a token(userId + timestamp + signature string) when authenticated using username:password. Server returns the token in the response.
   2. Client stores the token in the local storage and sends the token to the server in subsequent request headers until the token expires.
   3. Advanced token implementations require periodic refresh of the token.
   4. No CSRF attacks as the token is not stored in cookies on the client side.
   5. No server storage overhead of the tokens as the tokens are signed cryptographically.
   6. JWT(JSON web token) is a token format specification for improved security and functionality. JWT token contains both authentication(user identifiers) and authorization(roles or permissions) info.
   7. Drawbacks
      1. Token can be stolen to compromise security. Token needs to be stored securely.


##### Password storage in the backend
1. Do not store the password directly in the database
   1. Employees can see the password.
   2. Database hacks would leak passwords.
2. Compute salt, hash of the password and store it in the database.
   1. Difficult to guess password from hash.
   2. Difficult to generate/find passwords of same hash.
   3. Use slow and cryptographically secure hash functions like bcrypt. Don't use MD5, SHA-1. MD5 and SHA1 are fast and insecure.
   4. Use (password + salt) string to generate hash. Using salt makes hash pre-computation/lookup attacks hard. Store the salt also in the database in plain text.

Outer message encryption happens with a shared key. Key exchange happens with public key cryptography during [SSL/TLS handshake](https://www.ibm.com/docs/en/ibm-mq/7.5?topic=ssl-overview-tls-handshake). Once the shared key is established, all further messages are encrypted using the shared key.