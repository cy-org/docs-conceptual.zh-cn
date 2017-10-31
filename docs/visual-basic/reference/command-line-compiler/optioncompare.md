---
title: "/optioncompare |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- /optioncompare
dev_langs:
- VB
helpviewer_keywords:
- optioncompare compiler option [Visual Basic]
- -optioncompare compiler option [Visual Basic]
- /optioncompare compiler option [Visual Basic]
ms.assetid: 7237b766-b44d-4cc5-9a3c-885348a7d9e4
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
ms.openlocfilehash: 53dee5bb50e20204725f031e3e04f5c37c5b3f96
ms.lasthandoff: 03/13/2017

---
# <a name="optioncompare"></a>/optioncompare
指定如何进行字符串比较。  
  
## <a name="syntax"></a>语法  
  
```  
/optioncompare:{binary | text}  
```  
  
## <a name="remarks"></a>备注  
 您可以指定`/optioncompare`在两种形式之一︰`/optioncompare:binary`使用二进制字符串比较和`/optioncompare:text`使用文本字符串比较。 默认情况下，编译器将使用`/optioncompare:binary`。  
  
 在 Microsoft Windows 中，正在使用的代码页决定的二进制排序顺序。 以下是典型的二进制排序顺序︰  
  
 `A < B < E < Z < a < b < e < z < À < Ê < Ø < à < ê < ø`  
  
 基于文本的字符串比较将基于由您的系统区域设置确定的不区分大小写的文本排序顺序。 典型的文本排序顺序如下所述︰  
  
 `(A = a) < (À = à) < (B=b) < (E=e) < (Ê = ê) < (Z=z) < (Ø = ø)`  
  
### <a name="to-set-optioncompare-in-the-visual-studio-ide"></a>在 Visual Studio IDE 中设置 /optioncompare  
  
1.  在 **“解决方案资源管理器”**中选择一个项目。 在**项目**菜单上，单击**属性**。 有关详细信息，请参阅[项目设计器简介](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7)。  
  
2.  单击“编译”****选项卡。  
  
3.  在修改此值**Option Compare**框。  
  
### <a name="to-set-optioncompare-programmatically"></a>以编程方式设置 /optioncompare  
  
-   请参阅[Option Compare 语句](../../../visual-basic/language-reference/statements/option-compare-statement.md)。  
  
## <a name="example"></a>示例  
 下面的代码编译 P`rojFile.vb` ，并使用二进制字符串比较。  
  
```  
vbc /optioncompare:binary projFile.vb  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/optionexplicit](../../../visual-basic/reference/command-line-compiler/optionexplicit.md)   
 [/optionstrict](../../../visual-basic/reference/command-line-compiler/optionstrict.md)   
 [/optioninfer](../../../visual-basic/reference/command-line-compiler/optioninfer.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [Option Compare 语句](../../../visual-basic/language-reference/statements/option-compare-statement.md)   
 [“选项”对话框 ->“项目”->“Visual Basic 默认值”](https://docs.microsoft.com/visualstudio/ide/reference/visual-basic-defaults-projects-options-dialog-box)
