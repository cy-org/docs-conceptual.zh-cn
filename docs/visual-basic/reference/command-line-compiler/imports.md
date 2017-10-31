---
title: "/imports (Visual Basic 中) |Microsoft 文档"
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
- /imports compiler option [Visual Basic]
- imports compiler option [Visual Basic]
- -imports compiler option [Visual Basic]
ms.assetid: 9a93fb53-c080-497b-bf9b-441022dbbc39
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
ms.openlocfilehash: 1dcbba442413dba63aef31fd40a511bad5e8217b
ms.lasthandoff: 03/13/2017

---
# <a name="imports-visual-basic"></a>/imports (Visual Basic)
从指定的程序集导入的命名空间。  
  
## <a name="syntax"></a>语法  
  
```  
/imports:namespaceList  
```  
  
## <a name="arguments"></a>参数  
  
|术语|定义|  
|---|---|  
|`namespaceList`|必需。 要导入的命名空间的逗号分隔列表。|  
  
## <a name="remarks"></a>备注  
 `/imports`选项将导入在当前设置的源文件或任何引用的程序集中定义的任何命名空间。  
  
 使用指定的命名空间中的成员`/imports`可供在编译中的所有源代码文件。 使用[Imports 语句 （.NET Namespace 和类型）](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)若要在单个源代码文件中使用的命名空间。  
  
|若要设置/Visual Studio 集成的开发环境中导入|  
|---|  
|1.在 **“解决方案资源管理器”**中选择一个项目。 在**项目**菜单上，单击**属性**。 有关详细信息，请参阅[项目设计器简介](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7)。<br />2.单击**引用**选项卡。<br />3.在旁边的框中输入命名空间名称**添加用户导入**按钮。<br />4.单击**添加用户导入**按钮。|  
  
## <a name="example"></a>示例  
 下面的代码编译时`/imports:system`指定。  
  
 [!code-vb[VbVbalrCompiler #&21;](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/imports_1.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [引用和 Imports 语句](../../../visual-basic/programming-guide/program-structure/references-and-the-imports-statement.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
