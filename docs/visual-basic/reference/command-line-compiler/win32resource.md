---
title: "/win32resource |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- /win32resource
- win32resource
dev_langs:
- VB
helpviewer_keywords:
- /win32resource compiler option [Visual Basic]
- -win32resource compiler option [Visual Basic]
- win32resource compiler option [Visual Basic]
ms.assetid: e226946d-19ce-4cc9-91f5-aed24f77aa2b
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
ms.openlocfilehash: 37902590d5a05d7fdb2a521f3c3de2ad88c2c502
ms.lasthandoff: 03/13/2017

---
# <a name="win32resource"></a>/win32resource
在输出文件中插入 Win32 资源文件。  
  
## <a name="syntax"></a>语法  
  
```  
/win32resource:filename  
```  
  
## <a name="arguments"></a>参数  
 `filename`  
 要添加到输出文件的资源文件的名称。 将文件名括在双引号 ("") 如果包含空格。  
  
## <a name="remarks"></a>备注  
 您可以创建 Win32 资源文件与 Microsoft Windows 资源编译器 (RC)。  
  
 Win32 资源可以包含版本或位图 （图标） 信息，以帮助标识应用程序中的**文件资源管理器**。 如果未指定`/win32resource`，编译器将生成基于程序集版本的版本信息。 `/win32resource`和`/win32icon`是互相排斥的选项。  
  
 请参阅[/linkresource (Visual Basic 中)](../../../visual-basic/reference/command-line-compiler/linkresource.md)引用[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]资源文件或[/resource (Visual Basic 中)](../../../visual-basic/reference/command-line-compiler/resource.md)附加[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]资源文件。  
  
> [!NOTE]
>  `/win32resource`选项不是在 Visual Studio 开发环境中可用; 只有当从命令行进行编译，它才可用。  
  
## <a name="example"></a>示例  
 下面的代码编译`In.vb`，并将附加 Win32 资源文件， `Rf.res`:  
  
```  
vbc /win32resource:rf.res in.vb  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
