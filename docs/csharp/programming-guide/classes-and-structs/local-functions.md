---
title: "本地函数（C# 编程指南）"
ms.date: 2017-06-14
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- local functions [C#]
author: rpetrusha
ms.author: ronpet
ms.translationtype: HT
ms.sourcegitcommit: 4582cb0ee091526423cce3fc1d8243029f34f59c
ms.openlocfilehash: 069a6411e3d89fa1c2dba57f0b83badff1342763
ms.contentlocale: zh-cn
ms.lasthandoff: 08/16/2017

---
# <a name="local-functions-c-programming-guide"></a>本地函数（C# 编程指南）

从 C# 7 开始，C# 支持本地函数。 本地函数是一种嵌套在另一成员中的类型的私有方法。 仅能从其包含成员中调用它们。 可以在以下位置中声明和调用本地函数：

- 方法（尤其是迭代器方法和异步方法）
- 构造函数
- 属性访问器
- 事件访问器
- 匿名方法
- Lambda 表达式
- 终结器
- 其他本地函数

但是，不能在 expression-bodied 成员中声明本地函数。

> [!NOTE]
> 在某些情况下，可以使用 lambda 表达式实现本地函数也支持的功能。 有关比较，请参阅[本地函数与 Lambda 表达式比较](../../local-functions-vs-lambdas.md)。

本地函数可使代码意图明确。 任何读取代码的人都可以看到，此方法不可调用，包含方法除外。 对于团队项目，它们也使得其他开发人员无法直接从类或结构中的其他位置错误调用此方法。
 
## <a name="local-function-syntax"></a>本地函数语法

本地函数被定义为包含成员中的嵌套方法。 其定义具有以下语法：

```txt
<modifiers: async | unsafe> <return-type> <method-name> <parameter-list>
```

本地函数可以使用 [async](../../language-reference/keywords/async.md) 和 [unsafe](../../language-reference/keywords/unsafe.md) 修饰符。 

请注意，在包含成员中定义的所有本地变量（包括其方法参数）都可在本地函数中访问。 

与方法定义不同，本地函数定义不能包含下列元素：

- 成员访问修饰符。 因为所有本地函数都是私有的，包括访问修饰符（如 `private` 关键字）会生成编译器错误 CS0106“修饰符‘private’对于此项无效”。
 
- [Static](../../language-reference/keywords/static.md) 关键字。 包括 `static` 关键字将生成编译器错误 CS0106“修饰符‘static’对于此项无效”。

此外，属性不能应用于本地函数或其参数和类型参数。 
 
以下示例定义了一个名为 `AppendPathSeparator` 的本地函数，该函数对于名为 `GetText` 的方法是私有的：
   
[!code-cs[LocalFunctionExample](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/local-functions1.cs)]  
   
## <a name="local-functions-and-exceptions"></a>本地函数和异常

本地函数的一个实用功能是可以允许立即显示异常。 对于方法迭代器，仅在枚举返回的序列时才显示异常，而非在检索迭代器时。 对于异步方法，在等待返回的任务时，将观察到异步方法中引发的任何异常。 

以下示例定义 `OddSequence` 方法，用于枚举指定范围之间的奇数。 因为它会将一个大于 100 的数字传递到 `OddSequence` 迭代器方法，该方法将引发 <xref:System.ArgumentOutOfRangeException>。 如示例中的输出所示，仅当循环访问数字时才显示异常，而非检索迭代器时。

[!code-cs[LocalFunctionIterator1](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/local-functions-iterator1.cs)] 

相反，可以在执行验证时和通过从本地函数返回迭代器检索迭代器之前引发异常，如以下示例所示。

[!code-cs[LocalFunctionIterator2](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/local-functions-iterator2.cs)]

可以通过类似的方式使用本地函数来处理异步操作之外的异常。 异步方法中引发的异常通常都需要检查 <xref:System.AggregateException> 的内部异常。 本地函数允许代码快速失败，并允许同步引发和观察异常。

以下示例使用名为 `GetMultipleAsync` 的异步方法暂停指定的秒数并返回一个值，该值是该秒数的任意倍数。 最大延迟为 5 秒；如果该值大于 5，则结果为 <xref:System.ArgumentOutOfRangeException>。 如以下示例所示，开始执行 `GetMultipleAsync` 方法后，将值 6 传递到 `GetMultipleAsync` 方法时引发的异常将在 <xref:System.AggregateException> 中进行包装。

[!code-cs[LocalFunctionAsync`](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/local-functions-async1.cs)] 

正如处理方法迭代器一样，可以在调用异步方法之前重构本示例中的代码以执行验证。 如以下示例中的输出所示，<xref:System.ArgumentOutOfRangeException> 不在 <x:System.AggregateException> 中进行包装。

[!code-cs[LocalFunctionAsync`](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/local-functions-async2.cs)] 

## <a name="see-also"></a>请参阅
[方法](methods.md)

