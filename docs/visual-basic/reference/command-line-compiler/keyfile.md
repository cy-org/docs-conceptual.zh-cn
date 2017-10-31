---
title: "/keyfile |Microsoft 文档"
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
- /keyfile compiler option [Visual Basic]
- keyfile compiler option [Visual Basic]
- -keyfile compiler option [Visual Basic]
ms.assetid: ffa82a4b-517a-4c6c-9889-5bae7b534bb8
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
ms.openlocfilehash: c36eac96ac6302db0b567e8249af726c807c2c6c
ms.lasthandoff: 03/13/2017

---
# <a name="keyfile"></a>/keyfile
指定包含密钥或密钥对的文件从而为程序集赋予强名称。  
  
## <a name="syntax"></a>语法  
  
```  
/keyfile:file  
```  
  
## <a name="arguments"></a>参数  
 `file`  
 必需。 包含密钥的文件。 如果文件名包含空格，则将名称括在双引号 ("")。  
  
## <a name="remarks"></a>备注  
 编译器将公钥插入程序集清单，然后使用私钥对最终程序集进行签名。 若要生成的密钥文件，请键入`sn -k file`在命令行。 有关详细信息，请参阅 [Sn.exe （强名称工具）](https://msdn.microsoft.com/library/k5b5tt23)。  
  
 如果在编译时使用`/target:module`，保存在模块和合并到编译为程序集时创建的程序集密钥文件的名称[/addmodule](../../../visual-basic/reference/command-line-compiler/addmodule.md)。  
  
 此外可以将您的加密信息传递给编译器[/keycontainer](../../../visual-basic/reference/command-line-compiler/keycontainer.md)。 使用[/delaysign](../../../visual-basic/reference/command-line-compiler/delaysign.md)如果希望部分签名的程序集。  
  
 您还可以通过以下方式指定此选项的自定义特性 (<xref:System.Reflection.AssemblyKeyFileAttribute>) 中的任何 Microsoft 中间语言模块的源代码。</xref:System.Reflection.AssemblyKeyFileAttribute>  
  
 两者`/keyfile`和[/keycontainer](../../../visual-basic/reference/command-line-compiler/keycontainer.md)指定 （通过命令行选项或通过自定义特性） 在同一编译中，编译器将第一次尝试的密钥容器。 如果成功，则会将该程序集签名的密钥容器中的信息。 如果编译器没有找到密钥容器，它将尝试使用指定的文件`/keyfile`。 如果此操作成功，则使用密钥文件中的信息签名程序集密钥信息安装到密钥容器中 (类似于`sn -i`)，以便在下一步的编译中，密钥的容器才有效。  
  
 请注意，一个密钥文件可能包含仅将公钥。  
  
 请参阅[创建和使用具有强名称程序集](https://msdn.microsoft.com/library/xwb8f617)有关程序集进行签名的详细信息。  
  
> [!NOTE]
>  `/keyfile`选项不是可从[!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]开发环境中; 只有当从命令行进行编译，它才可用。  
  
## <a name="example"></a>示例  
 下面的代码编译源文件`Input.vb`和指定的密钥文件。  
  
```  
vbc /keyfile:myfile.sn input.vb  
```  
  
## <a name="see-also"></a>另请参阅  
 [程序集和全局程序集缓存](../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md)   
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/reference (Visual Basic)](../../../visual-basic/reference/command-line-compiler/reference.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
