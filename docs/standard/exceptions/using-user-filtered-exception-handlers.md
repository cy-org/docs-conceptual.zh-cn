---
title: "使用用户筛选的异常处理程序 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "异常, 用户筛选"
  - "用户筛选的异常"
ms.assetid: aa80d155-060d-41b4-a636-1ceb424afee8
caps.latest.revision: 10
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 8
---
# 使用用户筛选的异常处理程序
目前，Visual Basic 支持用户筛选的异常。  用户筛选的异常处理程序根据您为异常定义的要求捕捉和处理异常。  这些处理程序将 **Catch** 语句和 **When** 关键字结合使用。  
  
 当一个特定的异常对象对应于多个错误时，此方法很有用。  在那种情况下，对象通常有一个属性包含与错误关联的特定错误代码。  可以在表达式中使用此错误代码属性，仅选择要在 **Catch** 子句中处理的特定错误。  
  
 下面的 Visual Basic 示例阐释 **Catch\/When** 语句。  
  
```  
Try  
      'Try statements.  
   Catch When Err = VBErr_ClassLoadException  
      'Catch statements.  
End Try  
```  
  
 用户筛选的子句表达式不受任何形式的限制。  如果执行用户筛选的表达式时发生异常，将会丢弃该异常，并认为该筛选表达式的计算结果为 false。  在这种情况下，公共语言运行时继续搜索处理程序，以找到当前异常。  
  
## 组合特定异常与用户筛选的子句  
 Catch 语句可同时包含特定异常和用户筛选的子句。  运行时首先测试特定异常。  如果特定异常成功，则运行时执行用户筛选器。  一般筛选器可包含对类筛选器中声明的变量的引用。  请注意，两个筛选器子句的顺序不可逆转。  
  
 下面的 Visual Basic 示例演示 **Catch** 语句以及使用 **When** 关键字的用户筛选子句中的特定异常 `ClassLoadException`。  
  
```  
Try  
      'Try statements.  
   Catch cle As ClassLoadException When cle.IsRecoverable()  
      'Catch statements.  
End Try  
```  
  
## 请参阅  
 [如何：使用 Try\/Catch 块捕捉异常](../../../docs/standard/exceptions/how-to-use-the-try-catch-block-to-catch-exceptions.md)   
 [如何：在 Catch 块中使用特定异常](../../../docs/standard/exceptions/how-to-use-specific-exceptions-in-a-catch-block.md)   
 [异常的最佳做法](../../../docs/standard/exceptions/best-practices-for-exceptions.md)   
 [异常处理基础知识](../../../docs/standard/exceptions/exception-handling-fundamentals.md)