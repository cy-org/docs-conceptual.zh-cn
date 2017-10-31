---
title: "Main() 和命令行参数（C# 编程指南）"
ms.date: 2017-08-02
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- CS5001
- main_CSharpKeyword
- Main
dev_langs:
- CSharp
helpviewer_keywords:
- Main method [C#]
- C# language, command-line arguments
- arguments [C#], command-line
- command line [C#], arguments
- command-line arguments [C#], Main method
ms.assetid: 73a17231-cf96-44ea-aa8a-54807c6fb1f4
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
ms.sourcegitcommit: d019d1c5757a961c03439d756e808ae13fd8a67b
ms.openlocfilehash: 51408654abd0dcd2f7159438b507c44bd579bfd9
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="main-and-command-line-arguments-c-programming-guide"></a>Main() 和命令行参数（C# 编程指南）

`Main` 方法是 C# 应用程序的入口点。 （库和服务不要求使用 `Main` 方法作为入口点）。`Main` 方法是应用程序启动后调用的第一个方法。

 C# 程序中只能有一个入口点。 如果多个类包含 `Main` 方法，必须使用 **/main** 编译器选项来编译程序，以指定将哪个 `Main` 方法用作入口点。 有关详细信息，请参阅 [/main（C# 编译器选项）](../../../csharp/language-reference/compiler-options/main-compiler-option.md)。

 [!code-cs[csProgGuideMain#17](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/main-and-command-line-arguments_1.cs)]

## <a name="overview"></a>概述

- `Main` 方法是可执行程序的入口点，也是程序控制开始和结束的位置。
- `Main` 在类或结构中声明。 `Main` 必须是[静态](../../../csharp/language-reference/keywords/static.md)方法，不得为[公共](../../../csharp/language-reference/keywords/public.md)方法。 （在前面的示例中，它获得的是[私有](../../../csharp/language-reference/keywords/private.md)成员的默认访问权限）。封闭类或结构不一定要是静态的。
- `Main` 可以具有 `void`、`int`，或者以 C# 7.1、`Task` 或 `Task<int>` 返回类型开头。
- 当且仅当 `Main` 返回 `Task` 或 `Task<int>` 时，`Main` 的声明可包括 [`async`](../../language-reference/keywords/async.md) 修饰符。 请注意，该操作可明确排除 `async void Main` 方法。
- 使用或不使用包含命令行自变量的 `string[]` 参数声明 `Main` 方法都行。 使用 [!INCLUDE[vsprvs](~/includes/vsprvs-md.md)] 创建 Windows 应用程序时，可以手动添加此形参，也可以使用 <xref:System.Environment> 类来获取命令行实参。 参数被读取为从零开始编制索引的命令行自变量。 与 C 和 C++ 不同，程序的名称不被视为第一个命令行自变量。

添加 `async`、`Task` 和 `Task<int>` 返回类型可简化控制台应用程序需要启动时的程序代码，以及 `Main` 中的 `await` 异步操作。

## <a name="c-language-specification"></a>C# 语言规范

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>请参阅
[使用 csc.exe 生成的命令行](../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)
[C# 编程指南](../../../csharp/programming-guide/index.md)
[方法](../../../csharp/programming-guide/classes-and-structs/methods.md)
[在 C# 程序内部](../../../csharp/programming-guide/inside-a-program/index.md)

