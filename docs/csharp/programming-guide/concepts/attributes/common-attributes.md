---
title: "通用属性 (C#)"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 785a0526-6c0e-4599-8c61-ccdc88dd9965
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 98bb21ef0b5582202578b72fd6eaf459801747cc
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="common-attributes-c"></a>通用属性 (C#)
本主题介绍在 C# 程序中最常用的属性。  
  
-   [全局特性](#Global)  
  
-   [Obsolete 特性](#Obsolete)  
  
-   [Conditional 特性](#Conditional)  
  
-   [调用方信息特性](#CallerInfo)  
  
##  <a name="Global"></a> 全局特性  
 大多数特性应用于特定语言元素，如类或方法；但是，一些特性是全局特性 - 它们应用于整个程序集或模块。 例如，<xref:System.Reflection.AssemblyVersionAttribute> 属性可用于将版本信息嵌入程序集，如下所示：  
  
```csharp  
[assembly: AssemblyVersion("1.0.0.0")]  
```  
  
 全局特性出现在源代码中任何顶级 `using` 指令之后和任何类型、模块或命名空间声明之前。 全局特性可以出现在多个源文件中，但必须在单个编译过程中编译这些文件。 在 C# 项目中，全局特性放在 AssemblyInfo.cs 文件中。  
  
 程序集特性是提供程序集相关信息的值。 它们分为以下几类：  
  
-   程序集标识特性  
  
-   信息性特性  
  
-   程序集清单特性  
  
### <a name="assembly-identity-attributes"></a>程序集标识特性。  
 三个特性（与强名称（如果适用））组合起来可以确定程序集的标识：名称、版本和区域性。 这些特性构成程序集的全名，在代码中引用程序集时必需使用。 可使用特性设置程序集的版本和区域性。 但是，创建程序集时，根据包含程序集清单的文件，由编译器、[程序集信息对话框](/visualstudio/ide/reference/assembly-information-dialog-box)中的 Visual Studio IDE 或程序集链接器 (Al.exe) 设置名称值。 <xref:System.Reflection.AssemblyFlagsAttribute> 属性指定程序集的多个副本是否可以共存。  
  
 下表显示标识特性。  
  
|特性|目标|  
|---------------|-------------|  
|<xref:System.Reflection.AssemblyName>|详细描述程序集的标识。|  
|<xref:System.Reflection.AssemblyVersionAttribute>|指定程序集的版本。|  
|<xref:System.Reflection.AssemblyCultureAttribute>|指定程序集支持的区域性。|  
|<xref:System.Reflection.AssemblyFlagsAttribute>|指定程序集是否支持在同一计算机上、同一进程中或同一应用程序域中并行执行。|  
  
### <a name="informational-attributes"></a>信息性特性  
 信息性特性可用于提供程序集的其他公司或产品信息。 下表显示 <xref:System.Reflection?displayProperty=fullName> 命名空间中定义的信息性属性。  
  
|特性|目标|  
|---------------|-------------|  
|<xref:System.Reflection.AssemblyProductAttribute>|定义为程序集清单指定产品名称的自定义属性。|  
|<xref:System.Reflection.AssemblyTrademarkAttribute>|定义为程序集清单指定商标的自定义属性。|  
|<xref:System.Reflection.AssemblyInformationalVersionAttribute>|定义为程序集清单指定信息性版本的自定义属性。|  
|<xref:System.Reflection.AssemblyCompanyAttribute>|定义为程序集清单指定公司名称的自定义属性。|  
|<xref:System.Reflection.AssemblyCopyrightAttribute>|定义为程序集清单指定版权的自定义属性。|  
|<xref:System.Reflection.AssemblyFileVersionAttribute>|指示编译器使用 Win32 文件版本资源的特定版本号。|  
|<xref:System.CLSCompliantAttribute>|指示程序集是否符合公共语言规范 (CLS)。|  
  
### <a name="assembly-manifest-attributes"></a>程序集清单特性  
 程序集清单特性可用于提供程序集清单中的信息。 这些信息包括标题、说明、默认别名和配置。 下表显示 <xref:System.Reflection?displayProperty=fullName> 命名空间中定义的程序集清单属性。  
  
|特性|目标|  
|---------------|-------------|  
|<xref:System.Reflection.AssemblyTitleAttribute>|定义为程序集清单指定程序集标题的自定义属性。|  
|<xref:System.Reflection.AssemblyDescriptionAttribute>|定义为程序集清单指定程序集说明的自定义属性。|  
|<xref:System.Reflection.AssemblyConfigurationAttribute>|定义为程序集清单指定程序集配置（如零售或调试）的自定义属性。|  
|<xref:System.Reflection.AssemblyDefaultAliasAttribute>|定义程序集清单的友好默认别名|  
  
##  <a name="Obsolete"></a> Obsolete 特性  
 `Obsolete` 特性将程序实体标记为不再推荐使用。 每次使用标记为过时的实体后，将生成警告或错误，具体取决于该特性的配置方式。 例如：  
  
```csharp  
[System.Obsolete("use class B")]  
class A  
{  
    public void Method() { }  
}  
class B  
{  
    [System.Obsolete("use NewMethod", true)]  
    public void OldMethod() { }  
    public void NewMethod() { }  
}  
```  
  
 在此示例中，`Obsolete` 特性应用于类 `A` 和方法 `B.OldMethod`。 因为应用于 `B.OldMethod` 的特性构造函数的第二个参数设置为 `true`，所以此方法将导致编译器错误，而使用类 `A` 只会生成警告。 但是，调用 `B.NewMethod` 不会生成任何警告或错误。  
  
 作为特性构造函数的第一个参数提供的字符串将作为警告或错误的一部分显示。 例如，将其与先前的定义一起使用时，以下代码会生成两个警告和一个错误：  
  
```csharp  
// Generates 2 warnings:  
// A a = new A();  
  
// Generate no errors or warnings:  
B b = new B();  
b.NewMethod();  
  
// Generates an error, terminating compilation:  
// b.OldMethod();  
```  
  
 将生成类 `A` 的两个警告：一个用于声明类引用，另一个用于类构造函数。  
  
 `Obsolete` 特性可以在不带参数的情况下使用，但建议包括说明项目过时的原因以及改为使用哪个项目。  
  
 `Obsolete` 特性是一次性特性，可以应用于任何允许特性的实体。 `Obsolete` 是 <xref:System.ObsoleteAttribute> 的别名。  
  
##  <a name="Conditional"></a> Conditional 特性  
 `Conditional` 特性使得方法执行依赖于预处理标识符。 `Conditional` 属性是 <xref:System.Diagnostics.ConditionalAttribute> 的别名，可以应用于方法或特性类。  
  
 在此示例中，`Conditional` 应用于启用或禁用显示特定于程序的诊断信息的方法：  
  
```csharp  
#define TRACE_ON  
using System;  
using System.Diagnostics;  
  
public class Trace  
{  
    [Conditional("TRACE_ON")]  
    public static void Msg(string msg)  
    {  
        Console.WriteLine(msg);  
    }  
}  
  
public class ProgramClass  
{  
    static void Main()  
    {  
        Trace.Msg("Now in Main...");  
        Console.WriteLine("Done.");  
    }  
}  
```  
  
 如果未定义 `TRACE_ON` 标识符，则不会显示任何跟踪输出。  
  
 `Conditional` 特性通常与 `DEBUG` 标识符一起使用，以启用调试生成（而非发布生成）中的跟踪和日志记录功能，如下所示：  
  
```csharp  
[Conditional("DEBUG")]  
static void DebugMethod()  
{  
}  
```  
  
 当调用标记为 conditional 的方法时，指定的预处理符号是否存在将决定包括还是省略该调用。 如果定义了符号，则将包括调用；否则，将忽略该调用。 使用 `Conditional` 是将方法封闭在 `#if…#endif` 块内的更简洁且较不容易出错的替代方法，如下所示：  
  
```csharp  
#if DEBUG  
    void ConditionalMethod()  
    {  
    }  
#endif  
```  
  
 条件方法必须是类或结构声明中的方法，而且必须没有返回值。  
  
### <a name="using-multiple-identifiers"></a>使用多个标识符  
 如果某个方法具有多个 `Conditional` 特性，则如果至少定义了其中一个条件符号（换言之，通过使用 OR 运算符将这些符号逻辑链接在一起），则包含对该方法的调用。 在此示例中，存在 `A` 或 `B` 将导致方法调用：  
  
```csharp  
[Conditional("A"), Conditional("B")]  
static void DoIfAorB()  
{  
    // ...  
}  
```  
  
 若要使用 AND 运算符实现逻辑链接符号的效果，可以定义串行条件方法。 例如，仅当同时定义了 `A` 和 `B` 时才会执行下面的第二个方法：  
  
```csharp
[Conditional("A")]  
static void DoIfA()  
{  
    DoIfAandB();  
}  
  
[Conditional("B")]  
static void DoIfAandB()  
{  
    // Code to execute when both A and B are defined...  
}  
```  
  
### <a name="using-conditional-with-attribute-classes"></a>将 Conditional 用于特性类  
 `Conditional` 特性还可应用于特性类定义。 在本示例中，如果定义了 DEBUG，则自定义属性 `Documentation` 将仅向元数据添加信息。  
  
```csharp  
[Conditional("DEBUG")]  
public class Documentation : System.Attribute  
{  
    string text;  
  
    public Documentation(string text)  
    {  
        this.text = text;  
    }  
}  
  
class SampleClass  
{  
    // This attribute will only be included if DEBUG is defined.  
    [Documentation("This method displays an integer.")]  
    static void DoWork(int i)  
    {  
        System.Console.WriteLine(i.ToString());  
    }  
}  
```  
  
##  <a name="CallerInfo"></a>调用方信息特性  
 通过使用调用方信息特性，可获取有关方法的调用方的信息。 可以获取源代码的文件路径、源代码中的行号和调用方的成员名称。  
  
 若要获取成员调用方信息，可以使用应用于可选参数的特性。 每个可选参数指定一个默认值。 下表列出在 <xref:System.Runtime.CompilerServices?displayProperty=fullName> 命名空间中定义的调用方信息特性：  
  
|特性|描述|类型|  
|---|---|---|  
|<xref:System.Runtime.CompilerServices.CallerFilePathAttribute>|包含调用方的源文件的完整路径。 这是编译时的路径。|`String`|  
|<xref:System.Runtime.CompilerServices.CallerLineNumberAttribute>|源文件中调用方法的行号。|`Integer`|  
|<xref:System.Runtime.CompilerServices.CallerMemberNameAttribute>|调用方的方法名称或属性名称。 有关详细信息，请参阅[调用方信息 (C#)](../../../../csharp/programming-guide/concepts/caller-information.md)。|`String`|  
  
 有关调用方信息特性的详细信息，请参阅[调用方信息 (C#)](../../../../csharp/programming-guide/concepts/caller-information.md)。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Reflection>   
 <xref:System.Attribute>   
 [C# 编程指南](../../../../csharp/programming-guide/index.md)   
 [特性](https://msdn.microsoft.com/library/5x6cd29c)   
 [反射 (C#)](../../../../csharp/programming-guide/concepts/reflection.md)   
 [使用反射访问特性 (C#)](../../../../csharp/programming-guide/concepts/attributes/accessing-attributes-by-using-reflection.md)

