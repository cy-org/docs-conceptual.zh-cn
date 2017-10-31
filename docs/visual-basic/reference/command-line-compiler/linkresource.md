---
title: "/linkresource (Visual Basic 中) |Microsoft 文档"
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
- /linkresource compiler option [Visual Basic]
- -linkresource compiler option [Visual Basic]
- linkresource compiler option [Visual Basic]
- /linkres compiler option [Visual Basic]
- linkres compiler option [Visual Basic]
- -linkres compiler option [Visual Basic]
ms.assetid: cf4dcad8-17b7-404c-9184-29358aa05b15
caps.latest.revision: 16
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
ms.openlocfilehash: fafde6563340189108a879b82e7e880aca690b39
ms.lasthandoff: 03/13/2017

---
# <a name="linkresource-visual-basic"></a>/linkresource (Visual Basic)
创建指向托管资源的链接。  
  
## <a name="syntax"></a>语法  
  
```  
/linkresource:filename[,identifier[,public|private]]  
' -or-  
/linkres:filename[,identifier[,public|private]]  
```  
  
## <a name="arguments"></a>参数  
 `filename`  
 必需。 要链接到程序集的资源文件。 如果文件名包含空格，则将名称括在双引号 ("")。  
  
 `identifier`  
 可选。 资源的逻辑名称。 用于加载资源名称。 默认值是该文件的名称。 或者，您可以指定文件是否是公共的还是私有的程序集清单，例如︰ `/linkres:filename.res,myname.res,public`。 默认情况下，`filename`在程序集是公共的。  
  
## <a name="remarks"></a>备注  
 `/linkresource`选项不会在输出文件中嵌入的资源文件; 使用`/resource`选项以执行此操作。  
  
 `/linkresource`选项需要一个`/target`以外选项`/target:module`。  
  
 如果`filename`是[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]创建资源文件，例如，通过[Resgen.exe （资源文件生成器）](http://msdn.microsoft.com/library/8ef159de-b660-4bec-9213-c3fbc4d1c6f4)或在开发环境中，它可以访问其成员保持<xref:System.Resources>命名空间。</xref:System.Resources> (有关详细信息，请参阅<xref:System.Resources.ResourceManager>。)</xref:System.Resources.ResourceManager>若要在运行时访问所有其他资源，使用的方法，以开始`GetManifestResource`中<xref:System.Reflection.Assembly>类。</xref:System.Reflection.Assembly>  
  
 文件名称可以是任何文件格式。 例如，您可能想要使本机 DLL 程序集的一部分，以便它可以安装到全局程序集缓存中并从程序集中的托管代码访问。  
  
 缩写形式`/linkresource`是`/linkres`。  
  
> [!NOTE]
>  `/linkresource`选项不可用从 Visual Studio 开发环境，可仅编译时从命令行。  
  
## <a name="example"></a>示例  
 下面的代码编译`In.vb`并链接到资源文件`Rf.resource`。  
  
```  
vbc /linkresource:rf.resource in.vb  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/target (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)   
 [/resource (Visual Basic)](../../../visual-basic/reference/command-line-compiler/resource.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
