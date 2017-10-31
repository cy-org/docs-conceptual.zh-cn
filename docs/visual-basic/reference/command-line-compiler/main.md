---
title: "/main |Microsoft 文档"
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
- main compiler option [Visual Basic]
- /main compiler option [Visual Basic]
- -main compiler option [Visual Basic]
ms.assetid: 83fc339d-6652-415d-b205-b5133319b5b0
caps.latest.revision: 19
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
ms.openlocfilehash: dded7621845141896f353d69ab757010c825b975
ms.lasthandoff: 03/13/2017

---
# <a name="main"></a>/main
指定的类或模块，其中包含`Sub Main`过程。  
  
## <a name="syntax"></a>语法  
  
```  
/main:location  
```  
  
## <a name="arguments"></a>参数  
 `location`  
 必需。 完全限定的类或模块，其中包含位置`Sub Main`在程序启动时要调用的过程。 这可能是窗体中**/main:module**或**/main:namespace.module**。  
  
## <a name="remarks"></a>备注  
 当您创建可执行文件或 Windows 可执行程序时，请使用此选项。 如果**/main**省略选项，编译器将搜索有效的共享`Sub Main`所有公共类和模块中。  
  
 请参阅[在 Visual Basic 中的 Main 过程](../../../visual-basic/programming-guide/program-structure/main-procedure.md)有关的各种形式的讨论`Main`过程。  
  
 当`location`是一个类，继承自<xref:System.Windows.Forms.Form>，则编译器会提供默认值`Main`如果类没有启动该应用程序的过程`Main`过程。</xref:System.Windows.Forms.Form> 这样就可以在命令行在开发环境中创建的代码编译。  
  
 [!code-vb[VbVbalrCompiler #&16;](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/main_1.vb)]  
  
### <a name="to-set-main-in-the-visual-studio-integrated-development-environment"></a>在 Visual Studio 中设置 /main 集成开发环境  
  
1.  在 **“解决方案资源管理器”**中选择一个项目。 在**项目**菜单上，单击**属性**。  
  
     有关详细信息，请参阅[项目设计器简介](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7)。  
  
2.  单击“应用程序” **** 选项卡。  
  
3.  请确保**启用应用程序框架**未选中复选框。  
  
4.  在修改此值**启动对象**框。  
  
## <a name="example"></a>示例  
 下面的代码编译`T2.vb`和`T3.vb`，并指定该`Sub Main`将在中找到过程`Test2`类。  
  
```  
vbc t2.vb t3.vb /main:Test2  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/target (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [NIB: Hello，World Visual Basic 版本](http://msdn.microsoft.com/en-us/9d030b60-e148-4366-a462-69532f02294c)   
 [在 Visual Basic 中的 main 过程](../../../visual-basic/programming-guide/program-structure/main-procedure.md)
