---
title: "&lt;类型 1&gt;“&lt;类型名&gt;”必须为接口“&lt;接口名&gt;”实现“&lt;成员名&gt;” | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30154"
  - "bc30154"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30154"
ms.assetid: 259afdfa-3608-4760-adcb-88ec0da5020d
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# &lt;类型 1&gt;“&lt;类型名&gt;”必须为接口“&lt;接口名&gt;”实现“&lt;成员名&gt;”
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

“\<typename\>”必须为接口“\<interfacename\>”实现“\<membername\>”。实现属性必须有匹配的“ReadOnly”\/“WriteOnly”说明符。  
  
 类或结构要求实现接口，但没有实现由该接口定义的过程、属性或事件。  必须实现接口的每个成员。  
  
 **错误 ID：**BC30154  
  
### 更正此错误  
  
1.  用与接口中定义的名称和签名相同的名称和签名声明过程。  确保至少包含 `End Function`、`End Sub` 或 `End Property` 语句。  
  
2.  将一个 `Implements` 子句添加到 `Function`、`Sub`、`Property` 或 `Event` 语句的末尾。  例如：  
  
    ```  
    Public Event ItHappened() Implements IBaseInterface.ItHappened  
    ```  
  
3.  实现属性时，请确保其 `ReadOnly` 或 `WriteOnly` 的用法与接口定义中的一致。  
  
4.  实现属性时，请根据需要声明 `Get` 和 `Set` 过程。  
  
## 请参阅  
 [Implements 语句](../../../visual-basic/language-reference/statements/implements-statement.md)   
 [接口](../../../visual-basic/programming-guide/language-features/interfaces/index.md)