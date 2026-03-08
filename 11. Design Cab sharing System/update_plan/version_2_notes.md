# Fault tolerance focused

First and foremost, the architectural blueprint can shift its primary focus from raw-performance to __fault tolerance__.

Achieving six nines of availability is an exercise in anticipating and mitigating failure at __every possible point__.

The design can __mandate__ a __multi-region__, __multi-AZ__ deployment __strategy__ for all components, treating __infrastructure redundancy__ not as an option but as a __foundational requirement__.

Stateful components, particularly the __database__ and __message queues__, can be architected for resilience using proven techniques like __quorum-based replication__ and __consensus__ algorithms (e.g., Raft) to ensure durability and __continuous__ operation even during __node failures__.

The application layer can be hardened with standard __resilience patterns__ like __Circuit Breakers__ and __Bulkheads__ to prevent cascading failures, and all external dependencies can be treated as potentially unreliable.

Only after establishing this deeply fault-tolerant foundation should further optimizations for performance be introduced.

# Abbreviations

__AZ__	-	Available Zones