---
title: "事件概述（Windows 窗体） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "委托 [Windows 窗体], 事件和"
  - "委托 [Windows 窗体], multicast"
  - "事件 [Windows 窗体], 关于事件"
  - "多路广播事件委托"
  - "Windows 窗体控件, 事件"
  - "Windows 窗体, 事件处理"
ms.assetid: 814a6a43-a312-4791-88d8-f75f9a4f8c4c
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 事件概述（Windows 窗体）
事件是可以通过代码响应或“处理”的操作。  事件可由用户操作（例如单击鼠标或按某个键）、程序代码或系统生成。  
  
 事件驱动的应用程序执行代码以响应事件。  每个窗体和控件都公开一组预定义事件，你可根据这些事件进行编程。  如果发生其中一个事件并且在相关联的事件处理程序中有代码，则调用该代码。  
  
 对象引发的事件类型会发生变化，但对于大多数控件，很多类型都是通用的。  例如，大多数对象都会处理 <xref:System.Windows.Forms.Control.Click> 事件。  如果用户单击窗体，就会执行窗体的 <xref:System.Windows.Forms.Control.Click> 事件处理程序内的代码。  
  
> [!NOTE]
>  许多事件会与其他事件同时发生。  例如，在发生 <xref:System.Windows.Forms.Control.DoubleClick> 事件期间，还会发生 <xref:System.Windows.Forms.Control.MouseDown>、<xref:System.Windows.Forms.Control.MouseUp> 以及 <xref:System.Windows.Forms.Control.Click> 事件。  
  
 有关如何引发和使用事件的信息，请参阅[事件](../../../docs/standard/events/index.md)。  
  
## 委托及其角色  
 委托是 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 中通常用于建立事件处理机制的类。  委托大体上相当于 [!INCLUDE[vcprvc](../../../includes/vcprvc-md.md)] 和其他面向对象语言中常用的函数指针。  但与函数指针不同的是，委托是面向对象的、类型安全的和保险的。  另外，函数指针只包含对特定函数的引用，而委托由对对象的引用以及对该对象内一个或多个方法的引用组成。  
  
 此事件模型使用*“委托”*将事件绑定到用来处理它们的方法。  委托允许其他类通过指定处理程序方法来注册事件通知。  当发生事件时，委托会调用绑定的方法。  有关如何定义委托的详细信息，请参阅[事件](../../../docs/standard/events/index.md)。  
  
 委托可绑定到单个方法或多个方法，后者又称为多路广播。  当创建事件的委托时，你（或 Windows 窗体设计器）通常创建多路广播事件。  极少的例外情况是，某个事件会导致特定过程（例如显示对话框），而该过程在逻辑上不在每个事件中重复多次。  有关如何创建多播委托的信息，请参阅[如何：合并委托（多路广播委托）](../Topic/How%20to:%20Combine%20Delegates%20\(Multicast%20Delegates\)\(C%23%20Programming%20Guide\).md)。  
  
 多路广播委托维护它所绑定到的方法的调用列表。  多路广播委托支持将方法添加到调用列表的 <xref:System.Delegate.Combine%2A> 方法以及将其移除的 <xref:System.Delegate.Remove%2A> 方法。  
  
 当应用程序记录某个事件时，该控件将通过调用该事件的委托引发事件。  委托依次调用绑定的方法。  最常见的情况（多路广播委托）是，委托依次调用调用列表中的每个绑定方法，这样可提供一对多通知。  此策略意味着控件不需要维护事件通知的目标对象列表 \- 委托可处理所有的注册和通知。  
  
 委托还允许将多个事件绑定到同一个方法上，从而允许多对一通知。  例如，单击按钮事件和单击菜单命令事件都能调用同一委托，然后该委托调用单个方法以相同方式处理各个事件。  
  
 与委托一起使用的绑定机制是动态的：委托可在运行时绑定到其签名与事件处理程序的签名相匹配的任何方法上。  借助此功能，你可以根据条件设置或更改绑定方法，并动态地将事件处理程序附加到控件上。  
  
## 请参阅  
 [在 Windows 窗体中创建事件处理程序](../../../docs/framework/winforms/creating-event-handlers-in-windows-forms.md)   
 [事件处理程序概述](../../../docs/framework/winforms/event-handlers-overview-windows-forms.md)