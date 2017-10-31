---
title: "结构 - C# 指南"
description: "了解结构类型及其创建方式"
keywords: .NET, .NET Core, C#
author: BillWagner
ms.author: wiwagn
ms.date: 10/12/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: a7094b8c-7229-4b6f-82fc-824d0ea0ec40
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: e2a4bfdb46a69113d5eb8949df4ccf902acf9dee
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="structs"></a>结构
结构是一个值类型。 创建结构时，分配给结构的变量保留结构的实际数据。 将结构分配给新变量时，会复制结构。 因此，新变量和原始变量包含相同数据的副本（共两个）。 对一个副本所做的更改不会影响另一个副本。

值类型变量直接包含它们的值，这意味着在声明变量的任何上下文中内联分配内存。 对于值类型变量，没有单独的堆分配或垃圾回收开销。  
  
值类型分为两类：[结构](./language-reference/keywords/struct.md)和[枚举](./language-reference/keywords/enum.md)。  
  
内置的数值类型是结构，它们具有可访问的属性和方法：  
  
[!code-csharp静态方法[](../../samples/snippets/csharp/concepts/structs/static-method.cs)]
  
但可将这些类型视为简单的非聚合类型，为其声明并赋值：  
  
[!code-csharp[赋值](../../samples/snippets/csharp/concepts/structs/assign-value.cs)] 
  
例如，值类型为“密封”，这意味着不能从 @System.Int32 派生类型，并且不能将结构定义为从任何用户定义的类或结构继承，因为结构只能从 @System.ValueType 继承。 但是，一个结构可以实现一个或多个接口。 可将结构类型强制转换为接口类型；这将导致“装箱”操作，以将结构包装在托管堆上的引用类型对象内。 当将值类型传递到接受 @System.Object 作为输入参数的方法时，将发生装箱操作。 有关详细信息，请参阅[装箱和取消装箱](./programming-guide/types/boxing-and-unboxing.md )。  
  
使用 [struct](./language-reference/keywords/struct.md) 关键字可以创建你自己的自定义值类型。 结构通常用作一小组相关变量的容器，如以下示例所示：  
  
[!code-csharp[Struct 关键字](../../samples/snippets/csharp/concepts/structs/struct-keyword.cs)]  
  
有关 .NET Framework 中的值类型的详细信息，请参阅[通用类型系统](../standard/common-type-system.md)。  
    
结构与类具有许多相同的语法，但结构比类受到的限制更多：  
  
-   在结构声明中，除非将字段声明为 `const` 或 `static`，否则无法初始化。  
  
-   结构不能声明默认构造函数（没有参数的构造函数）或终结器。  
  
-   结构在分配时进行复制。 将结构分配给新变量时，将复制所有数据，并且对新副本所做的任何修改不会更改原始副本的数据。 使用值类型的集合（如 Dictionary<string, myStruct>）时，请务必记住这一点。  
  
-   结构是值类型，而类是引用类型。  
  
-   与类不同，无需使用 `new` 运算符即可对结构进行实例化。  
  
-   结构可以声明具有参数的构造函数。  
  
-   一个结构无法继承自另一个结构或类，并且它不能为类的基类。 所有结构都直接继承自 @System.ValueType，后者继承自 @System.Object。  
  
-   结构可以实现接口。

## <a name="literal-values"></a>文本值  
在 C# 中，文本值从编译器接收类型。 可以通过在数字末尾追加一个字母来指定数字文本应采用的类型。 例如，若要指定应按浮点数来处理值 4.56，则在该数字后追加一个“f”或“F”：`4.56f`。 如果没有追加字母，编译器将推断该文本的 `double` 类型。 若要详细了解可以使用字母后缀指定哪些类型，请参阅[值类型](./language-reference/keywords/value-types.md)中的各个类型参考页。  
  
由于文本已类型化，且所有类型最终都是从 @System.Object 派生，因此可以编写和编译如下所示的代码：  
  
[!code-csharp文本值[](../../samples/snippets/csharp/concepts/structs/literals.cs)]

最后两个示例演示 C# 7.0 中引入的语言功能。 第一个示例演示可使用下划线字符作为数值文本内的数字分隔符。 可将它们放在数字中的任意位置，从而提高可读性。 不会对值产生影响。

第二个示例演示二进制文本，使用二进制文本可直接指定位模式，无需使用十六进制表示法。

## <a name="nullable-types"></a>可以为 null 的类型  
普通值类型不能具有 [null](./language-reference/keywords/null.md) 值。 但是，可以通过在类型后面附加 **?** 来创建可以为 null 的值类型。 例如，**int?** 属于 **int** 类型，也可以具有值 [null](./language-reference/keywords/null.md)。 在 CTS 中，可以为 null 的类型是泛型结构类型 @System.Nullable%601 的实例。 在将数据传入和传出数据库（数值可能为 null）时，可以为 null 的类型特别有用。 有关详细信息，请参阅[可以为 Null 的类型（C# 编程指南）](./programming-guide/nullable-types/index.md)。

## <a name="see-also"></a>请参阅
[类](classes.md)

[基本类型](basic-types.md)

