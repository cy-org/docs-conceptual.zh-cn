---
title: "函数编程与命令式编程 (C#)"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 5e35c5a0-c949-422a-873b-fca6b2254f57
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: e26cf7946a2ee8d83683a31666b13c6685fbc045
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="functional-programming-vs-imperative-programming-c"></a>函数编程与命令式编程 (C#)
本主题对函数编程和更传统的命令性（过程性）编程进行比较。  
  
## <a name="functional-programming-vs-imperative-programming"></a>函数编程与命令式编程  
 为支持使用纯函数方法解决问题，特此创建了函数编程范例。 函数编程是一种声明性编程形式。 相比之下，大多数主流语言，包括面向对象的编程 (OOP) 语言（如 C#、Visual Basic、C++ 和 Java）主要都是为支持命令性（过程性）编程而设计的。  
  
 使用命令性方法时，开发人员编写的代码应严格细致地说明计算机为完成目标而必须执行的步骤。 这有时称为算法编程。 相比之下，函数方法涉及将问题编成一组要执行的函数。 您要仔细地定义每个函数的输入值和每个函数的返回值。 下表说明了这两种方法之间的一些总体差别。  
  
|特征|命令性方法|函数方法|  
|--------------------|-------------------------|-------------------------|  
|程序员关注点|如何执行任务（算法）和如何跟踪状态更改。|需要哪些信息和需要进行什么转换。|  
|状态更改|重要。|不存在。|  
|执行顺序|重要。|不太重要。|  
|主要流控制|循环、条件和函数（方法）调用。|函数调用，包括递归。|  
|主要操作单元|结构或类的实例。|作为第一类对象和数据集合的函。|  
  
 虽然多数语言旨在支持特定编程范例，但许多通用语言具有很高的灵活性，能够支持多个范例。 例如，包含函数指针的多数语言都可用于可靠地支持函数编程。 此外，C# 包含显式语言扩展以支持函数编程，包括 lambda 表达式和类型推理。 LINQ 技术是一种声明性函数编程形式。  
  
## <a name="functional-programming-using-xslt"></a>使用 XSLT 的函数编程  
 很多 XSLT 开发人员熟悉纯函数方法。 开发 XSLT 样式表的最有效方式是将每个模板视为一个独立的、可组合的转换。 执行顺序完全不重要。 XSLT 不允许副作用（但用于执行过程代码的转义机制除外，它可能引入可导致功能不纯的副作用）。 不过，虽然 XSLT 是一个有效的工具，但其某些特性并不是最佳的。 例如，在 XML 中表示编程构造会使代码相对繁琐，因此难于维护。 而且，流控制对递归的依赖性很强，因此会使代码的可读性较差。 有关 XSLT 的详细信息，请参阅 [XSLT 转换](../../../../standard/data/xml/xslt-transformations.md)。  
  
 但 XSLT 在使用纯函数方法将 XML 从一种形状转换为另一种形状方面确有其自身的价值。 使用 LINQ to XML 的纯函数编程在许多方面与 XSLT 类似。 但 LINQ to XML 和 C# 中引入的编程构造允许你编写比 XSLT 更具可读性且更容易维护的纯函数转换。  
  
## <a name="advantages-of-pure-functions"></a>纯函数的优点  
 以纯函数形式实现函数转换的主要原因是纯函数是可以组合的：即独立并且无状态。 这些特性可带来很多好处，包括以下各项：  
  
-   可读性和可维护性更高。 这是因为每个函数都设计为在给定参数的情况下完成特定任务。 函数不依赖于任何外部状态。  
  
-   更易于反复开发。 因为代码更容易重构，因此对设计的更改通常更容易实现。 例如，假设您编写了一个复杂的转换，但随后发现某些代码在转换中重复多次。 如果您通过纯方法重构，则可以随意调用纯方法而不必担心会有什么副作用。  
  
-   更易于测试和调试。 由于纯函数更容易单独测试，因此您可以编写使用典型值、有效边缘情况和无效边缘情况调用纯函数的测试代码。  
  
## <a name="transitioning-for-oop-developers"></a>针对 OOP 开发人员的转换  
 在传统的面向对象编程 (OOP) 中，大多数开发人员都习惯于命令性/过程式编程。 若要切换到纯函数式开发，开发人员必须转变开发思路和方法。  
  
 为了解决问题，OOP 开发人员需要设计类层次结构，注意进行恰当的包装并按照类约定进行思考。 对象类型的行为和状态至为重要，并提供语言功能（如类、接口、继承和多态性）以解除这些问题。  
  
 相比之下，函数编程将计算机的操作问题处理为数据集合的纯函数转换计算。 函数编程可以避免使用状态和可变数据，并改为强调函数的应用。  
  
 但 C# 并不要求完全转变为函数编程，因为它同时支持命令性编程和函数编程方法。 开发人员可以选择哪种方法最适合特定方案。 实际上，程序通常组合使用这两种方法。  
  
## <a name="see-also"></a>另请参阅  
 [纯函数转换简介 (C#)](../../../../csharp/programming-guide/concepts/linq/introduction-to-pure-functional-transformations.md)   
 [XSLT 转换](../../../../standard/data/xml/xslt-transformations.md)   
 [重构为纯函数 (C#)](../../../../csharp/programming-guide/concepts/linq/refactoring-into-pure-functions.md)

