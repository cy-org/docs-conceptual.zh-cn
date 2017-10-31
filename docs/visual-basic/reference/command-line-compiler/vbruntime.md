---
title: "/vbruntime |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbruntime
- /vbruntime
dev_langs:
- VB
helpviewer_keywords:
- vbruntime compiler option [Visual Basic]
- -vbruntime compiler option [Visual Basic]
- /vbruntime compiler option [Visual Basic]
ms.assetid: 1aa0239e-511a-4c29-957d-fd72877b350a
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
ms.openlocfilehash: 455f950988b540b74874ce38882c59059f77ea8f
ms.lasthandoff: 03/13/2017

---
# <a name="vbruntime"></a>/vbruntime
指定编译器应在不引用 Visual Basic 运行库的情况下进行编译，或在引用特定运行库的情况下进行编译。  
  
## <a name="syntax"></a>语法  
  
```  
/vbruntime:{ - | + | * | path }  
```  
  
## <a name="arguments"></a>参数  
 \-  
 编译而无需对 Visual Basic 运行库的引用。  
  
 \+  
 为 Visual Basic 运行库的默认值的引用来编译。  
  
 \*  
 对 Visual Basic 运行时库的引用的情况下编译，并将嵌入到程序集从 Visual Basic 运行库的核心功能。  
  
 `path`  
 对指定库 (DLL) 的引用来编译。  
  
## <a name="remarks"></a>备注  
 `/vbruntime`编译器选项可用于指定编译器应编译而无需对 Visual Basic 运行库的引用。 如果您对 Visual Basic 运行库的引用的情况下编译，错误或警告登录生成对 Visual Basic 运行时帮助器调用的代码或语言构造。 (A *Visual Basic 运行时帮助器*是在运行时执行特定的语言语义时调用的 Microsoft.VisualBasic.dll 中定义的函数。)  
  
 `/vbruntime+`选项将生成相同的行为，如果没有则会发生`/vbruntime`指定开关。 您可以使用`/vbruntime+`选项重写之前`/vbruntime`开关。  
  
 大多数对象的`My`使用时，类型将不可用`/vbruntime-`或`vbruntime:``path`选项。  
  
## <a name="embedding-visual-basic-runtime-core-functionality"></a>嵌入 Visual Basic 运行时的核心功能  
 `/vbruntime*`选项使您能够对运行时库的引用的情况下编译。 相反，从 Visual Basic 运行库的核心功能嵌入用户程序集。 如果在不包含 Visual Basic 运行时的平台上运行你的应用程序，可以使用此选项。  
  
 嵌入以下的运行库成员︰  
  
-   <xref:Microsoft.VisualBasic.CompilerServices.Conversions>类</xref:Microsoft.VisualBasic.CompilerServices.Conversions>  
  
-   <xref:Microsoft.VisualBasic.Strings.AscW%28System.Char%29>方法</xref:Microsoft.VisualBasic.Strings.AscW%28System.Char%29>  
  
-   <xref:Microsoft.VisualBasic.Strings.AscW%28System.String%29>方法</xref:Microsoft.VisualBasic.Strings.AscW%28System.String%29>  
  
-   <xref:Microsoft.VisualBasic.Strings.ChrW%28System.Int32%29>方法</xref:Microsoft.VisualBasic.Strings.ChrW%28System.Int32%29>  
  
-   <xref:Microsoft.VisualBasic.Constants.vbBack>常量</xref:Microsoft.VisualBasic.Constants.vbBack>  
  
-   <xref:Microsoft.VisualBasic.Constants.vbCr>常量</xref:Microsoft.VisualBasic.Constants.vbCr>  
  
-   <xref:Microsoft.VisualBasic.Constants.vbCrLf>常量</xref:Microsoft.VisualBasic.Constants.vbCrLf>  
  
-   <xref:Microsoft.VisualBasic.Constants.vbFormFeed>常量</xref:Microsoft.VisualBasic.Constants.vbFormFeed>  
  
-   <xref:Microsoft.VisualBasic.Constants.vbLf>常量</xref:Microsoft.VisualBasic.Constants.vbLf>  
  
-   <xref:Microsoft.VisualBasic.Constants.vbNewLine>常量</xref:Microsoft.VisualBasic.Constants.vbNewLine>  
  
-   <xref:Microsoft.VisualBasic.Constants.vbNullChar>常量</xref:Microsoft.VisualBasic.Constants.vbNullChar>  
  
-   <xref:Microsoft.VisualBasic.Constants.vbNullString>常量</xref:Microsoft.VisualBasic.Constants.vbNullString>  
  
-   <xref:Microsoft.VisualBasic.Constants.vbTab>常量</xref:Microsoft.VisualBasic.Constants.vbTab>  
  
-   <xref:Microsoft.VisualBasic.Constants.vbVerticalTab>常量</xref:Microsoft.VisualBasic.Constants.vbVerticalTab>  
  
-   某些对象`My`类型  
  
 如果在编译时使用`/vbruntime*`选项和您的代码引用的成员没有嵌入的核心功能的 Visual Basic 运行时库中，编译器将返回一个错误，指示该成员不可用。  
  
## <a name="referencing-a-specified-library"></a>引用指定的库  
 您可以使用`path`参数来编译到自定义运行时库而不是默认 Visual Basic 运行库的引用。  
  
 如果值为`path`参数是 DLL 的完全限定的路径，则编译器将使用该文件作为运行时库。 如果值为`path`参数不是对 DLL 的完全限定的路径、 Visual Basic 编译器将首先搜索当前文件夹中的标识 DLL。 它将会使用指定的路径中搜索[/sdkpath](../../../visual-basic/reference/command-line-compiler/sdkpath.md)编译器选项。 如果`/sdkpath`不使用编译器选项，编译器将搜索.NET Framework 文件夹中的标识 DLL (`%systemroot%\Microsoft.NET\Framework\versionNumber`)。  
  
## <a name="example"></a>示例  
 下面的示例演示如何使用`/vbruntime`选项来编译为一个自定义库的引用。  
  
```  
vbc /vbruntime:C:\VBLibraries\CustomVBLibrary.dll  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 核心 – Visual Studio 2010 SP1 中新的编译模式](http://blogs.msdn.com/b/vbteam/archive/2011/01/10/vb-core-new-compilation-mode-in-visual-studio-2010-sp1.aspx)   
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [/sdkpath](../../../visual-basic/reference/command-line-compiler/sdkpath.md)
