---
title: "/errorreport |Microsoft 文档"
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
- -errorreport compiler option [Visual Basic]
- /errorreport compiler option [Visual Basic]
- errorreport compiler option [Visual Basic]
ms.assetid: a7fe83a2-a6d8-460c-8dad-79a8f433f501
caps.latest.revision: 19
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 2ebe5646256926f68a1a900b91c25a1768505785
ms.lasthandoff: 03/13/2017

---
# <a name="errorreport"></a>/errorreport
指定 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] 编译器应报告内部编译器错误的方式。  
  
## <a name="syntax"></a>语法  
  
```  
/errorreport:{ prompt | queue | send | none }  
```  
  
## <a name="remarks"></a>备注  
 此选项可以方便地向报表[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]到内部编译器错误 (ICE) [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] Microsoft 团队。 默认情况下，编译器会向 Microsoft 发送任何信息。 但是，如果您遇到内部编译器错误，此选项允许您向 Microsoft 报告错误。 该信息将帮助确定的原因的 Microsoft 工程师以及可帮助改善的下一个版本[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]。  
  
 发送报告用户的能力取决于计算机和用户策略权限。  
  
 下表总结了的效果`/errorreport`选项。  
  
|选项|行为|  
|---|---|  
|`prompt`|如果内部编译器错误发生，弹出对话框，以便您可以查看编译器收集的确切数据。 可以确定是否存在任何错误报告中的敏感信息并决定是否将其发送给 Microsoft。 如果你决定发送它，并且计算机和用户策略设置允许这样，编译器会将数据发送给 Microsoft。|  
|`queue`|排入队列的错误报告。 当使用管理员权限登录时，可以报告自上次登录以来的任何失败 （将不会提示您发送失败报告一次以上每隔三天）。 这是默认行为时`/errorreport`未指定选项。|  
|`send`|如果发生内部编译器错误，并且计算机和用户策略设置允许这样，编译器会将数据发送给 Microsoft。<br /><br /> 该选项`/errorReport:send`尝试自动向 Microsoft 发送错误的信息。 此选项取决于注册表。 有关在注册表中设置适当的值的详细信息，请参阅[如何自动发送错误报告，在 Visual Studio 2008 命令行工具中打开](http://go.microsoft.com/fwlink/?LinkID=184695)。|  
|`none`|如果发生内部编译器错误，它不会收集或发送给 Microsoft。|  
  
 编译器将发送一个错误，它通常包含某些源代码次包括堆栈的数据。 如果`/errorreport`与使用[/bugreport](../../../visual-basic/reference/command-line-compiler/bugreport.md)选项，则发送整个源文件。  
  
 此选项适用于[/bugreport](../../../visual-basic/reference/command-line-compiler/bugreport.md)选项，因为它允许 Microsoft 工程师能更轻松地重现错误。  
  
> [!NOTE]
>  `/errorreport`选项不是在 Visual Studio 开发环境中可用; 只有当从命令行进行编译，它才可用。  
  
## <a name="example"></a>示例  
 下面的代码试图编译`T2.vb`，如果编译器遇到内部编译器错误，它会提示你向 Microsoft 发送错误报告。  
  
```  
vbc /errorreport:prompt t2.vb  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [/bugreport](../../../visual-basic/reference/command-line-compiler/bugreport.md)
