---
title: "/bugreport |Microsoft 文档"
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
- -bugreport compiler option [Visual Basic]
- bugreport compiler option [Visual Basic]
- /bugreport compiler option [Visual Basic]
ms.assetid: e4325406-8dbd-4b48-b311-9ee0799e48bb
caps.latest.revision: 22
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
ms.openlocfilehash: 9c64ec49d7e6842edbc0fed7407a34132a8f5a88
ms.lasthandoff: 03/13/2017

---
# <a name="bugreport"></a>/bugreport
创建时归档 bug 报告，可以使用一个文件。  
  
## <a name="syntax"></a>语法  
  
```  
/bugreport:file  
```  
  
## <a name="arguments"></a>参数  
  
|术语|定义|  
|---|---|  
|`file`|必需。 将包含错误报告文件的名称。 将文件名括在双引号 ("") 如果名称包含空格。|  
  
## <a name="remarks"></a>备注  
 以下信息添加到`file`:  
  
-   在编译中的所有源代码文件的副本。  
  
-   编译器选项编译中使用的列表。  
  
-   有关编译器、 公共语言运行时和操作系统版本信息。  
  
-   编译器输出中，如果有的话。  
  
-   此问题，它向您发出提示的说明。  
  
-   应先修复您的想法问题的说明，提示你。  
  
 因为所有源代码文件的副本包含在`file`，可能需要重现尽可能短的程序中 （可疑的） 代码缺陷。  
  
> [!IMPORTANT]
>  `/bugreport`选项将生成包含潜在的敏感信息的文件。 这包括当前时间，编译器版本[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]版本、 操作系统版本、 用户名称、 与其编译器是否运行，所有的源代码，以及二进制形式的所有被引用程序集的命令行参数。 此选项可以通过指定的服务器端汇集的 Web.config 文件中的命令行选项[!INCLUDE[vstecasp](../../../csharp/language-reference/preprocessor-directives/includes/vstecasp_md.md)]应用程序。 若要避免此情形，修改 Machine.config 文件，以便不允许用户在服务器上进行编译。  
  
 如果此选项用于`/errorreport:prompt`， `/errorreport:queue`，或`/errorreport:send`，并且您的应用程序遇到内部编译器错误中的信息`file`发送到 Microsoft Corporation。 该信息将帮助确定错误原因的 Microsoft 工程师以及可帮助改善的下一个版本[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]。 默认情况下，任何信息不发送给 Microsoft。 但是，当您编译应用程序使用`/errorreport:queue`，可以启用默认情况下，应用程序收集其错误报告。 然后，在计算机的管理员登录，错误报告系统将显示一个弹出窗口，使管理员能够将转发给 Microsoft 任何错误报告自登录之后发生。  
  
> [!NOTE]
>  `/bugreport`选项不是在 Visual Studio 开发环境中可用，可仅编译时从命令行。  
  
## <a name="example"></a>示例  
 下面的示例将编译`T2.vb`并将错误报告的所有信息都放入该文件`Problem.txt`。  
  
```  
vbc /bugreport:problem.txt t2.vb  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [/debug (Visual Basic)](../../../visual-basic/reference/command-line-compiler/debug.md)   
 [/errorreport](../../../visual-basic/reference/command-line-compiler/errorreport.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [（ASP.NET 设置架构） securityPolicy 的 trustLevel 元素](http://msdn.microsoft.com/en-us/729ab04c-03da-4ee5-86b1-be9d08a09369)
