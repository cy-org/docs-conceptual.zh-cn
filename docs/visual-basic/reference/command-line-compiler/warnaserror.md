---
title: "/warnaserror (Visual Basic 中) |Microsoft 文档"
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
- warnaserror compiler option [Visual Basic]
- /warnaserror compiler option [Visual Basic]
- -warnaserror compiler option [Visual Basic]
ms.assetid: 49819f1d-a1bd-4201-affe-5afe6d9712e1
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
ms.openlocfilehash: 28f232b1ad8200455550f2f4c1204818c8b143ab
ms.lasthandoff: 03/13/2017

---
# <a name="warnaserror-visual-basic"></a>/warnaserror (Visual Basic)
使编译器将视为错误的警告的第一个匹配项。  
  
## <a name="syntax"></a>语法  
  
```  
/warnaserror[+ | -][:numberList]  
```  
  
## <a name="arguments"></a>参数  
  
|术语|定义|  
|---|---|  
|+ &#124; -|可选。 默认情况下，`/warnaserror-`是有效，则警告不会阻止编译器生成的输出文件。 `/warnaserror`选项，这是相同作为`/warnaserror+`，会导致将警告视为错误。|  
|`numberList`|可选。 以逗号分隔的多个警告 ID 号向其`/warnaserror`选项适用。 如果指定无警告 ID，则`/warnaserror`选项适用于所有警告。|  
  
## <a name="remarks"></a>备注  
 `/warnaserror`选项将所有警告视为错误。 将通常报告为警告都视为错误报告的任何消息。 编译器将报告为警告相同的警告的后续匹配项。  
  
 默认情况下，`/warnaserror-`是起作用，则会导致只是信息性警告。 `/warnaserror`选项，这是相同作为`/warnaserror+`，会导致将警告视为错误。  
  
 如果您希望仅将一些特定警告视为错误，您可以指定逗号分隔警告编号，以将视为错误的列表。  
  
> [!NOTE]
>  `/warnaserror`选项不控制如何显示警告。 使用[/nowarn](../../../visual-basic/reference/command-line-compiler/nowarn.md)选项可禁用警告。  
  
|若要设置 /warnaserror 将所有警告视为 Visual Studio IDE 中的错误|  
|---|  
|1.在 **“解决方案资源管理器”**中选择一个项目。 在**项目**菜单上，单击**属性**。 有关详细信息，请参阅[项目设计器简介](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7)。<br />2.单击“编译”****选项卡。<br />3.请确保**禁用所有警告**复选框处于未选中状态。<br />4.检查**将所有警告视为错误**复选框。|  
  
|若要设置 /warnaserror 特定警告视为错误在 Visual Studio IDE 中|  
|---|  
|1.在 **“解决方案资源管理器”**中选择一个项目。 在**项目**菜单上，单击**属性**。<br />2.单击“编译”****选项卡。<br />3.请确保**禁用所有警告**复选框处于未选中状态。<br />4.请确保**将所有警告视为错误**复选框处于未选中状态。<br />5.选择**错误**从**通知**列应被视为错误的警告旁边。|  
  
## <a name="example"></a>示例  
 下面的代码编译`In.vb`并指示编译器显示为它找到的每个警告的首次出现的错误。  
  
```  
vbc /warnaserror in.vb  
```  
  
## <a name="example"></a>示例  
 下面的代码编译`T2.vb`和仅对未使用的局部变量 (42024) 警告视为错误。  
  
```  
vbc /warnaserror:42024 t2.vb  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [在 Visual Basic 中配置警告](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic)
