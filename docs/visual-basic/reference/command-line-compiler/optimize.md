---
title: "/optimize |Microsoft 文档"
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
- optimize compiler option [Visual Basic]
- /optimize compiler option [Visual Basic]
- optimization, enabling
- -optimize compiler option [Visual Basic]
ms.assetid: fcba4a97-3622-4b87-a891-0f77deab4998
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
ms.openlocfilehash: bb89b94ab0d431ed79f94f22afd0bd077728b754
ms.lasthandoff: 03/13/2017

---
# <a name="optimize"></a>/optimize
启用或禁用编译器优化。  
  
## <a name="syntax"></a>语法  
  
```  
/optimize[ + | - ]  
```  
  
## <a name="arguments"></a>参数  
  
|术语|定义|  
|---|---|  
|`+` &#124; `-`|可选。 `/optimize-`选项禁用编译器优化。 `/optimize+`选项将启用优化。 默认情况下，禁用优化。|  
  
## <a name="remarks"></a>备注  
 编译器优化使输出文件更小、 更快、 更高效。 但是，这是因为优化会导致代码中重新排列输出文件中，在`/optimize+`可能使调试困难。  
  
 使用生成的所有模块`/target:module`为程序集必须都使用相同`/optimize`与程序集的设置。 有关详细信息，请参阅[/target (Visual Basic 中)](../../../visual-basic/reference/command-line-compiler/target.md)。  
  
 您可以组合使用`/optimize`和`/debug`选项。  
  
|设置 / 优化在 Visual Studio 集成的开发环境|  
|---|  
|1.在 **“解决方案资源管理器”**中选择一个项目。 在**项目**菜单上，单击**属性**。<br />     有关详细信息，请参阅[项目设计器简介](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7)。<br />2.单击“编译”****选项卡。<br />3.单击 **“高级”** 按钮。<br />4.修改**启用优化**复选框。|  
  
## <a name="example"></a>示例  
 下面的代码编译`T2.vb`和允许进行编译器优化。  
  
```  
vbc t2.vb /optimize  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/debug (Visual Basic)](../../../visual-basic/reference/command-line-compiler/debug.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [/target (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)
