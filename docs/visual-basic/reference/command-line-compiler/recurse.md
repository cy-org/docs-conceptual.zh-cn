---
title: "/recurse |Microsoft 文档"
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
- /recurse compiler option [Visual Basic]
- -recurse compiler option [Visual Basic]
- recurse compiler option [Visual Basic]
ms.assetid: 84a0b670-33ae-44c4-a46a-b90388809317
caps.latest.revision: 12
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
ms.openlocfilehash: fbf7d67c7f70345e62ddbb03c8626b688b5c593b
ms.lasthandoff: 03/13/2017

---
# <a name="recurse"></a>/recurse
编译源代码文件的指定的目录或项目目录的所有子目录中。  
  
## <a name="syntax"></a>语法  
  
```  
/recurse:[dir\]file  
```  
  
## <a name="arguments"></a>参数  
 `dir`  
 可选。 要在其中执行搜索，以开始目录。 如果未指定，那么搜索将开始在项目目录中。  
  
 `file`  
 必需。 要搜索的文件。 允许使用通配符。  
  
## <a name="remarks"></a>备注  
 可以在文件名中使用通配符来编译项目目录中的所有匹配文件，而无需使用`/recurse`。 如果不指定任何输出文件的名称，则编译器将基于上处理的第一个输入文件的输出文件名称。 这通常是在编译时按字母顺序查看的文件列表中的第一个文件。 出于此原因，则最好指定输出文件中使用`/out`选项。  
  
> [!NOTE]
>  `/recurse`选项不是在 Visual Studio 开发环境中可用; 只有当从命令行进行编译，它才可用。  
  
## <a name="example"></a>示例  
 下面的代码编译所有[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]当前目录中的文件。  
  
```  
vbc *.vb  
```  
  
 下面的代码编译所有[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]中的文件`Test\ABC`目录和，在它下面的任何目录，然后生成`Test.ABC.dll`。  
  
```  
vbc /target:library /out:Test.ABC.dll /recurse:Test\ABC\*.vb  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/ 输出 (Visual Basic)](../../../visual-basic/reference/command-line-compiler/out.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
