---
title: "Implements 子句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.ImplementsClause"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Implements 关键字"
  - "Implements 语句, 关于 Implements"
  - "接口实现, Implements 关键字"
  - "接口实现, 重新实现"
  - "接口成员"
  - "接口成员, 实现"
  - "接口成员, Implements 关键字"
  - "接口成员, 重新实现"
  - "成员, 实现"
  - "成员, Implements 关键字"
  - "成员, 重新实现"
  - "重新实现"
ms.assetid: 5252cdf9-964d-4fc6-af0f-0449b7126b5a
caps.latest.revision: 15
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 15
---
# Implements 子句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指示类或结构成员正在为接口中所定义的成员提供实现。  
  
## 备注  
 `Implements` 关键字与 [Implements 语句](../../../visual-basic/language-reference/statements/implements-statement.md) 不同。  先使用 `Implements` 语句指定由类或结构实现一个或多个接口，然后再使用 `Implements` 关键字为每个成员指定该成员要实现哪个接口和成员。  
  
 如果类或结构实现了一个接口，那么它必须在 [Class 语句](../../../visual-basic/language-reference/statements/class-statement.md) 或 [Structure 语句](../../../visual-basic/language-reference/statements/structure-statement.md) 之后紧跟 `Implements` 语句，并且必须实现该接口所定义的所有成员。  
  
## 重新实现  
 在派生类中，您可以重新实现基类已经实现的接口成员。  这一点在以下方面与重写基类成员有所不同：  
  
-   若要被重新实现，基类成员不一定非得是 [Overridable](../../../visual-basic/language-reference/modifiers/overridable.md)。  
  
-   可以采用不同的名称重新实现该成员。  
  
 `Implements` 关键字可用于下面的上下文中：  
  
 [Event 语句](../../../visual-basic/language-reference/statements/event-statement.md)  
  
 [Function 语句](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Property 语句](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Sub 语句](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## 请参阅  
 [Implements 语句](../../../visual-basic/language-reference/statements/implements-statement.md)   
 [Interface 语句](../../../visual-basic/language-reference/statements/interface-statement.md)   
 [Class 语句](../../../visual-basic/language-reference/statements/class-statement.md)   
 [Structure 语句](../../../visual-basic/language-reference/statements/structure-statement.md)