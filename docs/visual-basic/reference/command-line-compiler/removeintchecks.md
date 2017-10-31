---
title: "/removeintchecks |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- removeintchecks
- /removeintchecks
dev_langs:
- VB
helpviewer_keywords:
- removeintchecks compiler option [Visual Basic]
- /removeintchecks compiler option [Visual Basic]
- -removeintchecks compiler option [Visual Basic]
ms.assetid: c1835bd5-1e38-4fba-bd2f-6984774765d4
caps.latest.revision: 14
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
ms.openlocfilehash: 8e50200b8755ccc6b1c173024856955f5075b67e
ms.lasthandoff: 03/13/2017

---
# <a name="removeintchecks"></a>/removeintchecks
将启用溢出错误检查整数运算打开或关闭。  
  
## <a name="syntax"></a>语法  
  
```  
/removeintchecks[+ | -]  
```  
  
## <a name="arguments"></a>参数  
  
|术语|定义|  
|---|---|  
|`+` &#124; `-`|可选。 `/removeintchecks-`选项将使编译器来检查所有整数计算中的溢出错误。 默认值为 `/removeintchecks-`。<br /><br /> 指定`/removeintchecks`或`/removeintchecks+`可禁止错误检查，并使整数计算速度更快。 但是，不进行错误检查，如果数据类型容量被超出，可能会不正确的结果存储而不会引发错误。|  
  
|在 Visual Studio 中设置 /removeintchecks 集成开发环境|  
|---|  
|1.在 **“解决方案资源管理器”**中选择一个项目。 在**项目**菜单上，单击**属性**。 有关详细信息，请参阅[项目设计器简介](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7)。<br />2.单击“编译”****选项卡。<br />3.单击 **“高级”** 按钮。<br />4.修改的值**整数溢出检查**框。|  
  
## <a name="example"></a>示例  
 下面的代码编译`Test.vb`并关闭整数溢出错误检查。  
  
```  
vbc /removeintchecks+ test.vb  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
