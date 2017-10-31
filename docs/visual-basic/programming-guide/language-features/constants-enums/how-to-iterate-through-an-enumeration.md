---
title: "如何：在 Visual Basic 中循环访问枚举 | Microsoft Docs"
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
  - "数组 [Visual Basic], 迭代"
  - "枚举 [Visual Basic], 迭代"
  - "ListBox 控件 [Windows 窗体], 使用枚举填充"
ms.assetid: e5aa10eb-cfcd-4a3b-8e76-f06b8f2002be
caps.latest.revision: 20
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 20
---
# 如何：在 Visual Basic 中循环访问枚举
[!INCLUDE[vs2017banner](../../../../visual-basic/includes/vs2017banner.md)]

枚举提供一种使用成组的相关常数以及将常数值与名称相关联的方便途径。  若要循环访问枚举，可以用 <xref:System.Enum.GetValues%2A> 方法将枚举移入数组中。  也可以使用 `For...Each` 语句循环访问枚举，使用 <xref:System.Enum.GetNames%2A> 或 <xref:System.Enum.GetValues%2A> 方法提取字符串或数值。  
  
### 循环访问枚举  
  
-   声明一个数组并用 <xref:System.Enum.GetValues%2A> 方法将枚举转换为该数组，然后像处理任何其他变量那样传递该数组。  下面的示例在循环访问枚举 <xref:Microsoft.VisualBasic.FirstDayOfWeek> 时显示枚举的每个成员。  
  
     [!code-vb[VbEnumsTask#7](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/how-to-iterate-through-an-enumeration_1.vb)]  
  
## 请参阅  
 [枚举概述](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-overview.md)   
 [如何：声明枚举](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-enumerations.md)   
 [何时使用枚举](../../../../visual-basic/programming-guide/language-features/constants-enums/when-to-use-an-enumeration.md)   
 [如何：确定与枚举值关联的字符串](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-determine-the-string-associated-with-an-enumeration-value.md)   
 [如何：引用枚举成员](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-refer-to-an-enumeration-member.md)   
 [枚举和名称限定](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)   
 [数组](../../../../visual-basic/programming-guide/language-features/arrays/index.md)