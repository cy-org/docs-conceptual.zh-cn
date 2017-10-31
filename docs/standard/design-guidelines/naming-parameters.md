---
title: "命名参数 | Microsoft Docs"
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
  - "参数名称"
  - "参数的名称 [.NET Framework]"
ms.assetid: ca3c956e-725a-441b-b4e3-eab5d472f41c
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# 命名参数
超出的可读性明显的原因，务必遵循参数名称的指南，因为参数显示在文档中且在设计器中时，可视化设计工具提供 Intellisense 和浏览功能的类。  
  
 **✓ 执行** 在参数名称中使用 camelcasing 大小写约定。  
  
 **✓ 执行** 使用描述性的参数名称。  
  
 **✓ 请考虑** 使用基于参数的含义，而不是参数的类型的名称。  
  
### 命名的运算符重载参数  
 **✓ 执行** 使用 `left` 和 `right` 为二元运算符重载参数名称是否存在到参数没有意义。  
  
 **✓ 执行** 使用 `value` 的一元运算符重载的参数名称，如果没有任何意义的参数。  
  
 **✓ 请考虑** 有意义的名称，运算符重载的参数，如果这样做会增加巨大的价值。  
  
 **X 不** 使用缩写或数值索引运算符重载的参数名称。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)   
 [命名准则](../../../docs/standard/design-guidelines/naming-guidelines.md)