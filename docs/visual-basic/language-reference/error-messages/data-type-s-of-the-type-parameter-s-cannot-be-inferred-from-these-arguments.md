---
title: "无法根据这些实参推断类型形参的数据类型 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc36644"
  - "bc36647"
  - "vbc36647"
  - "vbc36644"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC36644"
  - "BC36647"
ms.assetid: 0e0050f2-2039-4311-b260-f0ebfde84189
caps.latest.revision: 6
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 6
---
# 无法根据这些实参推断类型形参的数据类型
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

无法从这些实参推断类型形参的数据类型。此错误可以通过显式指定数据类型来更正。  
  
 当重载决策失败时发生此错误。  它以从属消息的形式发生，该消息指出已消除特定的重载候选。  此错误消息解释编译器无法使用类型推断功能来确定类型形参的数据类型。  
  
> [!NOTE]
>  当无法指定实参时（例如，对于查询表达式中的查询运算符），显示的错误消息不包括第二个句子。  
  
 下面的代码演示此错误。  
  
```vb#  
Module Module1  
  
    Sub Main()  
  
        '' Not Valid.  
        'OverloadedGenericMethod("Hello", "World")  
  
    End Sub  
  
    Sub OverloadedGenericMethod(Of T)(ByVal x As String,   
                                      ByVal y As InterfaceExample(Of T))  
    End Sub  
  
    Sub OverloadedGenericMethod(Of T, R)(ByVal x As T,   
                                         ByVal y As InterfaceExample(Of R))  
    End Sub  
  
End Module  
  
Interface InterfaceExample(Of T)  
End Interface  
```  
  
 **错误 ID：**BC36647 和 BC36644  
  
### 更正此错误  
  
-   您或许能够指定类型形参的数据类型，而无需依赖类型推断。  
  
## 请参阅  
 [宽松委托转换](../../../visual-basic/programming-guide/language-features/delegates/relaxed-delegate-conversion.md)   
 [Visual Basic 中的泛型过程](../../../visual-basic/programming-guide/language-features/data-types/generic-procedures.md)   
 [Visual Basic 中的类型转换](../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)