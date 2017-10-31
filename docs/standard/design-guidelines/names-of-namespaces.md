---
title: "命名空间的名称 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "冲突的名称 [.NET Framework]"
  - "命名空间的名称 [.NET Framework]"
  - "冲突的类型名称"
  - "命名空间 [.NET Framework] 名称"
  - "名称 [.NET Framework]，类型名称"
ms.assetid: a49058d2-0276-43a7-9502-04adddf857b2
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# 命名空间的名称
作为与其他命名准则命名命名空间时的目标创建足够清晰度为程序员使用 framework 立即知道该命名空间的内容是什么，可能需要。 下面的模板指定命名的命名空间的一般规则︰  
  
 `<Company>.(<Product>|<Technology>)[.<Feature>][.<Subnamespace>]`  
  
 示例如下︰  
  
 `Fabrikam.Math`   
 `Litware.Security`  
  
 **✓ 执行** 作为用公司名称，以防止不同公司开发具有相同名称的命名空间的命名空间名称的前缀。  
  
 **✓ 执行** 在命名空间名称的第二个级别上使用一个稳定、 独立于版本的产品名称。  
  
 **X 不** 使用组织的层次结构的基础命名空间层次结构中的名称，因为公司内的组名往往都很短。 将组织中的相关技术组周围的命名空间的层次结构。  
  
 **✓ 执行** 使用句点 PascalCasing 和单独的命名空间的组件 \(例如， `Microsoft.Office.PowerPoint`\)。 如果您的品牌采用了非传统的大小写，则应遵循由您的品牌、 定义的大小写，即使背离常用的命名空间的大小写。  
  
 **✓ 请考虑** 使用复数命名空间名称，在适当的位置。  
  
 例如，使用 `System.Collections` 而不是 `System.Collection`。 品牌名称和首字母缩写词不过是此规则的例外情况。 例如，使用 `System.IO` 而不是 `System.IOs`。  
  
 **X 不** 该命名空间中使用命名空间和类型相同的名称。  
  
 例如，不要使用 `Debug` 与命名空间名称，然后还提供一个名为类 `Debug` 同一命名空间中。 多个编译器需要这种类型是完全限定的。  
  
### 命名空间和类型的名称冲突  
 **X 不** 如引入了泛型类型名称 `Element`, ，`Node`, ，`Log`, ，和 `Message`。  
  
 没有这样做将导致类型名称冲突共同点方案的可能性非常非常高。 应限定的泛型类型名称 \(`FormElement`, ，`XmlNode`, ，`EventLog`, ，`SoapMessage`\)。  
  
 有用于避免为不同类别的命名空间的类型名称冲突的特定指导原则。  
  
-   **应用程序模型命名空间**  
  
     经常在一起，使用属于单个应用程序模型的命名空间，但几乎从不用于命名空间的其他应用程序模型。 例如， <xref:System.Windows.Forms?displayProperty=fullName> 以及很少使用命名空间 <xref:System.Web.UI?displayProperty=fullName> 命名空间。 下面是一个已知的应用程序模型命名空间组的列表︰  
  
     `System.Windows*`   
     `System.Web.UI*`  
  
     **X 不** 为单个应用程序模型内的命名空间中的类型提供相同的名称。  
  
     例如，不要将添加一个名为类型 `Page` 到 <xref:System.Web.UI.Adapters?displayProperty=fullName> 命名空间，因为 <xref:System.Web.UI?displayProperty=fullName> 命名空间中已包含名为的类型 `Page`。  
  
-   **基础结构命名空间**  
  
     此组包含在常见的应用程序的开发过程中很少会导入的命名空间。 例如， `.Design` 开发编程工具时，将主要使用命名空间。 这些命名空间中的类型以避免冲突并不重要。  
  
-   **核心命名空间**  
  
     核心命名空间包括所有 `System` 不包括命名空间中的，应用程序模型和基础结构命名空间的命名空间。 核心命名空间包括等， `System`, ，`System.IO`, ，`System.Xml`, ，和 `System.Net`。  
  
     **X 不** 使类型相冲突的名称与核心命名空间中的任何类型。  
  
     例如，永远不会使用 `Stream` 作为类型名。 它将与冲突 <xref:System.IO.Stream?displayProperty=fullName>, 、 一个十分常用的类型。  
  
-   **技术命名空间组**  
  
     此类别包括具有相同的前两个命名空间节点的所有命名空间 `(<Company>.<Technology>*`\)，如 `Microsoft.Build.Utilities` 和 `Microsoft.Build.Tasks`。 很重要类型属于一种技术不会彼此发生冲突。  
  
     **X 不** 向内一种技术的其他类型分配会发生冲突的类型名称。  
  
     **X 不** 引入技术命名空间中的类型和应用程序模型命名空间之间的类型名称冲突 （除非该技术不是为了与应用程序模型一起使用）。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)   
 [命名准则](../../../docs/standard/design-guidelines/naming-guidelines.md)