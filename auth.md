#### Website authentication methods
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
   2. Client stores the token in the [local storage](https://en.wikipedia.org/wiki/Web_storage) and sends the token to the server in subsequent request headers until the token expires.
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

Outer message encryption happens with a shared key. Key exchange happens with public key cryptography during [SSL/TLS handshake](https://www.ibm.com/docs/en/ibm-mq/7.5?topic=ssl-overview-tls-handshake). Once the shared key is established, all further messages are encrypted using the shared key
See [cookies](https://en.wikipedia.org/wiki/HTTP_cookie#Persistent_cookie) for information about cookies.

### Passwordless authentication
Password types
1. Knowledge factor(something you know) - password
2. Ownership factor(something you own) - phone, OTP to phone
3. Inherence factor(something you are) - Fingerprint

OTP
1. Valid for a limited time.
2. Requires remembering phone number of email id i.e knowledge factor.
3. SMS OTP delivery is not secure.
4. OTP can be used as MFA. Hardware or software key can be used to generate OTP. Google 2FA uses software key to generate OTP every 30 seconds.

#### SSO(Single sign on)
![SSO](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fff52780c-e94e-4d80-a083-7c9cbead8b6f_1600x1473.png)
1. Sign into google once and access all the Google services like gmail, youtube, docs etc.
2. Single Sign-On (SSO) is a user authentication method that allows us to access multiple systems or applications with a single set of credentials.
3. CAS - central authentication service.
4. Service login --> Redirect to CAS --> CAS verifies credentials, creates, saves TGT global session, generate ST(service token) and returns TGT(ticket granting token) cookie, ST with redirection to the service details --> client saves TGT in TGC(ticket granting cookie) cookie --> Redirect to service --> The service validates ST with CAS and provides access
5. If the ticket granting cookie is presented along with the request, then CAS issues service ticket if the TGC is valid.

#### OIDC
When using "Sign in with Google" or similar features, OAuth 2.0 and OIDC work together to streamline the authentication process.
OAuth 2.0 provides "secure delegated access" by issuing short-lived tokens instead of passwords, allowing ***third-party*** services to access protected resources with the resource owner's permission. This method enhances security, as the third-party service does not handle or store the user's password directly.
OIDC provides user identity data in the form of a standardized JSON Web Token (JWT). This token contains information about the authenticated user, allowing the third-party application to create a user profile without requiring a separate registration process.

1. SAML(security assertion markup language)
   1. Uses XML
   2. Popular in enterprise applications mostly.
2. OIDC 
   1. Builds on OAuth 2.0
   2. Provides user identity info in the form of JWT tokens.
   3. Popular in consumer applications.
   4. Various client types, including web-based, mobile, and JavaScript clients.
   5. Preferred for new application.
   6. OAuth 2.0 authorization framework, OIDC adds authentication layer to OAuth 2.0.
   7. Sign in with Google feature uses OIDC.
   8. OAuth 2.0 different types of authorization for different scenarios -- Authorization code grant used mostly.

#### FIDO (Fast Identity Online)
![FIDO](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F591c34d5-1d9e-4cdf-8524-bd83f910b425_1600x1384.png)

Takes biometric authentication further by leveraging the biometrics stored on the users’ devices for website registration and authentication. 
1. Even with OIDC, password hash needs to be stored on servers.
2. FIDO provides a way to move away from server stored passwords.
3. Standards developed by FIDO alliance and W3C.
4. Google, Apple, Microsoft pledged support on platforms in 2022.
5. FIDO enables users to sign in using passkeys across their devices with biometric or security key authentication.
6. The FIDO2 framework includes WebAuthn, which defines a standard web API with built-in authenticators like on-device biometrics or PINs, and CTAP (Client-to-Authenticator Protocols), which enables the use of external authenticators (FIDO Security Keys, mobile devices, wearables, etc) for authentication.
7. The basic idea is that the credentials (private keys) are owned by the user and managed by an authenticator. The application server only stores the public key, the private keys never leave the users’ devices.
8. It's important to note that FIDO is not intended to replace existing federation authentication protocols (SSO, OAuth) but can work alongside them. For more information, refer to this document.

#### MFA multifactor authentication
By requiring multiple factors, MFA provides an extra layer of security and makes it harder for unauthorized users to access protected resources.

##### TOTP
![TOTP](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fa1faded0-3f8b-43de-9ede-017f88e75a10_1600x915.png)
1. TOTP App on phone generates a new OTP every X(for example 30) seconds. TOTP App uses seed and timestamp(changing factor) to generate OTP. HOTP(HMAC based OTP) uses a counter as changing factor.
2. 
