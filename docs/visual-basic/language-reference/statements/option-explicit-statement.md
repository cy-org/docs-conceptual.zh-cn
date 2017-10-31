---
title: "Option Explicit 语句 (Visual Basic 中) |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Explicit
- vb.OptionExplicit
dev_langs:
- VB
helpviewer_keywords:
- declaring variables, explicit
- forced variable declaration in Option Explicit statement
- Explicit keyword
- explicit variable declaration
- Option Explicit statement
ms.assetid: e82ac1ad-2cd3-49b2-b985-8bcf016f3fcc
caps.latest.revision: 17
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
ms.openlocfilehash: 020f12f1fbb9a06647215f1fac6324e3b74e8a77
ms.lasthandoff: 03/13/2017

---
# <a name="option-explicit-statement-visual-basic"></a>Option Explicit 语句 (Visual Basic)
强制显式声明所有变量在文件中，或允许隐式声明变量。  
  
## <a name="syntax"></a>语法  
  
```  
Option Explicit { On | Off }  
```  
  
## <a name="parts"></a>部件  
 `On`  
 可选。 使`Option Explicit`检查。 如果`On`或`Off`未指定，则默认值是`On`。  
  
 `Off`  
 可选。 禁用`Option Explicit`检查。  
  
## <a name="remarks"></a>备注  
 当`Option Explicit On`或`Option Explicit`出现在文件中，您必须通过使用显式声明所有变量`Dim`或`ReDim`语句。 如果您尝试使用未声明的变量名，在编译时就会出错。 `Option Explicit Off`语句允许隐式声明变量。  
  
 使用时，`Option Explicit` 语句必须在文件中任何其他源代码语句之前。  
  
> [!NOTE]
>  设置`Option Explicit`到`Off`通常不是一个好的做法。 您可能拼错中一个或多个位置，这会导致意外的结果，当程序运行的变量名。  
  
## <a name="when-an-option-explicit-statement-is-not-present"></a>Option Explicit 语句不存在  
 如果源代码不包含`Option Explicit`语句， **Option Explicit**上设置[编译页，项目设计器 (Visual Basic 中)](https://docs.microsoft.com/visualstudio/ide/reference/compile-page-project-designer-visual-basic)使用。 如果使用命令行编译器， [/optionexplicit](../../../visual-basic/reference/command-line-compiler/optionexplicit.md)使用编译器选项。  
  
#### <a name="to-set-option-explicit-in-the-ide"></a>若要在 IDE 中设置 Option Explicit  
  
1.  在**解决方案资源管理器**，选择一个项目。 在**项目**菜单上，单击**属性**。 有关详细信息，请参阅[项目设计器简介](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7)。  
  
2.  单击“编译”****选项卡。  
  
3.  中的值设置**Option Explicit**框。  
  
 当您创建一个新项目， **Option Explicit**上设置**编译**选项卡上设置为**Option Explicit**中设置**VB 默认值**对话框。 访问**VB 默认值**对话框中，在**工具**菜单上，单击**选项**。 在**选项**对话框框中，展开**项目和解决方案**，然后单击**VB 默认值**。 中的初始默认设置**VB 默认值**是`On`。  
  
#### <a name="to-set-option-explicit-on-the-command-line"></a>若要在命令行上设置 Option Explicit  
  
-   包括[/optionexplicit](../../../visual-basic/reference/command-line-compiler/optionexplicit.md)中的编译器选项**vbc**命令。  
  
## <a name="example"></a>示例  
 下面的示例使用`Option Explicit`语句来强制显式声明所有变量。 尝试使用未声明的变量，将导致在编译时出现错误。  
  
 [!code-vb[VbVbalrStatements #&47;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/option-explicit-statement_1.vb)]  
  
 [!code-vb[VbVbalrStatements #&48;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/option-explicit-statement_2.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [Dim 语句](../../../visual-basic/language-reference/statements/dim-statement.md)   
 [ReDim 语句](../../../visual-basic/language-reference/statements/redim-statement.md)   
 [Option Compare 语句](../../../visual-basic/language-reference/statements/option-compare-statement.md)   
 [Option Strict 语句](../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [/optioncompare](../../../visual-basic/reference/command-line-compiler/optioncompare.md)   
 [/optionexplicit](../../../visual-basic/reference/command-line-compiler/optionexplicit.md)   
 [/optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md)   
 [“选项”对话框 ->“项目”->“Visual Basic 默认值”](https://docs.microsoft.com/visualstudio/ide/reference/visual-basic-defaults-projects-options-dialog-box)
