---
title: "&lt;httpTransport&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: 8b30c065-b32a-4fa3-8eb4-5537a9c6b897
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# &lt;httpTransport&gt;
为自定义绑定指定用于传输 SOAP 消息的 HTTP 传输。  
  
## 语法  
  
```  
  
<httpTransport  
    allowCookies=Boolean"  
    authenticationScheme="Digest/Negotiate/Ntlm/Basic/Anonymous"  
    bypassProxyOnLocal=Boolean"  
    hostnameComparisonMode="StrongWildcard/Exact/WeakWildcard"  
    keepAliveEnabled="Boolean"  
    maxBufferSize="Integer"  
    proxyAddress="Uri"  
    proxyAuthenticationScheme="None/Digest/Negotiate/Ntlm/Basic/Anonymous"  
IntegratedWindowsAuthentication: Specifies Windows authentication"  
    realm="String"  
    transferMode="Buffered/Streamed/StreamedRequest/StreamedResponse"  
        unsafeConnectionNtlmAuthentication="Boolean"  
        useDefaultWebProxy="Boolean" />  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|allowCookies|一个布尔值，指定客户端是否接受 Cookie 并在今后的请求中传播这些 Cookie。  默认值为 `false`。<br /><br /> 在与使用 Cookie 的 ASMX Web 服务进行交互时，可以使用此属性。  通过这种方式，可以确保从服务器返回的 Cookie 自动复制到客户端今后对该服务的所有请求。|  
|authenticationScheme|指定用来验证 HTTP 侦听器正在处理的客户端请求的协议。  包括以下有效值：<br /><br /> -   Digest：指定摘要式身份验证。<br />-   Negotiate：和客户端协商以确定身份验证方案。  如果客户端和服务器均支持 Kerberos，则使用 Kerberos；否则使用 NTLM。<br />-   Ntlm：指定 NTLM 身份验证。<br />-   Basic：指定基本身份验证。<br />-   Anonymous：指定匿名身份验证。<br /><br /> 默认值为 Anonymous。  此属性的类型为 <xref:System.Net.AuthenticationSchemes>。  此属性只能设置一次。|  
|bypassProxyOnLocal|一个布尔值，指示是否对本地地址不使用代理服务器。  默认值为 `false`。<br /><br /> 本地地址是指位于本地 LAN 或 Intranet 上的地址。<br /><br /> 如果服务地址以 http:\/\/localhost 开头，则 [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 总是忽略代理。<br /><br /> 如果希望客户端在与同一台计算机上的服务通话时使用代理，则应使用主机名称而非 localhost。|  
|hostnameComparisonMode|指定用于分析 URI 的 HTTP 主机名比较模式。  有效值为<br /><br /> -   StrongWildcard：\(“\+”\) 与指定方案、端口和相对 URI 的上下文中所有可能的主机名进行匹配。<br />-   Exact：无通配符<br />-   WeakWildcard：\(“\*”\) 与指定方案、端口和相对 UIR 的上下文中尚未显式匹配或尚未通过强通配符机制匹配的所有可能的主机名进行匹配。<br /><br /> 默认值为 StrongWildcard。  此属性的类型为 <xref:System.ServiceModel.HostnameComparisonMode>。|  
|keepAliveEnabled|一个布尔值，指定是否与 Internet 资源建立持久性连接。|  
|maxBufferSize|一个正整数，指定缓冲区的最大大小。  默认值为 524288。|  
|proxyAddress|一个指定 HTTP 代理的地址的 URI。  如果 `useSystemWebProxy` 为 `true`，则此设置必须为 `null`。  默认值为 `null`。|  
|proxyAuthenticationScheme|指定用于验证 HTTP 代理正在处理的客户端请求的协议。  包括以下有效值：<br /><br /> -   None：不执行任何身份验证。<br />-   Digest：指定摘要式身份验证。<br />-   Negotiate：和客户端协商以确定身份验证方案。  如果客户端和服务器均支持 Kerberos，则使用 Kerberos；否则使用 NTLM。<br />-   Ntlm：指定 NTLM 身份验证。<br />-   Basic：指定基本身份验证。<br />-   Anonymous：指定匿名身份验证。<br />-   IntegratedWindowsAuthentication：指定 Windows 身份验证。<br /><br /> 默认值为 Anonymous。  此属性的类型为 <xref:System.Net.AuthenticationSchemes>。|  
|realm|一个指定要在代理\/服务器上使用的领域的字符串。  默认值为一个空字符串。<br /><br /> 服务器使用领域将受保护的资源分区。  每个分区都可以有自己的身份验证方案和\/或授权数据库。  领域仅用于基本和摘要式身份验证。  在客户端成功进行身份验证之后，该身份验证对给定领域内的所有资源都有效。  有关领域的详细说明，请参见位于 http:\/\/www.ietf.org 的 RFC 2617。|  
|transferMode|指定对消息进行缓冲处理还是流式处理，或者指定消息是请求还是响应。  包括以下有效值：<br /><br /> -   Buffered：对请求和响应消息进行缓冲处理。<br />-   Streamed：对请求和响应消息进行流式处理。<br />-   StreamedRequest：对请求消息进行流式处理，对响应消息进行缓冲处理。<br />-   StreamedResponse：对请求消息进行缓冲处理，对响应消息进行流式处理。<br /><br /> 默认值为 Buffered。  此属性的类型为 <xref:System.ServiceModel.TransferMode>。|  
|unsafeConnectionNtlmAuthentication|一个布尔值，指定是否在服务器上启用不安全连接共享。  默认值为 `false`。  如果启用，将对每个 TCP 连接执行一次 NTLM 身份验证。|  
|useDefaultWebProxy|一个布尔值，指定是否使用计算机范围的代理设置，而不使用用户特定的设置。  默认值为 `true`。|  
  
### 子元素  
 无  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<绑定\>](../../../../../docs/framework/misc/binding.md)|定义自定义绑定的所有绑定功能。|  
  
## 备注  
 `httpTransport` 元素是创建实现 HTTP 传输协议的自定义绑定的起始点。  HTTP 是用于互操作性用途的主要传输。  [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 支持此传输以确保与其他非 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] Web 服务堆栈的互操作性。  
  
## 请参阅  
 <xref:System.ServiceModel.Configuration.HttpTransportElement>   
 <xref:System.ServiceModel.Channels.HttpTransportBindingElement>   
 <xref:System.ServiceModel.Channels.TransportBindingElement>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 [传输](../../../../../docs/framework/wcf/feature-details/transports.md)   
 [选择传输方式](../../../../../docs/framework/wcf/feature-details/choosing-a-transport.md)   
 [绑定](../../../../../docs/framework/wcf/bindings.md)   
 [扩展绑定](../../../../../docs/framework/wcf/extending/extending-bindings.md)   
 [自定义绑定](../../../../../docs/framework/wcf/extending/custom-bindings.md)   
 [\<customBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)