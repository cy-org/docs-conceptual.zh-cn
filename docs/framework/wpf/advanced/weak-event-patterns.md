---
title: "弱事件模式 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "事件处理程序, 弱事件模式"
  - "IWeakEventListener 接口"
  - "弱事件模式实现"
  - "WeakEventManager 类"
ms.assetid: e7c62920-4812-4811-94d8-050a65c856f6
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# 弱事件模式
在应用程序中，为了与将处理程序附加到事件源的侦听器对象配合，附加到该事件源的处理程序可能不会被破坏。  这种情况可能会导致内存泄漏。  [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 引入了可用于解决此问题的设计模式，该模式为特定事件提供专用管理器类并为该事件的侦听器实现接口。  此设计模式称为“弱事件模式”。  
  
## 为什么实现弱事件模式？  
 侦听事件可能会导致内存泄漏。  侦听事件的一般方法是使用语言特定的语法，该语法将处理程序附加到源上的事件。  例如，在 [!INCLUDE[TLA#tla_cshrp](../../../../includes/tlasharptla-cshrp-md.md)] 中，该语法是：`source.SomeEvent += new SomeEventHandler(MyEventHandler)`。  
  
 此方法创建从事件源到事件侦听器的强引用。  通常，为侦听器附加事件处理程序会导致侦听器具有对象生存期，该生存期受源的对象生存期影响（除非显式移除了事件处理程序）。  但在某些情况下，您可能希望侦听器的对象生存期受其他因素（例如对象生存期当前是否属于应用程序的可视化树）控制，而不受源的生存期控制。  如果源对象生存期超出了侦听器的对象生存期，则常规事件模式会导致内存泄漏：侦听器保持活动状态的时间比预期要长。  
  
 弱事件模式旨在解决此内存泄漏问题。  每当侦听器需要注册事件，而该侦听器并不明确了解什么时候注销时，就可以使用弱事件模式。  当源的对象生存期超出侦听器的有用对象生存期时，也可以使用弱事件模式。  （在这种情况下，*有用*由您确定。）使用弱事件模式，侦听器可以注册和接收事件，同时不会对侦听器的对象生存期特征产生任何影响。  实际上，来自源的隐含引用无法确定侦听器是否适合进行垃圾回收。  该引用为弱引用，仅是弱事件模式和相关 [!INCLUDE[TLA2#tla_api#plural](../../../../includes/tla2sharptla-apisharpplural-md.md)] 的命名。  可以对侦听器进行垃圾回收或销毁，在不保留对现在销毁的对象的非可收集处理程序引用的情况下，源可以继续。  
  
## 谁应实现弱事件模式？  
 实现弱事件模式主要是对于控件作者而言是很有趣味的。  这是因为控件作者主要负责控件的行为和包容以及控件对其所插入到的应用程序的影响。  这包括控件对象生存期行为，特别是对所描述的内存泄漏问题的处理。  
  
 某些方案本质上适合应用弱事件模式。  数据绑定就是这样一个方案。  在数据绑定中，通常源对象完全独立于侦听器对象，而该侦听器对象是绑定的目标。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 数据绑定的许多方面在实现事件的方式上已应用了弱事件模式。  
  
## 如何实现弱事件模式  
 可通过三种方式实现弱事件模式。  ，当您应使用每一时，下表列出了三种方法并提供某些指南。  
  
|方法|在实现|  
|--------|---------|  
|使用现有弱事件管理器类|如果希望订阅的事件具有相应的 <xref:System.Windows.WeakEventManager>，使用现有的弱事件管理器。  有关所附带的 WPF 弱事件管理器的列表，请参见。 <xref:System.Windows.WeakEventManager> 类的继承层次结构。  但是，请注意，具有相对包含 WPF 的较弱事件管理器，因此，您可能需要选择其他方法之一。|  
|使用泛型弱事件管理器类|使用泛型 <xref:System.Windows.WeakEventManager%602> ，当现有 <xref:System.Windows.WeakEventManager> 不可用时，您需要一种简单的方法实现，因此，您不考虑性能。  泛型 <xref:System.Windows.WeakEventManager%602> 比现有或自定义弱事件管理器效率低。  例如，泛型类执行更多反射发现命名该事件的名称。  此外，注册的代码使用常规 <xref:System.Windows.WeakEventManager%602> 事件使用现有或自定义 <xref:System.Windows.WeakEventManager>详细的速度。|  
|创建自定义弱事件管理器类|创建自定义 <xref:System.Windows.WeakEventManager> ，在现有 <xref:System.Windows.WeakEventManager> 不可用时，并且您希望在最好的性能。  使用自定义 <xref:System.Windows.WeakEventManager> 订阅事件将更为有效的，但是，则会先编写更多代码的成本。|  
  
 以下各节描述如何实现弱事件模式。  在本讨论中的目的，订阅的事件具有下列特征。  
  
-   操作名称为 `SomeEvent`。  
  
-   事件由 `EventSource` 类引发。  
  
-   事件处理程序具有类型: `SomeEventEventHandler` \(或 `EventHandler<SomeEventEventArgs>`\)。  
  
-   事件通过类型 `SomeEventEventArgs` 的参数为事件处理程序。  
  
### 使用现有弱事件管理器类  
  
1.  查找现有弱事件管理器。  
  
     有关所附带的 WPF 弱事件管理器的列表，请参见。 <xref:System.Windows.WeakEventManager> 类的继承层次结构。  
  
2.  使用新的弱事件管理器而不是常规事件挂接。  
  
     例如，因此，如果代码使用以下模式订阅事件:  
  
    ```  
    source.SomeEvent += new SomeEventEventHandler(OnSomeEvent);  
    ```  
  
     将其更改为以下模式:  
  
    ```  
    SomeEventWeakEventManager.AddHandler(source, OnSomeEvent);  
    ```  
  
     同样，因此，如果代码使用以下模式取消订阅事件:  
  
    ```  
    source.SomeEvent -= new SomeEventEventHandler(OnSome);  
    ```  
  
     将其更改为以下模式:  
  
    ```  
    SomeEventWeakEventManager.RemoveHandler(source, OnSomeEvent);  
    ```  
  
### 使用泛型弱事件管理器类  
  
1.  使用泛型 <xref:System.Windows.WeakEventManager%602> 类而不是常规事件挂接。  
  
     当您使用 <xref:System.Windows.WeakEventManager%602> 注册事件侦听器时，如下面的代码所示，可以提供事件源和 <xref:System.EventArgs> 类型为类型参数提供类并调用 <xref:System.Windows.WeakEventManager%602.AddHandler%2A> :  
  
    ```  
    WeakEventManager<EventSource, SomeEventEventArgs>.AddHandler(source, "SomeEvent", source_SomeEvent);  
    ```  
  
### 创建自定义弱事件管理器类  
  
1.  复制下面的类模板添加到项目。  
  
     此类从 <xref:System.Windows.WeakEventManager> 类继承。  
  
     [!code-csharp[WeakEvents#WeakEventManagerTemplate](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WeakEvents/CSharp/WeakEventManagerTemplate.cs#weakeventmanagertemplate)]  
  
2.  将替换 `SomeEventWeakEventManager` 名称拥有名称。  
  
3.  用相应的名称替换前面所述的三个名称事件。  \(`SomeEvent`、 `EventSource`和 `SomeEventEventArgs`\)  
  
4.  设置可见性 \(公共\/内部\/私有\) 弱事件管理器类将与事件它管理的可见性。  
  
5.  使用新的弱事件管理器而不是常规事件挂接。  
  
     例如，因此，如果代码使用以下模式订阅事件:  
  
    ```  
    source.SomeEvent += new SomeEventEventHandler(OnSomeEvent);  
    ```  
  
     将其更改为以下模式:  
  
    ```  
    SomeEventWeakEventManager.AddHandler(source, OnSomeEvent);  
    ```  
  
     同样，因此，如果代码使用以下模式取消订阅事件:  
  
    ```  
    source.SomeEvent -= new SomeEventEventHandler(OnSome);  
    ```  
  
     将其更改为以下模式:  
  
    ```  
    SomeEventWeakEventManager.RemoveHandler(source, OnSomeEvent);  
    ```  
  
## 请参阅  
 <xref:System.Windows.WeakEventManager>   
 <xref:System.Windows.IWeakEventListener>   
 [路由事件概述](../../../../docs/framework/wpf/advanced/routed-events-overview.md)   
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)