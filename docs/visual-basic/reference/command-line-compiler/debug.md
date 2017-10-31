---
title: "/debug (Visual Basic 中) |Microsoft 文档"
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
- debug compiler switches
- /debug compiler option [Visual Basic]
- -debug compiler option [Visual Basic]
- debug compiler option [Visual Basic]
ms.assetid: c2b0bea5-1d5e-499f-9bd5-4f6c6b715ea2
caps.latest.revision: 18
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
ms.openlocfilehash: 7384e69f066022e861a4277f418df3f4d094c3be
ms.lasthandoff: 03/13/2017

---
# <a name="debug-visual-basic"></a>/debug (Visual Basic)
使编译器生成调试信息并将其放在输出文件。  
  
## <a name="syntax"></a>语法  
  
```  
/debug[+ | -]  
' -or-  
/debug:[full | pdbonly]  
```  
  
## <a name="arguments"></a>参数  
  
|术语|定义|  
|---|---|  
|`+` &#124; `-`|可选。 指定`+`或`/debug`使编译器生成调试信息并将其放置在.pdb 文件。 指定`-`具有相同的效果与不指定`/debug`。|  
|`full` &#124; `pdbonly`|可选。 指定编译器生成的调试信息的类型。 如果未指定`/debug:pdbonly`，默认值是`full`，这样您就可以将调试器附加到正在运行的程序。 `pdbonly`参数允许源代码进行调试时在调试器中，启动该程序，但仅当正在运行的程序附加到调试器时显示程序集语言代码。|  
  
## <a name="remarks"></a>备注  
 使用此选项以创建调试版本。 如果未指定`/debug`， `/debug+`，或`/debug:full`，将不能调试您的程序的输出文件。  
  
 默认情况下，调试信息不会发出 (`/debug-`)。 若要发出调试信息，请指定`/debug`或`/debug+`。  
  
 有关如何配置应用程序的调试性能的信息，请参阅[令映像更易于调试](http://msdn.microsoft.com/library/7d90ea7a-150f-4f97-98a7-f9c26541b9a3)。  
  
|在 Visual Studio 中设置 /debug 集成开发环境|  
|---|  
|1.在“解决方案资源管理器” ****中选择了项目的情况下，在“项目” **** 菜单上单击“属性” ****。 有关详细信息，请参阅[项目设计器简介](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7)。<br />2.单击“编译”****选项卡。<br />3.单击**高级编译选项**。<br />4.在修改此值**生成调试信息**框。|  
  
## <a name="example"></a>示例  
 下面的示例将调试信息放入输出文件`App.exe`。  
  
```  
vbc /debug /out:app.exe test.vb  
```  
  
## <a name="see-also"></a>请参见  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/bugreport](../../../visual-basic/reference/command-line-compiler/bugreport.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
