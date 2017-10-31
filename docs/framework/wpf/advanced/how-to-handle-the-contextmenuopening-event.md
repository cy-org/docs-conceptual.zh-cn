---
title: "如何：处理 ContextMenuOpening 事件 | Microsoft Docs"
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
  - "ContextMenuOpening 事件"
ms.assetid: 789652fb-1951-4217-934a-7843e355adf4
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：处理 ContextMenuOpening 事件
可以在应用程序中处理 <xref:System.Windows.FrameworkElement.ContextMenuOpening> 事件，以便在显示现有上下文菜单之前对其进行调整，或者通过将事件数据中的 <xref:System.Windows.RoutedEventArgs.Handled%2A> 属性设置为 `true` 来禁止显示该菜单。  将事件数据中的 <xref:System.Windows.RoutedEventArgs.Handled%2A> 设置为 `true` 通常是为了用一个新的 <xref:System.Windows.Controls.ContextMenu> 对象完全替换菜单，有时这需要取消操作并启动一个新的打开操作。  如果您为 <xref:System.Windows.FrameworkElement.ContextMenuOpening> 事件编写处理程序，应注意 <xref:System.Windows.Controls.ContextMenu> 控件与一般情况下负责打开和定位控件上下文菜单的服务之间的计时问题。  本主题将介绍适用于各种上下文菜单打开方案的一些代码技巧，另外还将介绍一种会出现计时问题的情况。  
  
 <xref:System.Windows.FrameworkElement.ContextMenuOpening> 事件的处理方案有以下几种：  
  
-   在显示之前调整菜单项。  
  
-   在显示之前替换整个菜单。  
  
-   完全禁止显示任何现有的上下文菜单，不显示任何上下文菜单。  
  
## 示例  
  
