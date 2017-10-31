---
title: "“&lt;成员名&gt;”不能通过 &lt;容器类型&gt;“&lt;容器类名&gt;”在项目外部公开类型“&lt;类名&gt;” | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc30909"
  - "vbc30909"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30909"
ms.assetid: ffa7395d-e182-4087-8ce8-079810fdae54
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# “&lt;成员名&gt;”不能通过 &lt;容器类型&gt;“&lt;容器类名&gt;”在项目外部公开类型“&lt;类名&gt;”
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

变量、过程参数或函数返回在其容器外公开，但却声明为不得在容器外公开的类型。  
  
 下面的主干代码演示了生成此错误的情况。  
  
```  
Private Class privateClass  
End Class  
Public Class mainClass  
    Public exposedVar As New privateClass  
End Class  
```  
  
 声明为 `Protected`、`Friend`、`Protected Friend` 或 `Private` 的类型被设计为在其声明上下文外具有有限的访问权限。  如果将它用作访问限制较少的变量的数据类型，将无法实现这一用途。  在上述主干代码中，`exposedVar` 的数据类型为 `Public`，并将 `privateClass` 公开为不应访问的代码。  
  
 **错误 ID：**BC30909  
  
### 更正此错误  
  
-   将变量、过程参数或函数返回的访问级别更改为至少与其数据类型的访问级别具有相同的限制性。  
  
## 请参阅  
 [Visual Basic 中的访问级别](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)