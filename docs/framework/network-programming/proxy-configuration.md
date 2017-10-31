---
title: "代理配置"
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
- Networking
- adaptive proxies
- static proxies
- Network Resources
- Internet, proxy configuration
- proxies
- network, proxy configuration
- proxies, configuring
ms.assetid: 353c0a8b-4cee-44f6-8e65-60e286743df9
caps.latest.revision: 14
author: mcleblanc
ms.author: markl
manager: markl
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: d2576050310c9b1926ee413e4fb1bbcf0c4bf4be
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="proxy-configuration"></a>代理配置
代理服务器处理客户端对资源的请求。 代理可以从其缓存中返回已请求的资源，或将请求转发到资源驻留的服务器。 代理可以通过减少发送到远程服务器的请求数量来提高网络性能。 代理还可以用于限制对资源的访问。  
  
## <a name="adaptive-proxies"></a>自适应代理  
 在 .NET Framework 中，有两种代理：自适应和静态。 自适应代理会在网络配置更改时调整它们的设置。 例如，如果便携式计算机用户启动拨号网络连接,自适应代理会识别此更改,发现并运行其新配置脚本，然后相应调整其设置。  
  
 自适应代理是通过配置脚本配置的（请参阅[自动代理检测](../../../docs/framework/network-programming/automatic-proxy-detection.md)）。 脚本针对每个协议生成一组应用程序协议和一个代理。  
  
 多个选项控制配置脚本的运行方式。 可以指定以下各项：  
  
-   下载和运行配置脚本的频率。  
  
-   下载脚本需要等待多长时间。  
  
-   你的系统应使用哪些凭据访问代理。  
  
-   你的系统应使用哪些凭据下载配置脚本。  
  
 网络环境的变化可能要求系统使用一组新代理。 如果网络连接不可用或新的网络连接已初始化，系统必须在新环境中发现相应的配置脚本源并运行新脚本。  
  
 下表显示了自适应代理的配置选项。  
  
|特性、属性或配置文件设置|描述|  
|--------------------------------------------------------|-----------------|  
|`scriptDownloadInterval`|用秒计算的脚本下载之间的运行时间。|  
|`scriptDownloadTimeout`|下载脚本的等待时间（用秒计算）。|  
|`useDefaultCredentials` 或 <xref:System.Net.WebProxy.UseDefaultCredentials>|控制系统是否使用默认网络凭据访问代理。|  
|`useDefaultCredentialForScriptDownload`|控制系统是否使用默认网络凭据下载配置脚本。|  
|`usesystemdefaults`|控制是否应从用户的 Internet Explorer 代理设置读取静态代理设置（代理地址、跳过列表和跳过本地）。 如果这个值设置为“true”，那么将使用来自 Internet Explorer 的静态代理设置。<br /><br /> 如果这个值设置为“false”或未设置，那么静态代理设置可在配置中指定并将替代 Internet Explorer 代理设置。 此外，这个值必须设置为“false”或不设置，才能启用自适应代理。|  
  
 以下例子显示了典型的自适应代理配置。  
  
```xml  
<system.net>  
    <defaultProxy>  
      <proxy  scriptDownloadInterval="600"  
              scriptDownloadTimeout="30"  
              useDefaultCredentials="true"  
              usesystemdefaults="true"  
      />  
    </defaultProxy>  
</system.net>  
```  
  
## <a name="static-proxies"></a>静态代理  
 静态代理通常由应用程序显示配置，或者当配置文件被应用程序或系统调用时配置。 静态代理在拓扑结构更改不频繁的网络中很有用，比如连接到企业网络的台式计算机。  
  
 多个选项控制静态代理的运行方式。 可以指定以下各项：  
  
-   代理的地址。  
  
-   是否应对本地地址不使用代理。  
  
-   是否应对一组地址不使用代理。  
  
 下表显示了静态代理的配置选项。  
  
|特性、属性或配置文件设置|描述|  
|--------------------------------------------------------|-----------------|  
|`proxyaddress` 或 <xref:System.Net.WebProxy.Address>|要使用的代理地址。|  
|`bypassonlocal` 或 <xref:System.Net.WebProxy.BypassProxyOnLocal>|控制是否对本地地址不使用代理。|  
|`bypasslist` 或 <xref:System.Net.WebProxy.BypassArrayList>|用正则表达式描述不使用代理的一组地址。|  
|`usesystemdefaults`|控制是否应从用户的 Internet Explorer 代理设置读取静态代理设置（代理地址、跳过列表和跳过本地）。 如果这个值设置为“true”，那么将使用来自 Internet Explorer 的静态代理设置。 在 .NET Framework 2.0 中，当这个值设置为“true”时，Internet Explorer 代理设置不会被配置文件中的其他代理设置替代。 在 .NET Framework 1.1 中，Internet Explorer 代理设置可以被配置文件中的其他代理设置替代。<br /><br /> 如果这个值设置为“false”或未设置，那么静态代理设置可在配置中指定并将替代 Internet Explorer 代理设置。 此外，这个值必须设置为“false”或不设置，才能启用自适应代理。|  
  
 以下示例显示了一个典型的静态代理配置。  
  
```xml  
<system.net>  
    <defaultProxy>  
        <proxy  proxyaddress="http://proxy.contoso.com:3128"  
                bypassonlocal="true"  
        />  
        <bypasslist>  
            <add address="[a-z]+.blueyonderairlines.com$" />  
        </bypasslist>  
    </defaultProxy>  
</system.net>  
```  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Net.WebProxy>   
 <xref:System.Net.GlobalProxySelection>   
 [自动代理检测](../../../docs/framework/network-programming/automatic-proxy-detection.md)

