---
title: "/win32icon |Microsoft 文档"
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
- win32icon compiler option [Visual Basic]
- -win32icon compiler option [Visual Basic]
- /win32icon compiler option [Visual Basic]
ms.assetid: aecaab01-9353-46c5-941c-6edabd4eff92
caps.latest.revision: 13
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
ms.openlocfilehash: 110a3861d6628dc2c3fb251aaa31762fb94f04c9
ms.lasthandoff: 03/13/2017

---
# <a name="win32icon"></a>/win32icon
在输出文件中插入.ico 文件。 此.ico 文件表示该输出文件**文件资源管理器**。  
  
## <a name="syntax"></a>语法  
  
```  
/win32icon:filename  
```  
  
## <a name="arguments"></a>参数  
  
|术语|定义|  
|---|---|  
|`filename`|要添加到输出文件的.ico 文件。 将文件名括在双引号 ("") 如果包含空格。|  
  
## <a name="remarks"></a>备注  
 您可以使用 Microsoft Windows 资源编译器 (RC) 创建.ico 文件。 资源编译器当编译 Visual c + + 程序;.ico 文件创建从.rc 文件中。 `/win32icon`和`/win32resource`是互相排斥的选项。  
  
 请参阅[/linkresource (Visual Basic 中)](../../../visual-basic/reference/command-line-compiler/linkresource.md)引用[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]资源文件或[/resource (Visual Basic 中)](../../../visual-basic/reference/command-line-compiler/resource.md)附加[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]资源文件。 请参阅[/win32resource](../../../visual-basic/reference/command-line-compiler/win32resource.md) .res 文件导入。  
  
|在 Visual Studio IDE 中设置 /win32icon|  
|---|  
|1.在 **“解决方案资源管理器”**中选择一个项目。 在**项目**菜单上，单击**属性**。 有关详细信息，请参阅[项目设计器简介](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7)。<br />2.单击“应用程序” **** 选项卡。<br />3.在修改此值**图标**框。|  
  
## <a name="example"></a>示例  
 下面的代码编译`In.vb`并附加一个.ico 文件、 `Rf.ico`。  
  
```  
vbc /win32icon:rf.ico in.vb  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
