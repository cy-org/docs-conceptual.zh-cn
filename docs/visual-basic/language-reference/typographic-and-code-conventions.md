---
title: "版式和代码约定 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "最佳做法, 编码约定"
  - "编码约定, Visual Basic"
  - "约定, 文档"
  - "约定, Visual Basic代码"
  - "文档约定"
  - "版式规则"
  - "Visual Basic 代码, 约定"
ms.assetid: 1916cd81-ea9d-4faa-81f7-4a0d864b60f4
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# 版式和代码约定 (Visual Basic)
[!INCLUDE[vs2017banner](../../visual-basic/includes/vs2017banner.md)]

Visual Basic 文档使用下面的版式和代码约定。  
  
## 版式约定  
  
|示例|说明|  
|--------|--------|  
|`Sub`, `If`, `ChDir`, `Print`, `True`, `Debug`|语言特定的关键字和运行时成员的首字母大写，其格式如本示例所示。|  
|SmallProject、ButtonCollection|指示您键入的单词和短语格式如本示例所示。|  
|[Module 语句](../../visual-basic/language-reference/statements/module-statement.md)|您可以单击以进入另一个帮助页的链接格式如本示例所示。|  
|*object*、*variableName*、`argumentList`|您提供的信息的占位符格式如本示例所示。|  
|\[ Shadows \]、\[ *expressionList* \]|在语法中，可选项括在中括号中。|  
|{ `Public` &#124; `Friend` &#124; `Private` }|在语法中，必须在两项或多项中选择一个时，这些项括在大括号中，由竖线隔开。<br /><br /> 必须选择一项且只能选择一项。|  
|\[ `Protected` &#124; `Friend` \]|在语法中，可以在两项或多项中选择一个时，这些项括在方括号中，由竖线隔开。<br /><br /> 您可以选择这些项的任意组合，也可以一项都不选。|  
|\[{ `ByVal` &#124; `ByRef` }\]|在语法中，您至多可以选择一项，但也可以完全省略这些项时，这些项包含在由大括号括起来的方括号中，由竖线隔开。|  
|*成员名称* 1、*成员名称*2、*成员名称*3|同一占位符的多个实例由下标区分，如本示例所示。|  
|*成员名称1*<br /><br /> ...<br /><br /> *成员名称N*|在语法中，省略号 \(...\) 用于表示省略号前面的任意多个同类项。<br /><br /> 用在代码中，省略号表示为清楚起见省略了部分代码。|  
|Esc、Enter|键盘上的按键名称和组合按键以全大写字母表示。|  
|Alt\+F1|如果两个按键名称间出现加号 \(\+\)，则表示在按住一个键的同时必须按下另一个键。  例如，Alt\+F1 表示按住 Alt 键再按 F1 键。|  
  
## 代码约定  
  
|示例|说明|  
|--------|--------|  
|`sampleString = "Hello, world!"`|代码示例以固定间距的字体显示，其格式如本示例所示。|  
|上一语句将 `sampleString` 的值设置为“Hello, world\!”|解释性文本中的代码元素以固定间距的字体显示，如本示例所示。|  
|`' This is a comment.`<br /><br /> `REM This is also a comment.`|代码注释由撇号 \('\) 或 REM 关键字引入。|  
|`sampleVar = "This is an " _`<br /><br /> `& "example" _`<br /><br /> `& " of how to continue code."`|在每行的最后，一个空格后跟一个下划线 \( \_\) 表示该语句续行。|  
  
## 请参阅  
 [Visual Basic 语言参考](../../visual-basic/language-reference/index.md)   
 [关键字](../../visual-basic/language-reference/keywords/index.md)   
 [Visual Basic 运行库成员](../../visual-basic/language-reference/runtime-library-members.md)   
 [Visual Basic 命名约定](../../visual-basic/programming-guide/program-structure/naming-conventions.md)   
 [如何：在代码中拆分和合并语句](../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)   
 [代码中的注释](../../visual-basic/programming-guide/program-structure/comments-in-code.md)