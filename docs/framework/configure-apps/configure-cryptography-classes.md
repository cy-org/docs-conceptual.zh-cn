---
title: "配置加密类 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - ".NET Framework 应用程序配置, 密码系统"
  - "配置文件 [.NET Framework], 密码系统"
  - "加密算法"
  - "密码系统, 类"
  - "默认密码系统"
  - "安全性 [.NET Framework], 加密"
ms.assetid: eee3ccb8-2c0d-4f35-b38d-6892a46c14e5
caps.latest.revision: 9
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 9
---
# 配置加密类
[!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)] 允许计算机管理员配置默认加密算法和算法实现，供 .NET Framework 和正确编写的应用程序使用。例如，一个企业可以将自己的加密算法实现设置为默认实现，而不是使用 [!INCLUDE[winsdkshort](../../../includes/winsdkshort-md.md)] 中提供的算法实现。  虽然使用加密技术的托管应用程序总是可以选择显式地绑定到特定的实现，但仍建议它们通过使用加密配置系统来创建加密对象。  
  
## 本节内容  
 [将算法名称映射到加密类](../../../docs/framework/configure-apps/map-algorithm-names-to-cryptography-classes.md)  
 描述如何将算法名称映射到加密类。  
  
 [将对象标识符映射到加密算法](../../../docs/framework/configure-apps/map-object-identifiers-to-cryptography-algorithms.md)  
 描述如何将对象标识符映射到加密算法。  
  
## 相关章节  
 [加密服务](../../../docs/standard/security/cryptographic-services.md)  
 概述 [!INCLUDE[winsdkshort](../../../includes/winsdkshort-md.md)] 所提供的加密服务。  
  
 [加密设置架构](../../../docs/framework/configure-apps/file-schema/cryptography/index.md)  
 描述将友好算法名映射到实现密码算法的类的元素。