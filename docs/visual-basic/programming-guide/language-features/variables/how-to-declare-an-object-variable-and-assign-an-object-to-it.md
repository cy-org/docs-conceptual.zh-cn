---
title: "如何：在 Visual Basic 中声明对象变量并为它分配对象 | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "声明对象变量"
  - "对象变量, 声明"
ms.assetid: 2fa77dde-1fb2-439a-80d4-3e9787649fad
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# 如何：在 Visual Basic 中声明对象变量并为它分配对象
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

通过在 [Dim 语句](../../../../visual-basic/language-reference/statements/dim-statement.md) 中指定 `As Object`，可以声明 [Object 数据类型](../../../../visual-basic/language-reference/data-types/object-data-type.md) 的变量。  您可以通过在分配语句或初始化子句中将某对象放置在等号 \(`=`\) 后面来为这种变量分配该对象。  
  
## 示例  
 下面的示例声明 `Object` 变量并将当前实例分配给它。  
  
```  
  
      Dim thisObject As Object  
thisObject = "This is an Object"  
```  
  
 您可以将声明和分配合并在一起，方法为：将变量初始化为它的声明的一部分。  下面的示例与前一个示例是等效的。  
  
```  
Dim thisObject As Object = "This is an Object"  
```  
  
## 编译代码  
 此示例需要：  
  
-   对 <xref:System> 命名空间的引用。  
  
-   要在其中放置 `Dim` 语句的类、结构或模块。  
  
-   要在其中放置分配语句的过程。  
  
## 请参阅  
 [变量声明](../../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [对象变量](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)   
 [对象变量声明](../../../../visual-basic/programming-guide/language-features/variables/object-variable-declaration.md)   
 [Object 数据类型](../../../../visual-basic/language-reference/data-types/object-data-type.md)   
 [Dim 语句](../../../../visual-basic/language-reference/statements/dim-statement.md)   
 [局部类型推理](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Option Strict 语句](../../../../visual-basic/language-reference/statements/option-strict-statement.md)