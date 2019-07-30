# Cloud-Azure-Single-Arm-FW-for-East-West-no-SNAT

## Brief Description
This skillet deploys 2 VM-Series NGFW with an internal load balancer in single arm mode for East-West communication between applications without the need for configuring SNAT. The skillet also deploys two ubuntu servers to test the east west traffic.

### Target Audience
A list of the target audience for the skillet.  
-	Core SE’s

-	Public Cloud SE’s



## Skillet Details
Authoring Group:  Public Cloud

Documentation:  

Github Location:  https://github.com/ceskillets/Cloud-Azure-Inbound-Transit-VNET-with-Standard-LB.git 

PAN-OS Supported: 8.1, 9.0 

Cloud Provider(s) Supported:  AZURE

Type of Skillet:  Public Cloud

Purpose:  Demo

Status:  Completed


## Detail Description
There are customer requirements where they want to retain the original source IP of the application servers when they communicate across multiple applications. Some of the primary reasons for this requirement could be because of hardcoded IP address, whitelisting requirement or logging the transaction source IP. In the regular VM-series deployment, SNAT is configured to ensure symmetric traffic routing to the NGFW where the session is maintained.

To achieve this requirement, VM-series is deployed in single arm as shown in the figure below. Load Balancer deployed in trust subnet to distribute traffic to both firewall maintains the session information of the traffic flow. This allows the load balance to ensure the response to the request from the destination server is always sent to the same NGFW that processed the request.

 

### Traffic Flow
The below diagram depicts the traffics flow from server in APP1 subnet to server in APP2 subnet. The original source and destination IP of the requesting host and server is retained in the IP header. 

 

This design ensures the east-west traffic flow within the VNET between multiple subnets are symmetric and always passes the same NGFW for a single transaction.

With this demo you can demonstrate the value of deploying VM-Series NGFW in Azure cloud while retaining the original source IP address.

### Outcome
In the single VNet single arm VM-Series deployment, a common set of firewalls provides visibility and control of all traffic profiles (East-West). The firewalls are deployed in a single VNet that are deployed in HA using Internal load balancer to avoid downtime caused by maintenance activities or failure.
