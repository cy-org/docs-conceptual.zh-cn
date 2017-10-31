---
title: "/nowarn |Microsoft 文档"
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
- nowarn compiler option [Visual Basic]
- /nowarn compiler option [Visual Basic]
- -nowarn compiler option [Visual Basic]
ms.assetid: 7ebf2106-0652-4fdc-bf60-70fc86465d83
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
ms.openlocfilehash: 61b145a9eb95f5357c7aa2983a96c31e8f2cef6a
ms.lasthandoff: 03/13/2017

---
# <a name="nowarn"></a>/nowarn
禁止编译器生成警告的能力。  
  
## <a name="syntax"></a>语法  
  
```  
/nowarn[:numberList]  
```  
  
## <a name="arguments"></a>参数  
  
|术语|定义|  
|---|---|  
|`numberList`|可选。 应该禁止显示编译器警告 ID 号的以逗号分隔列表。 如果未指定 Id 的警告，则会抑制所有警告。|  
  
## <a name="remarks"></a>备注  
 `/nowarn`选项将使编译器不生成警告。 若要禁止显示个别警告，请提供警告 ID`/nowarn`冒号之后的选项。 用逗号分隔多个警告编号。  
  
 您需要指定只有警告标识符的数值部分。 例如，如果您想要禁止显示 BC42024，未使用的局部变量，该警告指定`/nowarn:42024`。  
  
 警告 ID 号的详细信息，请参阅[在 Visual Basic 中配置警告](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic)。  
  
|在 Visual Studio 中设置 /nowarn 集成开发环境|  
|---|  
|1.在 **“解决方案资源管理器”**中选择一个项目。 在**项目**菜单上，单击**属性**。 有关详细信息，请参阅[项目设计器简介](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7)。<br />2.单击“编译”****选项卡。<br />3.选择**禁用所有警告**复选框以都禁用所有警告。<br />     - 或 -<br />     若要禁用特定警告，请单击**无**警告旁边的下拉列表中。|  
  
## <a name="example"></a>示例  
 下面的代码编译`T2.vb`并且不显示任何警告。  
  
```  
vbc /nowarn t2.vb  
```  
  
## <a name="example"></a>示例  
 下面的代码编译`T2.vb`并且不显示未使用的局部变量 (42024) 的警告。  
  
```  
vbc /nowarn:42024 t2.vb  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [在 Visual Basic 中配置警告](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic)
