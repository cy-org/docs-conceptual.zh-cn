---
title: "如何：在 Visual Basic 中对数组进行排序 | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "Array.Sort"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "数组 [Visual Basic], 排序"
  - "示例 [Visual Basic], 数组"
ms.assetid: 9289aeaa-9626-4698-94a7-1d1fd3702b87
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# 如何：在 Visual Basic 中对数组进行排序
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

此示例声明名为 `zooAnimals` 的 `String` 对象的数组，填充它，然后按字母顺序对其排序。  
  
## 示例  
  
```  
Private Sub sortAnimals()  
    Dim zooAnimals(2) As String  
    zooAnimals(0) = "lion"  
    zooAnimals(1) = "turtle"  
    zooAnimals(2) = "ostrich"  
    Array.Sort(zooAnimals)  
End Sub  
```  
  
## 编译代码  
 此示例需要：  
  
-   对 Mscorlib.dll 和 <xref:System> 命名空间的访问权限。  
  
## 可靠编程  
 以下情况可能会导致异常：  
  
-   数组是空的（<xref:System.ArgumentNullException> 类）  
  
-   数组是多维的（<xref:System.RankException> 类）  
  
-   数组的一个或多个元素没有实现 <xref:System.IComparable> 接口（<xref:System.InvalidOperationException> 类）  
  
## 请参阅  
 <xref:System.Array.Sort%2A?displayProperty=fullName>   
 [数组](../../../../visual-basic/programming-guide/language-features/arrays/index.md)   
 [数组疑难解答](../../../../visual-basic/programming-guide/language-features/arrays/troubleshooting-arrays.md)   
 [集合](../Topic/Collections%20\(C%23%20and%20Visual%20Basic\).md)   
 [For Each...Next 语句](../../../../visual-basic/language-reference/statements/for-each-next-statement.md)