---
title: "预览事件 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "事件, 预览"
  - "事件, 取消显示"
  - "预览事件"
  - "取消显示事件"
ms.assetid: b5032308-aa9c-4d02-af11-630ecec8df7e
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 预览事件
预览事件（也称为隧道事件）是路由事件，路由的方向是从应用程序根元素到引发该事件并在事件数据中报告为源的元素。  并非所有的事件方案都支持或需要预览事件；本主题介绍存在预览事件的情形，说明应用程序或组件应如何处理预览事件，并指出可能适宜在自定义组件或类中创建预览事件的情形。  
  
## 预览事件和输入  
 当您通常处理预览事件时，应谨慎地在事件数据中将事件标记为已处理。  在引发预览事件的元素（在事件数据中报告为源的元素）之外的任何元素上处理该事件都有这样的后果：使得元素没有机会处理源自于它的事件。  有时这是希望的结果，尤其当该元素存在于控件的复合关系内时。  
  
 特别是对于输入事件而言，预览事件还与对等的冒泡事件共享事件数据实例。  如果您使用预览事件类处理程序将输入事件标记为已处理，将不会调用冒泡输入事件类处理程序。  或者，如果您使用预览事件实例处理程序将事件标记为已处理，则通常不会调用冒泡事件的处理程序。  可以使用即使事件已标记为已处理也将调用的选项来注册或附加类处理程序或实例处理程序，但此技术不常用。  
  
 有关类处理以及它与预览事件的关系的更多信息，请参见[将路由事件标记为“已处理”和“类处理”](../../../../docs/framework/wpf/advanced/marking-routed-events-as-handled-and-class-handling.md)。  
  
### 通过控件解决事件禁止问题  
 通常使用预览事件的一种情形是复合控件的输入事件处理。  有时，控件创作者禁止从其控件引发某一事件，这样做可能是为了替换上携带更多信息或者暗指更具体的行为的组件定义事件。  例如，[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] <xref:System.Windows.Controls.Button> 禁止 <xref:System.Windows.Controls.Button> 或它的组成元素所引发的 <xref:System.Windows.UIElement.MouseLeftButtonDown> 和 <xref:System.Windows.UIElement.MouseLeftButtonDown> 冒泡事件，以便于捕获鼠标并引发始终由 <xref:System.Windows.Controls.Button> 本身引发的 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件。  事件及其数据仍然沿着路由继续，但是因为 <xref:System.Windows.Controls.Button> 将事件数据标记为 <xref:System.Windows.RoutedEventArgs.Handled%2A>，所以只会调用明确指出它们应当在 `handledEventsToo` 情况下起作用的事件处理程序。  如果在应用程序根元素之前的其他元素仍然希望有机会处理被控件禁止的事件，那么一个替代方法是在代码中附加 `handledEventsToo` 指定为 `true` 的处理程序。  但是，一种更简单的方法通常是将您处理的路由方向改为输入事件的等效预览事件。  例如，如果控件禁止 <xref:System.Windows.UIElement.MouseLeftButtonDown>，则应尝试为 <xref:System.Windows.UIElement.PreviewMouseLeftButtonDown> 附加处理程序。  此方法仅适应于基元素输入事件，如 <xref:System.Windows.UIElement.MouseLeftButtonDown>。  这些输入事件使用隧道\/冒泡对，引发两个事件，并共享事件数据。  
  
 上述每种方法都有副作用或局限性。  处理预览事件的副作用是在该点处理此事件可能会禁用计划处理冒泡事件的处理程序，因此局限性在于：将仍在路由的预览部分的事件标记为已处理通常是不明智的。  `handledEventsToo` 方法的局限性在于：您不能将 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中的 `handledEventsToo` 处理程序指定为特性，而必须在获得对将附加事件处理程序的元素的对象引用后，在代码中注册该处理程序。  
  
## 请参阅  
 [将路由事件标记为“已处理”和“类处理”](../../../../docs/framework/wpf/advanced/marking-routed-events-as-handled-and-class-handling.md)   
 [路由事件概述](../../../../docs/framework/wpf/advanced/routed-events-overview.md)