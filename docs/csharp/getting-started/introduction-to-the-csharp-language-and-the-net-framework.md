---
title: "C# 语言和 .NET Framework 介绍"
description: "了解 C# 和 .NET 的基础知识。 概述了 C# 语言和 .NET 生态系统。"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- C# language, about C# language
- Visual C#, about
ms.assetid: 0a2dff4e-cd84-42ff-8141-e89889b24081
caps.latest.revision: 32
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
ms.sourcegitcommit: 9bb64ea7199f5699ff166d1affb7f8126dcc6612
ms.openlocfilehash: c7fac541dd233111bfffb9c0f67ba048f8d271be
ms.contentlocale: zh-cn
ms.lasthandoff: 09/25/2017

---
# <a name="introduction-to-the-c-language-and-the-net-framework"></a>C# 语言和 .NET Framework 介绍
C# 是类型安全的面向对象的精妙语言，可帮助开发者生成在 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] 上运行的各种安全可靠的应用程序。 C# 可用于创建 Windows 客户端应用程序、XML Web service、分布式组件、客户端服务器应用程序、数据库应用程序等。 Visual C# 提供高级代码编辑器、方便使用的用户界面设计器、集成调试器和其他许多工具，以便你可以更轻松地开发基于 C# 语言和 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] 的应用程序。  
  
> [!NOTE]
> 阅读 [!INCLUDE[csprcs](~/includes/csprcs-md.md)] 文档的前提是，你已了解基本的编程概念。 如果是完完全全的初学者，不妨探索 [!INCLUDE[csprcsxpr](~/includes/csprcsxpr-md.md)]（可从 Web 获取）。 还可以利用介绍 C# 的书籍和 Web 资源来学习实用的编程技巧。  
  
## <a name="c-language"></a>C# 语言  
 C# 语法高度重视表达，但学习起来也很简单轻松。 任何熟悉 C、C++ 或 Java 的人都可以立即认出 C# 的大括号语法。 通常情况下，了解上述任何一种语言的开发者可以在很短的时间内就开始使用 C# 高效工作。 C# 语法简化了 C++ 的许多复杂操作，并提供强大功能，如可以为 null 的值类型、枚举、委托、lambda 表达式和直接内存访问，而 Java 并不提供这些功能。 C# 不仅支持泛型方法和类型，提升了类型安全性和性能，还支持迭代器，以便集合类的实现者可以定义方便客户端代码使用的自定义迭代行为。 [!INCLUDE[vbteclinqext](~/includes/vbteclinqext-md.md)] 表达式让强类型查询成为最高级的语言构造。  
  
 作为面向对象的语言，C# 支持封装、继承和多形性这些概念。 所有变量和方法（包括作为应用程序入口点的 `Main` 方法）都封装在类定义中。 虽然类可能会直接继承一个父类，但可以实现任意数量的接口。 若要用方法重写父类中的虚方法，必须使用 `override` 关键字，以免发生意外重定义。 在 C# 中，结构就像是轻量级类，是可以实现接口但不支持继承的堆栈分配类型。  
  
 除了这些面向对象的基本原则，使用 C# 还可以通过以下多个创新语言构造更加轻松地开发软件组件：  
  
-   封装的方法签名（名为“*委托*”），可实现类型安全事件通知。  
  
-   用作私有成员变量的访问器的属性。  
  
-   在运行时提供有关类型的声明性元数据的特性。  
  
-   内联的 XML 文档注释。  
  
-   [!INCLUDE[vbteclinqext](~/includes/vbteclinqext-md.md)]，提供跨各种数据源的内置查询功能。  
  
 如果需要与其他 Windows 软件（如 COM 对象或本机 Win32 DLL）进行交互，可以在 C# 中通过名为“互操作”的过程来实现。 借助互操作，C# 程序可以执行本机 C++ 应用程序可以执行的几乎任何操作。 在直接内存访问非常关键的情况下，C# 甚至支持指针和“不安全”代码的概念。  
  
 C# 生成过程比 C 和 C++ 更简单，比 Java 更灵活。 没有单独的头文件，也不要求按特定顺序声明方法和类型。 C# 源文件可以定义任意数量的类、结构、接口和事件。  
  
 可参阅下面的其他 C# 资源：  
  
-   有关语言的实用概述，请参阅 [C# 语言规范](../../csharp/language-reference/language-specification/index.md)的第 1 章。  
  
-   有关 C# 语言特定方面的详细信息，请参阅 [C# 参考](../../csharp/language-reference/index.md)。  
  
-   有关 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 的详细信息，请参阅 [LINQ（语言集成查询）](http://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d)。  
  
-   若要获取 Visual C# 团队发布的最新文章和资源，请访问 [Visual C# 开发者中心](http://go.microsoft.com/fwlink/?LinkId=47811)。  
  
## <a name="net-framework-platform-architecture"></a>.NET Framework 平台体系结构  
 C# 程序在 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] 上运行，这是 Windows 不可或缺的一部分，包括名为“公共语言运行时 (CLR)”的虚执行系统和一组统一的类库。 CLR 是由 Microsoft 执行的公共语言基础结构 (CLI) 的商业实现，CLI 是作为执行和开发环境（语言和库在其中无缝协作）创建依据的国际标准。  
  
 用 C# 编写的源代码被编译成符合 CLI 规范的中间语言 (IL)。 IL 代码和资源（如位图和字符串）存储在磁盘上名为“程序集”的可执行文件（扩展名通常为 .exe 或 .dll）中。 程序集包含一个介绍程序集的类型、版本、区域性和安全要求的清单。  
  
 当 C# 程序执行时，程序集会加载到 CLR 中，可能根据清单中的信息执行各种操作。 然后，如果满足安全要求，CLR 会直接执行实时 (JIT) 编译，将 IL 代码转换成本机指令。 CLR 还提供其他与自动垃圾回收、异常处理和资源管理相关的服务。 CLR 执行的代码有时称为“托管代码”（而不是“非托管代码”），被编译成面向特定系统的本机语言。 下图展示了 C# 源代码文件、.NET Framework 类库、程序集和 CLR 的编译时和运行时关系。  
  
 ![从 C&#35; 源代码到计算机执行](../../csharp/getting-started/media/netarchitecture.png "NET 体系结构")  
  
 语言互操作性是 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] 的一项重要功能。 由于 C# 编译器生成的 IL 代码符合公共类型规范 (CTS)，因此 C# 生成的 IL 代码可以与 .NET 版本 Visual Basic、Visual C++ 或其他任何符合 CTS 的超过 20 种语言生成的代码进行交互。 一个程序集可能包含多个用不同 .NET 语言编写的模块，且类型可以相互引用，就像是用同一种语言编写的一样。  
  
 除了运行时服务之外，[!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] 还包括一个由 4000 多个已整理到命名空间中的类构成的扩展库，这些类提供各种实用功能，包括文件输入输出、字符串控制、XML 分析和 Windows 窗体控件。 典型的 C# 应用程序广泛使用 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] 类库来处理常见的“管道”零碎工作。  
  
 有关 .NET Framework 的详细信息，请参阅 [Microsoft.NET Framework 概述](http://msdn.microsoft.com/en-us/d05daf50-00fe-45c7-8383-06fe41697355)。  
  
## <a name="see-also"></a>另请参阅  
 [C#](../../csharp/index.md) [Visual C# 和 Visual Basic 入门](/visualstudio/ide/getting-started-with-visual-csharp-and-visual-basic)

