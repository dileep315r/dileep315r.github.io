### API architecture styles
Architecture styles define how different components of an application programming interface (API) interact with one another. As a result, they ensure efficiency, reliability, and ease of integration with other systems by providing a standard approach to designing and building APIs.
* SOAP
  * Mature, comprehensive, XML-based
  * best for enterprise applications
* RESTful
  * Popular, easy to implement
  * Ideal for web servers
  * Resources and operations on resources. Architectural constraints given below.
    1. Uniform interface: Must define API interfaces for resources.
    2. Client–Server: client and server must evolve separately.
    3. Stateless: All client-server interactions are stateless.
    4. Cacheable. Data and responses are cached wherever possible.
    5. Layered system. APIs, services, and data can be deployed on different servers.
    6. Code on demand (optional). This optional constraint allows the server to return executable code if needed.
* GraphQL
  * Request for specific piece of data from client
  * Reduces network overhead. Results in faster response times.
* gRPC
  * High performance, keys not transmitted over and over. Binary protocol.
  * Suitable for microservices.
* Websocket
  * Real-time, bi-directional, persistent connections
  * Low latency data exchange
* Webhook
  * Event-driven, HTTP callbacks, asynchronous 
  * Notifies systems when events occur

### API first design
![image](https://substack.com/redirect/5ba16725-28dd-4d6a-968d-fc5287c12ccd?j=eyJ1IjoicW1lMnkifQ.7-BOlDe0-cVGIO2ucJq1oJbdhz7gqMyiprATy13HI3E)
The diagram below compares the “Code First” and “API First” approaches. In the “Code First” model, APIs are byproducts of system designs, often referred to as “documentation”. The "API First" model begins with API specifications and concludes with API-driven tests, making APIs the driving force behind the entire software development cycle.

Advantages
1. Improved system integration: Reducing the need for ongoing modifications during development.
2. Enhanced collaboration and quality
3. Increased scalability: scaling becomes more manageable by spinning up new instances and adjusting load balancer settings.

### Signs that APIdesign is bad
1. Users are not able to understand the API easily. Need collaboration from owners.
2. front-end and back-end teams find themselves needing to collaborate extensively just to test and validate API behaviors. 
3. If we find ourselves constantly fielding API usage queries, it is like we are wearing a part-time customer service hat.
4. Another telltale sign can be an influx of requests for minor enhancements. If it feels like we are always tweaking and adjusting our APIs,

### HATEOAS(Hypermedia as the Engine of Application State)
HATEOAS makes our APIs self-descriptive, improving their usability and discoverability. When a client interacts with a resource, the API provides information not just about the resource itself, but also about related resources and possible actions, all represented through hypermedia links.

#### RSocket
##### Goals
1. support for interaction models beyond request/response such as streaming responses and push
   1. Reactive semantics supported
   2. Supports both RPC and event based messaging
2. Open source layer 5/6 communication protocol
   1. Works on top of web sockets, QUIC or any later 4 protocol
3. Application level flow control
   1. application-level flow control semantics (async pull/push of bounded batch sizes) across network boundaries
4. Binary protocol
5. Quicker than Http
   1. Performance via multiplexing
   2. binary, multiplexed use of a single connection
6. Backpressure built in. credit based flow control.
7. Resilience advanced
   1. Server sales capacity to clients
   2. Natural rate limiting
8. support resumption of long-lived subscriptions across transport connections
9. need of an application protocol in order to use transport protocols such as WebSockets and Aeron
10. Ultimately all of the above motivations could be accomplished on top of most anything with enough effort. Those involved with starting this project desired something cleaner and more formalized. In other words, it was desired to have a solution that was not a hack.
11. 

#### Websocket
1. WebSocket is a computer communications protocol, providing full-duplex communication channels over a single ***TCP connection***. 
2. Websocket compatibility with http. Draft to make websocket use HTTP3. https://stackoverflow.com/questions/57378204/is-websocket-compatible-with-http-3
3. Websocket vs SSE https://ably.com/blog/websockets-vs-sse

#### QUIC - layer 4 protocol
![img](https://en.wikipedia.org/wiki/TLS_1.2)
1. QUIC (not an acronym; pronounced as 'quick') is a general-purpose transport-layer protocol published as an IETF Proposed Standard in 2021 — one year before HTTP/3. It can be used with any compatible application-layer protocol, but HTTP/3 is its most frequent use case.
2. It is a grossly inaccurate simplification, but at its simplest level, QUIC is simply TCP encapsulated and encrypted in a User Datagram Protocol (UDP) payload. To the external network, QUIC has the appearance of a bidirectional UDP packet sequence where the UDP payload is concealed. 
3. Built on UDP
4. QUIC is a transport layer protocol that provides a number of improvements over TCP and TLS. QUIC’s main advantages are reduced latency, improved multiplexing, and connection migration. QUIC is designed to be a general-purpose transport layer protocol that can be used by any application that currently uses TCP and TLS
   1. Introduces streams as first class citizen.
   2. easy network switch
      1. Uses connection id concept to switch networks easily

#### HTTP evolution
1. HTTP 1 - keep alive
2. HTTP 1.1 - pipelining, head of line blocking problem
3. HTTP 2 - multiplexing - multiple requests and responses at the same time, binary protocol, header compression, server push
   1. Some comments from RFC
      1. “This effort was chartered to work on a revision of the wire protocol — i.e., how HTTP headers, methods, etc. are put ‘onto the wire’, not change HTTP’s semantics.”
      2. “The primary goals for HTTP/2 are to reduce latency by enabling full request and response multiplexing, minimize protocol overhead via efficient compression of HTTP header fields, and add support for request prioritization and server push.”
      3. “HTTP/2 does not define any new methods, as compared to HTTP/1.1.”
      4. “HTTP/2 does not define a way to ensure that the server is able to send push promises for a given request before the client sends that request.”
         1. “Pushed responses are always associated with an explicit request from the client.”
      5. This means we still need SSE or WebSockets (and SSE is a text protocol so requires Base64 encoding to UTF-8) for push.
4. HTTP 3 - QUIC, multiplexing, header compression, server push
