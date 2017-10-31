---
title: "公共特性 (Visual Basic 中) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 11fe4894-1bf9-4525-a36b-cddcd3a5d22b
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: f470e6ff3e316076d71a34346f741cc4504471a3
ms.lasthandoff: 03/13/2017

---
# <a name="common-attributes-visual-basic"></a>公共特性 (Visual Basic)
本主题介绍在 Visual Basic 程序中最常用的属性。  
  
-   [全局属性](#Global)  
  
-   [已过时的特性](#Obsolete)  
  
-   [条件属性](#Conditional)  
  
-   [调用方信息特性](#CallerInfo)  
  
-   [Visual Basic 特性](#VB)  
  
##  <a name="Global"></a>全局属性  
 大多数属性应用于特定语言元素，如类或方法; 这些方法但是，有些属性是全局 — 它们应用于整个程序集或模块。 例如，<xref:System.Reflection.AssemblyVersionAttribute>属性可用于嵌入到程序集，像这样的版本信息︰</xref:System.Reflection.AssemblyVersionAttribute>  
  
```vb  
<Assembly: AssemblyVersion("1.0.0.0")>  
```  
  
 全局属性在任何后会出现在源代码中顶级`Imports`语句和任何类型、 模块或命名空间声明之前。 全局特性可以出现在多个源文件，但必须在单一编译传递中编译这些文件。 对于 Visual Basic 项目，通常将全局属性放在 AssemblyInfo.vb 文件 （该文件自动创建在 Visual Studio 中创建项目时）。  
  
 程序集特性是提供程序集相关信息的值。 这些内容分为以下类别︰  
  
-   程序集标识属性  
  
-   信息性特性  
  
-   程序集清单特性  
  
### <a name="assembly-identity-attributes"></a>程序集标识特性。  
 三个特性 （还有一个强名称，如果适用） 确定程序集的标识︰ 名称、 版本和区域性。 这些属性构成该程序集的完整名称和时，需要在代码中引用。 您可以设置程序集的版本和使用属性的区域性。 但是，由编译器，Visual Studio IDE 中设置的名称值[程序集信息对话框](https://docs.microsoft.com/visualstudio/ide/reference/assembly-information-dialog-box)，或程序集链接器 (Al.exe) 创建程序集，基于包含程序集清单的文件。 <xref:System.Reflection.AssemblyFlagsAttribute>属性指定的程序集的多个副本可以相互共存。</xref:System.Reflection.AssemblyFlagsAttribute>  
  
 下表显示标识属性。  
  
|特性|目标|  
|---------------|-------------|  
|<xref:System.Reflection.AssemblyName></xref:System.Reflection.AssemblyName>|详细描述程序集的标识。|  
|<xref:System.Reflection.AssemblyVersionAttribute></xref:System.Reflection.AssemblyVersionAttribute>|指定程序集的版本。|  
|<xref:System.Reflection.AssemblyCultureAttribute></xref:System.Reflection.AssemblyCultureAttribute>|指定程序集支持的区域性。|  
|<xref:System.Reflection.AssemblyFlagsAttribute></xref:System.Reflection.AssemblyFlagsAttribute>|指定程序集是否支持在相同的过程中，或在同一应用程序域中的同一计算机上的并行执行。|  
  
### <a name="informational-attributes"></a>信息性特性  
 信息性特性可用于提供程序集的其他公司或产品信息。 下表显示中定义的信息性特性<xref:System.Reflection?displayProperty=fullName>命名空间。</xref:System.Reflection?displayProperty=fullName>  
  
|特性|目标|  
|---------------|-------------|  
|<xref:System.Reflection.AssemblyProductAttribute></xref:System.Reflection.AssemblyProductAttribute>|定义指定程序集清单的产品名称的自定义属性。|  
|<xref:System.Reflection.AssemblyTrademarkAttribute></xref:System.Reflection.AssemblyTrademarkAttribute>|定义一个自定义特性指定为程序集清单的商标。|  
|<xref:System.Reflection.AssemblyInformationalVersionAttribute></xref:System.Reflection.AssemblyInformationalVersionAttribute>|定义指定的程序集清单是信息性版本的自定义属性。|  
|<xref:System.Reflection.AssemblyCompanyAttribute></xref:System.Reflection.AssemblyCompanyAttribute>|定义指定公司名称为程序集清单的自定义属性。|  
|<xref:System.Reflection.AssemblyCopyrightAttribute></xref:System.Reflection.AssemblyCopyrightAttribute>|定义一个自定义特性指定为程序集清单版权。|  
|<xref:System.Reflection.AssemblyFileVersionAttribute></xref:System.Reflection.AssemblyFileVersionAttribute>|指示编译器使用 Win32 文件版本资源特定的版本号。|  
|<xref:System.CLSCompliantAttribute></xref:System.CLSCompliantAttribute>|指示该程序集是否符合公共语言规范 (CLS)。|  
  
### <a name="assembly-manifest-attributes"></a>程序集清单特性  
 程序集清单特性可用于提供程序集清单中的信息。 这包括标题、 说明、 默认别名和配置。 下表显示中定义的程序集清单特性<xref:System.Reflection?displayProperty=fullName>命名空间。</xref:System.Reflection?displayProperty=fullName>  
  
|特性|目标|  
|---------------|-------------|  
|<xref:System.Reflection.AssemblyTitleAttribute></xref:System.Reflection.AssemblyTitleAttribute>|定义指定为程序集清单的程序集标题的自定义属性。|  
|<xref:System.Reflection.AssemblyDescriptionAttribute></xref:System.Reflection.AssemblyDescriptionAttribute>|定义指定程序集清单的程序集描述的自定义属性。|  
|<xref:System.Reflection.AssemblyConfigurationAttribute></xref:System.Reflection.AssemblyConfigurationAttribute>|为程序集清单中定义的指定程序集配置 （如发布或调试） 的自定义属性。|  
|<xref:System.Reflection.AssemblyDefaultAliasAttribute></xref:System.Reflection.AssemblyDefaultAliasAttribute>|定义程序集清单的友好默认别名|  
  
##  <a name="Obsolete"></a>已过时的特性  
 `Obsolete`特性标记为不再推荐使用的一个程序实体。 每个使用标记为已过时的实体随后将生成警告或错误，具体取决于该属性的配置方式。 例如:   
  
```vb  
<System.Obsolete("use class B")>   
Class A  
    Sub Method()  
    End Sub  
End Class  
  
Class B  
    <System.Obsolete("use NewMethod", True)>   
    Sub OldMethod()  
    End Sub  
  
    Sub NewMethod()  
    End Sub  
End Class  
```  
  
 在此示例中`Obsolete`属性应用到类`A`和方法`B.OldMethod`。 因为特性构造函数的第二个参数应用于`B.OldMethod`设置为`true`，此方法将导致编译器错误，而使用类`A`只会产生一条警告。 调用`B.NewMethod`，然而，将生成任何警告或错误。  
  
 作为第一个参数传递给特性构造函数提供的字符串都显示为警告或错误的一部分。 例如，当您使用它前面的定义，下面的代码将生成两个警告和一个错误︰  
  
```vb  
' Generates 2 warnings:  
' Dim a As New A  
' Generate no errors or warnings:  
  
Dim b As New B  
b.NewMethod()  
  
' Generates an error, terminating compilation:  
' b.OldMethod()  
```  
  
 类有两个警告`A`生成︰ 一个用于类引用声明，另一个用于类构造函数。  
  
 `Obsolete`属性可以使用不带参数，但其中的原因包括项已过时，并改为使用哪种建议。  
  
 `Obsolete`属性是一个单用途属性和可以应用于任何允许属性的实体。 `Obsolete`是<xref:System.ObsoleteAttribute>。</xref:System.ObsoleteAttribute>的别名  
  
##  <a name="Conditional"></a>条件属性  
 `Conditional`属性使执行方法依赖于预处理标识符。 `Conditional`属性是其别名<xref:System.Diagnostics.ConditionalAttribute>，并可以应用于方法或属性类</xref:System.Diagnostics.ConditionalAttribute>  
  
 在此示例中，`Conditional`应用于方法，以启用或禁用特定于程序的诊断信息的显示︰  
  
```vb  
#Const TRACE_ON = True  
Imports System  
Imports System.Diagnostics  
Module TestConditionalAttribute  
    Public Class Trace  
        <Conditional("TRACE_ON")>   
        Public Shared Sub Msg(ByVal msg As String)  
            Console.WriteLine(msg)  
        End Sub  
  
    End Class  
  
    Sub Main()  
        Trace.Msg("Now in Main...")  
        Console.WriteLine("Done.")  
    End Sub  
End Module  
```  
  
 如果`TRACE_ON`未定义标识符时，将显示任何跟踪输出。  
  
 `Conditional`属性通常用于`DEBUG`标识符来启用跟踪和日志记录功能，实现 debug，但不是在发布版本，如下所示︰  
  
```vb  
<Conditional("DEBUG")>   
Shared Sub DebugMethod()  
  
End Sub  
```  
  
 当调用一个方法标记为条件时，是包含还是省略该调用会确定存在指定的预处理符号。 如果定义了该符号，则将包括调用;否则，将忽略该调用。 使用`Conditional`是整洁、 为封闭方法中的替代方法更为妥当，并且不容易出错`#if…#endif`块，如下︰  
  
```vb  
#If DEBUG Then  
    Sub ConditionalMethod()  
    End Sub  
#End If  
```  
  
 条件的方法必须是类或结构声明中的方法，而且必须没有返回值。  
  
### <a name="using-multiple-identifiers"></a>使用多个标识符  
 如果某个方法具有多个`Conditional`属性，对方法的调用则将包含定义了至少其中一个条件符号 （换而言之，这些符号在逻辑上连接在一起通过使用或运算符）。 在此示例中，或者是否存在`A`或`B`，则会在方法调用︰  
  
```vb  
<Conditional("A"), Conditional("B")>   
Shared Sub DoIfAorB()  
  
End Sub  
```  
  
 若要实现在逻辑上将符号链接通过与运算符的效果，可以定义序列条件方法。 例如，将执行下面的第二个方法，仅当`A`和`B`定义︰  
  
```vb  
<Conditional("A")>   
Shared Sub DoIfA()  
    DoIfAandB()  
End Sub  
  
<Conditional("B")>   
Shared Sub DoIfAandB()  
    ' Code to execute when both A and B are defined...  
End Sub  
```  
  
### <a name="using-conditional-with-attribute-classes"></a>使用具有特性类的条件  
 `Conditional`特性还可应用于属性类定义。 在此示例中，自定义特性`Documentation`将只将信息添加到元数据如果定义了 DEBUG 时。  
  
```vb  
<Conditional("DEBUG")>   
Public Class Documentation  
    Inherits System.Attribute  
    Private text As String  
    Sub New(ByVal doc_text As String)  
        text = doc_text  
    End Sub  
End Class  
  
Class SampleClass  
    ' This attribute will only be included if DEBUG is defined.  
    <Documentation("This method displays an integer.")>   
    Shared Sub DoWork(ByVal i As Integer)  
        System.Console.WriteLine(i)  
    End Sub  
End Class  
```  
  
##  <a name="CallerInfo"></a>调用方信息特性  
 通过使用调用方信息特性，可获取有关方法的调用方的信息。 您可以获取源代码的文件路径、 源代码和调用方的成员名称中的行号。  
  
 若要获取成员调用方信息，您可以使用应用于可选参数的属性。 每个可选参数指定默认值。 下表列出了在中定义的调用方信息特性<xref:System.Runtime.CompilerServices?displayProperty=fullName>命名空间︰</xref:System.Runtime.CompilerServices?displayProperty=fullName>  
  
|特性|描述|类型|  
|---|---|---|  
|<xref:System.Runtime.CompilerServices.CallerFilePathAttribute></xref:System.Runtime.CompilerServices.CallerFilePathAttribute>|包含调用方的源文件的完整路径。 这是在编译时的路径。|`String`|  
|<xref:System.Runtime.CompilerServices.CallerLineNumberAttribute></xref:System.Runtime.CompilerServices.CallerLineNumberAttribute>|从中调用该方法的源文件中的行号。|`Integer`|  
|<xref:System.Runtime.CompilerServices.CallerMemberNameAttribute></xref:System.Runtime.CompilerServices.CallerMemberNameAttribute>|方法名称或调用方的属性名称。 有关详细信息，请参阅[调用方信息 (Visual Basic 中)](../../../../visual-basic/programming-guide/concepts/caller-information.md)。|`String`|  
  
 有关调用方信息特性的详细信息，请参阅[调用方信息 (Visual Basic 中)](../../../../visual-basic/programming-guide/concepts/caller-information.md)。  
  
##  <a name="VB"></a>Visual Basic 特性  
 下表列出了 Visual Basic 特有的属性。  
  
|特性|目标|  
|---------------|-------------|  
|<xref:Microsoft.VisualBasic.ComClassAttribute></xref:Microsoft.VisualBasic.ComClassAttribute>|向编译器指示应将此类公开为 COM 对象。|  
|<xref:Microsoft.VisualBasic.HideModuleNameAttribute></xref:Microsoft.VisualBasic.HideModuleNameAttribute>|允许使用所需的模块限定访问模块成员。|  
|<xref:Microsoft.VisualBasic.VBFixedStringAttribute></xref:Microsoft.VisualBasic.VBFixedStringAttribute>|与文件输入和输出指定一个固定长度的字符串的大小用于结构中的函数。|  
|<xref:Microsoft.VisualBasic.VBFixedArrayAttribute></xref:Microsoft.VisualBasic.VBFixedArrayAttribute>|使用输入和输出文件指定用于结构中的固定数组的大小的函数。|  
  
### <a name="comclassattribute"></a>COMClassAttribute  
 使用`COMClassAttribute`来简化从 Visual Basic 创建 COM 组件的过程。 COM 对象是从.NET Framework 程序集，而有很大差异`COMClassAttribute`，你需要遵循的步骤，在 Visual Basic 中生成一个 COM 对象数。 为类标记为`COMClassAttribute`，编译器会自动执行其中很多步骤。  
  
### <a name="hidemodulenameattribute"></a>HideModuleNameAttribute  
 使用`HideModuleNameAttribute`以允许访问通过使用所需的模块限定模块成员。  
  
### <a name="vbfixedstringattribute"></a>VBFixedStringAttribute  
 使用`VBFixedStringAttribute`强制 Visual Basic 中创建一个固定长度的字符串。 字符串的变量长度在默认情况下，并且此特性将字符串存储到文件时很有用。 下面的代码演示这一︰  
  
```vb  
Structure Worker  
    ' The runtime uses VBFixedString to determine   
    ' if the field should be written out as a fixed size.  
    <VBFixedString(10)> Public LastName As String  
    <VBFixedString(7)> Public Title As String  
    <VBFixedString(2)> Public Rank As String  
End Structure  
```  
  
### <a name="vbfixedarrayattribute"></a>VBFixedArrayAttribute  
 使用`VBFixedArrayAttribute`声明固定大小的数组。 Visual Basic 像字符串一样，数组是默认情况下的可变长度。 此属性是在序列化或数据写入文件时很有用。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Reflection></xref:System.Reflection>   
 <xref:System.Attribute></xref:System.Attribute>   
 [Visual Basic 编程指南](../../../../visual-basic/programming-guide/index.md)   
 [属性](https://msdn.microsoft.com/library/5x6cd29c)   
 [反射 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/reflection.md)   
 [使用反射 (Visual Basic 中) 访问特性](../../../../visual-basic/programming-guide/concepts/attributes/accessing-attributes-by-using-reflection.md)
