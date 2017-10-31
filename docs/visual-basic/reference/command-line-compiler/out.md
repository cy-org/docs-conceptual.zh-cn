---
title: "/ 输出 (Visual Basic 中) |Microsoft 文档"
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
- /out compiler option [Visual Basic]
- -out compiler option [Visual Basic]
- out compiler option [Visual Basic]
ms.assetid: 9f148c15-0909-4cb8-a2db-777f8a8b45ae
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
ms.openlocfilehash: e3eb7af88869e4fb161a12914c02f2bc2f41864e
ms.lasthandoff: 03/13/2017

---
# <a name="out-visual-basic"></a>/out (Visual Basic)
指定输出文件的名称。  
  
## <a name="syntax"></a>语法  
  
```  
/out:filename  
```  
  
## <a name="arguments"></a>参数  
  
|术语|定义|  
|---|---|  
|`filename`|必需。 编译器会创建输出文件的名称。 如果文件名包含空格，则将名称括在双引号 ("")。|  
  
## <a name="remarks"></a>备注  
 指定的完整名称和要创建的文件扩展名。 如果不这样做，.exe 文件采用从源代码文件包含其名称`Sub Main`过程中和.dll 文件的第一个源代码文件采用其名称。  
  
 如果指定一个不带扩展名为.exe 或.dll 的文件名称，编译器会自动添加该扩展，具体取决于为指定的值`/target`编译器选项。  
  
|若要在 Visual Studio 集成的开发环境中设置 /out|  
|---|  
|1.在 **“解决方案资源管理器”**中选择一个项目。 在**项目**菜单上，单击**属性**。 有关详细信息，请参阅[项目设计器简介](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7)。<br />2.单击“应用程序” **** 选项卡。<br />3.在修改此值**程序集名称**框。|  
  
## <a name="example"></a>示例  
 下面的代码编译`T2.vb`并创建输出文件`T2.exe`。  
  
```  
vbc t2.vb /out:t3.exe  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/target (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
