---
title: "&lt;socket&gt; 元素（网络设置） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/settings/socket"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#socket"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<socket> 元素"
  - "socket 元素"
ms.assetid: 366c634c-7d16-478f-aedf-053eda94a1a0
caps.latest.revision: 21
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 21
---
# &lt;socket&gt; 元素（网络设置）
指定套接字操作是否使用完成端口。  
  
## 语法  
  
```  
  
      <socket  
  alwaysUseCompletionPortsForConnect="true|false"  
  alwaysUseCompletionPortsForAccept="true|false"  
  ipProtectionLevel ="EdgeRestricted|Restricted|Unrestricted|Unspecified"  
/socket>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|**特性**|**说明**|  
|------------|------------|  
|`alwaysUseCompletionPortsForAccept`|指示套接字是否应当始终对 Accept 方法调用使用完成端口。  默认值为 `false`。|  
|`alwaysUseCompletionPortsForConnect`|指示套接字是否应当始终对 Connect 方法调用使用完成端口。  默认值为 `false`。|  
|`ipProtectionLevel`|指定用于套接字的默认 <xref:System.Net.Sockets.IPProtectionLevel?displayProperty=fullName>。  默认值取决于 Windows 的版本。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|**元素**|**说明**|  
|------------|------------|  
|[设置](../../../../../docs/framework/configure-apps/file-schema/network/settings-element-network-settings.md)|配置 <xref:System.Net> 命名空间的基本网络选项。|  
  
## 备注  
 `alwaysUseCompletionPortsForAccept` and `alwaysUseCompletionPortsForConnect`属性被用来指定关于<xref:System.Net.Sockets?displayProperty=fullName>命名空间中的类使用完全端口的默认的行为。  对于高性能的服务器应用程序，建议使用完成端口。  
  
 `alwaysUseCompletionPortsForAccept` 和 `alwaysUseCompletionPortsForConnect` 特性的默认值是 **false**。  
  
 <xref:System.Net.Configuration.SocketElement.AlwaysUseCompletionPortsForAccept%2A> 属性可用于从适用的配置文件获取 `alwaysUseCompletionPortsForAccept` 特性的当前值。  <xref:System.Net.Configuration.SocketElement.AlwaysUseCompletionPortsForConnect%2A> 属性可用于从适用的配置文件获取 `alwaysUseCompletionPortsForConnect` 特性的当前值。  
  
 `ipProtectionLevel` 特性指定用于套接字的默认 <xref:System.Net.Sockets.IPProtectionLevel?displayProperty=fullName>。  <xref:System.Net.Configuration.SocketElement.IPProtectionLevel%2A> 属性允许将 IPv6 套接字限制配置为一个指定范围，例如限制为具有相同的链接本地或站点本地前缀的地址。  通过使用此选项，应用程序可限制对 IPv6 套接字的访问。  通过应用此类限制，可让在专用局域网上运行的应用程序能够通过简单的方式很好地增强自身的安全性，以便防范外部攻击。  此选项可扩大或缩小侦听套接字的范围，从而使得公共用户和私人用户可以在适当情况下对站点进行无限制的访问，或者可以根据需要对同一站点进行有限制的访问。  
  
 此 `ipProtectionLevel` 特性设置仅影响初始传入网络流量：  
  
-   侦听套接字的传入连接的 TCP 服务器。  
  
-   接收套接字的数据包的 UDP 应用程序。  
  
 此配置设置不会影响已建立的 TCP 连接（通信在两个方向上无限制）并且不会影响应用程序发送 UDP 包。  
  
 `ipProtectionLevel` 特性设置的可能值与 <xref:System.Net.Sockets.IPProtectionLevel?displayProperty=fullName> 枚举中指定的已定义保护级别对应，如下所示：  
  
|||  
|-|-|  
|**特性值**|**说明**|  
|EdgeRestricted|IP 保护级别是“边缘受限的”。  此值应由设计为在 Internet 上运行的应用程序使用。  此设置不允许使用 Windows Teredo 实现的网络地址转换 \(NAT\) 遍历。  这些应用程序可能会绕过 IPv4 防火墙，因此，必须加强应用程序的安全性以防范针对开放端口的 Internet 攻击。  在 Windows Server 2003 和 Windows XP 中，针对套接字的 IP 保护级别的默认值是“边缘受限的”。|  
|Restricted|IP 保护级别是“受限的”。  此值应由未实现 Internet 方案的 Intranet 应用程序使用。  一般情况下，不会针对 Internet 样式的攻击来对这些应用程序进行测试或加强安全性。  此设置将限制仅接收链接本地的通信。|  
|无限制|IP 保护级别是“不受限的”。  此值应由设计为在 Internet 上运行的应用程序使用，包括利用 Windows 中内置的 IPv6 NAT 遍历功能（例如，Teredo）的应用程序。  这些应用程序可能会绕过 IPv4 防火墙，因此，必须加强应用程序的安全性以防范针对开放端口的 Internet 攻击。  在 Windows Server 2008 R2 和 Windows Vista 中，针对套接字的 IP 保护级别的默认值是“不受限的”。|  
|Unspecified|IP 保护级别是“未指定的”。  在 Windows 7 和 Windows Server 2008 R2 中，针对套接字的 IP 保护级别的默认值是“未指定的”。|  
  
 `ipProtectionLevel` 特性的默认值是 **Unspecified**。  
  
 <xref:System.Net.Configuration.SocketElement.IPProtectionLevel%2A> 属性可用于从适用的配置文件获取 `ipProtectionLevel` 特性的当前值。  
  
## 配置文件  
 此元素可以用在应用程序配置文件或计算机配置文件 \(Machine.config\) 中。  
  
## 示例  
 下面的代码示例演示如何指定应使用的完成端口以及应该不受限制的默认 <xref:System.Net.Sockets.IPProtectionLevel?displayProperty=fullName>。  
  
```  
<configuration>  
  <system.net>  
    <settings>  
      <socket  
        alwaysUseCompletionPortsForAccept="true"  
        alwaysUseCompletionPortsForConnect="true"  
        ipProtectionLevel="Unrestricted"  
       />  
    </settings>  
  </system.net>  
</configuration>  
```  
  
## 请参阅  
 <xref:System.Net?displayProperty=fullName>   
 <xref:System.Net.Configuration.SocketElement?displayProperty=fullName>   
 <xref:System.Net.Sockets?displayProperty=fullName>   
 <xref:System.Net.Sockets.IPProtectionLevel?displayProperty=fullName>   
 <xref:System.Net.Sockets.SocketOptionName?displayProperty=fullName>   
 [网络设置架构](../../../../../docs/framework/configure-apps/file-schema/network/index.md)