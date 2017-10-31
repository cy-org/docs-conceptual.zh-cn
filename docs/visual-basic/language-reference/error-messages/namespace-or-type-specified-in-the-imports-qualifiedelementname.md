---
title: "Imports“&lt;限定元素名&gt;”中指定的命名空间或类型不包含任何公共成员，或者找不到该命名空间或类型 | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc40056"
  - "vbc40056"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC40056"
ms.assetid: b59f5754-444f-4378-9272-9678b437e84a
caps.latest.revision: 8
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 8
---
# Imports“&lt;限定元素名&gt;”中指定的命名空间或类型不包含任何公共成员，或者找不到该命名空间或类型
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

Imports“\<qualifiedelementname\>”中指定的命名空间或类型不包含任何公共成员，或者找不到该命名空间或类型。请确保已定义命名空间或类型，且其中至少包含一个公共成员。请确保别名中不包含其他别名。  
  
 `Imports` 语句指定的包含元素无法被找到，或未定义任何 `Public` 成员。  
  
 *“包含元素”*可以是命名空间、类、结构、模块、接口或枚举。  包含元素可包含成员，如变量、过程或其他包含元素。  
  
 导入的目的是允许代码访问命名空间或类型成员，而无须对它们进行限定。  项目还可能需要添加对命名空间或类型的引用。  有关更多信息，请参见 [对已声明元素的引用](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md) 中的“导入包含元素”。  
  
 如果编译器无法找到指定的包含元素，则无法解析使用该包含元素的引用。  如果编译器找到的元素没有公开任何 `Public` 成员，则引用将不会成功。  在这两种情况下，导入元素是没有意义的。  
  
 请记住，如果导入包含元素并为它分配导入别名，您将无法使用该导入别名导入其他元素。  下面的代码可生成编译器错误。  
  
 `Imports`   `winfrm`   `= System.Windows.Forms`  
  
 `' The following statement is`   `INVALID`   `because it reuses an import alias.`  
  
 `Imports behav =`   `winfrm`  `.Design.Behavior`  
  
 **错误 ID：**BC40056  
  
### 更正此错误  
  
1.  验证是否可以从项目中访问包含元素。  
  
2.  验证包含元素的规范是否包括任何其他导入的导入别名。  
  
3.  验证包含元素是否至少公开了一个 `Public` 成员。  
  
## 请参阅  
 [Imports 语句（.NET 命名空间和类型）](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)   
 [Namespace 语句](../../../visual-basic/language-reference/statements/namespace-statement.md)   
 [Public](../../../visual-basic/language-reference/modifiers/public.md)   
 [Visual Basic 中的命名空间](../../../visual-basic/programming-guide/program-structure/namespaces.md)   
 [对已声明元素的引用](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)