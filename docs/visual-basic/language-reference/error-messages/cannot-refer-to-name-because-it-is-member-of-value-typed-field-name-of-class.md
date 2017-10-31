---
title: "“&lt;名称&gt;”是使用“System.MarshalByRefObject”作为基类的类“&lt;类名&gt;”的值类型字段“&lt;名称&gt;”的成员，无法引用 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30310"
  - "bc30310"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30310"
ms.assetid: 2aeb8872-7c87-4f01-98ef-9714ba3eebbe
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# “&lt;名称&gt;”是使用“System.MarshalByRefObject”作为基类的类“&lt;类名&gt;”的值类型字段“&lt;名称&gt;”的成员，无法引用
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

`System.MarshalByRefObject` 类使应用程序支持远程访问跨越应用程序域边界的对象。  当跨越应用程序域边界使用类型时，类型必须从 `MarshalByRejectObject` 类继承。  由于对象的成员无法在创建它们的应用程序域之外使用，因此不能复制对象的状态。  
  
 **错误 ID：**BC30310  
  
### 更正此错误  
  
1.  检查引用以确保被引用的成员是有效的。  
  
2.  用 `Me` 关键字显式限定该成员。  
  
## 请参阅  
 <xref:System.MarshalByRefObject>   
 [Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md)