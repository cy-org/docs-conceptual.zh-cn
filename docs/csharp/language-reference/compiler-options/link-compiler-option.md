---
title: "-link（C# 编译器选项）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- /l compiler option [C#]
- /link compiler option [C#]
- -l compiler option [C#]
- EmbedInteropTypes
- l compiler option [C#]
- embed interop types [COM Interop]
- -link compiler option [C#]
- link compiler option [C#]
ms.assetid: 00da70c6-9ea1-43c2-86f2-aa7f26c03475
caps.latest.revision: 13
author: BillWagner
ms.author: wiwagn
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
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: c08f2e7f13a51fb1a350acadff5224cfa8d61aaa
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="link-c-compiler-options"></a>/link（C# 编译器选项）
使编译器让指定程序集中的 COM 类型信息可供当前正在编译的项目使用。  
  
## <a name="syntax"></a>语法  
  
```console  
/link:fileList  
// -or-  
/l:fileList  
```  
  
## <a name="arguments"></a>参数  
 `fileList`  
 必需。 程序集文件名的逗号分隔列表。 如果文件名包含空格，则将名称括在引号内。  
  
## <a name="remarks"></a>备注  
 `/link` 选项使你可以部署具有嵌入类型信息的应用程序。 应用程序随后可以使用运行时程序集中实现嵌入类型信息的类型，而无需引用运行时程序集。 如果发布了各种版本的运行时程序集，则包含嵌入类型信息的应用程序可以使用各种版本，而无需重新编译。 有关示例，请参阅[演练：嵌入托管程序集中的类型](http://msdn.microsoft.com/library/b28ec92c-1867-4847-95c0-61adfe095e21)。  
  
 在使用 COM 互操作时，使用 `/link` 选项会尤其有用。 可以嵌入 COM 类型，以便应用程序在目标计算机上不再需要主互操作程序集 (PIA)。 `/link` 选项指示编译器将引用的互操作程序集中的 COM 类型信息嵌入到生成的已编译代码中。 COM 类型由 CLSID (GUID) 值进行标识。 因此，应用程序可以在安装了具有相同 CLSID 值的相同 COM 类型的目标计算机上运行。 自动执行 Microsoft Office 的应用程序是一个很好的示例。 由于 Office 等应用程序通常在不同版本间保持相同的 CLSID 值，因此只要在目标计算机上安装了 .NET Framework 4 或更高版本，并且应用程序使用引用的 COM 类型中包含的方法、属性或事件，应用程序便可以使用引用的 COM 类型。  
  
 `/link` 选项只嵌入接口、结构和委托。 不支持嵌入 COM 类。  
  
> [!NOTE]
>  在代码中创建嵌入 COM 类型的实例时，必须使用适当的接口创建该实例。 尝试使用组件类创建嵌入 COM 类型的实例会导致错误。  
  
 若要在 [!INCLUDE[vsprvs](~/includes/vsprvs-md.md)] 中设置 `/link` 选项，请添加程序集引用并将 `Embed Interop Types` 属性设置为 **true**。 `Embed Interop Types` 属性的默认值为 **false**。  
  
 如果链接到本身引用了其他 COM 程序集（程序集 B）的 COM 程序集（程序集 A），则在满足以下任一条件时，还必须链接到程序集 B：  
  
-   程序集 A 中的类型继承自程序集 B 中的类型或实现程序集 B 中的接口。  
  
-   调用具有程序集 B 中的返回类型或参数类型的字段、属性、事件或方法。  
  
 与 [/reference](../../../csharp/language-reference/compiler-options/reference-compiler-option.md) 编译器选项一样，`/link` 编译器选项使用 Csc.rsp 响应文件，该文件引用常用的 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] 程序集。 如果不希望编译器使用 Csc.rsp 文件，则使用 [/noconfig](../../../csharp/language-reference/compiler-options/noconfig-compiler-option.md) 编译器选项。  
  
 `/link` 的缩写形式是 `/l`。  
  
## <a name="generics-and-embedded-types"></a>泛型类型和嵌入类型  
 以下各部分介绍对在嵌入互操作类型的应用程序中使用泛型类型的限制。  
  
### <a name="generic-interfaces"></a>泛型接口  
 不能使用从互操作程序集中嵌入的泛型接口。 这在下面的示例中显示。  
  
 [!code-cs[VbLinkCompilerCS#1](../../../csharp/language-reference/compiler-options/codesnippet/CSharp/link-compiler-option_1.cs)]  
  
### <a name="types-that-have-generic-parameters"></a>具有泛型参数的类型  
 对于具有类型是从互操作程序集嵌入的泛型参数的类型，如果该类型来自外部程序集，则无法使用这种类型。 此限制不适用于接口。 例如，考虑在 <xref:Microsoft.Office.Interop.Excel> 程序集中定义的 <xref:Microsoft.Office.Interop.Excel.Range> 接口。 如果某个库从 <xref:Microsoft.Office.Interop.Excel> 程序集嵌入互操作类型，并且公开的一个方法返回具有类型是 <xref:Microsoft.Office.Interop.Excel.Range> 接口的参数的泛型类型，则该方法必须返回泛型接口，如下面的代码示例所示。  
  
 [!code-cs[VbLinkCompilerCS#2](../../../csharp/language-reference/compiler-options/codesnippet/CSharp/link-compiler-option_2.cs)]  
[!code-cs[VbLinkCompilerCS#3](../../../csharp/language-reference/compiler-options/codesnippet/CSharp/link-compiler-option_3.cs)]  
[!code-cs[VbLinkCompilerCS#4](../../../csharp/language-reference/compiler-options/codesnippet/CSharp/link-compiler-option_4.cs)]  
  
 在下面的示例中，客户端代码可以调用返回 <xref:System.Collections.IList> 泛型接口的方法而不会出现错误。  
  
 [!code-cs[VbLinkCompilerCS#5](../../../csharp/language-reference/compiler-options/codesnippet/CSharp/link-compiler-option_5.cs)]  
  
## <a name="example"></a>示例  
 下面的代码编译源文件 `OfficeApp.cs` 并引用来自 `COMData1.dll` 和 `COMData2.dll` 的程序集以生成 `OfficeApp.exe`。  
  
```csharp  
csc /link:COMData1.dll,COMData2.dll /out:OfficeApp.exe OfficeApp.cs  
```  
  
## <a name="see-also"></a>请参阅  
 [（C# 编译器选项）](../../../csharp/language-reference/compiler-options/index.md)   
 [演练：嵌入托管程序集中的类型](http://msdn.microsoft.com/library/b28ec92c-1867-4847-95c0-61adfe095e21)   
 [/reference（C# 编译器选项）](../../../csharp/language-reference/compiler-options/reference-compiler-option.md)   
 [/noconfig (C# 编译器选项)](../../../csharp/language-reference/compiler-options/noconfig-compiler-option.md)   
 [在命令行上使用 csc.exe 生成](../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)   
 [互操作性概述](../../../csharp/programming-guide/interop/interoperability-overview.md)

