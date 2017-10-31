---
title: "“&lt;类型名&gt;”将对基 &lt;类型&gt; 的访问扩展到程序集的外部，因此无法从 &lt;类型&gt;“&lt;基类名&gt;”继承 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30910"
  - "bc30910"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30910"
ms.assetid: 68fc05c5-5d55-4742-9a3b-ea04312594f4
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# “&lt;类型名&gt;”将对基 &lt;类型&gt; 的访问扩展到程序集的外部，因此无法从 &lt;类型&gt;“&lt;基类名&gt;”继承
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

类或接口从某个基类或接口继承，但具有限制性较小的访问级别。  
  
 例如，`Public` 接口从 `Friend` 接口继承，或者 `Protected` 类从 `Private` 类继承。  这样将会使基类或接口受到意外访问。  
  
 **错误 ID：**BC30910  
  
### 更正此错误  
  
-   更改派生类或接口的访问级别，使它的限制性至少与基类或接口的访问级别持平。  
  
     \- 或 \-  
  
-   如果需要限制性较小的访问级别，请移除 `Inherits` 语句。  您将无法从限制性较强的基类或接口继承。  
  
## 请参阅  
 [Class 语句](../../../visual-basic/language-reference/statements/class-statement.md)   
 [Interface 语句](../../../visual-basic/language-reference/statements/interface-statement.md)   
 [Inherits 语句](../../../visual-basic/language-reference/statements/inherits-statement.md)   
 [Visual Basic 中的访问级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)