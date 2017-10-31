---
title: "如何：修改计算机配置文件以启用 IPv6 支持"
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
ms.assetid: 5611b677-b9cc-43b8-a434-60e18d89aada
caps.latest.revision: 18
author: mcleblanc
ms.author: markl
manager: markl
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 6a23a2690b0df30eaa815d0b321200af3a3403e5
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="how-to-modify-the-computer-configuration-file-to-enable-ipv6-support"></a>如何：修改计算机配置文件以启用 IPv6 支持
下面的代码示例演示如何修改计算机配置文件 machine.config，以启用 IPv6 支持。 machine.config 文件存储在 Windows 安装目录的 %Windir%\Microsoft.NET\Framework 文件夹中。 安装在计算机上的每个 .NET Framework 版本，在 %Windir%\Microsoft.NET\Framework 下的文件夹中分别有一个单独的 machine.config 文件（例如，C:\WINDOWS\Microsoft.NET\Framework\v2.0.50727\machine.config）。  
  
 也可以在应用程序的配置文件中做出这些设置，其优先级别高于计算机配置文件。  
  
 对于 .NET Framework 1.1 及更早版本，ipv6 enabled 配置开关的值指定 <xref:System.Net.Dns?displayProperty=fullName> 类的成员是否返回 IPv6 地址。  
  
 对于 .NET Framework 2.0 和更高版本，如果 Windows 支持 IPv6，则 <xref:System.Net.Dns?displayProperty=fullName> 类的所有成员（例如 <xref:System.Net.Dns.GetHostEntry%2A?displayProperty=fullName> 方法）将返回含一个限制的 IPv6 地址。 <xref:System.Net.Dns?displayProperty=fullName> 类的已过时成员（例如，<xref:System.Net.Dns.Resolve%2A?displayProperty=fullName> 方法）将读取并识别配置文件中的值。  
  
> [!NOTE]
>  .NET Framework 2.0 及更高版本默认启用 IPv6。 .NET Framework 1.1 及更低版本默认禁用 IPv6。  
  
## <a name="example"></a>示例  
  
```xml  
<system.net>  
    …………  
    <settings>  
        …………  
        <ipv6 enabled="true"/>   
    ……………  
    </settings>  
    ………………  
<system.net>  
```  
  
## <a name="see-also"></a>另请参阅  
 [IPv6 寻址](../../../docs/framework/network-programming/ipv6-addressing.md)   
 [网络设置架构](../../../docs/framework/configure-apps/file-schema/network/index.md)   
 [\<ipv6> 元素（网络设置）](../../../docs/framework/configure-apps/file-schema/network/ipv6-element-network-settings.md)

