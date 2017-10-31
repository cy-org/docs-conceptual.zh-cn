---
title: "使用命名空间（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- cs.names
dev_langs:
- CSharp
helpviewer_keywords:
- fully qualified names [C#]
- namespaces [C#], how to use
ms.assetid: 1fe8bf39-addc-438a-bd9e-86410e32381d
caps.latest.revision: 26
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
ms.openlocfilehash: 61b5d78f1c4924e3858c14876d36e52d4ee46ceb
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="using-namespaces-c-programming-guide"></a>使用命名空间（C# 编程指南）
在 C# 编程中，命名空间在两个方面被大量使用。 首先，.NET Framework 类使用命名空间来组织它的众多类。 其次，在较大的编程项目中，声明自己的命名空间可以帮助控制类名称和方法名称的范围。  
  
## <a name="accessing-namespaces"></a>访问命名空间  
 大多数 C# 应用程序以 `using` 指令开头。 本部分列出了应用程序将频繁使用的命名空间，使程序员避免在每次使用包含在命名空间中的方法时都要指定完全限定名称。  
  
 例如，通过包括行：  
  
 [!code-cs[csProgGuide#1](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/using-namespaces_1.cs)]  
  
 在程序的开始，程序员可以使用代码：  
  
 [!code-cs[csProgGuide#31](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/using-namespaces_2.cs)]  
  
 而不是：  
  
 [!code-cs[csProgGuide#30](../../../csharp/programming-guide/inside-a-program/codesnippet/CSharp/using-namespaces_3.cs)]  
  
## <a name="namespace-aliases"></a>命名空间别名  
 [Using 指令](../../../csharp/language-reference/keywords/using-directive.md)还可用于创建[命名空间](../../../csharp/language-reference/keywords/namespace.md)的别名。 例如，如果使用之前编写的含嵌套命名空间的命名空间，建议你声明一个别名，特别提供一种快速的引用方法，如以下示例所示：  
  
 [!code-cs[csProgGuideNamespaces#7](../../../csharp/programming-guide/namespaces/codesnippet/CSharp/using-namespaces_4.cs)]  
  
## <a name="using-namespaces-to-control-scope"></a>使用命名空间控制范围  
 `namespace` 关键字用于声明范围。 在项目内创建范围有助于整理代码，并允许创建全局唯一类型。 在下面的示例中，名为 `SampleClass` 的类在两个命名空间中定义，其中一个嵌套在另一个之中。 [。运算符](../../../csharp/language-reference/operators/member-access-operator.md) 用于区分调用的方法。  
  
 [!code-cs[csProgGuideNamespaces#8](../../../csharp/programming-guide/namespaces/codesnippet/CSharp/using-namespaces_5.cs)]  
  
## <a name="fully-qualified-names"></a>完全限定名  
 命名空间和类型具有指示逻辑层次结构的完全限定名称所描述的唯一标题。 例如，语句 `A.B` 意味着 `A` 是命名空间或类型的名称，而 `B` 嵌套在其中。  
  
 以下示例中具有嵌套的类和命名空间。 完全限定名称表示为跟随每个实体的注释。  
  
 [!code-cs[csProgGuideNamespaces#9](../../../csharp/programming-guide/namespaces/codesnippet/CSharp/using-namespaces_6.cs)]  
  
 在前面的代码片段中：  
  
-   命名空间 `N1` 是全局命名空间的成员。 其完全限定名称为 `N1`。  
  
-   命名空间 `N2` 是 `N1` 的成员。 其完全限定名称为 `N1.N2`。  
  
-   类 `C1` 是 `N1` 的成员。 其完全限定名称为 `N1.C1`。  
  
-   类名 `C2` 在此代码中使用了两次。 但完全限定名称是唯一的。 `C2` 的第一个实例在 `C1` 中声明；因此，其完全限定名称是：`N1.C1.C2`。 `C2` 的第二个实例在命名空间 `N2` 中声明；因此，其完全限定名称是 `N1.N2.C2`。  
  
 使用前面的代码段，可向命名空间 `N1.N2` 添加新的类成员 `C3`，如下所示：  
  
 [!code-cs[csProgGuideNamespaces#10](../../../csharp/programming-guide/namespaces/codesnippet/CSharp/using-namespaces_7.cs)]  
  
 一般情况下，使用 `::` 来引用命名空间别名，或使用 `global::` 来引用全局命名空间，以及使用 `.` 来限定类型或成员。  
  
 将 `::` 与引用类型而非引用命名空间的别名一起使用是错误的。 例如:   
  
 [!code-cs[csProgGuideNamespaces#11](../../../csharp/programming-guide/namespaces/codesnippet/CSharp/using-namespaces_8.cs)]  
  
 [!code-cs[csProgGuideNamespaces#12](../../../csharp/programming-guide/namespaces/codesnippet/CSharp/using-namespaces_9.cs)]  
  
 请记住，单词 `global` 不是预定义的别名；因此，`global.X` 不具有任何特殊含义。 仅当将其与 `::` 一起使用时，它才具有特殊意义。  
  
 定义名为 global 的别名时将生成编译器警告 CS0440，因为 `global::` 始终引用全局命名空间而非别名。 例如，以下行将生成该警告：  
  
 [!code-cs[csProgGuideNamespaces#13](../../../csharp/programming-guide/namespaces/codesnippet/CSharp/using-namespaces_10.cs)]  
  
 将 `::` 与别名一起使用是一个不错的主意，可防止意外引入其他类型。 例如，请考虑以下示例：  
  
 [!code-cs[csProgGuideNamespaces#14](../../../csharp/programming-guide/namespaces/codesnippet/CSharp/using-namespaces_11.cs)]  
  
 [!code-cs[csProgGuideNamespaces#15](../../../csharp/programming-guide/namespaces/codesnippet/CSharp/using-namespaces_12.cs)]  
  
 这是可行的，但如果随后要引入名为 `Alias` 的类型，`Alias.` 将改为绑定到该类型。 使用 `Alias::Exception` 确保 `Alias` 被视为命名空间别名，而不被误解为类型。  
  
 有关 `global` 别名的详细信息，请参阅主题[如何：使用全局命名空间别名](../../../csharp/programming-guide/namespaces/how-to-use-the-global-namespace-alias.md)。  
  
## <a name="see-also"></a>另请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [命名空间](../../../csharp/programming-guide/namespaces/index.md)   
 [命名空间关键字](../../../csharp/language-reference/keywords/namespace-keywords.md)   
 [。运算符](../../../csharp/language-reference/operators/member-access-operator.md)   
 [:: Operator](../../../csharp/language-reference/operators/namespace-alias-qualifer.md)   
 [extern](../../../csharp/language-reference/keywords/extern.md)

