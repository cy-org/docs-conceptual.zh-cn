---
title: "/rootnamespace |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- /rootnamespace
- rootnamespace
dev_langs:
- VB
helpviewer_keywords:
- /rootnamespace compiler option [Visual Basic]
- -rootnamespace compiler option [Visual Basic]
- rootnamespace compiler option [Visual Basic]
ms.assetid: e9245edf-6bef-420d-a7c7-324117752783
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
ms.openlocfilehash: 7b261efeb829a6c0b035d7364c63074412a91c7f
ms.lasthandoff: 03/13/2017

---
# <a name="rootnamespace"></a>/rootnamespace
指定所有类型声明的命名空间。  
  
## <a name="syntax"></a>语法  
  
```  
/rootnamespace:namespace  
```  
  
## <a name="arguments"></a>参数  
  
|术语|定义|  
|---|---|  
|`namespace`|包含为当前项目的所有类型声明的命名空间的名称。|  
  
## <a name="remarks"></a>备注  
 如果您使用 Visual Studio 可执行文件 (Devenv.exe) 来编译创建的项目在 Visual Studio 集成的开发环境中，使用`/rootnamespace`指定的值<xref:VSLangProj80.VBProjectProperties3.RootNamespace%2A>属性。</xref:VSLangProj80.VBProjectProperties3.RootNamespace%2A> 请参阅[Devenv 命令行开关](https://docs.microsoft.com/visualstudio/ide/reference/devenv-command-line-switches)有关详细信息。  
  
 使用公共语言运行时 MSIL 反汇编程序 (我`ldasm.exe`) 以查看输出文件中的命名空间名称。  
  
|在 Visual Studio 中设置 /rootnamespace 集成开发环境|  
|---|  
|1.在 **“解决方案资源管理器”**中选择一个项目。 在**项目**菜单上，单击**属性**。 有关详细信息，请参阅[项目设计器简介](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7)。<br />2.单击“应用程序” **** 选项卡。<br />3.在修改此值**根 Namespace**框。|  
  
## <a name="example"></a>示例  
 下面的代码编译`In.vb`和命名空间中包含所有类型声明`mynamespace`。  
  
```  
vbc /rootnamespace:mynamespace in.vb  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Ildasm.exe （IL 反汇编程序）](https://msdn.microsoft.com/library/f7dy01k1)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
