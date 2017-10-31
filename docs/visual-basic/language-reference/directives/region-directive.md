---
title: "#Region 指令 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Region
- vb.#Region
dev_langs:
- VB
helpviewer_keywords:
- Visual Basic compiler, compiler directives
- '#region directive'
- region directive (#region)
- '#Region keyword'
ms.assetid: 90a6a104-3cbf-47d0-bdc4-b585d0921b87
caps.latest.revision: 14
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
ms.openlocfilehash: 1c429602a7eee27944f58256992879d25d533d34
ms.lasthandoff: 03/13/2017

---
# <a name="region-directive"></a>#Region 指令
折叠并隐藏 Visual Basic 文件中的代码段。  
  
## <a name="syntax"></a>语法  
  
```  
  
      #Region "identifier_string"  
#End Region  
```  
  
## <a name="parts"></a>部件  
  
|术语|定义|  
|---|---|  
|`identifier_string`|必需。 当区域处于折叠状态时充当区域标题的字符串。 默认情况下，区域处于折叠状态。|  
|`#End Region`|终止 `#Region` 块。|  
  
## <a name="remarks"></a>备注  
 使用 `#Region` 指令指定使用 Visual Studio 代码编辑器的大纲显示功能时要展开或折叠的代码块。 您可以放置或*嵌套*，在其他区域分为一组类似的区域。  
  
## <a name="example"></a>示例  
 此示例使用 `#Region` 指令。  
  
 [!code-vb[VbVbalrConditionalComp #&4;](../../../visual-basic/language-reference/directives/codesnippet/VisualBasic/region-directive_1.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [#If...Then...#Else 指令](../../../visual-basic/language-reference/directives/if-then-else-directives.md)   
 [大纲显示](https://docs.microsoft.com/visualstudio/ide/outlining)   
 [如何：折叠和隐藏代码节](../../../visual-basic/programming-guide/program-structure/how-to-collapse-and-hide-sections-of-code.md)
