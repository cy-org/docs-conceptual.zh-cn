---
title: "Auto (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Auto"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Auto 关键字"
  - "Auto 关键字, 外部引用"
  - "Auto 关键字, 封送处理字符串"
  - "Declare 语句, 封送处理字符串"
ms.assetid: bf79ba95-a62c-48a5-916f-0ac7a52c13ec
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# Auto (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定 Visual Basic 应根据基于被声明的外部过程的外部名称的 .NET Framework 规则封送字符串。  
  
 调用在项目外定义的过程时，Visual Basic 编译器不能访问正确调用过程所需的信息。  这些信息包括过程所在位置、标识方式、调用序列和返回类型以及它所使用的字符串字符集。  [Declare 语句](../../../visual-basic/language-reference/statements/declare-statement.md) 创建一个对外部过程的引用并提供这些必需的信息。  
  
 `Declare` 语句中的 `charsetmodifier` 部分提供在调用外部过程期间封送字符串所需的字符集信息。  它还影响 Visual Basic 在外部文件中搜索外部过程名称的方式。  `Auto` 修饰符指定 Visual Basic 应根据 .NET Framework 规则封送字符串，并指定 Visual Basic 应确定运行时平台的基字符集，并且在最初搜索失败的情况下，修改外部过程名称。  有关更多信息，请参见 [Declare 语句](../../../visual-basic/language-reference/statements/declare-statement.md) 中的“字符集”。  
  
 如果没有指定字符集修饰符，则默认使用 `Ansi`。  
  
## 备注  
 `Auto` 修饰符可用于下面的上下文中：  
  
 [Declare 语句](../../../visual-basic/language-reference/statements/declare-statement.md)  
  
## 智能设备开发人员说明  
 不支持此关键字。  
  
## 请参阅  
 [Ansi](../../../visual-basic/language-reference/modifiers/ansi.md)   
 [Unicode](../../../visual-basic/language-reference/modifiers/unicode.md)   
 [关键字](../../../visual-basic/language-reference/keywords/index.md)