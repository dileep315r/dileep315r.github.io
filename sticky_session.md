#### Scenarios requiring pinning users to servers i.e sticky sessions
1. Websocket connection
   1. Connect device to a single server throughout the lifetime of the session. 
   2. Reverse lookup server to client info to push data to the client.


#### Load balancer scaling
1. Dynamically resolve DNS to one of the load balancer addresses.
2. Client connects to the LB throughout the processing of the request

#### SSL/TLS connection and load balancers
1. Client and server needs to store shared encryption keys
   1. Client to server encrypted connection terminate at LB. Terminate the connection from user client to server once the request is processed.
      1. Maintain several encrypted connections from LB to servers. Send the client request along one of the encrypted connection.
   2. Maintain encrypted connections from the microservice client to another microservice LBs as well.

#### General LB stuff
1. LB operates at HTTP level
2. External LB maintains persistent connections to API gateway servers. Persistent connections reduce the response time by avoiding TCP handshake everytime.
3. LB handles the connection with the client. Sends the HTTP request from client to one of the servers through one of the persistent connections.