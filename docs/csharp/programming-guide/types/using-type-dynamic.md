---
title: "使用类型 dynamic（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- dynamic [C#], about dynamic type
- dynamic type [C#]
ms.assetid: 3828989d-c967-4a51-b948-857ebc8fdf26
caps.latest.revision: 30
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
ms.openlocfilehash: 36e10ef6a63aae2e901be50b9286370caec50e6a
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="using-type-dynamic-c-programming-guide"></a>使用类型 dynamic（C# 编程指南）
[!INCLUDE[csharp_dev10_long](~/includes/csharp-dev10-long-md.md)] 引入了一个新类型 `dynamic`。 该类型是一种静态类型，但类型为 `dynamic` 的对象会跳过静态类型检查。 大多数情况下，该对象就像具有类型 `object` 一样。 在编译时，将假定类型化为 `dynamic` 的元素支持任何操作。 因此，不必考虑对象是从 COM API、从动态语言（例如 IronPython）、从 HTML 文档对象模型 (DOM)、从反射还是从程序中的其他位置获取自己的值。 但是，如果代码无效，则在运行时会捕获到错误。  
  
 例如，如果以下代码中的实例方法 `exampleMethod1` 只有一个形参，则编译器会将对该方法的第一个调用 `ec.exampleMethod1(10, 4)` 识别为无效，因为它包含两个实参。 该调用将导致编译器错误。 编译器不会检查对该方法的第二个调用 `dynamic_ec.exampleMethod1(10, 4)`，因为 `dynamic_ec` 的类型为 `dynamic`。 因此，不会报告编译器错误。 但是，该错误不会被无限期疏忽。 它将在运行时被捕获，并导致运行时异常。  
  
 [!code-cs[CsProgGuideTypes#50](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-type-dynamic_1.cs)]  
  
 [!code-cs[CsProgGuideTypes#56](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-type-dynamic_2.cs)]  
  
 在这些示例中，编译器的作用是将有关每个语句的预期作用的信息一起打包到类型化为 `dynamic` 的对象或表达式。 在运行时，将对存储的信息进行检查，并且任何无效的语句都将导致运行时异常。  
  
 大多数动态操作的结果是其本身 `dynamic`。 例如，如果将鼠标指针放在以下示例中使用的 `testSum` 上，则 IntelliSense 将显示类型“（局部变量）dynamic testSum”。  
  
 [!code-cs[CsProgGuideTypes#51](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-type-dynamic_3.cs)]  
  
 结果不是 `dynamic` 的操作包括从 `dynamic` 到另一种类型的转换，以及包括类型为 `dynamic` 的参数的构造函数调用。 例如，以下声明中 `testInstance` 的类型为 `ExampleClass`，而不是 `dynamic`。  
  
 [!code-cs[CsProgGuideTypes#52](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-type-dynamic_4.cs)]  
  
 下一节“转换”中介绍了转换示例。  
  
## <a name="conversions"></a>转换  
 动态对象和其他类型之间的转换非常简单。 这样，开发人员将能够在动态行为和非动态行为之间切换。  
  
 任何对象都可隐式转换为动态类型，如以下示例所示。  
  
 [!code-cs[CsProgGuideTypes#53](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-type-dynamic_5.cs)]  
  
 反之，隐式转换也可动态地应用于类型为 `dynamic` 的任何表达式。  
  
 [!code-cs[CsProgGuideTypes#54](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-type-dynamic_6.cs)]  
  
## <a name="overload-resolution-with-arguments-of-type-dynamic"></a>使用类型为 dynamic 的参数重载决策  
 如果方法调用中的一个或多个参数的类型为 `dynamic`，或者方法调用的接收方的类型为 `dynamic`，则会在运行时（而不是在编译时）进行重载决策。 在以下示例中，如果唯一可访问的 `exampleMethod2` 方法定义为接受字符串参数，则将 `d1` 作为参数发送不会导致编译器错误，但却会导致运行时异常。 重载决策之所以会在运行时失败，是因为 `d1` 的运行时类型为 `int`，而 `exampleMethod2` 要求为字符串。  
  
 [!code-cs[CsProgGuideTypes#55](../../../csharp/programming-guide/nullable-types/codesnippet/CSharp/using-type-dynamic_7.cs)]  
  
## <a name="dynamic-language-runtime"></a>动态语言运行时  
 动态语言运行时 (DLR) 是 [!INCLUDE[net_v40_short](~/includes/net-v40-short-md.md)] 中的一个新 API。 它提供了支持 C# 中 `dynamic` 类型的基础结构，还提供了 IronPython 和 IronRuby 等动态编程语言的实现。 有关 DLR 的详细信息，请参阅[动态语言运行时概述](../../../framework/reflection-and-codedom/dynamic-language-runtime-overview.md)。  
  
## <a name="com-interop"></a>COM 互操作  
 [!INCLUDE[csharp_dev10_long](~/includes/csharp-dev10-long-md.md)] 包括若干功能，这些功能改善了与 COM API（例如 Office 自动化 API）的互操作体验。 这些改进之处包括 `dynamic` 类型以及[命名参数和可选参数](../../../csharp/programming-guide/classes-and-structs/named-and-optional-arguments.md)的用法。  
  
 通过将类型指定为 `object`，许多 COM 方法都允许参数类型和返回类型发生变化。 这样，就必须显式强制转换值，以便与 C# 中的强类型变量保持协调。 如果使用 [/link（C# 编译器选项）](../../../csharp/language-reference/compiler-options/link-compiler-option.md)选项进行编译，则可以通过引入 `dynamic` 类型将 COM 签名中出现的 `object` 看作是 `dynamic` 类型，从而避免大量的强制转换。 例如，以下语句对比了在使用 `dynamic` 类型和不使用 `dynamic` 类型的情况下如何访问 Microsoft Office Excel 电子表格中的单元格。  
  
 [!code-cs[csOfficeWalkthrough#12](../../../csharp/programming-guide/interop/codesnippet/CSharp/using-type-dynamic_8.cs)]  
  
 [!code-cs[csOfficeWalkthrough#13](../../../csharp/programming-guide/interop/codesnippet/CSharp/using-type-dynamic_9.cs)]  
  
## <a name="related-topics"></a>相关主题  
  
|标题|描述|  
|-----------|-----------------|  
|[动态](../../../csharp/language-reference/keywords/dynamic.md)|描述 `dynamic` 关键字的用法。|  
|[动态语言运行时概述](../../../framework/reflection-and-codedom/dynamic-language-runtime-overview.md)|提供有关 DLR 的概述，DLR 是一种运行时环境，它将一组适用于动态语言的服务添加到公共语言运行时 (CLR)。|  
|[演练：创建和使用动态对象](../../../csharp/programming-guide/types/walkthrough-creating-and-using-dynamic-objects.md)|提供有关如何创建自定义动态对象以及创建访问 `IronPython` 库的对象的分步说明。|  
|[如何：通过使用 Visual C# 功能访问 Office 互操作对象](../../../csharp/programming-guide/interop/how-to-access-office-onterop-objects.md)|演示如何创建一个项目，该项目使用命名参数和可选参数、`dynamic` 类型以及可简化对 Office API 对象的访问的其他增强功能。|

