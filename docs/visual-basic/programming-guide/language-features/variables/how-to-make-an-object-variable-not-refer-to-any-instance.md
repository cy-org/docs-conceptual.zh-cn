---
title: "如何：使对象变量不引用任何实例 (Visual Basic) | Microsoft Docs"
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
  - "Nothing 关键字, 变量赋值"
  - "对象变量, null 引用"
ms.assetid: e6d30578-bdae-4142-a3ac-a10697bf696a
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# 如何：使对象变量不引用任何实例 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

可以通过将对象变量设置为 [Nothing](../../../../visual-basic/language-reference/nothing.md) 来取消对象变量与任何对象实例的关联。  
  
### 取消对象变量与任何对象实例的关联  
  
-   在赋值语句中将变量设置为 `Nothing`。  
  
    ```  
    ' Assume account is a defined class  
    Dim currentAccount As account  
    currentAccount = Nothing  
    ```  
  
## 可靠编程  
 如果代码尝试访问一个已经设置为 `Nothing` 的对象变量的成员，则会发生 <xref:System.NullReferenceException>。  如果要经常将一个对象变量设置为 `Nothing`，或对象变量可能未初始化，则最好将成员访问包含在一个 `Try...Catch...Finally` 块中。  
  
## .NET Framework 安全性  
 如果对象变量要用于包含机密或敏感数据的对象，则可以在不主动处理这些对象时将该变量设置为 `Nothing`。  这可以减少恶意代码获得数据访问的机会。  
  
## 请参阅  
 <xref:System.NullReferenceException>   
 [对象变量](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)   
 [对象变量赋值](../../../../visual-basic/programming-guide/language-features/variables/object-variable-assignment.md)   
 [Nothing](../../../../visual-basic/language-reference/nothing.md)   
 [Try...Catch...Finally 语句](../../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)   
 [关于异常的疑难解答：System.NullReferenceException](../Topic/Troubleshooting%20Exceptions:%20System.NullReferenceException.md)