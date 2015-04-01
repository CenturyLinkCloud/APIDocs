{{{
  "title": "Shared Load Balancers Overview",
  "date": "3-26-2015",
  "author": "Bryan Friedman",
  "sticky": true,
  "attachments": []
}}}

### Load Balancer

A **shared load balancer** is made up of a VIP (virtual IP) and a set of servers grouped by pools (i.e. access ports). The load balancer entity is merely a named container with an IP address that can further be configured to include multiple pools of servers behind the same IP.

### Load Balancer Pool

Within a shared load balancer definition, multiple **pools** can be configured. Each pool defines the _port_ that will respond to and redirect traffic to the server nodes in the pool. The pool is also where the load balancing _method_ and _persistence_ types are set.

The method can either be set to "round robin" or "least connection." For the round robin option, the load balancer cycles through a list of all the servers bound to it. It does not take into account server workload or latency and simply distributes traffic evenly across servers. The least connection option routes traffic to the server with the fewest active connections. An "active" connection is considered one where the HTTP request has not yet received a response. This is considered the best performing of the two algorithms.  

The persistence type can be either "standard" or "sticky." The standard option employs no persistence and is best for stateless web applications. If an application does require server-based state, then choose the sticky option. The sticky choice uses source IP + destination IP address-based persistence to tie users to the target server.

If you choose round robin or least connection along with standard persistence, then requests are routed without any concern for where the last user's request came from. If you choose round robin or least connection along with sticky persistence, then the FIRST request will be routed based on either round robin or least connection, and each subsequent request from that source IP address will return to the server that responded to the initial request.

### Load Balancer Node

For each pool, one or more **nodes** are configured corresponding to a server that is included in the load balancing pool. The node definition includes the server's private IP address and the port that is serving the content.

### Example
