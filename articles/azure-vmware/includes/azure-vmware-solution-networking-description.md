---
title: Azure VMware Solution networking and connectivity
description: Azure VMware Solution networking and connectivity description.
ms.topic: include
ms.service: azure-vmware
ms.date: 08/10/2021
author: suzizuber
ms.author: v-szuber
---

<!-- Used in introduction.md and concepts-networking.md -->

Azure VMware Solution offers a private cloud environment accessible from on-premises and Azure-based resources. Services such as Azure ExpressRoute, VPN connections, or Azure Virtual WAN deliver the connectivity. However, these services require specific network address ranges and firewall ports for enabling the services.

When deploying a private cloud, private networks for management, provisioning, and vMotion get created. You'll use these private networks to access vCenter and NSX-T Manager and virtual machine vMotion or deployment.

[!INCLUDE [expressroute-global-reach](expressroute-global-reach.md)]

Virtual machines deployed on the private cloud are accessible to the internet through the [Azure Virtual WAN public IP](../enable-public-internet-access.md) functionality. For new private clouds, internet access is disabled by default. 



