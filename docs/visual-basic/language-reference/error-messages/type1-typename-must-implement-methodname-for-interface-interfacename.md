---
title: "&lt;类型 1&gt;“&lt;类型名&gt;”必须为接口“&lt;接口名&gt;”实现“&lt;方法名&gt;” | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30149"
  - "bc30149"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30149"
ms.assetid: 29d1b7f4-dca7-478c-bbe7-c657f342c183
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# &lt;类型 1&gt;“&lt;类型名&gt;”必须为接口“&lt;接口名&gt;”实现“&lt;方法名&gt;”
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

类或结构要求实现接口，但没有实现由该接口定义的过程。  必须实现接口的每个成员。  
  
 **错误 ID：**BC30149  
  
### 更正此错误  
  
1.  用与接口中定义的名称和签名相同的名称和签名声明一个过程。  确保至少包含 `End Function` 或 `End Sub` 语句。  
  
2.  将一个 `Implements` 子句添加到 `Function` 或 `Sub` 语句的末尾。  例如：  
  
    ```  
    Public Sub DoSomething() Implements IBaseInterface.DoSomething  
    ```  
  
## 请参阅  
 [Implements 语句](../../../visual-basic/language-reference/statements/implements-statement.md)   
 [接口](../../../visual-basic/programming-guide/language-features/interfaces/index.md)