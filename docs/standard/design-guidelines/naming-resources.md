---
title: "命名资源 | Microsoft Docs"
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
  - "名称 [.NET Framework] 本地化资源"
  - "本地化，命名准则"
  - "资源名称"
  - "全局应用程序，命名准则"
  - "国际应用程序，命名准则"
ms.assetid: 8b0e97f3-7877-44fd-bc76-e05d36d5d79c
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# 命名资源
可本地化的资源可通过某些对象引用，就好像属性，因为资源的命名准则在类似于属性指南。  
  
 **✓ 执行** 使用 PascalCasing 中的资源键。  
  
 **✓ 执行** 提供描述性而不是短标识符。  
  
 **X 不** 使用主 CLR 语言的特定于语言的关键字。  
  
 **✓ 执行** 使用仅字母数字字符和下划线在命名资源中的。  
  
 **✓ 执行** 对异常消息资源使用以下命名约定。  
  
 资源标识符应为异常类型名称加上该异常的短标识符︰  
  
 `ArgumentExceptionIllegalCharacters`   
 `ArgumentExceptionInvalidName`   
 `ArgumentExceptionFileNameIsMalformed`  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)   
 [命名准则](../../../docs/standard/design-guidelines/naming-guidelines.md)