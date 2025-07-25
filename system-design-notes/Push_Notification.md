# Push Notification

[Zuul Push Youtube Video](https://www.youtube.com/watch?v=6w6E_B55p0E)
## Notes
- randomize connection lifetime
- better to ask client to close connections (based on randomized connection lifetime)
- the above 2 help in preventing thundering herd scenario. By recycling connections periodically (20-30 mins) the connections are switched to different servers. This can reduce
  chances of thundering herd to same server. For ex: if servers crashes all clients will attempt to re-connect and storm the server
- clients can also open another connection first before terminating the first connection and switch to the other connection after draining the first connection
- Use protocol-aware (websocket/SSE) LB or use TCP LB as it won't look at L7 (HTTP)
- Use kafka for queueing (different topics for different priorities)
- Use dynomite for client to server registry
- Push servers are deployed to network edges so that clients can connect to nearest server. Push message processors check with registry
  and connect directly with the specific push server for the client
      
