---
title: "值 (F#)"
description: "值 (F#)"
keywords: "visual f#, f#, 函数编程"
author: cartermp
ms.author: phcart
ms.date: 05/16/2016
ms.topic: language-reference
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: 5e1e73c3-5adb-4bba-9976-d57f1ff6cd8d
translationtype: Human Translation
ms.sourcegitcommit: 0a01ec92a90d99fafaacbd3f71f5177e5cf94a68
ms.openlocfilehash: 31d28a5ff1bb7d9a88949bcaee895a405a5e7014
ms.lasthandoff: 04/05/2017

---

# <a name="values"></a>值

F# 形式的值是具有特定类型的数量；值可以是整数或浮点数、字符或文本、列表、序列、数组、元组、可区分联合、记录、类类型或函数值。


## <a name="binding-a-value"></a>绑定值
术语“绑定”意指将名称与定义关联。 `let` 关键字将绑定值，如下例所示：

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-1/snippet601.fs)]

值的类型根据定义推断得出。 对于基元类型（例如整数或浮点数），类型由文本的类型确定。 因此，在前面的示例中，编译器将 `b` 的类型推断为 `unsigned int`，而将 `a` 的类型推断为 `int`。 函数值的类型由函数体中的返回值确定。 有关函数值类型的详细信息，请参阅[函数](../functions/index.md)。 有关文本类型的详细信息，请参阅[文本](../literals.md)。


## <a name="why-immutable"></a>为何不可变？
不可变值是指在程序的整个执行过程中无法更改的值。 如果习惯于使用 C++、Visual Basic 或 C# 之类的语言，可能会惊奇地发现，F# 认为不可变值最为重要，而不是可在程序执行过程中赋予新值的变量。 不可变数据是函数编程中的一个重要元素。 在多线程环境中，可由许多不同线程更改的共享可变变量管理起来很困难。 此外，若使用可变变量，有时很难判断变量在传递到另一个函数时是否可更改。

纯粹的函数语言中没有变量，函数的行为与数学函数的行为类似 - 常的严格。 如果过程语言中的代码使用变量赋值来更改值，函数语言中的等效代码会有一个作为输入的不可变值、一个不可变函数以及作为输出的其他不可变值。 这种数学严格性实现了有关程序行为的更严格推理。 通过这种更严格的推理，编译器将能够更严格地检查代码，并更有效地进行优化，还可以让开发人员更轻松地理解和编写正确的代码。 因此，与普通的过程代码相比，函数代码可能更易于调试。

F# 不是纯粹的函数语言，但它完全支持函数编程。 使用不可变值是一种很好的做法，因为这样做可以使代码从函数编程的一个重要方面中获益。


## <a name="mutable-variables"></a>可变变量
可使用关键字 `mutable` 指定可以更改的变量。 F# 中的可变变量范围通常有限，要么是类型字段形式，要么是本地值形式。 具有有限范围的可变值更易于控制，并且被错误修改的可能性也更小。

可以使用 `let` 关键字，采用像定义值一样的方式将初始值赋给可变变量。 但区别在于，随后可以使用 `<-` 运算符将新值赋给可变变量，如下例所示。

[!code-fsharp[Main](../../../../samples/snippets/fsharp/lang-ref-1/snippet602.fs)]
    
## <a name="related-topics"></a>相关主题


|标题|说明|
|-----|-----------|
|[let 绑定](../functions/let-bindings.md)|提供有关使用 `let` 关键字的信息，将名称绑定到值和函数。|
|[函数](../functions/index.md)|提供 F# 中函数的概述。|

## <a name="see-also"></a>另请参阅
[Null 值](null-Values.md)

[F# 语言参考](../index.md)

