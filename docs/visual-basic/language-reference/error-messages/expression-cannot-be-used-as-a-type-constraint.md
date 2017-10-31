---
title: "“&lt;表达式&gt;”不能用作类型约束 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc32061"
  - "vbc32061"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC32061"
ms.assetid: b17821b7-fa14-4397-a211-6e2a14079f09
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# “&lt;表达式&gt;”不能用作类型约束
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

约束列表包括了无法对类型形参进行有效约束的表达式。  
  
 约束列表对传递给类型形参的类型实参有一定要求。  您可以以任何组合指定下列要求：  
  
-   类型实参必须实现一个或多个接口  
  
-   类型实参必须从最多一个类中继承  
  
-   类型实参必须公开创建的代码可访问的无形参构造函数（包括 `New` 约束）  
  
 如果您在约束列表中未包括任何特定的类或接口，则可以通过指定以下条件之一提出更一般的要求：  
  
-   类型实参必须是值类型（包括 `Structure` 约束）  
  
-   类型实参必须是引用类型（包括 `Class` 约束）  
  
 不能为同一类型形参同时指定 `Structure` 和 `Class`，并且它们两个都只能指定一次。  
  
 **错误 ID：**BC32061  
  
### 更正此错误  
  
-   验证表达式及其元素的拼写是否正确无误。  
  
-   如果表达式不符合前面列出的各项要求，请将其从约束列表中移除。  
  
-   如果表达式引用接口或类，请验证编译器是否有访问该接口或类的权限。  您可能需要限定其名称，并且，可能需要添加对项目的引用。  有关更多信息，请参见 [对已声明元素的引用](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md) 中的“项目引用”。  
  
## 请参阅  
 [Visual Basic 中的泛型类型](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [值类型和引用类型](../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [对已声明元素的引用](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [如何：使用“添加引用”对话框添加或移除引用](http://msdn.microsoft.com/zh-cn/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)