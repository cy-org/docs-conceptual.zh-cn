---
title: ".NET Framework 中的泛型"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- generic methods, type inference
- generics [.NET Framework], collections
- generic interfaces [.NET Framework]
- constructed generic types
- nested generic types
- generic type definitions
- generic classes [.NET Framework]
- generics [.NET Framework], interfaces
- generics [.NET Framework], about
- generics [.NET Framework]
- generic collections [.NET Framework]
- generic delegates [.NET Framework]
- generic type arguments
- generics [.NET Framework], delegates
- generics [.NET Framework], features
- constraints [.NET Framework]
- generic types
- generic type parameters
ms.assetid: 2994d786-c5c7-4666-ab23-4c83129fe39c
caps.latest.revision: 23
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: ef0b251add573c7aaed75b866523b5fdcd3d8e5a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/05/2017

---
# <a name="generics-in-the-net-framework"></a>.NET Framework 中的泛型
<a name="top"></a> 泛型使你可将方法、类、结构或界面定制为其所操作的精确数据类型。 例如，不使用允许键和值为任意类型的 <xref:System.Collections.Hashtable> 类，而使用 <xref:System.Collections.Generic.Dictionary%602> 泛型类并指定允许的密钥类型和允许的值的类型。 泛型的优点包括：代码的可重用性增加，类型安全性提高。  
  
 本主题提供对 .NET Framework 中泛型的概述以及泛型类型和方法的摘要。 它包含下列部分：  
  
