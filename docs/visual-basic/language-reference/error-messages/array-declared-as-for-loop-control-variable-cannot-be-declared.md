---
title: "声明为 For Each 循环控制变量的数组在声明时不能指定初始大小值 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc32039"
  - "bc32039"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC32039"
ms.assetid: 1d8b6560-c9eb-4b71-a038-24c6f5a5ce46
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# 声明为 For Each 循环控制变量的数组在声明时不能指定初始大小值
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

`For Each` 循环使用一个数组作为其*元素* 迭代变量，但会初始化该数组。  
  
 下面的语句演示此错误是如何生成的。  
  
```  
Dim arrayList As New List(Of Integer())  
For Each listElement() As Integer In arrayList  
For Each listElement(1) As Integer In arrayList  
```  
  
 第一条 `For Each` 语句是访问 `arrayList` 的元素的正确方法。  第二条 `For Each` 语句生成此错误。  
  
 **错误 ID：**BC32039  
  
### 更正此错误  
  
-   从*元素* 迭代变量的声明中移除该初始化。  
  
## 请参阅  
 [For...Next 语句](../../../visual-basic/language-reference/statements/for-next-statement.md)   
 [数组](../../../visual-basic/programming-guide/language-features/arrays/index.md)   
 [集合](../Topic/Collections%20\(C%23%20and%20Visual%20Basic\).md)