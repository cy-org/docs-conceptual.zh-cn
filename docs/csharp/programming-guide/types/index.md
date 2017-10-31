---
title: "类型（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- value types [C#]
- reference types [C#]
- types [C#]
- C# language, data types
- common type system [C#]
- data types [C#]
- C# language, types
- strong typing [C#]
ms.assetid: f782d7cc-035e-4500-b1b1-36a9881130ad
caps.latest.revision: 53
author: BillWagner
ms.author: wiwagn
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
ms.translationtype: HT
ms.sourcegitcommit: 81117b1419c2a9c3babd6a7429052e2b23e08a70
ms.openlocfilehash: d5dfee413f459c5b38b30ac9116d73e828f3aa17
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="types-c-programming-guide"></a>类型（C# 编程指南）
## <a name="types-variables-and-values"></a>类型、变量和值  
 C# 是一种强类型语言。 每个变量和常量都有一个类型，每个求值的表达式也是如此。 每个方法签名指定了每个输入参数和返回值的类型。 .NET Framework 类库定义了一组内置数值类型以及表示各种逻辑构造的更复杂类型（如文件系统、网络连接、对象的集合和数组以及日期）。 典型的 C# 程序使用类库中的类型，以及对程序问题域的专属概念进行建模的用户定义类型。  
  
 类型中可存储以下信息：  
  
-   类型变量所需的存储空间。  
  
-   可以表示的最大值和最小值。  
  
-   包含的成员（方法、字段、事件等）。  
  
-   继承自的基类型。  
  
-   在运行时分配变量内存的位置。  
  
-   允许执行的运算种类。  
  
 编译器使用类型信息来确保在代码中执行的所有操作都是*类型安全*。 例如，如果声明 [int](../../../csharp/language-reference/keywords/int.md) 类型的变量，那么编译器允许在加法和减法运算中使用此变量。 如果尝试对 [bool](../../../csharp/language-reference/keywords/bool.md) 类型的变量执行这些相同操作，则编译器将生成错误，如以下示例所示：  
  
 [!code-cs[csProgGuideTypes#42](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/index_1.cs)]  
  
> [!NOTE]
>  C 和 C++ 开发人员请注意，在 C# 中，[bool](../../../csharp/language-reference/keywords/bool.md) 不能转换为 [int](../../../csharp/language-reference/keywords/int.md)。  
  
 编译器将类型信息作为元数据嵌入可执行文件中。 公共语言运行时 (CLR) 在运行时使用相应的元数据，从而在分配和回收内存时进一步保证类型安全性。  
  
### <a name="specifying-types-in-variable-declarations"></a>在变量声明中指定类型  
 在程序中声明变量或常量时，必须指定其类型，或使用 [var](../../../csharp/language-reference/keywords/var.md) 关键字，以便编译器能够推断出其类型。 以下示例显示了一些使用内置数值类型和复杂用户定义类型的变量声明：  
  
 [!code-cs[csProgGuideTypes#36](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/index_2.cs)]  
  
 方法签名指定方法参数的类型和返回值。 以下签名显示了需要 [int](../../../csharp/language-reference/keywords/int.md) 作为输入参数并返回字符串的方法：  
  
 [!code-cs[csProgGuideTypes#35](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/index_3.cs)]  
  
 在声明变量后，不能使用新类型重新声明该变量，并且不能为其分配与其声明的类型不兼容的值。 例如，不能在声明 [int](../../../csharp/language-reference/keywords/int.md) 后向其赋值 [true](../../../csharp/language-reference/keywords/true-literal.md) 布尔值。 不过，可以将值转换成其他类型。例如，在将值赋给新变量或作为方法自变量传递时。 编译器会自动执行不会导致数据丢失的*类型转换*。 如果类型转换可能会导致数据丢失，必须在源代码中进行*显式转换*。  
  
 有关详细信息，请参阅[显式转换和类型转换](../../../csharp/programming-guide/types/casting-and-type-conversions.md)。  
  
## <a name="built-in-types"></a>内置类型  
 C# 提供了一组标准的内置数值类型来表示整数、浮点值、布尔表达式、文本字符、十进制值和其他类型数据。 还有内置的 `string` 和 `object` 类型。 这些类型可供在任何 C# 程序中使用。 有关内置类型的详细信息，请参阅[类型参考表](../../../csharp/language-reference/keywords/reference-tables-for-types.md)。  
  
## <a name="custom-types"></a>自定义类型  
 可以使用[结构](../../../csharp/language-reference/keywords/struct.md)、[类](../../../csharp/language-reference/keywords/class.md)、[接口](../../../csharp/language-reference/keywords/interface.md)和[枚举](../../../csharp/language-reference/keywords/enum.md)构造来创建你自己的自定义类型。 .NET Framework 类库本身就是 Microsoft 提供的一组自定义类型，以供你在自己的应用程序中使用。 默认情况下，类库中最常用的类型在任何 C# 程序中均可用。 对于其他类型，只有在显式添加对定义这些类型的程序集的项目引用时才可用。 在编译器获取对程序集的引用后，便可以在源代码中声明在此程序集中声明的类型的变量（和常量）。 有关详细信息，请参阅 [.NET Framework 类库](http://go.microsoft.com/fwlink/?LinkID=217856)。  
  
## <a name="the-common-type-system"></a>通用类型系统  
 对于 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] 中的类型系统，请务必了解以下两个基本要点：  
  
-   支持继承原则。 类型可以派生自其他类型（称为*基类型*）。 派生类型继承（有一些限制）基类型的方法、属性和其他成员。 基类型可以转而派生自其他某种类型，在这种情况下，派生类型可以继承其继承层次结构中两个基类型的成员。 所有类型（包括 <xref:System.Int32?displayProperty=nameWithType>C# 关键字：[int](../../../csharp/language-reference/keywords/int.md)等内置数值类型）最终都派生自单个基类型，即 <xref:System.Object?displayProperty=nameWithType>（C# 关键字：[object](../../../csharp/language-reference/keywords/object.md)。 这样的统一类型层次结构称为[通用类型系统](../../../standard/base-types/common-type-system.md) (CTS)。 若要详细了解 C# 中的继承，请参阅[继承](../../../csharp/programming-guide/classes-and-structs/inheritance.md)。  
  
-   CTS 中的每种类型被定义为值类型或引用类型。 这包括 .NET Framework 类库中的所有自定义类型以及你自己的用户定义类型。 使用 [struct](../../../csharp/language-reference/keywords/struct.md) 关键字定义的类型是值类型；所有内置数值类型都是 `structs`。 使用 [class](../../../csharp/language-reference/keywords/class.md) 关键字定义的类型是引用类型。 引用类型和值类型遵循不同的编译时规则和运行时行为。  
  
 下图展示了 CTS 中值类型和引用类型之间的关系。  
  
 ![值类型和引用类型](../../../csharp/programming-guide/types/media/valuetypescts.png "ValueTypesCTS")  
CTS 中的值类型和引用类型  
  
> [!NOTE]
>  你可能会发现，最常用的类型全都被整理到了 <xref:System> 命名空间中。 不过，包含类型的命名空间与类型是值类型还是引用类型没有关系。  
  
### <a name="value-types"></a>值类型  
 值类型派生自<xref:System.ValueType?displayProperty=nameWithType>（派生自 <xref:System.Object?displayProperty=nameWithType>）。 派生自 <xref:System.ValueType?displayProperty=nameWithType> 的类型在 CLR 中具有特殊行为。 值类型变量直接包含值。也就是说，内存在声明变量的任何上下文中进行内联分配。 对于值类型变量，没有单独的堆分配或垃圾回收开销。  
  
 值类型分为两类：[结构](../../../csharp/language-reference/keywords/struct.md)和[枚举](../../../csharp/language-reference/keywords/enum.md)。  
  
 内置数值类型是结构，包含可以访问的属性和方法：  
  
```csharp  
// Static method on type Byte.  
byte b = Byte.MaxValue;  
```  
  
 不过，可以声明数值类型并向其赋值，就像它们是简单的非聚合类型一样：  
  
```csharp  
byte num = 0xA;  
int i = 5;  
char c = 'Z';  
```  
  
 例如，值类型为“密封”，这意味着不能从 <xref:System.Int32?displayProperty=nameWithType> 派生类型，并且不能将结构定义为从任何用户定义的类或结构继承，因为结构只能从 <xref:System.ValueType?displayProperty=nameWithType> 继承。 但是，一个结构可以实现一个或多个接口。 可以将结构类型显式转换成接口类型；这就触发了*装箱*操作，将结构包装在托管堆上的引用类型对象内。 当将值类型传递到接受 <xref:System.Object?displayProperty=nameWithType> 作为输入参数的方法时，将发生装箱操作。 有关详细信息，请参阅[装箱和取消装箱](../../../csharp/programming-guide/types/boxing-and-unboxing.md)。  
  
 使用 [struct](../../../csharp/language-reference/keywords/struct.md) 关键字可以创建你自己的自定义值类型。 结构通常用作一小组相关变量的容器，如以下示例所示：  
  
 [!code-cs[csProgGuideObjects#1](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/index_4.cs)]  
  
 有关结构的详细信息，请参阅[结构](../../../csharp/programming-guide/classes-and-structs/structs.md)。 若要详细了解 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] 中的值类型，请参阅[通用类型系统](../../../standard/base-types/common-type-system.md)。  
  
 另一种值类型是[枚举](../../../csharp/language-reference/keywords/enum.md)。 枚举定义的是一组已命名的整型常量。 例如，.NET Framework 类库中的 <xref:System.IO.FileMode?displayProperty=nameWithType> 枚举包含一组已命名的常量整数，用于指定应采用的文件打开方式。 下面的示例展示了具体定义：  
 
 [!code-cs[csProgGuideTypes#44](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/index_5.cs)]  
  
 `System.IO.FileMode.Create` 常量的值为 2。 不过，名称对于阅读源代码的人来说更有意义，因此，最好使用枚举，而不是常量数字文本。 有关详细信息，请参阅<xref:System.IO.FileMode?displayProperty=nameWithType>。  
  
 所有枚举从 <xref:System.Enum?displayProperty=nameWithType>（继承自 <xref:System.ValueType?displayProperty=nameWithType>）继承。 适用于结构的所有规则也适用于枚举。 有关枚举的详细信息，请参阅[枚举类型](../../../csharp/programming-guide/enumeration-types.md)。  
  
### <a name="reference-types"></a>引用类型  
 定义为[类](../../../csharp/language-reference/keywords/class.md)、[委托](../../../csharp/language-reference/keywords/delegate.md)、数组或[接口](../../../csharp/language-reference/keywords/interface.md)的类型是*引用类型*。 在运行时，当声明引用类型的变量时，该变量会一直包含值 [null](../../../csharp/language-reference/keywords/null.md)，直至使用 [new](../../../csharp/language-reference/keywords/new.md) 运算符显式创建对象的实例，或者为该变量分配已经在其他位置使用 `new` 创建的对象，如下所示：
  
```csharp  
MyClass mc = new MyClass();  
MyClass mc2 = mc;  
```  
   接口必须与实现它的类对象一起初始化。 如果 `MyClass` 实现 `IMyInterface`，则按以下示例所示创建 `IMyInterface` 的实例：  
  
```csharp  
IMyInterface iface = new MyClass();  
```  
  
 创建对象后，内存会在托管堆上进行分配，并且变量只保留对对象位置的引用。 对于托管堆上的类型，在分配内存和 CLR 自动内存管理功能（称为“*垃圾回收*”）回收内存时都会产生开销。 不过，垃圾回收功能也已经过高度优化，大多数情况下，都不会导致性能问题出现。 有关垃圾回收的详细信息，请参阅[自动内存管理](../../../standard/automatic-memory-management.md)。  
  
 所有数组都是引用类型，即使元素是值类型，也不例外。 虽然数组隐式派生自 <xref:System.Array?displayProperty=nameWithType> 类，但可以使用 C# 提供的简化语法声明和使用数组，如以下示例所示：  
  
 [!code-cs[csProgGuideTypes#45](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/index_6.cs)]  
  
 引用类型完全支持继承。 创建类时，可以继承自其他任何未定义为[密封](../../../csharp/language-reference/keywords/sealed.md)的接口或类，而其他类也可以继承自你的类并重写你的虚方法。 若要详细了解如何创建你自己的类，请参阅[类和结构](../../../csharp/programming-guide/classes-and-structs/index.md)。 有关继承和虚方法的详细信息，请参阅[继承](../../../csharp/programming-guide/classes-and-structs/inheritance.md)。  
  
## <a name="types-of-literal-values"></a>文本值的类型  
 在 C# 中，文本值可从编译器获取类型。 可以通过在数字末尾追加一个字母来指定数字文本应采用的类型。 例如，若要将值 4.56 指定为应按浮点值处理，请在数字后面追加“f”或“F”：`4.56f`。 如果没有追加字母，那么编译器就会推断文本值的类型。 若要详细了解可以使用字母后缀指定哪些类型，请参阅[值类型](../../../csharp/language-reference/keywords/value-types.md)中的各个类型参考页。  
  
 由于文本已类型化，且所有类型最终都是从 <xref:System.Object?displayProperty=nameWithType> 派生，因此可以编写和编译如下所示的代码：  
  
 [!code-cs[csProgGuideTypes#37](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/index_7.cs)]  
  
## <a name="generic-types"></a>泛型类型  
 类型可使用一个或多个*类型参数*进行声明，这些参数用作客户端代码在创建类型实例时提供的实际类型（*具体类型*）的占位符。 这种类型称为*泛型类型*。 例如，.NET Framework 类型 <xref:System.Collections.Generic.List%601?displayProperty=nameWithType> 具有一个类型参数，它按照惯例被命名为 *T*。创建类型实例时，指定列表将包含的对象类型，例如字符串：  
 
```csharp
List<string> stringList = new List<string>();
stringList.Add("String example");
// compile time error adding a type other than a string:
stringList.Add(4);
```
 使用类型参数，可以重用同一个类来保留任何类型的元素，而无需将每个元素转换成[对象](../../../csharp/language-reference/keywords/object.md)。 泛型集合类称为*强类型集合*，因为编译器知道集合元素的具体类型，并能在编译时抛出错误，例如当尝试向上面示例中的 `strings` 对象添加整数时。 有关详细信息，请参阅[泛型](../../../csharp/programming-guide/generics/index.md)。  
  
## <a name="implicit-types-anonymous-types-and-nullable-types"></a>隐式类型、匿名类型和可以为 null 的类型  
 如上所述，可以使用 [var](../../../csharp/language-reference/keywords/var.md) 关键字隐式键入局部变量（但不是类成员）。 变量仍可在编译时获取类型，但类型是由编译器提供。 有关详细信息，请参阅[隐式类型局部变量](../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md)。  
  
 在某些情况下，为不打算在方法边界外存储或传递的各组简单的相关值创建已命名的类型并不方便。 因此，可以创建*匿名类型*。 有关详细信息，请参阅[匿名类型](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)。  
  
 普通值类型不能包含值 [null](../../../csharp/language-reference/keywords/null.md)。 不过，可以在类型后面附加 `?`，创建可以为 null 的值类型。 例如，`int?` 是还可以包含值 [null](../../../csharp/language-reference/keywords/null.md) 的 `int` 类型。 在 CTS 中，可以为 null 的类型是泛型结构类型 <xref:System.Nullable%601?displayProperty=nameWithType> 的实例。 将数据传入数据库和从中传出数据（数值可能为 null）时，可以为 null 的类型就特别有用。 有关详细信息，请参阅[可以为 null 的类型](../../../csharp/programming-guide/nullable-types/index.md)。  
  
## <a name="related-sections"></a>相关章节  
 有关详细信息，请参阅下列主题：  
  
-   [强制转换和类型转换](../../../csharp/programming-guide/types/casting-and-type-conversions.md)  
  
-   [装箱和取消装箱](../../../csharp/programming-guide/types/boxing-and-unboxing.md)  
  
-   [使用类型 dynamic](../../../csharp/programming-guide/types/using-type-dynamic.md)  
  
-   [值类型](../../../csharp/language-reference/keywords/value-types.md)  
  
-   [引用类型](../../../csharp/language-reference/keywords/reference-types.md)  
  
-   [类和结构](../../../csharp/programming-guide/classes-and-structs/index.md)  
  
-   [匿名类型](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)  
  
-   [泛型](../../../csharp/programming-guide/generics/index.md)  

## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [C# 参考](../../../csharp/language-reference/index.md)   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [XML 数据类型转换](../../../standard/data/xml/conversion-of-xml-data-types.md)   
 [整型表](../../../csharp/language-reference/keywords/integral-types-table.md)

