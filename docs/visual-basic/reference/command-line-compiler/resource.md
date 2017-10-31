---
title: "/resource (Visual Basic 中) |Microsoft 文档"
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
- /resource compiler option [Visual Basic]
- -resource compiler option [Visual Basic]
- /res compiler option [Visual Basic]
- res compiler option [Visual Basic]
- -res compiler option [Visual Basic]
- resource compiler option [Visual Basic]
ms.assetid: eee2f227-91f2-4f2b-a9d6-1c51c5320858
caps.latest.revision: 19
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
ms.openlocfilehash: b46800322fd03eb2578cc558cc1d9bb78550aa61
ms.lasthandoff: 03/13/2017

---
# <a name="resource-visual-basic"></a>/resource (Visual Basic)
将托管资源嵌入程序集。  
  
## <a name="syntax"></a>语法  
  
```  
/resource:filename[,identifier[,public|private]]  
' -or-  
/res:filename[,identifier[,public|private]]  
```  
  
## <a name="arguments"></a>参数  
  
|术语|定义|  
|---|---|  
|`filename`|必需。 要在输出文件中嵌入的资源文件的名称。 默认情况下，`filename`在程序集是公共的。 将文件名括在双引号 ("") 如果包含空格。|  
|`identifier`|可选。 资源; 的逻辑名称用来加载它的名称。 默认值是该文件的名称。 或者，您可以指定资源与以下是否是公有或私有程序集清单中︰ `/res:``filename.res`，`myname.res`，`public`|  
  
## <a name="remarks"></a>备注  
 使用`/linkresource`若要将资源链接到程序集，而无需将资源文件放置在输出文件。  
  
 如果`filename`是[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]创建资源文件，例如，通过[Resgen.exe （资源文件生成器）](http://msdn.microsoft.com/library/8ef159de-b660-4bec-9213-c3fbc4d1c6f4)或在开发环境中，它可以访问其成员保持<xref:System.Resources>命名空间 (请参阅<xref:System.Resources.ResourceManager>有关详细信息)。</xref:System.Resources.ResourceManager> </xref:System.Resources> 若要在运行时访问所有其他资源，请使用以下方法之一︰ <xref:System.Reflection.Assembly.GetManifestResourceInfo%2A>， <xref:System.Reflection.Assembly.GetManifestResourceNames%2A>，或<xref:System.Reflection.Assembly.GetManifestResourceStream%2A>.</xref:System.Reflection.Assembly.GetManifestResourceStream%2A> </xref:System.Reflection.Assembly.GetManifestResourceNames%2A> </xref:System.Reflection.Assembly.GetManifestResourceInfo%2A>  
  
 缩写形式`/resource`是`/res`。  
  
 有关如何设置`/resource`在 Visual Studio IDE 中，请参阅[管理应用程序资源 (.NET)](https://docs.microsoft.com/visualstudio/ide/managing-application-resources-dotnet)。  
  
## <a name="example"></a>示例  
 下面的代码编译`In.vb`和附加的资源文件`Rf.resource`。  
  
```  
vbc /res:rf.resource in.vb  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/win32resource](../../../visual-basic/reference/command-line-compiler/win32resource.md)   
 [/linkresource (Visual Basic)](../../../visual-basic/reference/command-line-compiler/linkresource.md)   
 [/target (Visual Basic)](../../../visual-basic/reference/command-line-compiler/target.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
