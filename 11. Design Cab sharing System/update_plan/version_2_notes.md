# Fault tolerance focused

First and foremost, the architectural blueprint can shift its primary focus from raw-performance to __fault tolerance__.

Achieving six nines of availability is an exercise in anticipating and mitigating failure at __every possible point__.

The design can __mandate__ a __multi-region__, __multi-AZ__ deployment __strategy__ for all components, treating __infrastructure redundancy__ not as an option but as a __foundational requirement__.

Stateful components, particularly the __database__ and __message queues__, can be architected for resilience using proven techniques like __quorum-based replication__ and __consensus__ algorithms (e.g., Raft) to ensure durability and __continuous__ operation even during __node failures__.

The application layer can be hardened with standard __resilience patterns__ like __Circuit Breakers__ and __Bulkheads__ to prevent cascading failures, and all external dependencies can be treated as potentially unreliable.

Only after establishing this deeply fault-tolerant foundation should further optimizations for performance be introduced.

# Expected changes in the design

1. Multi-CDN Strategy / Dynamic API traffic: Add multi-region CDN flow before user requests backend server wherever it is required.
    - DNS-based Traffic Manager (Global Server Load Balancer)
        - The Client requests standard web address instead of pointing directly to one CDN.
        - Our DNS provider analyzes the client's location, CDN health, and latency.
        - It then returns the IP address of the best available CDN.
    - Key considerations
        - Cache Synchronization: We can ensure that data is identical on CDN 1 and all other CDNs. If we purge content, then we need to purge it across all CDNs simultaneously.
        - Complexity
            - Configurations: CDN locations, health status etc.
            - SSL certificates: Secure communication
            - Logging for multiple providers: Event tracing that include CDN communication, errors, acknowledgements etc.
        - Cost: Traffic Manager/DNS service plus the egress costs of multiple CDNs.
        - Debugging: Troubleshooting becomes harder unless distributed logging mechanism.
2. We can add Active-Active load balancers across multiple AZs.
    - All nodes are available to serve the client(s) request(s).
3. Update database flow with replication detail along with relevant algorithms.
4. We can update application layer service between load balancer and other core services of backend system with Circuit Breakers pattern.
    - Circuit Breakers pattern
        - We can detect failures and encapsulates the logic of preventing a failure from constantly recurring during maintenance, temporary external system failure, or unexpected system difficulties.

# Abbreviations

__AZ__      -  Available Zones
__GSLB__    -  Global Server Load Balancing