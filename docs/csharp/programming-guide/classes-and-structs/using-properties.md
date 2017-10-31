---
title: "使用属性（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- set accessor [C#]
- get accessor [C#]
- properties [C#], about properties
ms.assetid: f7f67b05-0983-4cdb-96af-1855d24c967c
caps.latest.revision: 24
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
ms.openlocfilehash: 6b1b1dbffa3af7fdaf1f3a93ecdf6183fe1c1cf2
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="using-properties-c-programming-guide"></a>使用属性（C# 编程指南）
属性结合了字段和方法的多个方面。 对于对象的用户来说，属性似乎是一个字段，访问属性需要相同的语法。 对于类的实现者来说，属性是一两个代码块，表示 [get](../../../csharp/language-reference/keywords/get.md) 访问器和/或 [set](../../../csharp/language-reference/keywords/set.md) 访问器。 读取属性时，执行 `get` 访问器的代码块；向属性赋予新值时，执行 `set` 访问器的代码块。 将不带 `set` 访问器的属性视为只读。 将不带 `get` 访问器的属性视为只写。 将具有以上两个访问器的属性视为读写。  
  
 与字段不同，属性不会被归类为变量。 因此，不能将属性作为 [ref](../../../csharp/language-reference/keywords/ref.md) 或 [out](../../../csharp/language-reference/keywords/out.md) 参数传递。  
  
 属性具有许多用途：它们可以先验证数据，再允许进行更改；可以在类上透明地公开数据，其中数据实际是从某个其他源（如数据库）检索到的；可以在数据发生更改时采取措施，例如引发事件或更改其他字段的值。  
  
 通过依次指定字段的访问级别、属性类型、属性名、声明 `get` 访问器和/或 `set` 访问器的代码块，在类块中声明属性。 例如:   
  
 [!code-cs[csProgGuideProperties#7](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-properties_1.cs)]  
  
 此示例中将 `Month` 声明为属性，以便 `set` 访问器可确保 `Month` 值设置在 1 至 12 之间。 `Month` 属性使用私有字段跟踪实际值。 属性的数据的实际位置通常被称为属性的“后备存储”。 属性使用私有字段作为后备存储，这很常见。 将字段被标记为私有，确保只能通过调用属性来对其进行更改。 有关公共和专用访问限制的详细信息，请参阅[访问修饰符](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)。  
  
 自动实现的属性为简单属性声明提供简化的语法。 有关详细信息，请参阅[自动实现的属性](../../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md)。  
  
## <a name="the-get-accessor"></a>get 访问器  
 `get` 访问器的正文类似于方法。 它必须返回属性类型的值。 执行 `get` 访问器等效于读取字段的值。 例如，在从 `get` 访问器返回私有变量且已启用优化时，对 `get` 访问器方法的调用由编译器内联，因此不存在方法调用开销。 但是，无法内联虚拟 `get` 访问器方法，因为编译器在编译时不知道在运行时实际可调用哪些方法。 以下是一个 `get` 访问器，它返回私有字段 `name` 的值：  
  
 [!code-cs[csProgGuideProperties#8](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-properties_2.cs)]  
  
 引用属性时，除了作为赋值目标外，还调用 `get` 访问器读取属性值。 例如:   
  
 [!code-cs[csProgGuideProperties#9](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-properties_3.cs)]  
  
 `get` 访问器必须以 [return](../../../csharp/language-reference/keywords/return.md) 或 [throw](../../../csharp/language-reference/keywords/throw.md) 语句结尾，且控件不能超出访问器正文。  
  
 使用 `get` 访问器更改对象的状态是一种糟糕的编程风格。 例如，以下访问器将产生在每次访问 `number` 字段时更改对象状态的副作用。  
  
 [!code-cs[csProgGuideProperties#10](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-properties_4.cs)]  
  
 `get` 访问器可以用于返回字段值或计算并返回字段值。 例如:   
  
 [!code-cs[csProgGuideProperties#11](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-properties_5.cs)]  
  
 在上一个代码段中，如果不给 `Name` 属性赋值，则它将返回值 NA。  
  
## <a name="the-set-accessor"></a>set 访问器  
 `set` 访问器类似于返回类型为 [void](../../../csharp/language-reference/keywords/void.md) 的方法。 它使用名为 `value` 的隐式参数，该参数的类型为属性的类型。 在下面的示例中，将 `set` 访问器添加到 `Name` 属性：  
  
 [!code-cs[csProgGuideProperties#12](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-properties_6.cs)]  
  
 向属性赋值时，通过使用提供新值的自变量调用 `set` 访问器。 例如:   
  
 [!code-cs[csProgGuideProperties#13](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-properties_7.cs)]  
  
 为 `set` 访问器中的本地变量声明使用隐式参数名 `value` 是错误的。  
  
## <a name="remarks"></a>备注  
 可以将属性标记为 `public`、`private`、`protected`、`internal` 或 `protected internal`。 这些访问修饰符定义该类的用户访问该属性的方式。 相同属性的 `get` 和 `set` 访问器可以具有不同的访问修饰符。 例如，`get` 可能为 `public`允许从类型外部进行只读访问；而 `set` 可能为 `private` 或 `protected`。 有关详细信息，请参阅[访问修饰符](../../../csharp/programming-guide/classes-and-structs/access-modifiers.md)。  
  
 可以通过使用 `static` 关键字将属性声明为静态属性。 这使属性可供调用方在任何时候使用，即使不存在类的任何实例。 有关详细信息，请参阅[静态类和静态类成员](../../../csharp/programming-guide/classes-and-structs/static-classes-and-static-class-members.md)。  
  
 可以通过使用 [virtual](../../../csharp/language-reference/keywords/virtual.md) 关键字将属性标记为虚拟属性。 这可使派生类使用 [override](../../../csharp/language-reference/keywords/override.md) 关键字重写属性行为。 有关这些选项的详细信息，请参阅[继承](../../../csharp/programming-guide/classes-and-structs/inheritance.md)。  
  
 重写虚拟属性的属性也可以是 [sealed](../../../csharp/language-reference/keywords/sealed.md)，指定对于派生类，它不再是虚拟的。 最后，可以将属性声明为 [abstract](../../../csharp/language-reference/keywords/abstract.md)。 这意味着类中没有实现，派生类必须写入自己的实现。 有关这些选项的详细信息，请参阅[抽象类、密封类及类成员](../../../csharp/programming-guide/classes-and-structs/abstract-and-sealed-classes-and-class-members.md)。  
  
> [!NOTE]
>  在 [static](../../../csharp/language-reference/keywords/static.md) 属性的访问器上使用 [virtual](../../../csharp/language-reference/keywords/virtual.md)、[abstract](../../../csharp/language-reference/keywords/abstract.md) 或 [override](../../../csharp/language-reference/keywords/override.md) 修饰符是错误的。  
  
## <a name="example"></a>示例  
 此示例演示实例、静态和只读属性。 它接收通过键盘键入的员工姓名，按 1 递增 `NumberOfEmployees`，并显示员工姓名和编号。  
  
 [!code-cs[csProgGuideProperties#2](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-properties_8.cs)]  
  
## <a name="example"></a>示例  
 此示例演示如何访问由派生类中同名的另一属性隐藏的基类中的属性。  
  
 [!code-cs[csProgGuideProperties#3](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-properties_9.cs)]  
  
 以下内容是前一示例中的要点：  
  
-   派生类中的属性 `Name` 隐藏基类中的属性 `Name`。 在这种情况下，`new` 修饰符用于派生类的属性声明中：  
  
     [!code-cs[csProgGuideProperties#4](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-properties_10.cs)]  
  
-   `(Employee)` 转换用于访问基类中的隐藏属性：  
  
     [!code-cs[csProgGuideProperties#5](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-properties_11.cs)]  
  
     有关隐藏成员的详细信息，请参阅 [new 修饰符](../../../csharp/language-reference/keywords/new-modifier.md)。  
  
## <a name="example"></a>示例  
 在此示例中，两个类（`Cube` 和 `Square`）实现抽象类 `Shape`，并重写其抽象 `Area` 属性。 请注意属性上的 [override](../../../csharp/language-reference/keywords/override.md) 修饰符的使用。 程序接受将边长作为输入，计算正方形和立方体的面积。 它还接受将面积作为输入，计算正方形和立方体的相应边长。  
  
 [!code-cs[csProgGuideProperties#6](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-properties_12.cs)]  
  
## <a name="see-also"></a>另请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [属性](../../../csharp/programming-guide/classes-and-structs/properties.md)   
 [接口属性](../../../csharp/programming-guide/classes-and-structs/interface-properties.md)   
 [自动实现的属性](../../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md)