## 在显示之前调整菜单项  
 调整现有的菜单项相当简单，这可能是最常见的方案。  这样做的目的可能是为了增加或减少上下文菜单选项，以响应应用程序中的当前状态信息，或响应请求上下文菜单的对象上作为属性提供的特定状态信息。  
  
 一般的方法是获取事件源（即被右击的具体控件），并从中获取 <xref:System.Windows.FrameworkElement.ContextMenu%2A> 属性。  通常您需要检查 <xref:System.Windows.Controls.ItemsControl.Items%2A> 集合，以了解菜单中已存在哪些上下文菜单项，然后在该集合中添加相应的新 <xref:System.Windows.Controls.MenuItem> 项或从中移除项。  
  
 [!code-csharp[ContextMenuOpeningHandlers#AddItemNoHandle](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ContextMenuOpeningHandlers/CSharp/Pane1.xaml.cs#additemnohandle)]  
  
## 在显示之前替换整个菜单  
 另一种方案假设您希望替换整个上下文菜单。  当然，您也可以使用上面代码的变体移除现有上下文菜单中的所有项，然后再从头开始添加新项。  但是，要替换上下文菜单中的所有项，更直观的方法是创建一个新的 <xref:System.Windows.Controls.ContextMenu>，在其中填充项，然后将控件的 <xref:System.Windows.FrameworkElement.ContextMenu%2A?displayProperty=fullName> 属性设置为这个新的 <xref:System.Windows.Controls.ContextMenu>。  
  
 下面是用于替换 <xref:System.Windows.Controls.ContextMenu> 的简单处理程序代码。  该代码引用一个自定义的 `BuildMenu` 方法，由于不止一个示例处理程序调用此方法，因此该方法被分隔。  
  
 [!code-csharp[ContextMenuOpeningHandlers#ReplaceNoReopen](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ContextMenuOpeningHandlers/CSharp/Pane1.xaml.cs#replacenoreopen)]  
  
 [!code-csharp[ContextMenuOpeningHandlers#BuildMenu](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ContextMenuOpeningHandlers/CSharp/Pane1.xaml.cs#buildmenu)]  
  
 但是，如果您对 <xref:System.Windows.FrameworkElement.ContextMenuOpening> 使用此处理程序样式，那么，当您在其中设置 <xref:System.Windows.Controls.ContextMenu> 的对象上没有预先存在的上下文菜单时，可能会出现计时问题。  当用户右击某个控件时，即使现有 <xref:System.Windows.Controls.ContextMenu> 为空或 Null，也会引发 <xref:System.Windows.FrameworkElement.ContextMenuOpening>。  但在这种情况下，在源元素上设置的任何新的 <xref:System.Windows.Controls.ContextMenu> 都由于传递延时而无法显示。  同时，如果用户碰巧再次右击该控件，则这次您的新 <xref:System.Windows.Controls.ContextMenu> 将会出现，其值非 Null。当处理程序再次运行时，将正确替换并显示该菜单。  对于这种问题，建议采用以下两种可行的解决方法：  
  
1.  确保始终针对至少有一个可用占位符 <xref:System.Windows.Controls.ContextMenu>（您打算用处理程序代码替换它）的控件运行 <xref:System.Windows.FrameworkElement.ContextMenuOpening> 处理程序。  在这种情况下，您仍然可以使用上面示例中显示的处理程序，但通常需要在初始标记中分配占位符 <xref:System.Windows.Controls.ContextMenu>：  
  
     [!code-xml[ContextMenuOpeningHandlers#XAMLWithInitCM](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ContextMenuOpeningHandlers/CSharp/Pane1.xaml#xamlwithinitcm)]  
  
2.  根据某些初步逻辑，假设初始 <xref:System.Windows.Controls.ContextMenu> 值可能为 Null。  您可以检查 <xref:System.Windows.Controls.ContextMenu> 是否为 Null，或者在代码中使用标志来检查处理程序是否已至少运行一次。  因为您假设即将显示 <xref:System.Windows.Controls.ContextMenu>，所以处理程序将事件数据中的 <xref:System.Windows.RoutedEventArgs.Handled%2A> 设置为 `true`。  对于负责显示上下文菜单的 <xref:System.Windows.Controls.ContextMenuService>，如果事件数据中的 <xref:System.Windows.RoutedEventArgs.Handled%2A> 的值为 `true`，则表示请求取消显示引发该事件的上下文菜单\/控件组合。  
  
 禁止显示可能有问题的上下文菜单后，接下来提供一个新的菜单，然后显示该菜单。  设置新菜单基本上与上一个处理程序相同：生成一个新的 <xref:System.Windows.Controls.ContextMenu>，并使用它设置控件源的 <xref:System.Windows.FrameworkElement.ContextMenu%2A?displayProperty=fullName> 属性。  额外的步骤是您现在必须强制显示上下文菜单，因为您取消了第一次尝试。  若要强制显示，需要在处理程序中将 <xref:System.Windows.Controls.Primitives.Popup.IsOpen%2A?displayProperty=fullName> 属性设置为 `true`。  执行此操作时请务必小心，因为在处理程序中打开上下文菜单将再次引发 <xref:System.Windows.FrameworkElement.ContextMenuOpening> 事件。  如果再次进入该处理程序，它将无限递归。  因此，当您从 <xref:System.Windows.FrameworkElement.ContextMenuOpening> 事件处理程序内部打开上下文菜单时，始终需要检查 `null` 值或使用标志。  
  
## 禁止显示任何现有的上下文菜单，不显示任何上下文菜单  
 最后一种方案是编写一个完全禁止显示菜单的处理程序，此方案并不常用。  也许还有更合适的方法可以禁止某个给定控件显示上下文菜单，而不是仅在用户请求时才禁止显示菜单。  但是，如果您要使用处理程序来禁止显示上下文菜单且不显示任何内容，您的处理程序只需将事件数据中的 <xref:System.Windows.RoutedEventArgs.Handled%2A> 设置为 `true`。  负责显示上下文菜单的 <xref:System.Windows.Controls.ContextMenuService> 将检查在该控件上引发的事件的事件数据。  如果该事件在路由中的任何位置被标记为 <xref:System.Windows.RoutedEventArgs.Handled%2A>，则会禁止启动该事件的上下文菜单的打开操作。  
  
 [!code-csharp[ContextMenuOpeningHandlers#ReplaceReopen](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ContextMenuOpeningHandlers/CSharp/Pane1.xaml.cs#replacereopen)]  
  
## 请参阅  
 <xref:System.Windows.Controls.ContextMenu>   
 <xref:System.Windows.FrameworkElement.ContextMenu%2A?displayProperty=fullName>   
 [基元素概述](../../../../docs/framework/wpf/advanced/base-elements-overview.md)   
 [ContextMenu 概述](../../../../docs/framework/wpf/controls/contextmenu-overview.md)