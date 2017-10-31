---
title: "Erase 语句 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Erase"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Erase 关键字"
  - "Erase 语句"
ms.assetid: 7a8133d7-b750-4d74-8b66-ba1dd9778d4b
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# Erase 语句 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

用来释放数组变量和解除分配用于它们的元素的内存。  
  
## 语法  
  
```  
Erase arraylist  
```  
  
## 部件  
 `arraylist`  
 必选。  要删除的数组变量列表。  以逗号分隔多个变量。  
  
## 备注  
 `Erase` 语句只能出现在过程级别。  这意味着可以在过程中而不是在类或模块级释放数组。  
  
 `Erase` 语句等效于将 `Nothing` 分配给每一数组变量。  
  
## 示例  
 下面的示例使用 `Erase` 语句清除两个数组并释放其内存（分别保存有 1000 和 100 个存储元素）。  然后，`ReDim` 语句将新的数组实例赋给其中的三维数组。  
  
 [!code-vb[VbVbalrStatements#19](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/erase-statement_1.vb)]  
  
## 请参阅  
 [Nothing](../../../visual-basic/language-reference/nothing.md)   
 [ReDim 语句](../../../visual-basic/language-reference/statements/redim-statement.md)