---
title: "using static 指令（C# 参考）"
ms.date: 2017-03-10
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- using static directive [C#]
ms.assetid: 8b8f9e34-c75e-469b-ba85-6f2eb4090314
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
ms.openlocfilehash: b7d69d0262ba6f450e2cc0d5b30692bba181f9d9
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="using-static-directive-c-reference"></a>using static 指令（C# 参考）

`using static` 指令指定无需指定类型名称即可访问其静态成员的类型。 语法为：

```csharp
using static <fully-qualified-type-name>
```

其中，*fully-qualified-type-name* 是无需指定类型名称即可访问其静态成员的类型的名称。 如果不提供完全限定的类型名称（完整的命名空间名称以及类型名称），则 C# 将生成编译器错误 CS0246：“找不到‘<type-name>’的类型或命名空间名称。”

`using static` 指令适用于任何具有静态成员的类型，即使该类型还具有实例成员。 但是，只能通过类型实例来调用实例成员。

`using static` 指令是在 C# 6 中引入的。

## <a name="remarks"></a>备注
 
通常，调用某个静态成员时，即会提供类型名称以及成员名称。 重复输入相同的类型名称来调用该类型的成员将生成详细的晦涩代码。 例如，`Circle` 类的以下定义引用 @System.Math 类的成员数。
  
[!code-cs[using-static#1](../../../../samples/snippets/csharp/language-reference/keywords/using/using-static1.cs#1)]

通过消除每次引用成员时，显式引用 @System.Math 类的需求，`using static` 指令将生成更简洁的代码：

[!code-cs[using-static#2](../../../../samples/snippets/csharp/language-reference/keywords/using/using-static2.cs#1)]

`using static` 仅导入可访问的静态成员和指定类型中声明的嵌套类型。  不导入继承的成员。  可以从任何带 using static 指令的已命名类型导入，包括 Visual Basic 模块。  如果 F# 顶级函数在元数据中显示为一个已命名类型（其名称是有效的 C# 标识符）的静态成员，则可以导入该 F# 函数。  
  
 `using static` 使指定类型中声明的扩展方法可用于扩展方法查找。  但是，扩展方法的名称不导入到代码中非限定引用的作用域中。  
  
 同一编译单元或命名空间中通过不同 `using static` 命令从不同类型导入的具有相同名称的方法组成一个方法组。  这些方法组内的重载解决方法遵循一般 C# 规则。  
  
## <a name="example"></a>示例

以下示例使用 `using static` 指令来提供 @System.Console、@System.Math 和 @System.String 类的静态成员，而无需指定其类型名称。

[!code-cs[using-static#3](../../../../samples/snippets/csharp/language-reference/keywords/using/using-static3.cs)]

在此示例中，`using static` 指令也已经应用于 @System.Double 类型。 这使得在未指定类型名称情况下调用 @System.Double.TryParse(System.String,System.Double@) 方法成为可能。 但是，如此创建的代码可读性较差，因为这样有必要检查 `using static` 语句，以确定所调用的数值类型的 `TryParse` 方法。

## <a name="see-also"></a>请参阅

[using 指令](using-directive.md)   
[C# 参考](../../../csharp/language-reference/index.md)   
[C# 关键字](../../../csharp/language-reference/keywords/index.md)   
[Using 命名空间](../../../csharp/programming-guide/namespaces/using-namespaces.md)   
[命名空间关键字](../../../csharp/language-reference/keywords/namespace-keywords.md)   
[命名空间](../../../csharp/programming-guide/namespaces/index.md)   

