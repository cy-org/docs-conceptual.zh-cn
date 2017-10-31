---
title: "/langversion (Visual Basic 中) |Microsoft 文档"
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
- /langversion compiler option [Visual Basic]
- langversion compiler option [Visual Basic]
- -langversion compiler option [Visual Basic]
ms.assetid: 59b7b0c8-2dde-4e9b-94e7-0237f7e0bafb
caps.latest.revision: 8
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
ms.openlocfilehash: 9970df0c9babc368210169fae0490b423d77f40d
ms.lasthandoff: 03/13/2017

---
# <a name="langversion-visual-basic"></a>/langversion (Visual Basic)
使编译器接受包含指定版本的 Visual Basic 语言的语法。  
  
## <a name="syntax"></a>语法  
  
```  
/langversion:version  
```  
  
## <a name="arguments"></a>参数  
 `version`  
 必需。 要在编译期间使用的语言版本。 接受的值是`9`， `9.0`， `10`，和`10.0`。  
  
## <a name="remarks"></a>备注  
 `/langversion`选项指定编译器接受的语法。 例如，如果您指定的语言版本是 9.0，编译器将生成有关仅在版本 10.0 中有效和更高版本的语法错误。  
  
 在面向不同版本的.NET framework 开发的应用程序时，可以使用此选项。 例如，如果您面向的.NET Framework 3.5，您可以使用此选项以确保不使用语言版本 10.0 的语法。  
  
 您可以设置`/langversion`直接只能通过使用命令行。 有关详细信息，请参阅[面向特定的 .NET Framework 版本](https://docs.microsoft.com/visualstudio/ide/targeting-a-specific-dotnet-framework-version)。  
  
## <a name="example"></a>示例  
 下面的代码编译`sample.vb`对于 Visual Basic 9.0 版。  
  
```  
vbc /langversion:9.0 sample.vb  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [面向特定的 .NET Framework 版本](https://docs.microsoft.com/visualstudio/ide/targeting-a-specific-dotnet-framework-version)
