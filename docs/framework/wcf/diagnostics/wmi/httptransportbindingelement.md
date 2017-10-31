---
title: "HttpTransportBindingElement | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 088a7bce-6bb2-4839-ad74-f68d4b1aa0f9
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# HttpTransportBindingElement
HttpTransportBindingElement  
  
## 语法  
  
```  
class HttpTransportBindingElement : TransportBindingElement  
{  
  boolean AllowCookies;  
  string AuthenticationScheme;  
  boolean BypassProxyOnLocal;  
  string HostNameComparisonMode;  
  boolean KeepAliveEnabled;  
  sint32 MaxBufferSize;  
  string ProxyAddress;  
  string ProxyAuthenticationScheme;  
  string Realm;  
  string TransferMode;  
  boolean UnsafeConnectionNtlmAuthentication;  
  boolean UseDefaultWebProxy;  
};  
```  
  
## 方法  
 HttpTransportBindingElement 类未定义任何方法。  
  
## 属性  
 HttpTransportBindingElement 类具有以下属性：  
  
### AllowCookies  
 数据类型：Boolean  
  
 访问类型：只读  
  
 一个值，指示客户端是否接受 cookie 并根据将来的请求对其进行传播。  
  
### AuthenticationScheme  
 数据类型：String  
  
 访问类型：只读  
  
 用来验证 HTTP 侦听器正在处理的客户端请求的身份验证方案。  
  
### BypassProxyOnLocal  
 数据类型：Boolean  
  
 访问类型：只读  
  
 一个值，指示是否忽略本地地址的代理。  
  
### HostNameComparisonMode  
 数据类型：String  
  
 访问类型：只读  
  
 一个值，指示在对 URI 进行匹配时，是否使用主机名来访问服务。  
  
### KeepAliveEnabled  
 数据类型：Boolean  
  
 访问类型：只读  
  
 启用后，HTTP 连接将保持活动状态，无论是什么活动级别。  
  
### MaxBufferSize  
 数据类型：sint32  
  
 访问类型：只读  
  
 缓冲池的最大大小。  
  
### ProxyAddress  
 数据类型：String  
  
 访问类型：只读  
  
 一个 URI，包含用于 HTTP 请求的代理地址。  
  
### ProxyAuthenticationScheme  
 数据类型：String  
  
 访问类型：只读  
  
 用来验证 HTTP 代理正在处理的客户端请求的身份验证方案。  
  
### Realm  
 数据类型：String  
  
 访问类型：只读  
  
 身份验证领域。  
  
### TransferMode  
 数据类型：String  
  
 访问类型：只读  
  
 一个值，指定对消息进行缓冲处理还是流式处理，或者指定消息是请求还是响应。  
  
### UnsafeConnectionNtlmAuthentication  
 数据类型：Boolean  
  
 访问类型：只读  
  
 一个值，指示服务器上是否启用了不安全连接共享。  
  
### UseDefaultWebProxy  
 数据类型：Boolean  
  
 访问类型：只读  
  
 一个值，指示是否使用计算机范围的代理设置，而不使用用户特定的设置。  
  
## 要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|------------------------------|  
|命名空间|已在 root\\ServiceModel 中定义|  
  
## 请参阅  
 <xref:System.ServiceModel.Channels.HttpTransportBindingElement>