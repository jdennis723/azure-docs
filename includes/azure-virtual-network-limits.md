---
 title: include file
 description: include file
 services: networking
 author: anavinahar
 ms.service: networking
 ms.topic: include
 ms.date: 01/14/2020
 ms.author: anavin
 ms.custom: include file

---
### <a name="azure-resource-manager-virtual-networking-limits"></a>Networking limits - Azure Resource Manager
The following limits apply only for networking resources managed through **Azure Resource Manager** per region per subscription. Learn how to [view your current resource usage against your subscription limits](../articles/networking/check-usage-against-limits.md).

> [!NOTE]
> We recently increased all default limits to their maximum limits. If there's no maximum limit column, the resource doesn't have adjustable limits. If you had these limits increased by support in the past and don't see updated limits in the following tables, [open an online customer support request at no charge](../articles/azure-resource-manager/templates/error-resource-quota.md)

| Resource | Limit | 
| --- | --- |
| Virtual networks |1,000 |
| Subnets per virtual network |3,000 |
| Virtual network peerings per virtual network |500 |
| [Virtual network gateways (VPN gateways) per virtual network](../articles/vpn-gateway/vpn-gateway-about-vpngateways.md#gwsku) |1 |
| [Virtual network gateways (ExpressRoute gateways) per virtual network](../articles/expressroute/expressroute-about-virtual-network-gateways.md#gwsku) |1 |
| DNS servers per virtual network |20 |
| Private IP addresses per virtual network |65,536 |
| Private IP addresses per network interface |256 |
| Private IP addresses per virtual machine |256 |
| Public IP addresses per network interface |256 |
| Public IP addresses per virtual machine |256 |
| [Concurrent TCP or UDP flows per NIC of a virtual machine or role instance](../articles/virtual-network/virtual-machine-network-throughput.md#flow-limits-and-active-connections-recommendations) |500,000 |
| Network interface cards |65,536 |
| Network Security Groups |5,000 |
| NSG rules per NSG |1,000 |
| IP addresses and ranges specified for source or destination in a security group |4,000 |
| Application security groups |3,000 |
| Application security groups per IP configuration, per NIC |20 |
| IP configurations per application security group |4,000 |
| Application security groups that can be specified within all security rules of a network security group |100 |
| User-defined route tables |200 |
| User-defined routes per route table |400 |
| Point-to-site root certificates per Azure VPN Gateway |20 |
| Point-to-site revoked client certificates per Azure VPN Gateway |300 |
| Virtual network TAPs |100 |
| Network interface TAP configurations per virtual network TAP |100 |

#### <a name="publicip-address"></a>Public IP address limits
| Resource | Default limit | Maximum limit |
| --- | --- | --- |
| Public IP addresses<sup>1,2</sup> | 10 for Basic. | Contact support. |
| Static Public IP addresses<sup>1</sup> | 10 for Basic. | Contact support. |
| Standard Public IP addresses<sup>1</sup> | 10 | Contact support. |
| [Public IP addresses per Resource Group](../articles/azure-resource-manager/management/resources-without-resource-group-limit.md#microsoftnetwork) | 800 | Contact support. | 
| Public IP Prefixes | limited by number of Standard Public IPs in a subscription | Contact support. |
| Public IP prefix length | /28 | Contact support. |

<sup>1</sup>Default limits for Public IP addresses vary by offer category type, such as Free Trial, Pay-As-You-Go, CSP. For example, the default for Enterprise Agreement subscriptions is 1000.

<sup>2</sup>Public IP addresses limit refers to the total amount of Public IP addresses, including Basic and Standard. 

#### <a name="load-balancer"></a>Load balancer limits
The following limits apply only for networking resources managed through Azure Resource Manager per region per subscription. Learn how to [view your current resource usage against your subscription limits](../articles/networking/check-usage-against-limits.md).

**Standard Load Balancer**

| Resource                                | Limit         |
|-----------------------------------------|-------------------------------|
| Load balancers                          | 1,000                         |
| Rules (Load Balancer + Inbound NAT) per resource                      | 1,500                         |
| Rules per NIC (across all IPs on a NIC) | 300                           |
| Frontend IP configurations              | 600                           |
| Backend pool size                       | 1,000 IP configurations, single virtual network |
| Backend resources per Load Balancer <sup>1<sup> | 1,200                 |
| High-availability ports rule            | 1 per internal frontend       |
| Outbound rules per Load Balancer        | 600                           |
| Load Balancers per VM <sup>2<sup>       | 2 (1 Public and 1 internal)   |

<sup>1</sup> The limit is up to 1,200 resources, in any combination of standalone virtual machine resources, availability set resources, and virtual machine scale-set placement groups.
<sup>2</sup> An exception to this limit is that 2 public load balancers can be in front of a VM if an IPv4 address config is used for one load balancer and IPv6 address config is used for the second.

**Gateway Load Balancer**

| Resource                                | Limit        |
|-----------------------------------------|------------------------------|
| Resources chained per Load Balancer (LB frontend configurations or VM NIC IP configurations combined) | 100 |
 
**Basic Load Balancer**

| Resource                                | Limit        |
|-----------------------------------------|------------------------------|
| Load balancers                          | 1,000                        |
| Rules per resource                      | 250                          |
| Rules per NIC (across all IPs on a NIC) | 300                          |
| Frontend IP configurations <sup>3<sup>  | 200                          |
| Backend pool size                       | 300 IP configurations, single availability set |
| Availability sets per Load Balancer     | 1                            |
| Load Balancers per VM                   | 2 (1 Public and 1 internal)  |

<sup>3</sup> The limit for a single discrete resource in a backend pool (standalone virtual machine, availability set, or virtual machine scale-set placement group) is to have up to 250 Frontend IP configurations across a single Basic Public Load Balancer and Basic Internal Load Balancer.

<a name="virtual-networking-limits-classic"></a>The following limits apply only for networking resources managed through the **classic** deployment model per subscription. Learn how to [view your current resource usage against your subscription limits](../articles/networking/check-usage-against-limits.md).

| Resource | Default limit | Maximum limit |
| --- | --- | --- |
| Virtual networks |100 |100 |
| Local network sites |20 |50 |
| DNS servers per virtual network |20 |20 |
| Private IP addresses per virtual network |4,096 |4,096 |
| Concurrent TCP or UDP flows per NIC of a virtual machine or role instance |500,000, up to 1,000,000 for two or more NICs. |500,000, up to 1,000,000 for two or more NICs. |
| Network Security Groups (NSGs) |200 |200 |
| NSG rules per NSG |200 |1,000 |
| User-defined route tables |200 |200 |
| User-defined routes per route table |400 |400 |
| Public IP addresses (dynamic) |500 |500 |
| Reserved public IP addresses |500 |500 |
| Public IP per deployment |5 |Contact support |
| Private IP (internal load balancing) per deployment |1 |1 |
| Endpoint access control lists (ACLs) |50 |50 |
