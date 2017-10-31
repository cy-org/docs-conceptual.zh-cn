---
title: "如何︰ 折叠和隐藏代码 (Visual Basic 中) 的部分 |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Visual Basic, code collapsing
- Visual Basic, code hiding
- Visual Basic code, collapsing and hiding
ms.assetid: b770e8f5-e07d-491a-ab4b-a977980f9ba2
caps.latest.revision: 11
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 200a90b6983277d46b6e5c7b27ee4a90ecf88c40
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-collapse-and-hide-sections-of-code-visual-basic"></a>如何：折叠和隐藏代码节 (Visual Basic)
`#Region`指令，可以折叠和隐藏代码节[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]文件。 `#Region`指令可让您在使用时指定的一段代码，你可以展开或折叠[!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]代码编辑器中。 有选择地隐藏代码的能力使您的文件更易于管理且更易于阅读。 有关详细信息，请参阅[大纲显示](https://docs.microsoft.com/visualstudio/ide/outlining)。  
  
 `#Region`指令支持代码块语义，如`#If...#End If`。 这意味着它们不能在一个块中开始和结束在另一个;开始和结束必须位于同一个块。 `#Region`指令不支持在函数内。  
  
### <a name="to-collapse-and-hide-a-section-of-code"></a>若要折叠和隐藏代码节  
  
-   将之间的代码节放`#Region`和`#End Region`语句，如以下示例所示︰  
  
     [!code-vb[VbVbalrConditionalComp #&6;](../../../visual-basic/language-reference/directives/codesnippet/VisualBasic/how-to-collapse-and-hide-sections-of-code_1.vb)]  
  
     `#Region`块可以多次使用的代码文件中; 因此，用户可以定义自己的块过程和，反过来，可折叠的类。 `#Region`块也可以嵌套在其他`#Region`块。  
  
    > [!NOTE]
    >  隐藏代码不会阻止它正在编译，并且不影响`#If...#End If`语句。  
  
## <a name="see-also"></a>另请参阅  
 [条件编译](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)   
 [#Region 指令](../../../visual-basic/language-reference/directives/region-directive.md)   
 [#If...Then...#Else 指令](../../../visual-basic/language-reference/directives/if-then-else-directives.md)   
 [大纲显示](https://docs.microsoft.com/visualstudio/ide/outlining)
