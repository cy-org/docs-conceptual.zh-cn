---
title: "枚举设计 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "类型设计准则枚举"
  - "简单枚举"
  - "枚举 [.NET Framework] 设计准则"
  - "类库设计准则 [.NET Framework] 枚举"
  - "标志枚举"
ms.assetid: dd53c952-9d9a-4736-86ff-9540e815d545
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# 枚举设计
枚举是一种特殊的值类型。 有两种枚举︰ 简单的枚举和标志枚举。  
  
 简单枚举表示小闭的集的选项。 简单枚举的一个常见示例是一组颜色。  
  
 标志枚举都设计为支持的枚举值的按位运算。 标志枚举的一个常见示例是选项的列表。  
  
 **✓ 执行** 使用 enum 强类型化参数、 属性和返回值表示的值集。  
  
 **✓ 执行** 倾向于使用而不静态常量的枚举。  
  
 **X 不** 对开放集 （如操作系统版本、 朋友、 等的名称。），才使用。  
  
 **X 不** 供将来使用提供的旨在保留的枚举值。  
  
 始终只可以在以后的阶段到的现有枚举添加值。 请参阅 [将值添加到枚举](#add_value) 有关将值添加到枚举的更多详细信息。 保留的值只需污染的实际值集，并往往会导致用户错误。  
  
 **X 避免** 公开枚举只有一个值。  
  
 确保将来扩展的 C Api 的常见做法是将保留的参数添加到方法签名。 此类保留的参数可以表示为具有一个默认值的枚举。 这不应进行托管 Api 中。 方法重载允许添加参数在将来的版本。  
  
 **X 不** 在枚举中包括 sentinel 值。  
  
 尽管它们有时会对 framework 开发人员有所帮助，sentinel 值是给框架的用户造成混淆。 它们用于从表示枚举集来跟踪枚举而不是值之一的状态。  
  
 **✓ 执行** 提供的值为零简单枚举。  
  
 请考虑调用值类似于"None。 如果这样的值不适合于此特定枚举，则应的基础值零的分配的最常见的默认值为枚举。  
  
 **✓ 请考虑** 使用 <xref:System.Int32> （在大多数编程语言默认值） 作为枚举的基础类型除非以下任一条件成立︰  
  
-   枚举是一个标志枚举，且 32 个以上的标志，或者还期望能够在将来的详细信息。  
  
-   基础类型必须是不同于 <xref:System.Int32> 更容易与预期不同大小的枚举的非托管代码的互操作性。  
  
-   小的基础类型将导致节省大量空间。 如果您希望将枚举主要用作有关控制流的参数，其大小就只有细微的变化。 节省的大小可能会很明显如果︰  
  
    -   您将发现要用作非常频繁地实例化的结构或类中的字段的枚举。  
  
    -   指望用户能创建大型数组或集合的枚举实例。  
  
    -   您预计大量枚举要序列化的实例。  
  
 对于内存中使用情况，请注意托管的对象始终是 `DWORD`\-对齐，因此，您实际上需要多个枚举中的或其他小结构一个实例，以便为了发挥影响力，包具有较小枚举，因为总实例的大小始终要将向上舍入到 `DWORD`。  
  
 **✓ 执行** 命名用归类的复数名词或名词短语标志枚举，与采用单数形式的名词或名词短语的简单枚举。  
  
 **X 不** 扩展 <xref:System.Enum?displayProperty=fullName> 直接。  
  
 <xref:System.Enum?displayProperty=fullName> 是一种特殊类型用于由 CLR 创建用户定义的枚举。 大多数编程语言提供了与此功能使您可以访问的编程元素。 例如，在 C\# `enum` 关键字用于定义枚举。  
  
<a name="design"></a>   
### 设计标志枚举  
 **✓ 执行** 应用 <xref:System.FlagsAttribute?displayProperty=fullName> 到标志枚举。 不将此特性应用于简单枚举。  
  
 **✓ 执行** 使用的两个用于标志的枚举值的幂，所以它们可以自由地组合使用按位或运算。  
  
 **✓ 请考虑** 通常提供特殊的枚举值使用标志的组合。  
  
 按位运算是一个高级的概念并不是必需的简单任务。<xref:System.IO.FileAccess> 为举例说明这样的特殊值。  
  
 **X 避免** 创建标志的值的某些组合是无效的枚举。  
  
 **X 避免** 使用标志枚举值为零，除非值表示"清除所有标志"，并且适当地下, 一项准则中规定命名。  
  
 **✓ 执行** 命名的零值的标志枚举 `None`。 对于标志枚举值必须始终是指"清除所有标志。"  
  
<a name="add_value"></a>   
### 将值添加到枚举  
 它是很常见，来发现您需要将值添加到枚举后对已发布它。 没有潜在的应用程序兼容性问题从现有的 API，返回新添加的值时因为编写得非常糟糕的应用程序可能不正确地处理的新值。  
  
 **✓ 请考虑** 将值添加到枚举，尽管有小型兼容性风险。  
  
 如果您有关于应用程序不兼容引起的枚举的新增功能的实际数据，请考虑添加，则返回新的和旧值的新 API 并弃用旧的 API，应继续返回只是旧值。 这将确保现有的应用程序保持兼容。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [类型设计准则](../../../docs/standard/design-guidelines/type.md)   
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)