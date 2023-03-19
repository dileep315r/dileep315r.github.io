1. How to maintain the shared TLS key on application server with load balancer distributing the traffic and cluster of servers setup.
   1. Needed for internal service to service connectivity with SSL/TLS.
   2. Solution given [here](./sticky_session.html)
2. How does the CDN ensure that the user has access rights to the content.
   1. CDN can contact the origin server to validate the credentials presented by the user. Allow if valid user for the service.
   2. URL/body may contain token and CDN server may validate the token by sending the token to the origin server.

