---
title: "服务：Security Validation and Authentication Failures Per Second（每秒安全验证和身份验证失败次数） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4af18009-e778-490b-9ba6-e76485285830
caps.latest.revision: 9
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 9
---
# 服务：Security Validation and Authentication Failures Per Second（每秒安全验证和身份验证失败次数）
计数器名称：Security Validation and Authentication Failures Per Second（每秒安全验证和身份验证失败次数）。  
  
## 说明  
 每当消息由于“Security Calls Not Authorized”（未授权的安全调用次数）计数器中未包括的安全问题而遭到拒绝时，此计数器即会递增。此类问题包括：  
  
-   无法从消息中读取客户端令牌。  
  
-   客户端令牌身份验证失败（如密码错误）。  
  
-   签名验证失败（如消息已被篡改）。  
  
-   消息与上一条消息重复，这种情况可能在重放攻击过程中发生。  
  
-   已发生解密失败。  
  
-   消息中缺少一些必需元素（如缺少时间戳或加密的数据块）。  
  
-   TLSNEGO\/SPNEGO 握手过程中已发生错误。  
  
 此计数器为性能计数器类型 [PERF\_COUNTER\_COUNTER](http://go.microsoft.com/fwlink/?LinkID=94649)，其值是使用以下公式计算的：  
  
 \(N 1 \- N 0 \) \/ \( \(D 1 \-D 0 \) \/ F\)