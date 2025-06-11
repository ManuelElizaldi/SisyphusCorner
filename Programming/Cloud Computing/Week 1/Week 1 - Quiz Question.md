A parent account can be used for consolidated billing of multiple child accounts?
- AWS Organizations allows you to set up a management account (parent), invite members (child) accounts into the organization. This enables rolled up billing 

If your organization does not allow shared tenancy as per security compliance policies, which of the following EC2 features would you take advantage of?
- Dedicated host. If you are not allowed shared tenancy, you need to ensure that your EC2 instance is running on a physical server dedicated solely to your use, not shared with other AWS customers. 
- By default

What is not required to ssh to an instance on cloud?
- Name of the instance

You are not charged by AWS if your EC2 instance is in ___________
- Terminated state
- Hibernate State
- Stopped State

In order to send your requests to a specific application server (which your application has authenticated with), you should use:
- Session Affinity
- By default, an Application Load Balancer routes each request independently to a registered target based on the chosen load-balancing algorithm. However, you can use the sticky session feature (also known as session affinity) to enable the load balancer to bind a user's session to a specific target. This ensures that all requests from the user during the session are sent to the same target. This feature is useful for servers that maintain state information in order to provide a continuous experience to clients. To use sticky sessions, the client must support cookies.

A new functionality has been developed by the development team. The business is looking to release the new functionality gradually to their customers. The intention is to have the levers to rollback in case there is a production or deployment trouble. The customer is looking for -
- Canary release

If a user selects the region and availability zone as per the user proximity, it will help ___________________
- to minimize network latency

An EC2 instance is running an application which will require access to multiple AWS services (in the same account). Which is the best way to provide access?
- Create a single role with the required policies for the services as needed and attach it to the instance