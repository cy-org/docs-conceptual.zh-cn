---
title: "/link (Visual Basic 中) |Microsoft 文档"
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
- l compiler option [Visual Basic]
- EmbedInteropTypes
- embed interop types [COM Interop]
- -link compiler option [Visual Basic]
- /link compiler option [Visual Basic]
- link compiler option [Visual Basic]
- -l compiler option [Visual Basic]
- /l compiler option [Visual Basic]
ms.assetid: 1885f24a-86f5-486c-a064-9fb7e455ccec
caps.latest.revision: 27
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
ms.openlocfilehash: e98c855f0a0185e9d1b6682df9fc734e9f1f07bc
ms.lasthandoff: 03/13/2017

---
# <a name="link-visual-basic"></a>/link (Visual Basic)
使编译器将在指定的程序集的 COM 类型信息提供给当前正在编译项目。  
  
## <a name="syntax"></a>语法  
  
```  
/link:fileList  
' -or-  
/l:fileList  
```  
  
## <a name="arguments"></a>参数  
  
|术语|定义|  
|---|---|  
|`fileList`|必需。 程序集文件名称的以逗号分隔列表。 如果文件名包含空格，则将名称括在引号内。|  
  
## <a name="remarks"></a>备注  
 `/link`选项使你可以部署的应用程序包含嵌入类型信息。 然后，应用程序可以使用运行时程序集中实现嵌入的类型信息，而无需对运行时程序集引用的类型。 如果发布了各种版本的运行时程序集，则包含嵌入的类型信息的应用程序可以使用的各种版本，而无需重新编译。 有关示例，请参阅[演练︰ 嵌入托管程序集的类型](http://msdn.microsoft.com/library/b28ec92c-1867-4847-95c0-61adfe095e21)。  
  
 使用`/link`选项将特别有用，当您正在使用 COM 互操作。 嵌入 COM 类型，以便您的应用程序不再需要主互操作程序集 (PIA) 的目标计算机上。 `/link`选项指示编译器将嵌入到生成的已编译代码引用的互操作程序集的 COM 类型信息。 CLSID (GUID) 值被标识的 COM 类型。 因此，您的应用程序可以安装有相同的 CLSID 值相同的 COM 类型的目标计算机上运行。 自动执行 Microsoft Office 的应用程序是一个很好示例。 由于 Office 等应用程序通常在不同版本中保持相同的 CLSID 值，您的应用程序可以使用所引用的 COM 类型，长时间为.NET Framework 4 或更高版本安装在目标计算机上以及你的应用程序使用的方法、 属性或包含在引用的 COM 类型的事件。  
  
 `/link`选项嵌入接口、 结构和委托。 不支持嵌入 COM 类。  
  
> [!NOTE]
>  当在代码中创建嵌入 COM 类型的实例时，必须通过使用适当的接口来创建该实例。 尝试使用组件类创建嵌入 COM 类型的实例会导致错误。  
  
 若要设置`/link`选项[!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]、 添加程序集引用和设置`Embed Interop Types`属性设置为**true**。 默认值为`Embed Interop Types`属性是**false**。  
  
 如果链接 COM 程序集 （程序集 A） 到其本身引用了另一个 COM 程序集 (程序集 B)，您还必须链接到程序集 B 中，如果下列任一条件为真︰  
  
-   程序集 A 中的类型继承自的类型或实现程序集 B 中的接口  
  
-   字段、 属性、 事件或程序集 B 中的返回类型或形参类型的方法被调用。  
  
 使用[/libpath](../../../visual-basic/reference/command-line-compiler/libpath.md)若要指定一个或多个程序集引用所在的目录。  
  
 如[/引用](../../../visual-basic/reference/command-line-compiler/reference.md)编译器选项，则`/link`编译器选项使用频繁地使用引用的 Vbc.rsp 响应文件[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]程序集。 使用[/noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md)编译器选项，如果不希望使用 Vbc.rsp 文件的编译器。  
  
 缩写形式`/link`是`/l`。  
  
## <a name="generics-and-embedded-types"></a>泛型和嵌入的类型  
 以下各节描述在嵌入互操作类型的应用程序中使用泛型类型的限制。  
  
### <a name="generic-interfaces"></a>泛型接口  
 不能使用从互操作程序集中嵌入的泛型接口。 这在下面的示例中显示。  
  
 [!code-vb[VbLinkCompiler #&1;](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/link_1.vb)]  
  
### <a name="types-that-have-generic-parameters"></a>拥有的泛型参数的类型  
 具有其类型嵌入互操作程序集从一个泛型参数类型，如果无法使用该类型为从外部程序集。 此限制不适用于接口。 例如，考虑<xref:Microsoft.Office.Interop.Excel.Range>中定义的接口<xref:Microsoft.Office.Interop.Excel>程序集。</xref:Microsoft.Office.Interop.Excel> </xref:Microsoft.Office.Interop.Excel.Range> 如果库嵌入互操作类型从<xref:Microsoft.Office.Interop.Excel>程序集并返回其类型的泛型类型具有参数的方法是的公开<xref:Microsoft.Office.Interop.Excel.Range>接口，该方法必须返回泛型接口，如下面的代码示例中所示。</xref:Microsoft.Office.Interop.Excel.Range> </xref:Microsoft.Office.Interop.Excel>  
  
 [!code-vb[VbLinkCompiler #&2;](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/link_2.vb)]  
[!code-vb[VbLinkCompiler #&3;](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/link_3.vb)]  
[!code-vb[VbLinkCompiler #&4;](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/link_4.vb)]  
  
 在下面的示例中，客户端代码可以调用该方法返回<xref:System.Collections.IList>泛型接口，但没有错误。</xref:System.Collections.IList>  
  
 [!code-vb[VbLinkCompiler #&5;](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/link_5.vb)]  
  
## <a name="example"></a>示例  
 下面的代码编译源文件`OfficeApp.vb`和引用程序集从`COMData1.dll`和`COMData2.dll`以生成`OfficeApp.exe`。  
  
```vb  
vbc /link:COMData1.dll,COMData2.dll /out:OfficeApp.exe OfficeApp.vb  
```  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 命令行编译器](../../../visual-basic/reference/command-line-compiler/index.md)   
 [演练︰ 嵌入托管程序集中的类型](http://msdn.microsoft.com/library/b28ec92c-1867-4847-95c0-61adfe095e21)   
 [/reference (Visual Basic)](../../../visual-basic/reference/command-line-compiler/reference.md)   
 [/noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md)   
 [/libpath](../../../visual-basic/reference/command-line-compiler/libpath.md)   
 [示例编译命令行](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [COM 互操作介绍](../../../visual-basic/programming-guide/com-interop/introduction-to-com-interop.md)
