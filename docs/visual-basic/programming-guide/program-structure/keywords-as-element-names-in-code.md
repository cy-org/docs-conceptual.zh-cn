---
title: "代码中用作元素名称的关键字 (Visual Basic) | Microsoft Docs"
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
  - "元素名称, 在代码中"
  - "关键字 [Visual Basic], 在代码中"
  - "名称冲突"
  - "Visual Basic 代码, 命名规则"
ms.assetid: 2e4e8e02-23f7-49b9-a1c8-2b0402b6b525
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# 代码中用作元素名称的关键字 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

任何程序元素（如变量、类或成员）都可以将相同的名称当作限制性关键字。  例如，可以创建一个名为 `Loop` 的变量。  但是，若要引用这个变量（其名称与限制性关键字 `Loop` 相同）的版本，必须在该变量的前面添加完全限定字符串或将该变量括在方括号 \(`[ ]`\) 中，如下面的示例所示。  
  
 [!code-vb[VbVbcnConventions#8](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/keywords-as-element-names-in-code_1.vb)]  
  
 如果不执行上述任何一种操作，则 Visual Basic 假设使用的是内部 `Loop` 关键字而产生错误，如下面的示例所示：  
  
 `' The following statement causes a compiler error.`  
  
 `Loop.Visible = True`  
  
 在引用窗体和控件，以及在声明变量或以与限制性关键字相同的名称定义过程时可以使用方括号。  人们很容易忘记对名称进行限制或加方括号，因而导致代码错误并使其难以阅读。  有鉴于此，建议您不要将限制性关键字用作程序元素的名称。  可是，如果将来的 Visual Basic 版本定义了与现有窗体或控件名冲突的新关键字，则在更新代码以适应新版本时可以使用该技术。  
  
> [!NOTE]
>  程序也可以加入其他引用程序集提供的元素名。  如果这些名称与限制性关键字冲突，则在其前后加上方括号会导致 Visual Basic 将它们解释为您定义的元素。  
  
## 请参阅  
 [Visual Basic 命名约定](../../../visual-basic/programming-guide/program-structure/naming-conventions.md)   
 [程序结构和代码约定](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)   
 [关键字](../../../visual-basic/language-reference/keywords/index.md)