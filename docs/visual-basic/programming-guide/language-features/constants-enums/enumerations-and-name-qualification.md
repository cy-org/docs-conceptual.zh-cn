---
title: "枚举和名称限定 (Visual Basic) | Microsoft Docs"
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
  - "多义性的名称, 枚举"
  - "声明, 枚举"
  - "声明, 命名空间"
  - "声明枚举"
  - "声明命名空间, 枚举"
  - "枚举 [Visual Basic], 名称限定"
  - "Imports 语句, 命名空间声明"
  - "名称冲突"
  - "名称, 避免冲突"
  - "命名空间, 声明"
  - "命名冲突, 枚举"
  - "命名冲突, 限定名称"
  - "命名规则, 命名冲突"
  - "引用, 枚举成员"
ms.assetid: 08ba2738-df52-4140-bc55-f57c871c9b73
caps.latest.revision: 20
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 20
---
# 枚举和名称限定 (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

通常，当引用枚举成员时，必须使用枚举名称限定成员名称。  例如，若要引用 `Days` 枚举的 `Sunday` 成员，应使用下面的语法：  
  
 [!code-vb[VbEnumsTask#18](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/enumerations-and-name-qualification_1.vb)]  
  
## 使用 Imports 语句  
 为避免使用完全带限定名称，可以在代码的命名空间声明部分添加一条 `Imports` 语句，如下例所示：  
  
 [!code-vb[VbEnumsTask#22](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/enumerations-and-name-qualification_2.vb)]  
  
 `Imports` 语句从引用的项目和程序集以及出现该语句的模块所在同一项目中导入命名空间名称。  一旦添加该语句，无需限定就可以引用枚举成员，如下例所示：  
  
 [!code-vb[VbEnumsTask#24](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/enumerations-and-name-qualification_3.vb)]  
  
 通过将几组相关的常数组织到枚举中，可以在不同的上下文中使用相同的常数名。  例如，可以在 `Days` 和 `WorkDays` 枚举中对工作日常数使用相同的名称。  如果将 `Imports` 语句与枚举一起使用，则必须小心避免不明确的引用。  请看下面的示例：  
  
 [!code-vb[VbEnumsTask#22](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/enumerations-and-name-qualification_2.vb)]  
  
 [!code-vb[VbEnumsTask#25](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/enumerations-and-name-qualification_4.vb)]  
  
 假定 `Monday` 同时是 `Days` 枚举和 `Workdays` 枚举的成员，该代码将生成编译器错误。  当引用单个常数时为避免不明确的引用，应使用枚举名对常数名称加以限定。  下面的代码引用了 `Days` 枚举和 `WorkDays` 枚举中的 `Saturday` 常数。  
  
 [!code-vb[VbEnumsTask#32](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/enumerations-and-name-qualification_5.vb)]  
  
## 请参阅  
 [常量和枚举](../../../../visual-basic/language-reference/constants-and-enumerations.md)   
 [如何：声明枚举](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-enumerations.md)   
 [如何：引用枚举成员](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-refer-to-an-enumeration-member.md)   
 [如何：在 Visual Basic 中循环访问枚举](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-iterate-through-an-enumeration.md)   
 [如何：确定与枚举值关联的字符串](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-determine-the-string-associated-with-an-enumeration-value.md)   
 [何时使用枚举](../../../../visual-basic/programming-guide/language-features/constants-enums/when-to-use-an-enumeration.md)   
 [常量和 Literal 数据类型](../../../../visual-basic/programming-guide/language-features/constants-enums/constant-and-literal-data-types.md)   
 [Enum 语句](../../../../visual-basic/language-reference/statements/enum-statement.md)   
 [Imports 语句（.NET 命名空间和类型）](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)   
 [数据类型](../../../../visual-basic/language-reference/data-types/data-type-summary.md)