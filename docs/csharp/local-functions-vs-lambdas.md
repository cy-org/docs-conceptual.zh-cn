---
title: "本地函数与 Lambda 表达式"
description: "了解为什么选择本地函数比选择 Lambda 表达式更好。"
keywords: "C#, .NET, .NET Core, 最新功能, 新增功能, 本地函数, Lambda 表达式"
author: BillWagner
ms.author: wiwagn
ms.date: 06/27/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 368d1752-3659-489a-97b4-f15d87e49ae3
ms.translationtype: HT
ms.sourcegitcommit: 4582cb0ee091526423cce3fc1d8243029f34f59c
ms.openlocfilehash: 366d7465433f2786960e22418b8aa46ba10e1fd1
ms.contentlocale: zh-cn
ms.lasthandoff: 08/16/2017

---
# <a name="local-functions-compared-to-lambda-expressions"></a>本地函数与 Lambda 表达式比较

乍看之下，[本地函数](programming-guide/classes-and-structs/local-functions.md)和 [lambda 表达式](lambda-expressions.md)非常相似。
根据需要，本地函数可能是更好、更简单的解决方案。

让我们检查一下阶乘算法的本地函数实现和 lambda 表达式实现之间的差异。 首先使用本地函数的版本：

[!code-csharp[LocalFunctionFactorial](../../samples/snippets/csharp/new-in-7/MathUtilities.cs#37_LocalFunctionFactorial "使用本地函数实现阶乘递归")]

将该实现与使用 Lambda 表达式的版本对比：

[!code-csharp[26_LambdaFactorial](../../samples/snippets/csharp/new-in-7/MathUtilities.cs#38_LambdaFactorial "使用 lambda 表达式实现阶乘递归")]

首先，lambda 表达式是通过实例化委托并调用该委托来实现的。 而本地函数是作为方法调用来实现的。
Lambda 表达式所需的实例化意味着额外的内存分配，后者可能是时间关键代码路径中的性能因素。
本地函数不会产生这种开销。 在以上示例中，本地函数版本具有的分配比 lambda 表达式版本少 2 个。

此递归方法非常简单，可以将本地函数作为具有编译器生成名称的私有方法实现。 它与其它私有方法唯一的不同是，它在语义上作用于外部函数。

第二，本地函数可以在定义前进行调用。 必须先声明 Lambda 表达式，然后再进行定义。 这意味着本地函数在递归算法中更易于使用，如上所示。

请注意，使用 lambda 表达式的版本必须先定义 lambda 表达式 `nthFactorial`，然后再对其进行声明并实例化。 否则，会导致分配前引用 `nthFactorial` 时出现编译时错误。
使用本地函数创建递归算法更轻松。

第三，对于 lambda 表达式，编译器必须始终创建匿名类和该类的实例以存储任何由闭包捕获的变量。 请看以下异步示例：

[!code-csharp[TaskLambdaExample](../../samples/snippets/csharp/new-in-7/AsyncWork.cs#36_TaskLambdaExample "使用 lambda 表达式返回方法的任务")]

该 lambda 表达式的闭包包含 `address`、`index` 和 `name` 变量。 就本地函数而言，实现闭包的对象可能为 `struct` 类型。 这将保存在分配上。

> [!NOTE]
> 等效于此方法的本地函数还将类用于闭包。 实现详细信息包括本地函数的闭包是作为 `class` 还是 `struct` 实现。 本地函数可能使用 `struct`，而 lambda 将始终使用 `class`。

[!code-csharp[TaskLocalFunctionExample](../../samples/snippets/csharp/new-in-7/AsyncWork.cs#29_TaskExample "使用本地函数的 Task 返回方法")]

在本示例中尚未演示的最后一个优点是，可将本地函数作为迭代器实现，使用 `yield return` 语法生成一系列值。

虽然本地函数对 lambda 表达式可能有点冗余，但实际上它们的目的和用法都不一样。
如果想要编写仅从上下文或其他方法中调用的函数，则使用本地函数更高效。

