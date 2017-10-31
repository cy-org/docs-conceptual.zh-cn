---
title: "C# 类和对象 - C# 语言介绍"
description: "刚开始接触 C#？ 请阅读这篇概述类、对象和继承的文章"
keywords: ".NET, C#, 类, 实例, 对象, 继承, 多形性"
author: BillWagner
ms.author: wiwagn
ms.date: 08/10/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 63a89bde-0f05-4bc4-b0cd-4f693854f0cd
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: c71aee3dbfb6544973e1527955ca03deb6b569f3
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="classes-and-objects"></a>类和对象

*类*是最基本的 C# 类型。 类是一种数据结构，可在一个单元中就将状态（字段）和操作（方法和其他函数成员）结合起来。 类为动态创建的类*实例*（亦称为“*对象*”）提供了定义。 类支持*继承*和*多形性*，即*派生类*可以扩展和专门针对*基类*的机制。

新类使用类声明进行创建。 类声明的开头是标头，指定了类的特性和修饰符、类名、基类（若指定）以及类实现的接口。 标头后面是类主体，由在分隔符 `{` 和 `}` 内编写的成员声明列表组成。

以下是简单类 `Point` 的声明：

[!code-csharp[PointClass](../../../samples/snippets/csharp/tour/classes-and-objects/Point.cs#L3-L11)]

类实例是使用 `new` 运算符进行创建，此运算符为新实例分配内存，调用构造函数来初始化实例，并返回对实例的引用。 以下语句创建两个 Point 对象，并将对这些对象的引用存储在两个变量中：

[!code-csharp[PointExample](../../../samples/snippets/csharp/tour/classes-and-objects/Program.cs#L9-L10)]

当无法再访问对象时，对象占用的内存会被自动回收。 既没必要，也无法在 C# 中显式解除分配对象。

## <a name="members"></a>成员

类成员要么是静态成员，要么是实例成员。 静态成员属于类，而实例成员则属于对象（类实例）。

下面概述了类可以包含的成员类型。

* 常量
    - 与类相关联的常量值
* 字段
    - 类的常量
* 方法
    - 类可以执行的计算和操作
* 属性
    - 与读取和写入类的已命名属性相关联的操作
* 索引器
    - 与将类实例编入索引（像处理数组一样）相关联的操作
* 事件
    - 类可以生成的通知
* 运算符
    - 类支持的转换和表达式运算符
* 构造函数
    - 初始化类实例或类本身所需的操作
* 终结器
    - 永久放弃类实例前要执行的操作
* 类型
    - 类声明的嵌套类型

## <a name="accessibility"></a>可访问性

每个类成员都有关联的可访问性，用于控制能够访问成员的程序文本区域。 可访问性有五种可能的形式。 总结如下。

* `public`
    - 访问不受限
* `protected`
    - 只能访问此类或派生自此类的类
* `internal`
    - 访问限于当前程序集（.exe、.dll 等）
* `protected internal`
    - 访问限于包含类或派生自包含类的类
* `private`
    - 只能访问此类

## <a name="type-parameters"></a>类型参数

类定义可能会按如下方式指定一组类型参数：在类名后面用尖括号括住类型参数名称列表。 然后，可以在类声明的主体中使用类型参数来定义类成员。 在以下示例中，`Pair` 的类型参数是 `TFirst` 和 `TSecond`：

[!code-csharp[Pair](../../../samples/snippets/csharp/tour/classes-and-objects/Pair.cs#L3-L7)]

声明为需要使用类型参数的类类型被称为*泛型类类型*。 结构、接口和委托类型也可以是泛型。
使用泛型类时，必须为每个类型参数提供类型自变量：

[!code-csharp[PairExample](../../../samples/snippets/csharp/tour/classes-and-objects/Program.cs#L15-L17)]

包含类型自变量的泛型类型（如上面的 `Pair<int,string>`）被称为*构造泛型类型*。

## <a name="base-classes"></a>基类

类声明可能会按如下方式指定基类：在类名和类型参数后面编写冒号和基类名。 省略基类规范与从 `object` 类型派生相同。 在以下示例中，`Point3D` 的基类是 `Point`，`Point` 的基类是 `object`：

[!code-csharp[Point3DClass](../../../samples/snippets/csharp/tour/classes-and-objects/Point.cs#L3-L20)]

类继承其基类的成员。 继承是指隐式包含其基类的所有成员的类，实例和静态构造函数以及基类的终结器除外。 派生类可以其继承的类添加新成员，但无法删除继承成员的定义。 在上面的示例中，`Point3D` 从 `Point` 继承了 `x` 和 `y` 字段，每个 `Point3D` 实例均包含三个字段（`x`、`y` 和 `z`）。

可以将类类型隐式转换成其任意基类类型。 因此，类类型的变量可以引用相应类的实例或任意派生类的实例。 例如，类声明如上，`Point` 类型的变量可以引用 `Point` 或 `Point3D`：

[!code-csharp[Point3DExample](../../../samples/snippets/csharp/tour/classes-and-objects/Program.cs#L22-L23)]

## <a name="fields"></a>字段

*字段*是与类或类实例相关联的变量。

使用静态修饰符声明的字段定义的是静态字段。 静态字段只指明一个存储位置。 无论创建多少个类实例，永远只有一个静态字段副本。

不使用静态修饰符声明的字段定义的是实例字段。 每个类实例均包含相应类的所有实例字段的单独副本。

在以下示例中，每个 `Color` 类实例均包含 `r`、`g` 和 `b` 实例字段的单独副本，但分别只包含 `Black`、`White`、`Red`、`Green` 和 `Blue` 静态字段的一个副本：

[!code-csharp[ColorClass](../../../samples/snippets/csharp/tour/classes-and-objects/Color.cs#L3-L17)]

如上面的示例所示，可以使用 `readonly` 修饰符声明*只读字段*。 只能在字段声明期间或在同一个类的构造函数中向 `readonly` 字段赋值。

## <a name="methods"></a>方法

*方法*是实现对象或类可执行的计算或操作的成员。 *静态方法*是通过类进行访问。 *实例方法*是通过类实例进行访问。

方法可能具有*参数*列表，用于表示传递给方法的值或变量引用；并具有*返回类型*，用于指定方法计算并返回的值的类型。 如果方法未返回值，则其返回类型为 `void`。

方法可能也包含一组类型参数，必须在调用方法时指定类型自变量，这一点与类型一样。 与类型不同的是，通常可以根据方法调用的自变量推断出类型自变量，无需显式指定。

在声明方法的类中，方法的*签名*必须是唯一的。 方法签名包含方法名称、类型参数数量及其参数的数量、修饰符和类型。 方法签名不包含返回类型。

### <a name="parameters"></a>参数

参数用于将值或变量引用传递给方法。 方法参数从调用方法时指定的*自变量*中获取其实际值。 有四类参数：值参数、引用参数、输出参数和参数数组。

值参数用于传递输入自变量。 值参数对应于局部变量，从为其传递的自变量中获取初始值。 修改值参数不会影响为其传递的自变量。 

可以指定默认值，从而省略相应的自变量，这样值参数就是可选的。

引用参数用于按引用传递自变量。 为引用参数传递的自变量必须是具有明确值的变量，并且在方法执行期间，引用参数指明的存储位置与自变量相同。 引用参数使用 `ref` 修饰符进行声明。 下面的示例展示了如何使用 `ref` 参数。

[!code-csharp[swapExample](../../../samples/snippets/csharp/tour/classes-and-objects/RefExample.cs#L3-L18)]

输出参数用于按引用传递自变量。 输出参数与引用参数类似，不同之处在于，不要求向调用方提供的自变量显式赋值。 输出参数使用 `out` 修饰符进行声明。 下面的示例演示如何通过 C# 7 中引入的语法使用 `out` 参数。

[!code-csharp[OutExample](../../../samples/snippets/csharp/tour/classes-and-objects/OutExample.cs#L3-L17)]

*参数数组*允许向方法传递数量不定的自变量。 参数数组使用 `params` 修饰符进行声明。 参数数组只能是方法的最后一个参数，且参数数组的类型必须是一维数组类型。 `@System.Console` 类的 Write 和 WriteLine 方法是参数数组用法的典型示例。 它们的声明方式如下。

[!code-csharp[ConsoleExample](../../../samples/snippets/csharp/tour/classes-and-objects/Program.cs#L78-L83)]

在使用参数数组的方法中，参数数组的行为与数组类型的常规参数完全相同。 不过，在调用包含参数数组的方法时，要么可以传递参数数组类型的一个自变量，要么可以传递参数数组的元素类型的任意数量自变量。 在后一种情况中，数组实例会自动创建，并初始化为包含给定的自变量。 以下示例：

[!code-csharp[StringFormat](../../../samples/snippets/csharp/tour/classes-and-objects/Program.cs#L55-L55)]

等同于编写以下代码：

[!code-csharp[StringFormat2](../../../samples/snippets/csharp/tour/classes-and-objects/Program.cs#L30-L35)]

### <a name="method-body-and-local-variables"></a>方法主体和局部变量

方法主体指定了在调用方法时执行的语句。

方法主体可以声明特定于方法调用的变量。 此类变量称为*局部变量*。 局部变量声明指定了类型名称、变量名称以及可能的初始值。 下面的示例声明了初始值为零的局部变量 `i` 和无初始值的局部变量 `j`。

[!code-csharp[Squares](../../../samples/snippets/csharp/tour/classes-and-objects/Squares.cs#L3-L17)]

C# 要求必须先*明确赋值*局部变量，然后才能获取其值。 例如，如果上面的 `i` 声明未包含初始值，那么编译器会在后面使用 `i` 时报告错误，因为在后面使用时 `i` 不会在程序中进行明确赋值。

方法可以使用 `return` 语句将控制权返回给调用方。 在返回 `void` 的方法中，`return` 语句无法指定表达式。 在不返回 void 的方法中，`return` 语句必须包括用于计算返回值的表达式。

### <a name="static-and-instance-methods"></a>静态和实例方法

使用静态修饰符声明的方法是*静态方法*。 静态方法不对特定的实例起作用，只能直接访问静态成员。

不使用静态修饰符声明的方法是*实例方法*。 实例方法对特定的实例起作用，并能够访问静态和实例成员。 其中调用实例方法的实例可以作为 `this` 显式访问。 在静态方法中引用 `this` 会生成错误。

以下 `Entity` 类包含静态和实例成员。

[!code-csharp[Entity](../../../samples/snippets/csharp/tour/classes-and-objects/Entity.cs#L16-L36)]

每个 `Entity` 实例均有一个序列号（很可能包含此处未显示的其他一些信息）。 `Entity` 构造函数（类似于实例方法）将新实例初始化为包含下一个可用的序列号。 由于构造函数是实例成员，因此可以访问 `serialNo` 实例字段和 `nextSerialNo` 静态字段。

`GetNextSerialNo` 和 `SetNextSerialNo` 静态方法可以访问 `nextSerialNo` 静态字段，但如果直接访问 `serialNo` 实例字段，则会生成错误。

下面的示例展示了如何使用 Entity 类。

[!code-csharp[EntityExample](../../../samples/snippets/csharp/tour/classes-and-objects/Entity.cs#L3-L15)]

请注意，`SetNextSerialNo` 和 `GetNextSerialNo` 静态方法是在类中调用，而 `GetSerialNo` 实例方法则是在类实例中调用。

### <a name="virtual-override-and-abstract-methods"></a>虚方法、重写方法和抽象方法

如果实例方法声明中有 `virtual` 修饰符，可以将实例方法称为“*虚方法*”。 如果没有 virtual 修饰符，可以将实例方法称为“*非虚方法*”。

调用虚方法时，为其调用方法的实例的*运行时类型*决定了要调用的实际方法实现代码。 调用非虚方法时，实例的*编译时类型*是决定性因素。

可以在派生类中*重写*虚方法。 如果实例方法声明中有 override 修饰符，那么实例方法可以重写签名相同的继承虚方法。 但如果虚方法声明中引入新方法，重写方法声明通过提供相应方法的新实现代码，专门针对现有的继承虚方法。

*抽象方法*是没有实现代码的虚方法。 抽象方法使用 abstract 修饰符进行声明，只能在同样声明了 abstract 的类中使用。 必须在所有非抽象派生类中重写抽象方法。

下面的示例声明了一个抽象类 `Expression`，用于表示表达式树节点；还声明了三个派生类（`Constant`、`VariableReference` 和 `Operation`），用于实现常量、变量引用和算术运算的表达式树节点。 （这与表达式树类型相似，但不能与之混淆）。

[!code-csharp[ExpressionClass](../../../samples/snippets/csharp/tour/classes-and-objects/Expressions.cs#L3-L61)]

上面的四个类可用于进行算术表达式建模。 例如，使用这些类的实例，可以按如下方式表示表达式 `x + 3`。

[!code-csharp[ExpressionExample](../../../samples/snippets/csharp/tour/classes-and-objects/Program.cs#L40-L43)]

调用 `Expression` 实例的 `Evaluate` 方法可以计算给定的表达式并生成 `double` 值。 此方法需要使用自变量 `Dictionary`，其中包含变量名称（作为项键）和值（作为项值）。 因为 `Evaluate` 是一个抽象方法，因此派生自 `Expression` 的非抽象类必须替代 `Evaluate`。

`Constant` 的 `Evaluate` 实现代码只返回存储的常量。 `VariableReference` 实现代码查找字典中的变量名称，并返回结果值。 `Operation` 实现代码先计算左右操作数（以递归方式调用其 `Evaluate` 方法），然后执行给定的算术运算。

以下程序使用 `Expression` 类根据不同的 `x` 和 `y` 值计算表达式 `x * (y + 2)`。

[!code-csharp[ExpressionUsage](../../../samples/snippets/csharp/tour/classes-and-objects/Expressions.cs#L66-L89)]

### <a name="method-overloading"></a>方法重载

借助方法*重载*，同一类中可以有多个同名的方法，只要这些方法具有唯一签名即可。 编译如何调用重载的方法时，编译器使用*重载决策*来确定要调用的特定方法。 重载决策查找与自变量最匹配的方法；如果找不到最佳匹配项，则会报告错误。 下面的示例展示了重载决策的实际工作方式。 `Main` 方法中每个调用的注释指明了实际调用的方法。

[!code-csharp[OverloadUsage](../../../samples/snippets/csharp/tour/classes-and-objects/Overloading.cs#L3-L41)]

如示例所示，可以随时将自变量显式转换成确切的参数类型，并/或显式提供类型自变量，从而选择特定的方法。

## <a name="other-function-members"></a>其他函数成员

包含可执行代码的成员统称为类的*函数成员*。 上一部分介绍了作为主要函数成员类型的方法。 此部分将介绍 C# 支持的其他类型函数成员：构造函数、属性、索引器、事件、运算符和终结器。

下面的示例展示了 List<T> 泛型类，用于实现对象的可扩充列表。 此类包含最常见类型函数成员的多个示例。

[!code-csharp[ListClass](../../../samples/snippets/csharp/tour/classes-and-objects/ListBasedExamples.cs#L4-L89)]

### <a name="constructors"></a>构造函数

C# 支持实例和静态构造函数。 *实例构造函数*是实现初始化类实例所需执行的操作的成员。 *静态构造函数*是实现在首次加载类时初始化类本身所需执行的操作的成员。

构造函数的声明方式与方法一样，都没有返回类型，且与所含类同名。 如果构造函数声明包含静态修饰符，则声明的是静态构造函数。 否则，声明的是实例构造函数。

实例构造函数可以重载，并能包含可选参数。 例如，`List<T>` 类声明两个实例构造函数：一个没有参数，另一个需要使用 `int` 参数。 实例构造函数使用 `new` 运算符进行调用。 下面的语句使用包含和不包含可选自变量的 `List` 类构造函数来分配两个 `List<string>` 实例。

[!code-csharp[ListExample1](../../../samples/snippets/csharp/tour/classes-and-objects/ListBasedExamples.cs#L95-L96)]

与其他成员不同，实例构造函数不能被继承，且类中只能包含实际已声明的实例构造函数。 如果没有为类提供实例构造函数，则会自动提供不含参数的空实例构造函数。

### <a name="properties"></a>属性

*属性*是字段的自然扩展。 两者都是包含关联类型的已命名成员，用于访问字段和属性的语法也是一样的。 不过，与字段不同的是，属性不指明存储位置。 相反，属性包含*访问器*，用于指定在读取或写入属性值时要执行的语句。

属性的声明方式与字段类似，不同之处在于，属性声明以在分隔符 `{` 和 `}` 内写入的 get 访问器和/或 set 访问器结束，而不是以分号结束。 同时包含 get 访问器和 set 访问器的属性是*读写属性*，仅包含 get 访问器的属性是*只读属性*，仅包含 set 访问器的属性是*只写属性*。

get 访问器对应于包含属性类型的返回值的无参数方法。 如果在表达式中引用属性，除了作为赋值目标以外，调用的属性 get 访问器还可用于计算属性值。

set 访问器对应于包含一个名为 value 的参数但不含返回类型的方法。 如果将属性引用为赋值目标或 ++/-- 的操作数，将调用 set 访问器（由自变量提供新值）。

`List<T>` 类声明以下两个属性：Count 和 Capacity（分别是只读和只写属性）。 下面的示例展示了如何使用这些属性。

[!code-csharp[ListExample2](../../../samples/snippets/csharp/tour/classes-and-objects/ListBasedExamples.cs#L101-L104)]

类似于字段和方法，C# 支持实例属性和静态属性。 静态属性使用静态修饰符进行声明，而实例属性则不使用静态修饰符进行声明。

属性的访问器可以是虚的。 如果属性声明包含 `virtual`、`abstract` 或 `override` 修饰符，则适用于属性的访问器。

### <a name="indexers"></a>索引器

借助*索引器*成员，可以将对象编入索引（像处理数组一样）。 索引器的声明方式与属性类似，不同之处在于，索引器成员名称格式为后跟分隔符 `[` 和 `]`，其中写入参数列表。 这些参数在索引器的访问器中可用。 类似于属性，索引器分为读写、只读和只写索引器，且索引器的访问器可以是虚的。

`List` 类声明一个需要使用 `int` 参数的读写索引器。 借助索引器，可以使用 `int` 值将 `List` 实例编入索引。 例如：

[!code-csharp[ListExample3](../../../samples/snippets/csharp/tour/classes-and-objects/ListBasedExamples.cs#L109-L117)]

索引器可以进行重载。也就是说，类可以声明多个索引器，只要其参数的数量或类型不同即可。

### <a name="events"></a>事件

借助*事件*成员，类或对象可以提供通知。 事件的声明方式与字段类似，不同之处在于，事件声明包括事件关键字，且类型必须是委托类型。

在声明事件成员的类中，事件的行为与委托类型的字段完全相同（前提是事件不是抽象的，且不声明访问器）。 字段存储对委托的引用，委托表示已添加到事件的事件处理程序。 如果没有任何事件处理程序，则字段为 `null`。

`List<T>` 类声明一个 `Changed` 事件成员，指明已向列表添加了新项。 Changed 事件由 `OnChanged` 虚方法引发，此方法会先检查事件是否是 `null`（即不含任何处理程序）。 引发事件的概念恰恰等同于调用由事件表示的委托，因此，没有用于引发事件的特殊语言构造。

客户端通过*事件处理程序*响应事件。 使用 `+=` 和 `-=` 运算符分别可以附加和删除事件处理程序。 下面的示例展示了如何向 `List<string>` 的 `Changed` 事件附加事件处理程序。

[!code-csharp[EventExample](../../../samples/snippets/csharp/tour/classes-and-objects/ListBasedExamples.cs#L132-L148)]

对于需要控制事件的基础存储的高级方案，事件声明可以显式提供 `add` 和 `remove` 访问器，这在某种程度上与属性的 `set` 访问器类似。

### <a name="operators"></a>运算符

*运算符*是定义向类实例应用特定表达式运算符的含义的成员。 可以定义三种类型的运算符：一元运算符、二元运算符和转换运算符。 所有运算符都必须声明为 `public` 和 `static`。

`List<T>` 类声明两个运算符（`operator ==` 和 `operator !=`），因此定义了向 `List` 实例应用这些运算符的表达式的新含义。 具体而言，这些运算符定义的是两个 `List<T>` 实例的相等性（使用其 Equals 方法比较所包含的每个对象）。 下面的示例展示了如何使用 `==` 运算符比较两个 `List<int>` 实例。

[!code-csharp[OperatorExample](../../../samples/snippets/csharp/tour/classes-and-objects/ListBasedExamples.cs#L121-L129)]

第一个 `Console.WriteLine` 输出 `True`，因为两个列表包含的对象不仅数量相同，而且值和顺序也相同。 如果 `List<T>` 未定义 `operator ==`，那么第一个 `Console.WriteLine` 会输出 `False`，因为 `a` 和 `b` 引用不同的 `List<int>` 实例。

### <a name="finalizers"></a>终结器

*终结器*是实现完成类实例所需的操作的成员。 终结器既不能包含参数和可访问性修饰符，也不能进行显式调用。 实例的终结器在垃圾回收期间自动调用。

垃圾回收器在决定何时收集对象和运行终结器时有很大自由度。 具体来说，终结器的调用时间具有不确定性，可以在任意线程上执行终结器。 因为这样或那样的原因，只有在没有其他可行的解决方案时，类才能实现终结器。

处理对象析构的更好方法是使用 `using` 语句。

>[!div class="step-by-step"]
[上一页](statements.md)
[下一页](structs.md)

