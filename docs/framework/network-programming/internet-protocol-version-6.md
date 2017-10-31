---
title: "Internet 协议版本 6"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- IPv6, improvements
- IPv4
- IPv6
- Internet Protocol version 6, improvements
- Internet Protocol version 6
ms.assetid: e6fa8ebd-010a-4c48-a5ec-a5102c53c06f
caps.latest.revision: 11
author: mcleblanc
ms.author: markl
manager: markl
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 7901084f38099d74f3bcde086342bd3c90b34348
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# Internet 协议版本 6
Internet 协议版本 6 (IPv6) 是 Internet 的网络层的标准协议新套件。 IPv6 旨在解决当前版本的 Internet 协议套件（称作 IPv4）存在的许多问题，包括地址消耗、安全性、自动配置和扩展性等问题。 IPv6 扩展了 Internet 的功能以启用新型应用程序，包括对等和移动应用程序。 以下是当前 IPv4 协议的主要问题：  
  
-   地址空间快速消耗。  
  
     这导致使用网络地址转换器 (NAT) 将多个专用地址映射到一个公共 IP 地址。 此机制造成的主要问题是处理开销和端对端连接性的缺失。  
  
-   层次结构支持缺失。  
  
     因其固有的预定义类组织，IPv4 缺乏真正的层次结构支持。 无法通过真正地映射网络拓扑的方式构成 IP 地址。 由于存在这种重大的设计缺陷，所以需要通过大型路由表将 IPv4 数据包传送至 Internet 上的任何位置。  
  
-   复杂的网络配置。  
  
     对于 IPv4，地址必须以静态方式分配，或使用配置协议，如 DHCP。 在理想情况下，主机不需要依靠 DHCP 基础结构的管理。 主机可基于其所在的网络段自行配置。  
  
-   缺乏内置身份验证和保密性。  
  
     IPv4 不需要针对提供交换数据的身份验证或加密的机制的支持。 IPv6 在这一方面作出更改。 Internet 协议安全 (IPSec)是 IPv6 支持要求。  
  
 新协议套件必须满足以下基本需求：  
  
-   低开销的大规模路由和寻址。  
  
-   针对各种连接情况进行自动配置。  
  
-   内置身份验证和保密性。  
  
 有关详细信息，请参阅 [IPv6 寻址](../../../docs/framework/network-programming/ipv6-addressing.md)、[IPv6 路由](../../../docs/framework/network-programming/ipv6-routing.md)、[IPv6 自动配置](../../../docs/framework/network-programming/ipv6-auto-configuration.md)、[启用和禁用 IPv6](../../../docs/framework/network-programming/enabling-and-disabling-ipv6.md) 以及[如何：修改计算机配置文件以启用 IPv6 支持](../../../docs/framework/network-programming/how-to-modify-the-computer-configuration-file-to-enable-ipv6-support.md)。  
  
## 参考资料  
 以下是可以在 Internet 工程任务组站点（[http://www.ietf.org](http://www.ietf.org/)）找到的精选 RFC 文档：  
  
-   RFC 1287，面向未来的 Internet 体系结构。  
  
-   RFC 1454，下一 IP 版本的建议的比较。  
  
-   RFC 2373，IP 版本 6 寻址体系结构。  
  
-   RFC 2374，IPv6 可聚合全局单播地址格式。  
  
 还可以在 [Technet 上的 IPv6 区域](http://go.microsoft.com/fwlink/?LinkID=179658)中找到 IPv6 相关信息。  
  
## 另请参阅  
 [IPv6 套接字示例](http://go.microsoft.com/fwlink/?LinkID=179568)   
 [网络编程示例](../../../docs/framework/network-programming/network-programming-samples.md)   
 [套接字](../../../docs/framework/network-programming/sockets.md)

