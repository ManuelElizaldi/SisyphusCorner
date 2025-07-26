**In an e-commerce application which service seems like a good fit for processing a paid-up order that can be fulfilled at a later point in time?**
SQS - The order ID can be queued for later processing depending on logistics and warehouse operations.


**Your customer has an application which writes and reads a lot of data from a database. The application is under stress due to heavy demand, and so is the database. Due to its stateless nature, the application is leveraging elasticity principles to scale, but the database is struggling to keep up. What are your best fit options? (Select two)**

Evaluate a higher machine specification for the database perhaps with more CPU and Memory
Add a caching layer to cache frequently read data

Increasing the size of the database server enhances its processing power and memory capacity, allowing it to handle more simultaneous queries and transactions. This leads to improved response times and higher throughput, enabling the server to serve more requests per second.

Adding a cache stores frequently accessed data temporarily, allowing faster retrieval by reducing repeated database queries. This minimizes the load and improves overall performance and efficiency.

*why maintaining more the one copy was not an option:*
Splitting an RDBMS is challenging because maintaining ACID properties and ensuring data consistency across distributed nodes requires complex transaction management and synchronization. Additionally, optimizing query performance across split databases involves intricate data partitioning and balancing and hence it is not the right choice.


