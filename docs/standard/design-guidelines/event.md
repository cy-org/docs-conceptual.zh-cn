---
title: "事件设计 | Microsoft Docs"
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
  - "前期事件"
  - "设计准则的事件 [.NET Framework]"
  - "成员设计准则事件"
  - "事件处理程序 [.NET Framework] 事件设计准则"
  - "后期事件"
  - "签名，事件处理"
ms.assetid: 67b3c6e2-6a8f-480d-a78f-ebeeaca1b95a
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# 事件设计
事件是最常使用的窗体的回调 （允许框架，以调入用户代码的构造）。 其他回调机制包括撰写委托、 虚拟成员，以及使用基于接口的插件的成员。 从可用性研究数据表明大多数开发人员都更了解了如何使用事件不是他们正在使用其他回调机制。 事件可以很好地集成在一起 Visual Studio 和多种语言。  
  
 务必注意，有两个组的事件︰ 在调用前事件，以及之后状态更改时，引发的事件的系统更改状态之前引发的事件名后的事件。 事件前一个示例 `Form.Closing`, ，引发之前关闭窗体。 事件后的示例将 `Form.Closed`, ，其在窗体关闭后引发。  
  
 **✓ 执行** 使用术语"引发"的事件而不是"fire"或"触发器"。  
  
 **✓ 执行** 使用 <xref:System.EventHandler%601?displayProperty=fullName> 而不是手动创建新的委托，用于为事件处理程序。  
  
 **✓ 请考虑** 使用的一个子类 <xref:System.EventArgs> 作为事件参数中，除非您完全确定该事件将永远不会需要传输到的事件处理方法，任何数据，否则在这种情况下可以使用 `EventArgs` 直接键入。  
  
 如果您在发运 API 使用 `EventArgs` 直接，您永远不会将能够添加任何数据，以执行与该事件，而不会破坏兼容性。 如果您使用的子类，甚至是如果最初完全为空，您将能够将属性添加到需要时的子类。  
  
 **✓ 执行** 使用受保护的虚方法引发的每个事件。 此特性仅适用于未密封类，不适用于结构、 密封的类或静态事件上的非静态事件。  
  
 方法的用途是提供一种方法为派生类使用替代对事件进行处理。 重写是一种更灵活、 更快，且更自然的方式来处理基类派生类中的事件。 按照约定，该方法的名称应以"On"启动，且后面提供的事件名称。  
  
 派生的类可以选择不在其重写中调用该方法的基实现。 先做好这由基类才能正常工作所需的方法中不包括任何处理。  
  
 **✓ 执行** 引发事件的受保护方法采用一个参数。  
  
 该参数应命名为 `e` 和类型应为事件参数类。  
  
 **X 不** 时引发的非静态事件传递 null 值作为发件人。  
  
 **✓ 执行** 引发静态事件时将传递 null 值作为发件人。  
  
 **X 不** 将 null 作为事件数据参数传递时引发事件。  
  
 您应将传递 `EventArgs.Empty` 如果不想将任何数据传递给事件处理方法。 开发人员都期望此参数不能为 null。  
  
 **✓ 请考虑** 引发最终用户可以取消的事件。 这仅适用于事前事件。  
  
 使用 <xref:System.ComponentModel.CancelEventArgs?displayProperty=fullName> 或要允许最终用户若要取消事件的事件参数作为其子类。  
  
### 自定义事件处理程序设计  
 某些情况下，在其中 `EventHandler<T>` 不能使用，如框架需要与早期版本的 CLR 中，这并不支持泛型。 在这种情况下，您可能需要设计和开发自定义事件处理程序委托。  
  
 **✓ 执行** 对于事件处理程序使用返回类型为 void。  
  
 事件处理程序可以调用多个事件处理方法，可能在多个对象上。 如果允许事件处理方法的返回值，则可能会为每个事件调用多个返回值。  
  
 **✓ 执行** 使用 `object` 作为事件处理程序的第一个参数的类型并调用它 `sender`。  
  
 **✓ 执行** 使用 <xref:System.EventArgs?displayProperty=fullName> 或作为事件处理程序，第二个参数的类型及其子类并将其命名 `e`。  
  
 **X 不** 事件处理程序上有两个以上参数。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 [成员设计准则](../../../docs/standard/design-guidelines/member.md)   
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)