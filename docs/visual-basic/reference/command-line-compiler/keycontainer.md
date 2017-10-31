---
title: "/keycontainer |Microsoft 文档"
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
- -keycontainer compiler option [Visual Basic]
- keycontainer compiler option [Visual Basic]
- /keycontainer compiler option [Visual Basic]
ms.assetid: 6a9bc861-1752-4db1-9f64-b5252f0482cc
caps.latest.revision: 16
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
ms.openlocfilehash: 68fa09edce5c0c9af143197f9379d5a46afab52e
ms.lasthandoff: 03/13/2017

---
# <a name="keycontainer"></a>/keycontainer
指定密钥对的密钥容器名称从而为程序集赋予强名称。  
  
## <a name="syntax"></a>语法  
  
```  
/keycontainer:container  
```  
  
## <a name="arguments"></a>参数  
  
|术语|定义|  
|---|---|  
|`container`|必需。 包含密钥的容器文件。 将文件名括在双引号 ("") 如果名称包含空格。|  
  
## <a name="remarks"></a>备注  
 通过将公钥插入程序集清单，并使用私钥对最终的程序集进行签名，编译器将创建可共享的组件。 若要生成的密钥文件，请键入`sn -k``file`在命令行。 `-i`选项将密钥对安装到一个容器。 有关详细信息，请参阅 [Sn.exe （强名称工具）](https://msdn.microsoft.com/library/k5b5tt23)。  
  
 如果在编译时使用`/target:module`，保存在模块和合并到编译为程序集时创建的程序集密钥文件的名称[/addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md)。  
  
 您还可以通过以下方式指定此选项的自定义特性 (<xref:System.Reflection.AssemblyKeyNameAttribute>) 中的任何 Microsoft 中间语言 (MSIL) 模块的源代码。</xref:System.Reflection.AssemblyKeyNameAttribute>  
  
 此外可以将您的加密信息传递给编译器[/keyfile](../../../visual-basic/reference/command-line-compiler/keyfile.md)。 使用[/delaysign](../../../visual-basic/reference/command-line-compiler/delaysign.md)如果希望部分签名的程序集。  
  
 请参阅[创建和使用具有强名称程序集](https://msdn.microsoft.com/library/xwb8f617)有关程序集进行签名的详细信息。  
  
> [!NOTE]
>  `/keycontainer`选项不是在 Visual Studio 开发环境中可用; 只有当从命令行进行编译，它才可用。  
  
## <a name="example"></a>示例  
 下面的代码编译源文件`Input.vb`和指定的密钥容器。  
  
```  
vbc /keycontainer:key1 input.vb  
```  
  
## <a name="see-also"></a>另请参阅  
 [程序集和全局程序集缓存](../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md)   
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/keyfile](../../../visual-basic/reference/command-line-compiler/keyfile.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
