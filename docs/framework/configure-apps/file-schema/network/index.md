---
title: "网络设置架构"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- elements [.NET Framework], network configuration elements
- sending data, network configuration elements
- receiving data, network configuration elements
- configuration settings [.NET Framework], networks
- Internet, network configuration elements
- network configuration elements
- network settings
- connections [.NET Framework], network configuration elements
- network resources, network configuration elements
ms.assetid: f1de5a0f-76c5-4833-819f-5222b8146340
caps.latest.revision: 14
author: mcleblanc
ms.author: markl
manager: markl
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: a101b3d6ebf1c884bce08077a1138a4ab6376d1f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/05/2017

---
# <a name="network-settings-schema"></a>网络设置架构
网络设置指定 .NET Framework 与 Internet 的连接方式。 下表描述 [\<system.Net> 元素（网络设置）](../../../../../docs/framework/configure-apps/file-schema/network/system-net-element-network-settings.md)下每个子配置元素的功能。  
  
|元素|描述|  
|-------------|-----------------|  
|[\<authenticationModules> 元素（网络设置）](../../../../../docs/framework/configure-apps/file-schema/network/authenticationmodules-element-network-settings.md)|指定用于验证 Internet 请求的模块。|  
|[\<connectionManagement> 元素（网络设置）](../../../../../docs/framework/configure-apps/file-schema/network/connectionmanagement-element-network-settings.md)|指定到 Internet 主机的最大连接数。|  
|[\<defaultProxy> 元素（网络设置）](../../../../../docs/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings.md)|指定用于路由到 Internet 的 HTTP 请求的代理服务器。|  
|[\<mailSettings> 元素（网络设置）](../../../../../docs/framework/configure-apps/file-schema/network/mailsettings-element-network-settings.md)|包含邮件发送选项的设置。|  
|[\<requestCaching> 元素（网络设置）](../../../../../docs/framework/configure-apps/file-schema/network/requestcaching-element-network-settings.md)|指定用于从 Internet 主机请求信息的模块。|  
|[\<requestCaching> 元素（网络设置）](../../../../../docs/framework/configure-apps/file-schema/network/requestcaching-element-network-settings.md)|配置 <xref:System.Net?displayProperty=fullName> 命名空间的基本网络选项。|  
|[\<webRequestModules> 元素（网络设置）](../../../../../docs/framework/configure-apps/file-schema/network/webrequestmodules-element-network-settings.md)|指定用于从 Internet 主机请求信息的模块。|  
  
 URI 设置指定 .NET Framework 如何处理使用统一资源标识符 (URI) 表示的 Web 地址。 下表描述 [\<Uri> 元素（Uri 设置）](../../../../../docs/framework/configure-apps/file-schema/network/uri-element-uri-settings.md)下每个子配置元素的函数。  
  
|元素|描述|  
|-------------|-----------------|  
|[\<idn> 元素（Uri 设置）](../../../../../docs/framework/configure-apps/file-schema/network/idn-element-uri-settings.md)|指定是否对域名应用国际化域名 (IDN) 分析。|  
|[\<iriParsing> 元素（Uri 设置）](../../../../../docs/framework/configure-apps/file-schema/network/iriparsing-element-uri-settings.md)|指定是否对 <xref:System.Uri> 应用国际资源标识符 (IRI) 分析以及是否应该应用 IRI 分析规则。|  
|[\<schemeSettings> 元素（Uri 设置）](../../../../../docs/framework/configure-apps/file-schema/network/schemesettings-element-uri-settings.md)|指定如何分析特定方案的 <xref:System.Uri>。|  
  
## <a name="see-also"></a>另请参阅  
 [配置 Internet 应用程序](../../../../../docs/framework/network-programming/configuring-internet-applications.md)   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)

