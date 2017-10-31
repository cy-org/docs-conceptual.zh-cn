---
title: "LocalServiceSecuritySettings | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 490aa0e5-5242-4f8d-b505-5ec6287633b4
caps.latest.revision: 8
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 8
---
# LocalServiceSecuritySettings
LocalServiceSecuritySettings  
  
## 语法  
  
```  
class LocalServiceSecuritySettings  
{  
  boolean DetectReplays;  
  datetime InactivityTimeout;  
  datetime IssuedCookieLifetime;  
  sint32 MaxCachedCookies;  
  datetime MaxClockSkew;  
  sint32 MaxPendingSessions;  
  sint32 MaxStatefulNegotiations;  
  datetime NegotiationTimeout;  
  boolean ReconnectTransportOnFailure;  
  sint32 ReplayCacheSize;  
  datetime ReplayWindow;  
  datetime SessionKeyRenewalInterval;  
  datetime SessionKeyRolloverInterval;  
  datetime TimestampValidityDuration;  
};  
```  
  
## 方法  
 LocalServiceSecuritySettings 类未定义任何方法。  
  
## 属性  
 LocalServiceSecuritySettings 类具有以下属性：  
  
### DetectReplays  
 数据类型：Boolean  
  
 访问类型：只读  
  
 一个布尔值，指定是否自动检测和处理针对通道的重放攻击。  
  
### InactivityTimeout  
 数据类型：DateTime  
  
 访问类型：只读  
  
 服务支持的最大挂起安全会话数。  
  
### IssuedCookieLifetime  
 数据类型：DateTime  
  
 访问类型：只读  
  
 一个时间跨度，指定颁发给所有新的安全 Cookie 的生存期。  
  
### MaxCachedCookies  
 数据类型：sint32  
  
 访问类型：只读  
  
 可以缓存的最大 Cookie 数。  
  
### MaxClockSkew  
 数据类型：DateTime  
  
 访问类型：只读  
  
 一个时间跨度，指定通信双方系统时钟之间的最大时间差。  
  
### MaxPendingSessions  
 数据类型：sint32  
  
 访问类型：只读  
  
 服务上的最大挂起连接数。  
  
### MaxStatefulNegotiations  
 数据类型：sint32  
  
 访问类型：只读  
  
 可以同时处于活动状态的安全协商数。  
  
### NegotiationTimeout  
 数据类型：DateTime  
  
 访问类型：只读  
  
 一个时间跨度，指定服务器和客户端之间的安全协商阶段的最大持续时间。  
  
### ReconnectTransportOnFailure  
 数据类型：Boolean  
  
 访问类型：只读  
  
 一个布尔值，指定使用 WS\-ReliableMessaging 的连接是否将在传输失败后尝试重新连接。  
  
### ReplayCacheSize  
 数据类型：sint32  
  
 访问类型：只读  
  
 用于重播检测的缓存 Nonce 的数目。  
  
### ReplayWindow  
 数据类型：DateTime  
  
 访问类型：只读  
  
 一个时间跨度，指定单个消息 Nonce 的有效持续时间。  
  
### SessionKeyRenewalInterval  
 数据类型：DateTime  
  
 访问类型：只读  
  
 一个时间跨度，指定一个持续时间，发起方将在此段时间之后续订安全会话的密钥。  
  
### SessionKeyRolloverInterval  
 数据类型：DateTime  
  
 访问类型：只读  
  
 一个时间跨度，指定在密钥续订期间，上一个会话密钥对于传入消息有效的时间间隔。  
  
### TimestampValidityDuration  
 数据类型：DateTime  
  
 访问类型：只读  
  
 一个时间跨度，指定时间戳的有效持续时间。  
  
## 要求  
  
|MOF|在 Servicemodel.mof 中声明。|  
|---------|-----------------------------|  
|命名空间|已在 root\\ServiceModel 中定义|  
  
## 请参阅  
 <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings>