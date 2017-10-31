---
title: "安全和公共只读数组字段 | Microsoft Docs"
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
  - "安全性 [.NET Framework], 公共只读数组字段"
ms.assetid: 3df28dee-2a9f-40ff-9852-bfdbe59c27f3
caps.latest.revision: 7
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 7
---
# 安全和公共只读数组字段
一定不要使用托管库的公共只读数组字段来定义应用程序的边界行为或安全性，因为公共只读数组字段可以被修改。  
  
## 备注  
 某些 .NET Framework 类中提供包含平台特定边界参数的只读公共字段。例如，<xref:System.IO.Path.InvalidPathChars> 字段是一个数组，该数组描述文件路径字符串中不允许使用的字符。在整个 .NET Framework 中存在许多类似的字段。  
  
 可以通过您的代码或共享其应用程序域的代码来修改公共只读字段（如 <xref:System.IO.Path.InvalidPathChars>）的值。不应使用这样的公共只读数组字段来定义应用程序的边界行为。否则，恶意代码可能会更改边界定义并以出乎意料的方式使用您的代码。  
  
 在 .NET Framework 2.0 版和更高版本中，应使用可返回新数组的方法，而不应使用公共数组字段。例如，您不应使用 <xref:System.IO.Path.InvalidPathChars> 字段，而应使用 <xref:System.IO.Path.GetInvalidPathChars%2A> 方法。  
  
 注意，.NET Framework 类型不使用公共字段在内部定义边界类型。.NET Framework 改用单独的私有字段。更改这些公共字段的值不会改变 .NET Framework 类型的行为。  
  
## 请参阅  
 [代码安全维护指南](../../../docs/standard/security/secure-coding-guidelines.md)