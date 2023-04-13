### Peer to peer communication
1. WebRTC protocol can be used for establishing peer to peer connection.
   1. Collection of protocols. 
      1. STUN for discovering whether the host is behind a full code NAT etc. Google provides free STUN server.
      2. ICE protocol to find ways for two computers to talk to each other as directly as possible in peer-to-peer networking. And SDP describes media information. Signaling server helps in exchanging information between the clients using ICE and SDP servers.
      3. TURN server for relaying the traffic if the host NAT doesn't support direct connection.
      4. See https://stackoverflow.com/a/53293443 for more information.