-   [定义和使用泛型](#defining_and_using_generics)  
  
-   [泛型术语](#generics_terminology)  
  
-   [类库和语言支持](#class_library_and_language_support)  
  
-   [嵌套类型和泛型](#nested_types_and_generics)  
  
-   [相关主题](#related_topics)  
  
-   [参考](#reference)  
  
<a name="defining_and_using_generics"></a>   
## <a name="defining-and-using-generics"></a>定义和使用泛型  
 泛型是为所存储或使用的一个或多个类型具有占位符（类型形参）的类、结构、接口和方法。 泛型集合类可以将类型形参用作其存储的对象类型的占位符；类型形参呈现为其字段的类型和其方法的参数类型。 泛型方法可将其类型形参用作其返回值的类型或用作其形参之一的类型。 以下代码举例说明了一个简单的泛型类定义。  
  
 [!code-cpp[Conceptual.Generics.Overview#2](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.generics.overview/cpp/source.cpp#2)] [!code-csharp[Conceptual.Generics.Overview#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.generics.overview/cs/source.cs#2)] [!code-vb[Conceptual.Generics.Overview#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.generics.overview/vb/source.vb#2)]  
  
 创建泛型类的实例时，指定用于替代类型形参的实际类型。 在类型形参出现的每一处位置用选定的类型进行替代，这会建立一个被称为构造泛型类的新泛型类。 你将得到根据你选择的类型而定制的类型安全类，如以下代码所示。  
  
 [!code-cpp[Conceptual.Generics.Overview#3](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.generics.overview/cpp/source.cpp#3)] [!code-csharp[Conceptual.Generics.Overview#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.generics.overview/cs/source.cs#3)] [!code-vb[Conceptual.Generics.Overview#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.generics.overview/vb/source.vb#3)]  
  
<a name="generics_terminology"></a>   
### <a name="generics-terminology"></a>泛型术语  
 以下术语用于讨论 NET Framework 中的泛型：  
  
-   *泛型类型定义* 是用作模板的类、结构或接口声明，带有可包含或使用的类型的占位符。 例如， <xref:System.Collections.Generic.Dictionary%602?displayProperty=fullName> 类可以包含两种类型：密钥和值。 由于泛型类型定义只是一个模板，所以你无法创建作为泛型类型定义的类、结构或接口的实例。  
  
-   *泛型类型形参*（或 *类型形参*）是泛型类型或方法定义中的占位符。 <xref:System.Collections.Generic.Dictionary%602?displayProperty=fullName> 泛型类型具有两个类型形参 `TKey` 和 `TValue`，它们分别代表密钥和值的类型。  
  
-   *构造泛型类型*（或 *构造类型*）是为泛型类型定义的泛型类型形参指定类型的结果。  
  
-   *泛型类型实参* 是被泛型类型形参所替代的任何类型。  
  
-   一般术语 *泛型类型* 包括构造类型和泛型类型定义。  
  
-   泛型类型形参的*协变* 和 *逆变* of generic type parameters enable you to use constructed generic types whose type arguments are more derived (covariance) or less derived (逆变) than a target constructed type. 协变和逆变统称为“变体”。 有关详细信息，请参阅[协变和逆变](../../../docs/standard/generics/covariance-and-contravariance.md)。  
  
-   *约束* 是对泛型类型形参给予的限制。 例如，你可能会将一个类型形参限制为实现 <xref:System.Collections.Generic.IComparer%601?displayProperty=fullName> 泛型接口的类型，以确保可对该类型的实例进行排序。 此外，你还可以将类型形参限制为具有特定基类、具有默认构造函数或作为引用类型或值类型的类型。 泛型类型的用户不能替换不满足约束条件的类型实参。  
  
-   *泛型方法定义* 是具有两个形参列表的方法：泛型类型形参列表和形参列表。 类型形参可作为返回类型或形参类型出现，如以下代码所示。  
  
 [!code-cpp[Conceptual.Generics.Overview#4](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.generics.overview/cpp/source.cpp#4)] [!code-csharp[Conceptual.Generics.Overview#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.generics.overview/cs/source.cs#4)] [!code-vb[Conceptual.Generics.Overview#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.generics.overview/vb/source.vb#4)]  
  
 泛型方法可出现在泛型或非泛型类型中。 值得注意的是，方法不会仅因为它属于泛型类型或甚至因为它有类型为封闭类型泛型参数的形参而成为泛型方法。 只有当方法有属于自己的类型形参列表时才是泛型方法。 在以下代码中，只有方法 `G` 是泛型方法。  
  
 [!code-cpp[Conceptual.Generics.Overview#5](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.generics.overview/cpp/source.cpp#5)] [!code-csharp[Conceptual.Generics.Overview#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.generics.overview/cs/source.cs#5)] [!code-vb[Conceptual.Generics.Overview#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.generics.overview/vb/source.vb#5)]  
  
 [返回页首](#top)  
  
<a name="advantages_limitations"></a>   
## <a name="advantages-and-disadvantages-of-generics"></a>泛型的利与弊  
 使用泛型集合和委托有很多好处：  
  
-   类型安全。 泛型将类型安全的负担从你那里转移到编译器。 没有必要编写代码来测试正确的数据类型，因为它会在编译时强制执行。 降低了强制类型转换的必要性和运行时错误的可能性。  
  
-   代码更少且可以更轻松地重用代码。 无需从基类型继承，无需重写成员。 例如，可立即使用 <xref:System.Collections.Generic.LinkedList%601> 。 例如，你可以使用下列变量声明来创建字符串的链接列表：  
  
     [!code-cpp[HowToGeneric#24](../../../samples/snippets/cpp/VS_Snippets_CLR/HowToGeneric/cpp/source2.cpp#24)]  [!code-csharp[HowToGeneric#24](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToGeneric/CS/source2.cs#24)]  [!code-vb[HowToGeneric#24](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToGeneric/VB/source2.vb#24)]  
  
-   性能更好。 泛型集合类型通常能更好地存储和操作值类型，因为无需对值类型进行装箱。  
  
-   泛型委托可以在无需创建多个委托类的情况下进行类型安全的回调。 例如， <xref:System.Predicate%601> 泛型委托允许你创建一种为特定类型实现你自己的搜索标准的方法并将你的方法与 <xref:System.Array> 类型比如 <xref:System.Array.Find%2A>、 <xref:System.Array.FindLast%2A>和 <xref:System.Array.FindAll%2A>方法一起使用。  
  
-   泛型简化动态生成的代码。 使用具有动态生成的代码的泛型时，无需生成类型。 这会增加方案数量，在这些方案中你可以使用轻量动态方法而非生成整个程序集。 有关详细信息，请参阅“如何：定义和执行动态方法和 DynamicMethod。”  
  
 以下是泛型的一些局限：  
  
-   泛型类型可从多数基类中派生，如 <xref:System.MarshalByRefObject> （约束可用于要求泛型类型形参派生自诸如 <xref:System.MarshalByRefObject>的基类）。 然而 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 不支持上下文绑定的泛型类型。 泛型类型可派生自 <xref:System.ContextBoundObject>，但尝试创建该类型实例会导致 <xref:System.TypeLoadException>。  
  
-   枚举不能具有泛型类型形参。 枚举偶尔可为泛型（例如，因为它嵌套在被定义使用 Visual Basic、C# 或 C++ 的泛型类型中）。 有关详细信息，请参阅 [Common Type System](../../../docs/standard/base-types/common-type-system.md)中的“枚举”。  
  
-   轻量动态方法不能是泛型。  
  
-   在 Visual Basic、C# 和 C++ 中，包含在泛型类型中的嵌套类型不能被实例化，除非已将类型分配给所有封闭类型的类型形参。 另一种说法是：在反射中，定义使用这些语言的嵌套类型包括其所有封闭类型的类型形参。 这使封闭类型的类型形参可在嵌套类型的成员定义中使用。 有关详细信息，请参阅 <xref:System.Type.MakeGenericType%2A>中的“嵌套类型”。  
  
    > [!NOTE]
    >  通过在动态程序集中触发代码或通过使用 [Ilasm.exe (IL Assembler)](../../../docs/framework/tools/ilasm-exe-il-assembler.md) 定义的嵌套类型不需要包括其封闭类型的类型参数；然而，如果不包括，类型参数就不会在嵌套类的范围内。  
  
     有关详细信息，请参阅 <xref:System.Type.MakeGenericType%2A>中的“嵌套类型”。  
  
 [返回页首](#top)  
  
<a name="class_library_and_language_support"></a>   
## <a name="class-library-and-language-support"></a>类库和语言支持  
 .NET Framework 提供了许多以下命名空间中的泛型集合类：  
  
-   <xref:System.Collections.Generic> 命名空间编录了多数由 .NET Framework 提供的泛型集合类型，如 <xref:System.Collections.Generic.List%601> 和 <xref:System.Collections.Generic.Dictionary%602> 泛型类。  
  
-   <xref:System.Collections.ObjectModel> 命名空间编录了其他泛型集合类型，如 <xref:System.Collections.ObjectModel.ReadOnlyCollection%601> 泛型类，这有助于向你的类中的用户公开对象模型。  
  
 <xref:System> 命名空间提供实现排序和等同性比较的泛型接口，还提供事件处理程序、转换和搜索谓词的泛型委托类型。  
  
 已将对泛型的支持添加到： <xref:System.Reflection> 命名空间（以检查泛型类型和泛型方法）、 <xref:System.Reflection.Emit> （以发出包含泛型类型和方法的动态程序集）和 <xref:System.CodeDom> （以生成包括泛型的源图）。  
  
 公共语言运行时提供了新的操作码和前缀来支持 Microsoft 中间语言 (MSIL) 中的泛型类型，包括 <xref:System.Reflection.Emit.OpCodes.Stelem>、 <xref:System.Reflection.Emit.OpCodes.Ldelem>、 <xref:System.Reflection.Emit.OpCodes.Unbox_Any>、 <xref:System.Reflection.Emit.OpCodes.Constrained>和 <xref:System.Reflection.Emit.OpCodes.Readonly>。  
  
 Visual C++、C# 和 Visual Basic 都对定义和使用泛型提供完全支持。 有关语言支持的详细信息，请参阅 [Visual Basic 中的泛型类型](~/docs/visual-basic/programming-guide/language-features/data-types/generic-types.md)、[泛型简介](~/docs/csharp/programming-guide/generics/introduction-to-generics.md)和 [Visual C++ 中的泛型概述](/cpp/windows/overview-of-generics-in-visual-cpp)。  
  
 [返回页首](#top)  
  
<a name="nested_types_and_generics"></a>   
## <a name="nested-types-and-generics"></a>嵌套类型和泛型  
 嵌套在泛型类型中的类型可取决于封闭泛型类型的类型参数。 公共语言运行时将嵌套类型看作泛型，即使它们不具有自己的泛型类型形参。 创建嵌套类型的实例时，必须指定所有封闭泛型类型的类型实参。  
  
 [返回页首](#top)  
  
<a name="related_topics"></a>   
## <a name="related-topics"></a>相关主题  
  
|标题|说明|  
|-----------|-----------------|  
|[.NET Framework 中的泛型集合](../../../docs/standard/generics/collections.md)|描述 .NET Framework 中的泛型集合类和其他泛型类型。|  
|[用于控制数组和列表的泛型委托](../../../docs/standard/generics/delegates-for-manipulating-arrays-and-lists.md)|描述用于转换、搜索谓词以及要对数组或集合中的元素执行的操作的泛型委托。|  
|[泛型接口](../../../docs/standard/generics/interfaces.md)|描述跨泛型类型系列提供通用功能的泛型接口。|  
|[协变和逆变](../../../docs/standard/generics/covariance-and-contravariance.md)|描述泛型类型实参中的协变和逆变。|  
|[常用的集合类型](../../../docs/standard/collections/commonly-used-collection-types.md)|提供有关 .NET Framework 中集合类型的特征和使用方案的摘要信息，包括泛型类型。|  
|[何时使用泛型集合](../../../docs/standard/collections/when-to-use-generic-collections.md)|描述用于确定何时使用泛型集合类型的一般规则。|  
|[如何：使用 Reflection Emit 定义泛型类型](../../../docs/framework/reflection-and-codedom/how-to-define-a-generic-type-with-reflection-emit.md)|解释如何生成包括泛型类型和方法的动态程序集。|  
|[Generic Types in Visual Basic](~/docs/visual-basic/programming-guide/language-features/data-types/generic-types.md)|为 Visual Basic 用户描述泛型功能，包括有关使用和定义泛型类型的帮助主题。|  
|[泛型介绍](~/docs/csharp/programming-guide/generics/introduction-to-generics.md)|为 C# 用户概述定义和使用泛型类型。|  
|[Visual C++ 中的泛型概述](/cpp/windows/overview-of-generics-in-visual-cpp)|为 C++ 用户描述泛型功能，包括泛型和模板之间的差异。|  
  
<a name="reference"></a>   
## <a name="reference"></a>参考  
 <xref:System.Collections.Generic>  
  
 <xref:System.Collections.ObjectModel>  
  
 <xref:System.Reflection.Emit.OpCodes?displayProperty=fullName>  
  
 [返回页首](#top)

