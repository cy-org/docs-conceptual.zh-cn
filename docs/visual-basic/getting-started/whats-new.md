---
title: "Visual Basic 的新增功能"
ms.date: 2017-04-27
ms.prod: .net
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- VB.StartPage.WhatsNew
dev_langs:
- VB
helpviewer_keywords:
- new features, Visual Basic
- what's new [Visual Basic]
- Visual Basic, what's new
ms.assetid: d7e97396-7f42-4873-a81c-4ebcc4b6ca02
caps.latest.revision: 145
author: rpetrusha
ms.author: ronpet
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
ms.openlocfilehash: 0a9379d5dd2d1c6b3ed6820e350c19fb346ac84c
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="whats-new-for-visual-basic"></a>Visual Basic 的新增功能

本主题列出每个 Visual Basic 版本的重要功能名以及该语言最新版本中的新功能和增强功能的详细说明。
  
## <a name="current-version"></a>当前版本

Visual Basic/Visual Studio .NET 2017   
有关新功能，请参阅 [Visual Basic 2017](#visual-basic-2017)

## <a name="previous-versions"></a>早期版本

Visual Basic/Visual Studio .NET 2015   
有关新功能，请参阅 [Visual Basic 14](#visual-basic-14)

Visual Basic/Visual Studio .NET 2013  
.NET Compiler Platform (“Roslyn”) 的技术预览

Visual Basic/Visual Studio .NET 2012   
`Async` 和 `await` 关键字、迭代器、调用方信息特性

Visual Basic、Visual Studio .NET 2010   
自动实现的属性、集合初始值设定项、隐式行继续符、动态、泛型协变/逆变、全局命名空间访问

Visual Basic/Visual Studio .NET 2008   
语言集成查询 (LINQ)、XML 文本、本地类型推断、对象初始值设定项、匿名类型、扩展方法、本地 `var` 类型推断、lambda 表达式、`if` 运算符、分部方法、可以为 null 的值类型  

Visual Basic/Visual Studio .NET 2005   
`My` 类型和帮助程序类型（对应用、计算机、文件系统、网络的访问）

Visual Basic/Visual Studio .NET 2003   
移位运算符、循环变量声明

Visual Basic/Visual Studio .NET 2002   
Visual Basic.NET 的首次发布

## <a name="visual-basic-2017"></a>Visual Basic 2017

[元组](../programming-guide/language-features/data-types/tuples.md)

元组是一种轻量级数据结构，通常用于从单个方法调用返回多个值。 一般情况下，若要从方法返回多个值，必须执行以下操作之一：

- 定义自定义类型（`Class` 或 `Structure`）。 这是重量级解决方案。

- 定义一个或多个 `ByRef` 参数，以及从方法返回一个值。
 
通过 Visual Basic 对元组的支持，可快速定义元组、为其值分配语义名称（可选），并快速检索其值。 以下示例包装对 <xref:System.Int32.TryParse%2A> 方法的调用，并返回一个元组。

[!code-vb[元组](../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple-returns.vb#2)]

然后，可以调用该方法并使用如下所示的代码处理返回的元组。

[!code-vb[ReturnTuple](../../../samples/snippets/visualbasic/programming-guide/language-features/data-types/tuple-returns.vb#3)] 

**二进制文本和数字分隔符**

可通过使用前缀 `&B` 或 `&b` 定义二进制文本。 此外，可以将下划线字符 `_` 用作数字分隔符，以增强可读性。 以下示例使用这两项功能分配 `Byte` 值，并将其显示为十进制、十六进制和二进制数字。

[!code-vb[二进制](../../../samples/snippets/visualbasic/getting-started/bin-example.vb#1)]

有关详细信息，请参阅 [Byte](../language-reference/data-types/byte-data-type.md#literal-assignments)、[Integer](../language-reference/data-types/integer-data-type.md#literal-assignments)、[Long](../language-reference/data-types/long-data-type.md#literal-assignments)、[Short](../language-reference/data-types/short-data-type.md#literal-assignments)、[SByte](../language-reference/data-types/sbyte-data-type.md#literal-assignments)、[UInteger](../language-reference/data-types/uinteger-data-type.md#literal-assignments)、[ULong](../language-reference/data-types/ulong-data-type.md#literal-assignments) 和 [UShort](../language-reference/data-types/ushort-data-type.md#literal-assignments) 数据类型的“文本分配”部分。

**支持 C# 引用返回值**

从 C# 7 开始，C# 支持引用返回值。 也就是说，当调用方法收到引用返回的值时，可以更改引用的值。 Visual Basic 不允许使用引用返回值创建方法，但允许使用和修改引用返回值。

例如，用 C# 编写的以下 `Sentence` 类包括 `FindNext` 方法，该方法查找句子中以指定的子字符串开头的下一个单词。 该字符串作为引用返回值返回，方法引用传递的 `Boolean` 变量指示搜索是否成功。 这意味着调用方不仅可以读取返回的值；还可以修改此值，此修改在 `Sentence` 类中反映。

[!code-csharp[Ref-Return](../../../samples/snippets/visualbasic/getting-started/ref-returns.cs)]

在最简单的形式中，可以使用如下所示的代码修改句子中找到的单词。 请注意，不是将值分配到方法，而是将值分配到方法返回的表达式（即引用返回值）。

[!code-vb[Ref-Return](../../../samples/snippets/visualbasic/getting-started/ref-return.vb#1)]

但是，此代码的问题是，如果找不到匹配项，方法将返回第一个单词。 由于该示例不检查 `Boolean` 参数的值以确定是否找到匹配项，所以如果没有匹配项，则修改第一个单词。 以下示例对此进行了更正：如果没有匹配项，则将第一个单词替换为自身。

[!code-vb[Ref-Return](../../../samples/snippets/visualbasic/getting-started/ref-return.vb#2)]

更好的解决方案是使用引用将引用返回值传递到的帮助程序方法。 然后，帮助程序方法可以修改引用传递给其的参数。 以下示例执行该操作。

[!code-vb[Ref-Return](../../../samples/snippets/visualbasic/getting-started/ref-return-helper.vb#1)]

有关详细信息，请参阅[引用返回值](../programming-guide/language-features/procedures/ref-return-values.md)。

## <a name="visual-basic-14"></a>Visual Basic 14

[Nameof](../../csharp/language-reference/keywords/nameof.md)  
 可以在错误消息中使用类型或成员的非限定字符串名，而无需对字符串进行硬编码。  这使代码可以在重构时保持正确。  此功能也可用于挂接“模型-视图-控制器”MVC 链接并触发属性更改事件。  
  
[字符串内插](../../csharp/language-reference/keywords/interpolated-strings.md)  
 可以使用字符串内插表达式构造字符串。  内插字符串表达式类似于包含表达式的模板字符串。  与[复合格式设置](../../standard/base-types/composite-format.md)相比，内插字符串在自变量方面更易于理解。  
  
[null 条件成员访问和索引](../../csharp/language-reference/operators/null-conditional-operators.md)  
可以在执行成员访问 (`?.`) 或索引 (`?[]`) 操作之前以非常轻量的语法方式测试是否存在 null。  这些运算符可帮助编写更少的代码来处理 null 检查，尤其是对于下降到数据结构。  如果左操作数或对象引用为 null，则操作会返回 null。  
  
[多行字符串](../../visual-basic/programming-guide/language-features/strings/string-basics.md)  
 字符串可以包含换行符序列。  不再需要使用 `<xml><![CDATA[...text with newlines...]]></xml>.Value` 这种旧的解决方法  
  
注释  
可以在隐式行继续符之后、初始值设定项表达式内部以及 LINQ 表达式项之间放置注释。  
  
 更智能的完全限定名称解析  
 如果提供了 `Threading.Thread.Sleep(1000)` 这类代码，Visual Basic 过去会查找命名空间“Threading”，发现它在 System.Threading 与 System.Windows.Threading 混淆，然后报告错误。  Visual Basic 现在将这两个可能的命名空间结合在一起进行考虑。  如果显示完成列表，则 Visual Studio 编辑器会在完成列表中列出这两种类型中的成员。  
  
 以年份开头的日期文本  
 可以使用 yyyy-mm-dd 格式的日期文本 `#2015-03-17 16:10 PM#`。  
  
 只读接口属性  
 可以使用读写属性实现只读接口属性。  该接口可保证最小功能，不会阻止实现类允许设置属性。  
  
 [TypeOf \<表达式> IsNot \<类型>](../../visual-basic/language-reference/operators/typeof-operator.md)  
 为提高代码的可读性，现在可以将 `TypeOf` 与 `IsNot` 一起使用。  
  
 [#Disable Warning \<ID> 和 #Enable Warning \<ID>](../../visual-basic/language-reference/directives/directives.md)  
 可以对源文件中的区域禁用和启用特定警告。  
  
 XML 文档注释改进  
 编写文档注释时，可获取智能编辑器和生成支持，以用于验证参数名、正确处理 `crefs`（泛型、运算符等）、着色和重构。  
  
 [部分模块和接口定义](../../visual-basic/language-reference/modifiers/partial.md)  
 除了类和结构之外，还可以声明部分模块和接口。  
  
 [方法体中的 #Region 指令](../../visual-basic/language-reference/directives/region-directive.md)  
 可以将 #Region…#End Region 限定符放置在文件中、函数内部甚至是跨越函数体的任何位置。  
  
 [替代定义是隐式重载](../../visual-basic/language-reference/modifiers/overrides.md)  
 如果你向定义添加 `Overrides` 修饰符，则编译器会隐式添加 `Overloads`，以便你可以在常见情况下输入更少的代码。  
  
 特性参数中允许使用 CObj  
 当 CObj(...) 在特性构造中使用时，编译器过去会发出错误，指出它不是常量。  
  
 从不同接口声明和使用不明确的方法  
 以下代码以前会生成错误，从而阻止你声明 `IMock` 或调用 `GetDetails`（如果这些内容已在 C# 中声明）：  
  
```vb  
Interface ICustomer  
  Sub GetDetails(x As Integer)  
End Interface  
  
Interface ITime  
  Sub GetDetails(x As String)  
End Interface  
  
Interface IMock : Inherits ICustomer, ITime  
  Overloads Sub GetDetails(x As Char)  
End Interface  
  
Interface IMock2 : Inherits ICustomer, ITime  
End Interface  
```  
  
 现在，编译器会使用正常的重载决策规则来选择最合适的 `GetDetails` 进行调用，你可以在 Visual Basic 中声明接口关系（如示例中所示的这些关系）。  
  
## <a name="see-also"></a>请参阅  
 [Visual Studio 2017 中的新增功能](/visualstudio/ide/whats-new-in-visual-studio)

