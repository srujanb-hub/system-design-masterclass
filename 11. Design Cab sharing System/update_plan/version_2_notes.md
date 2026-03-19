# Fault tolerance focused

First and foremost, the architectural blueprint can shift its primary focus from raw-performance to __fault tolerance__.

Achieving six nines of availability is an exercise in anticipating and mitigating failure at __every possible point__.

The design can __mandate__ a __multi-region__, __multi-AZ__ deployment __strategy__ for all components, treating __infrastructure redundancy__ not as an option but as a __foundational requirement__.

Stateful components, particularly the __database__ and __message queues__, can be architected for resilience using proven techniques like __quorum-based replication__ and __consensus__ algorithms (e.g., Raft) to ensure durability and __continuous__ operation even during __node failures__.

The application layer can be hardened with standard __resilience patterns__ like __Circuit Breakers__ and __Bulkheads__ to prevent cascading failures, and all external dependencies can be treated as potentially unreliable.

Only after establishing this deeply fault-tolerant foundation should further optimizations for performance be introduced.

# Expected changes in the design

1. Add multi-region CDN flow before user requests backend server wherever it is required.
2. For dynamic API traffic, we can use GSLB or DNS-based Traffic Steering to direct users to the healthiest region, not just the closest static edge node.
3. We can add Active-Active load balancers across multiple AZs.
4. Update database flow with replication detail along with relevant algorithms.
5. We can update application layer service between load balancer and other core services of backend system with Circuit Breakers pattern.

# Abbreviations

__AZ__      -  Available Zones
__GSLB__    -  Global Server Load Balancing