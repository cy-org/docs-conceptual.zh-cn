---
title: "泛型（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- C# language, generics
- generics [C#]
ms.assetid: 75ea8509-a4ea-4e7a-a2b3-cf72482e9282
caps.latest.revision: 23
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
ms.openlocfilehash: de81058173b0985577474e8601aa84d4e83336a5
ms.contentlocale: zh-cn
ms.lasthandoff: 08/29/2017

---
# <a name="generics-c-programming-guide"></a>泛型（C# 编程指南）
C# 语言和公共语言运行时 (CLR) 的 2.0 版本中添加了泛型。 泛型将类型参数的概念引入 .NET Framework，这样就可以设计具有以下特征的类和方法：在客户端代码声明并初始化这些类和方法之前，这些类和方法会延迟指定一个或多个类型。 例如，通过使用泛型类型参数 T，可以编写其他客户端代码能够使用的单个类，而不会产生运行时转换或装箱操作的成本或风险，如下所示：  
  
 [!code-cs[csProgGuideGenerics#1](../../../csharp/programming-guide/generics/codesnippet/CSharp/index_1.cs)]  
  
## <a name="generics-overview"></a>泛型概述  
  
-   使用泛型类型可以最大限度地重用代码、保护类型安全性以及提高性能。  
  
-   泛型最常见的用途是创建集合类。  
  
-   .NET Framework 类库在 <xref:System.Collections.Generic> 命名空间中包含几个新的泛型集合类。 应尽可能使用这些类来代替某些类，如 <xref:System.Collections> 命名空间中的 <xref:System.Collections.ArrayList>。  
  
-   可以创建自己的泛型接口、泛型类、泛型方法、泛型事件和泛型委托。  
  
-   可以对泛型类进行约束以访问特定数据类型的方法。  
  
-   在泛型数据类型中所用类型的信息可在运行时通过使用反射来获取。  
  
## <a name="related-sections"></a>相关章节  
 更多相关信息：  
  
-   [泛型介绍](../../../csharp/programming-guide/generics/introduction-to-generics.md)  
  
-   [泛型的优点](../../../csharp/programming-guide/generics/benefits-of-generics.md)  
  
-   [泛型类型参数](../../../csharp/programming-guide/generics/generic-type-parameters.md)  
  
-   [类型参数的约束](../../../csharp/programming-guide/generics/constraints-on-type-parameters.md)  
  
-   [泛型类](../../../csharp/programming-guide/generics/generic-classes.md)  
  
-   [泛型接口](../../../csharp/programming-guide/generics/generic-interfaces.md)  
  
-   [泛型方法](../../../csharp/programming-guide/generics/generic-methods.md)  
  
-   [泛型委托](../../../csharp/programming-guide/generics/generic-delegates.md)  
  
-   [C++ 模板和 C# 泛型之间的区别](../../../csharp/programming-guide/generics/differences-between-cpp-templates-and-csharp-generics.md)  
  
-   [泛型和反射](../../../csharp/programming-guide/generics/generics-and-reflection.md)  
  
-   [运行时中的泛型](../../../csharp/programming-guide/generics/generics-in-the-run-time.md)  
  
-   [.NET Framework 类库中的泛型](../../../csharp/programming-guide/generics/generics-in-the-net-framework-class-library.md)  
  
## <a name="c-language-specification"></a>C# 语言规范  
 有关详细信息，请参阅 [C# 语言规范](../../../csharp/language-reference/language-specification/index.md)。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Collections.Generic>   
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [类型](../../../csharp/programming-guide/types/index.md)   
 [\<typeparam>](../../../csharp/programming-guide/xmldoc/typeparam.md)   
 [\<typeparamref>](../../../csharp/programming-guide/xmldoc/typeparamref.md)

