---
title: "/noconfig |Microsoft 文档"
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
- noconfig compiler option [Visual Basic]
- -noconfig compiler option [Visual Basic]
- /noconfig compiler option [Visual Basic]
ms.assetid: a7405067-bd21-4171-adf4-a126fa3ad6c3
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
ms.openlocfilehash: 304d0e7fc787adb1d7776a2c047090ffc230fcc1
ms.lasthandoff: 03/13/2017

---
# <a name="noconfig"></a>/noconfig
指定编译器应不会自动引用常使用[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]程序集或导入`System`和`Microsoft.VisualBasic`命名空间。  
  
## <a name="syntax"></a>语法  
  
```  
/noconfig  
```  
  
## <a name="remarks"></a>备注  
 `/noconfig`选项会告知编译器无法编译 Vbc.rsp 文件后，它位于 Vbc.exe 文件所在的同一目录中。 Vbc.rsp 文件引用常用[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]程序集和导入`System`和`Microsoft.VisualBasic`命名空间。 编译器隐式引用的 System.dll 程序集，除非`/nostdlib`指定选项。 `/nostdlib`选项会告知编译器不能使用 Vbc.rsp 进行编译或自动引用 System.dll 程序集。  
  
> [!NOTE]
>  始终引用 Mscorlib.dll 和 Microsoft.VisualBasic.dll 的程序集。  
  
 您可以修改该 Vbc.rsp 文件以指定应包括在每个 Vbc.exe 编译中的其他编译器选项 (除非指定`/noconfig`选项)。 有关详细信息，请参阅 [@（指定响应文件）](../../../visual-basic/reference/command-line-compiler/specify-response-file.md)。  
  
 编译器选项传递给处理`vbc`最后一个命令。 因此，在命令行上的任何选项将重写 Vbc.rsp 文件中的相同选项的设置。  
  
> [!NOTE]
>  `/noconfig`选项不是在 Visual Studio 开发环境中可用; 只有当从命令行进行编译，它才可用。  
  
## <a name="see-also"></a>另请参阅  
 [/nostdlib (Visual Basic)](../../../visual-basic/reference/command-line-compiler/nostdlib.md)   
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [@ （指定响应文件）](../../../visual-basic/reference/command-line-compiler/specify-response-file.md)   
 [/reference (Visual Basic)](../../../visual-basic/reference/command-line-compiler/reference.md)
