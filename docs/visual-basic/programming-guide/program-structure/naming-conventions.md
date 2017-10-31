---
title: "Visual Basic 命名约定 | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "约定, Visual Basic代码"
  - "名称, 命名规则"
  - "名称, Visual Basic 规则"
  - "命名规则"
  - "命名规则, 类"
  - "命名规则, Visual Basic"
  - "Visual Basic 代码, 命名规则"
ms.assetid: 164949a4-2a7c-4736-9d82-9c3078e2e56c
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# Visual Basic 命名约定
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

命名 Visual Basic 应用程序中的元素时，名称的首字符必须为字母字符或下划线。  但是，请注意，以下划线开头的名称不符合 [语言独立性和与语言无关的组件](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md) \(CLS\)。  
  
 以下建议适用于命名。  
  
-   名称中各单词首字母均为大写，如 `FindLastRecord` 和 `RedrawMyForm`。  
  
-   函数名和方法名以动词开始，如 `InitNameArray` 和 `CloseDialog`。  
  
-   类名、结构名、模块名和属性名以名词开始，如 `EmployeeName` 或 `CarAccessory` 中。  
  
-   接口名称以前缀“I”开始，后面接一个名词或名词词组（如 `IComponent`），或者接一个描述接口行为的形容词（如 `IPersistable`）。  不要使用下划线，不要过多使用缩写，因为缩写会引起混淆。  
  
-   事件处理程序的名称以一个描述事件类型的名词开始，后面接后缀“`EventHandler`”，如“`MouseEventHandler`”。  
  
-   事件参数类的名称里要加“`EventArgs`”后缀。  
  
-   如果某事件含有“之前”或“之后”的概念，请以现在时或过去时形式使用后缀，如“`ControlAdd`”或“`ControlAdded`”。  
  
-   对于长项或常用项，可使用缩写使名称长度适中，例如，可以使用“HTML”代替“HyperText Markup Language”。  通常，多于 32 个字符的变量名在低分辨率的监视器上难以阅读。  同时，请确保缩写在整个应用程序中保持一致。  在项目中随意在“HTML”和“HyperText Markup Language”之间切换可能会导致混淆。  
  
-   在内部范围中避免使用与外部范围中的名称相同的名称。  如果访问了错误的变量，则可能会产生错误结果。  若变量与同一名称的关键字冲突，则必须在关键字前加适当的类型库以作标识。  例如，如果有一个名为 `Date` 的变量，通过调用 <xref:System.DateTime.Date%2A?displayProperty=fullName> 只可以使用内部 `Date` 函数。  
  
## 请参阅  
 [代码中用作元素名称的关键字](../../../visual-basic/programming-guide/program-structure/keywords-as-element-names-in-code.md)   
 [Me、My、MyBase 和 MyClass](../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)   
 [已声明的元素名称](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)   
 [程序结构和代码约定](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)   
 [Visual Basic 语言参考](../../../visual-basic/language-reference/index.md)