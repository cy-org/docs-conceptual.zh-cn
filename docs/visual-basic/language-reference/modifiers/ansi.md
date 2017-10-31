---
title: "Ansi (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Ansi"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "ANSI"
  - "ANSI, Visual Basic"
  - "Declare 语句, 封送处理字符串"
ms.assetid: 4f1fa6ff-5557-41ab-b6da-90baf4c15917
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# Ansi (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

指定 Visual Basic 应将所有字符串封送到 American National Standards Institute \(ANSI\) 值，不管所声明的外部过程的名称是什么。  
  
 调用在项目外定义的过程时，Visual Basic 编译器不能访问正确调用过程所需的信息。  这些信息包括过程所在位置、标识方式、调用序列和返回类型以及它所使用的字符串字符集。  [Declare 语句](../../../visual-basic/language-reference/statements/declare-statement.md) 创建一个对外部过程的引用并提供这些必需的信息。  
  
 `Declare` 语句中的 `charsetmodifier` 部分提供在调用外部过程期间封送字符串所需的字符集信息。  它还影响 Visual Basic 在外部文件中搜索外部过程名称的方式。  `Ansi` 修饰符指定 Visual Basic 应将所有字符串封送到 ANSI 值，并应查询该过程，同时在搜索期间不修改过程的名称。  
  
 如果没有指定字符集修饰符，则默认使用 `Ansi`。  
  
## 备注  
 `Ansi` 修饰符可用于下面的上下文中：  
  
 [Declare 语句](../../../visual-basic/language-reference/statements/declare-statement.md)  
  
## 智能设备开发人员说明  
 不支持此关键字。  
  
## 请参阅  
 [Auto](../../../visual-basic/language-reference/modifiers/auto.md)   
 [Unicode](../../../visual-basic/language-reference/modifiers/unicode.md)   
 [关键字](../../../visual-basic/language-reference/keywords/index.md)