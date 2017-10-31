---
title: "命名实参和可选实参（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- namedParameter_CSharpKeyword
- cs_namedParameter
dev_langs:
- CSharp
helpviewer_keywords:
- parameters [C#], named
- named arguments [C#]
- arguments [C#], named
- optional arguments [C#]
- arguments [C#], optional
- parameters [C#], optional
- named and optional arguments [C#]
ms.assetid: 839c960c-c2dc-4d05-af4d-ca5428e54008
caps.latest.revision: 43
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
ms.sourcegitcommit: 1e548df4de2c07934313311a7ffcfae82be76000
ms.openlocfilehash: a7f05e3e0b19bf6457989f8db2b46741cf6b28c1
ms.contentlocale: zh-cn
ms.lasthandoff: 08/29/2017

---
# <a name="named-and-optional-arguments-c-programming-guide"></a>命名实参和可选实参（C# 编程指南）
[!INCLUDE[csharp_dev10_long](~/includes/csharp-dev10-long-md.md)] 介绍命名实参和可选实参。 通过*命名实参*，你可以为特定形参指定实参，方法是将实参与该形参的名称关联，而不是与形参在形参列表中的位置关联。 通过*可选参数*，你可以为某些形参省略实参。 这两种技术都可与方法、索引器、构造函数和委托一起使用。  
  
 使用命名参数和可选参数时，将按实参出现在实参列表（而不是形参列表）中的顺序计算这些实参。  
  
 命名形参和可选形参一起使用时，你可以只为可选形参列表中的少数形参提供实参。 此功能极大地方便了对 COM 接口（例如 Microsoft Office 自动化 API）的调用。  
  
## <a name="named-arguments"></a>命名实参  
 有了命名实参，你将不再需要记住或查找形参在所调用方法的形参列表中的顺序。 每个实参的形参都可按形参名称进行指定。 例如，可以采用标准方式调用计算体重指数 (BMI) 的函数，方法是按照该函数定义的顺序按位置发送体重和身高的实参。  
  
 `CalculateBMI(123, 64);`  
  
 如果不记得形参的顺序，但却知道其名称，则可以按任意顺序（体重优先或身高优先）发送实参。  
  
 `CalculateBMI(weight: 123, height: 64);`  
  
 `CalculateBMI(height: 64, weight: 123);`  
  
 命名实参还可以标识每个实参所表示的含义，从而改进代码的可读性。  
  
 命名实参可以放在位置实参后面，如此处所示。  
  
 `CalculateBMI(123, height: 64);`  
  
 但是，位置自变量不能位于命名的自变量之后。 下面的语句会导致编译器错误。  
  
 `//CalculateBMI(weight: 123, 64);`  
  
## <a name="example"></a>示例  
 以下代码执行本节中的示例。  
  
 [!code-cs[csProgGuideNamedAndOptional#1](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/named-and-optional-arguments_1.cs)]  
  
## <a name="optional-arguments"></a>可选实参  
 方法、构造函数、索引器或委托的定义可以指定其形参为必需还是可选。 任何调用都必须为所有必需的形参提供实参，但可以为可选的形参省略实参。  
  
 每个可选形参都有一个默认值作为其定义的一部分。 如果没有为该形参发送实参，则使用默认值。 默认值必须是以下类型的表达式之一：  
  
-   常量表达式；  
  
-   `new ValType()` 形式的表达式，其中 `ValType` 是值类型，例如 [enum](../../../csharp/language-reference/keywords/enum.md) 或 [struct](../../../csharp/programming-guide/classes-and-structs/structs.md)；  
  
-   [default(ValType)](../../../csharp/programming-guide/statements-expressions-operators/default-value-expressions.md) 形式的表达式，其中 `ValType` 是值类型。  
  
 可选参数定义于参数列表的末尾和必需参数之后。 如果调用方为一系列可选形参中的任意一个形参提供了实参，则它必须为前面的所有可选形参提供实参。 实参列表中不支持使用逗号分隔的间隔。 例如，在以下代码中，使用一个必选形参和两个可选形参定义实例方法 `ExampleMethod`。  
  
 [!code-cs[csProgGuideNamedAndOptional#15](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/named-and-optional-arguments_2.cs)]  
  
 下面对 `ExampleMethod` 的调用会导致编译器错误，原因是为第三个形参而不是为第二个形参提供了实参。  
  
 `//anExample.ExampleMethod(3, ,4);`  
  
 但是，如果知道第三个形参的名称，则可以使用命名实参来完成此任务。  
  
 `anExample.ExampleMethod(3, optionalint: 4);`  
  
 IntelliSense 使用括号表示可选形参，如下图所示。  
  
 ![ExampleMethod 方法的 IntelliSense 快速信息。](../../../csharp/programming-guide/classes-and-structs/media/optional_parameters.png "Optional_Parameters")  
ExampleMethod 中的可选形参  
  
> [!NOTE]
>  此外，还可通过使用 .NET <xref:System.Runtime.InteropServices.OptionalAttribute> 类声明可选参数。 `OptionalAttribute` 形参不需要默认值。  
  
## <a name="example"></a>示例  
 在以下示例中，`ExampleClass` 的构造函数具有一个可选形参。 实例方法 `ExampleMethod` 具有一个必选形参（`required`）和两个可选形参（`optionalstr` 和 `optionalint`）。 `Main` 中的代码演示了可用于调用构造函数和方法的不同方式。  
  
 [!code-cs[csProgGuideNamedAndOptional#2](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/named-and-optional-arguments_3.cs)]  
  
## <a name="com-interfaces"></a>COM 接口  
 命名实参和可选实参，以及对动态对象的支持和其他增强功能大大提高了与 COM API（例如 Office Automation API）的互操作性。  
  
 例如，Microsoft Office Excel 的 [Range](http://go.microsoft.com/fwlink/?LinkId=148196) 接口中的 [AutoFormat](http://go.microsoft.com/fwlink/?LinkId=148201) 方法具有 7 个可选形参。 这些形参如下图所示。  
  
 ![AutoFormat 方法的 IntelliSense 快速信息。](../../../csharp/programming-guide/classes-and-structs/media/autoformat_parameters.png "AutoFormat_Parameters")  
AutoFormat 形参  
  
 在 C# 3.0 以及早期版本中，每个形参都需要一个实参，如下例所示。  
  
 [!code-cs[csProgGuideNamedAndOptional#3](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/named-and-optional-arguments_4.cs)]  
  
 但是，可以通过使用 C# 4.0 中引入的命名实参和可选实参来大大简化对 `AutoFormat` 的调用。 如果不希望更改形参的默认值，则可以通过使用命名实参和可选实参来为可选形参省略实参。 在下面的调用中，仅为 7 个形参中的其中一个指定了值。  
  
 [!code-cs[csProgGuideNamedAndOptional#13](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/named-and-optional-arguments_5.cs)]  
  
 有关详细信息和示例，请参阅[如何：在 Office 编程中使用命名实参和可选实参](../../../csharp/programming-guide/classes-and-structs/how-to-use-named-and-optional-arguments-in-office-programming.md)和[如何：使用 Visual C# 功能访问 Office 互操作性对象](../../../csharp/programming-guide/interop/how-to-access-office-onterop-objects.md)。  
  
## <a name="overload-resolution"></a>重载决策  
 使用命名实参和可选实参将在以下方面对重载决策产生影响：  
  
-   如果方法、索引器或构造函数的每个参数是可选的，或按名称或位置对应于调用语句中的单个自变量，且该自变量可转换为参数的类型，则方法、索引器或构造函数为执行的候选项。  
  
-   如果找到多个候选项，则会将用于首选转换的重载决策规则应用于显式指定的自变量。 将忽略可选形参已省略的实参。  
  
-   如果两个候选项不相上下，则会将没有可选形参的候选项作为首选项，对于这些可选形参，已在调用中为其省略了实参。 这是重载决策中的常规引用的结果，该引用用于参数较少的候选项。  
  
## <a name="c-language-specification"></a>C# 语言规范  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [如何：在 Office 编程中使用命名实参和可选实参](../../../csharp/programming-guide/classes-and-structs/how-to-use-named-and-optional-arguments-in-office-programming.md)   
 [使用类型 dynamic](../../../csharp/programming-guide/types/using-type-dynamic.md)   
 [使用构造函数](../../../csharp/programming-guide/classes-and-structs/using-constructors.md)   
 [使用索引器](../../../csharp/programming-guide/indexers/using-indexers.md)

