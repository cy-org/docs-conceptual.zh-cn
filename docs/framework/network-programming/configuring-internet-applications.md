---
title: "配置 Internet 应用程序"
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
- downloading Internet resources, default proxy
- sending data, default proxy
- receiving data, default proxy
- downloading Internet resources, configuring Internet applications
- protocol-specific modules
- custom authentication modules
- receiving data, configuring Internet applications
- configuration settings [.NET Framework], Internet applications
- requesting data from Internet, configuring Internet applications
- requesting data from Internet, default proxy
- response to Internet request, default proxy
- Internet, configuring Internet applications
- response to Internet request, configuring Internet applications
- default proxy
- network resources, default proxy
- sending data, configuring Internet applications
- network resources, configuring Internet applications
- Internet, default proxy
ms.assetid: bb707c72-eed2-4a82-8800-c9e68df2fd4f
caps.latest.revision: 15
author: mcleblanc
ms.author: markl
manager: markl
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: a4a013b8a4ff60222bb88c6e9c4f14badd689b5d
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="configuring-internet-applications"></a>配置 Internet 应用程序
[\<System.Net > 元素（网络设置）](../../../docs/framework/configure-apps/file-schema/network/system-net-element-network-settings.md)配置元素包含应用程序的网络配置信息。 使用 [\<system.Net> 元素（网络设置）](../../../docs/framework/configure-apps/file-schema/network/system-net-element-network-settings.md)元素，可以设置代理服务器，设置连接管理参数，包括自定义应用程序内的身份验证和请求模块。  
  
 [\<defaultProxy>元素（网络设置）](../../../docs/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings.md)元素定义 `GlobalProxySelection` 类返回的代理服务器。 任何没有自身 <xref:System.Net.HttpWebRequest.Proxy%2A> 属性的 <xref:System.Net.HttpWebRequest> 都设置为使用默认代理的特定值。 除了设置代理地址外，还可以创建不使用代理的服务器地址列表，并指示不应将代理用于本地地址。  
  
 请注意，Microsoft Internet Explorer 设置与配置设置相结合，并且后者具有优先级。  
  
 以下示例将默认代理服务器地址设置为 http://proxyserver，指示不应将代理用于本地地址，并指定对位于 contoso.com 域中服务器的所有请求均应绕过该代理。  
  
```xml  
<configuration>  
    <system.net>  
        <defaultProxy>  
            <proxy  
                usesystemdefault = "false"  
                proxyaddress = "http://proxyserver:80"  
                bypassonlocal = "true"  
            />  
            <bypasslist>  
                <add address="http://[a-z]+\.contoso\.com/" />  
            </bypasslist>  
        </defaultProxy>  
    </system.net>  
</configuration>  
```  
  
 使用 [\<connectionManagement>元素（网络设置）](../../../docs/framework/configure-apps/file-schema/network/connectionmanagement-element-network-settings.md)元素来配置可与特定服务器或其他所有服务器进行的持久连接数。 下面的示例将应用程序配置为使用 2 个与服务器 www.contoso.com 的持久连接，4 个与 IP 地址为 192.168.1.2 的服务器的持久连接，以及 1 个与其他所有服务器的持久连接。  
  
```xml  
<configuration>  
    <system.net>  
        <connectionManagement>  
            <add address="http://www.contoso.com" maxconnection="2" />  
            <add address="192.168.1.2" maxconnection="4" />  
            <add address="*" maxconnection="1" />  
        </connectionManagement>  
    </system.net>  
</configuration>  
```  
  
 自定义身份验证模块已配置 [\<authenticationModules>元素（网络设置）](../../../docs/framework/configure-apps/file-schema/network/authenticationmodules-element-network-settings.md)元素。 自定义身份验证模块应实现 <xref:System.Net.IAuthenticationModule> 接口。  
  
 下面的示例配置自定义身份验证模块。  
  
```xml  
<configuration>  
    <system.net>  
        <authenticationModules>  
            <add type="MyAuthModule, MyAuthModule.dll" />  
        </authenticationModules>  
    </system.net>  
</configuration>  
```  
  
 可以使用 [\<webRequestModules> 元素（网络设置）](../../../docs/framework/configure-apps/file-schema/network/webrequestmodules-element-network-settings.md)元素将应用程序配置为使用自定义协议特定的模块，以请求 Internet 资源中的信息。 指定的模块应实现 <xref:System.Net.IWebRequestCreate> 接口。 可在配置文件中指定自定义模块来替代默认 HTTP、HTTPS 和文件请求模块，如下例所示。  
  
```xml  
<configuration>  
    <system.net>  
        <webRequestModules>  
            <add  
                prefix="HTTP"  
                type = "MyHttpRequest.dll, MyHttpRequestCreator"  
            />  
        </webRequestModules>  
    </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>另请参阅  
 [.NET Framework 中的网络编程](../../../docs/framework/network-programming/index.md)   
 [网络设置架构](../../../docs/framework/configure-apps/file-schema/network/index.md)   
 [\<system.Net> 元素（网络设置）](../../../docs/framework/configure-apps/file-schema/network/system-net-element-network-settings.md)

