---
title: "/addmodule |Microsoft 文档"
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
- /addmodule compiler option [Visual Basic]
- addmodule compiler option [Visual Basic]
- -addmodule compiler option [Visual Basic]
ms.assetid: fb4b89d4-4926-4f20-868d-427fa28497b2
caps.latest.revision: 14
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 949962905ec933dc42301bf8c21654e73dbe2f70
ms.lasthandoff: 03/13/2017

---
# <a name="addmodule"></a>/addmodule
使编译器让指定文件中的所有类型信息可供当前正在编译的项目使用。  
  
## <a name="syntax"></a>语法  
  
```  
/addmodule:fileList  
```  
  
## <a name="arguments"></a>参数  
 `fileList`  
 必需。 包含元数据，但不是包含程序集清单的文件以逗号分隔列表。 包含空格的文件名应该用引号引起来 ("")。  
  
## <a name="remarks"></a>备注  
 按列出的文件`fileList`参数必须与创建`/target:module`选项，或使用其他编译器等效于`/target:module`。  
  
 使用添加的所有模块`/addmodule`必须在运行时是与输出文件的相同目录中。 也就是说，您也可以在编译时，指定在任何目录中的模块，但在运行时模块必须在应用程序目录。 如果不是这样，您得到<xref:System.TypeLoadException>错误。</xref:System.TypeLoadException>  
  
 如果指定 （隐式或显式） 任何[/target (Visual Basic 中)](../../../visual-basic/reference/command-line-compiler/target.md)选项而不`/target:module`与`/addmodule`，文件将传递给`/addmodule`成为项目的程序集的一部分。 运行具有一个输出文件所需的程序集或使用更多的文件添加`/addmodule`。  
  
 使用[/reference (Visual Basic 中)](../../../visual-basic/reference/command-line-compiler/reference.md)从包含程序集文件中导入元数据。  
  
> [!NOTE]
>  `/addmodule`选项不是在 Visual Studio 开发环境中可用; 只有当从命令行进行编译，它才可用。  
  
## <a name="example"></a>示例  
 下面的代码创建一个模块。  
  
 [!code-vb[VbVbalrCompiler #&47;](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/addmodule_1.vb)]  
  
 下面的代码将导入该模块的类型。  
  
 [!code-vb[VbVbalrCompiler #&48;](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/addmodule_2.vb)]  
  
 当您运行`t1`，它将输出`802`。  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/target (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)   
 [/reference (Visual Basic)](../../../visual-basic/reference/command-line-compiler/reference.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
