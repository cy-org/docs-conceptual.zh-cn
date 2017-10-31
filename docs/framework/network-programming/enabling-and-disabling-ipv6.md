---
title: "启用和禁用 IPv6"
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
ms.assetid: 6408d3ef-c9ba-49d9-b15e-fe74bd3ef031
caps.latest.revision: 9
author: mcleblanc
ms.author: markl
manager: markl
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: dee5dd53a88bdd108b84d05cfb75799630836033
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="enabling-and-disabling-ipv6"></a>启用和禁用 IPv6
若要使用 IPv6 协议，请确保当前运行的操作系统版本支持 IPv6，并确保正确配置了操作系统和网络类。  
  
## <a name="configuration-steps"></a>配置步骤  
 下表列出了各种配置  
  
|支持 IPv6 的操作系统？|支持 IPv6 的网络类？|描述|  
|-------------------------------------|---------------------------------------|-----------------|  
|No|No|可以分析 IPv6 地址。|  
|No|是|可以分析 IPv6 地址。|  
|是|No|使用未标记为过时的名称解析方法，可以分析并解析 IPv6 地址。|  
|是|是|使用所有方法（包含标记为过时的方法），可以分析并解析 IPv6 地址。|  
  
 请注意，要为 System.Net 命名空间中的所有类启用 IPv6 支持，必须修改计算机配置文件或应用程序的配置文件。 应用程序的配置文件优先于计算机配置文件。  
  
 有关如何修改计算机配置文件 machine.config 以启用 Ipv6 支持的示例，请参阅[如何：修改计算机配置文件以启用 IPv6 支持](../../../docs/framework/network-programming/how-to-modify-the-computer-configuration-file-to-enable-ipv6-support.md)。 此外，请确保操作系统启用了 IPv6 支持。  
  
 .NET Framework 在配置文件中具有如下配置开关设置  
  
```xml  
<system.net>…  
    <settings>…  
        <ipv6 enabled="true"/>…  
    </settings>…  
</system.net>  
```  
  
 对于 .NET Framework 1.1 及更早版本，ipv6 enabled 配置开关的值指定 <xref:System.Net.Dns?displayProperty=fullName> 类的成员是否返回 IPv6 地址。  
  
 对于 .NET Framework 2.0 和更高版本，如果 Windows 支持 IPv6，则 <xref:System.Net.Dns?displayProperty=fullName> 类的成员（例如 <xref:System.Net.Dns.GetHostEntry%2A?displayProperty=fullName> 方法）将返回含一个限制的 IPv6 地址。 DNS <xref:System.Net.Dns?displayProperty=fullName> 的已过时成员（例如，<xref:System.Net.Dns.Resolve%2A?displayProperty=fullName> 方法）将读取并识别配置文件中 ipv6 enabled 设置的值。  
  
## <a name="see-also"></a>另请参阅  
 [Internet 协议版本 6](../../../docs/framework/network-programming/internet-protocol-version-6.md)   
 [套接字](../../../docs/framework/network-programming/sockets.md)   
 [网络设置架构](../../../docs/framework/configure-apps/file-schema/network/index.md)   
 [\<ipv6> 元素（网络设置）](../../../docs/framework/configure-apps/file-schema/network/ipv6-element-network-settings.md)

