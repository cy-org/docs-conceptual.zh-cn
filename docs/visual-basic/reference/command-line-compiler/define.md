---
title: "/define (Visual Basic 中) |Microsoft 文档"
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
- -d compiler option [Visual Basic]
- /d compiler option [Visual Basic]
- -define compiler option [Visual Basic]
- d compiler option [Visual Basic]
- /define compiler option [Visual Basic]
- define compiler option [Visual Basic]
ms.assetid: f735c57d-1cf9-4f2f-a26f-0de630fd4077
caps.latest.revision: 15
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
ms.openlocfilehash: 48c3bae1c6cf5831f95ce86dbcf6adadab9d5db8
ms.lasthandoff: 03/13/2017

---
# <a name="define-visual-basic"></a>/define (Visual Basic)
定义条件编译器常数。  
  
## <a name="syntax"></a>语法  
  
```  
/define:["]symbol[=value][,symbol[=value]]["]  
' -or-  
/d:["]symbol[=value][,symbol[=value]]["]  
```  
  
## <a name="arguments"></a>参数  
  
|术语|定义|  
|---|---|  
|`symbol`|必需。 要定义的符号。|  
|`value`|可选。 指派给 `symbol` 的值。 如果`value`是一个字符串，它必须放在反斜杠/双引号序列 (\\") 而不是引号引起来。 如果未指定值，则视为 True。|  
  
## <a name="remarks"></a>备注  
 `/define` 选项具有与在源文件中使用 `#Const` 预处理器指令类似的效果，只是使用 `/define` 定义的常数为公共的且应用于项目中的所有文件。  
  
 可以将由此选项创建的符号同 `#If`...`Then`...`#Else` 指令一起使用，以对源文件进行条件编译。  
  
 `/d` 是 `/define` 的缩写形式。  
  
 通过使用逗号分隔符号定义，可以用 `/define` 定义多个符号。  
  
|在 Visual Studio 集成开发环境中设置/定义|  
|---|  
|1.在 **“解决方案资源管理器”**中选择一个项目。 在**项目**菜单上，单击**属性**。 有关详细信息，请参阅[项目设计器简介](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7)。<br />2.单击“编译”****选项卡。<br />3.单击 **“高级”**。<br />4.在修改此值**自定义常数**框。|  
  
## <a name="example"></a>示例  
 下面的代码定义并使用两个条件编译器常数。  
  
 [!code-vb[VbVbalrCompiler #&45;](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/define_1.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [#If...Then...#Else 指令](../../../visual-basic/language-reference/directives/if-then-else-directives.md)   
 [#Const 指令](../../../visual-basic/language-reference/directives/const-directive.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
