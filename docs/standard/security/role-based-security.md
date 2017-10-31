---
title: "基于角色的安全性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "身份验证 [.NET Framework], 用户"
  - "权限 [.NET Framework], 用户"
  - "主体 [.NET Framework]"
  - "基于角色的安全性, 关于基于角色的安全"
  - "基于角色的安全性, 用户"
  - "安全性 [.NET Framework], 基于角色"
  - "用户身份验证, 用户"
ms.assetid: 578cc32b-5654-4d8b-9d8c-ebcbc5c75390
caps.latest.revision: 13
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 13
---
# 基于角色的安全性
在财务或业务应用程序中经常使用角色来强制执行策略。  例如，应用程序可能会根据发出请求的用户是否是指定角色的成员，以限制其所处理事务的大小。  职员处理事务的授权可能低于所指定阈值，主管可能具有更高的限制，而副总裁可能具有比主管更高的限制（或无限制）。  当应用程序需要多项审批来完成操作时，也可以使用基于角色的安全性。  这种情况可能发生在采购系统中，任何员工均可生成采购请求，但只有采购代理可以将此请求转换成可发送给供应商的采购订单。  
  
 .NET Framework 基于角色的安全性通过生成与主体相关的信息来支持授权，此主体用关联的标识进行构造，可用于当前线程。  标识（和其帮助定义的主体）可以基于 Windows 帐户，或可以为与 Windows 帐户无关的自定义标识。  .NET framework 应用程序可以基于主体的标识和\/或角色成员身份做出授权决策。  角色是指在安全性方面具有相同特权的一组命名主体（如出纳或经理）。  主体可以是一个或多个角色的成员。  因此，应用程序可以使用角色成员身份来确定主体是否有权执行所请求的操作。  
  
 若要使用代码访问安全性提供易用性和一致性，.NET Framework 基于角色的安全性会提供 <xref:System.Security.Permissions.PrincipalPermission?displayProperty=fullName> 对象，此对象启用公共语言运行时，从而以与代码访问安全性检查类似的方式执行授权。  <xref:System.Security.Permissions.PrincipalPermission> 类表示主体必须与之匹配，并且与两种声明性和命令性安全检查相兼容的标识和角色。  还可以直接访问主体的标识信息，并在需要时在代码中执行角色和标识检查。  
  
 .NET Framework 提供基于角色的安全性支持，其灵活并且可扩展，足以满足各种应用程序的需求。  你可以选择与现有身份验证基础结构进行交互操作（如 COM\+ 1.0 服务）或创建自定义身份验证系统。  基于角色的安全性非常适合在主要在服务器上进行处理 ASP.NET Web 应用程序中使用。  但是，.NET Framework 基于角色的安全性可以在客户端或服务器上使用。  
  
 在阅读此章节前，务必先理解[安全性的基础概念](../../../docs/standard/security/key-security-concepts.md)中的材料。  
  
## 相关主题  
  
|标题|描述|  
|--------|--------|  
|[主体和标识对象](../../../docs/standard/security/principal-and-identity-objects.md)|说明如何设置和管理 Windows 和通用的标识与主体。|  
|[安全性的基础概念](../../../docs/standard/security/key-security-concepts.md)|介绍使用.NET Framework 安全性之前必须了解的基本概念。|  
  
## 参考  
 <xref:System.Security.Permissions.PrincipalPermission?displayProperty=fullName>