---
title: "ContextMenu 概述 | Microsoft Docs"
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
  - "ContextMenu 控件 [WPF], 关于 ContextMenu 控件"
  - "控件, ContextMenu"
ms.assetid: 16909c42-799a-4561-91e0-7d69dcfeea91
caps.latest.revision: 25
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 24
---
# ContextMenu 概述
<xref:System.Windows.Controls.ContextMenu> 类表示使用特定于上下文的 <xref:System.Windows.Controls.Menu> 公开功能的元素。  通常，用户可以通过单击鼠标右键在[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 中公开 <xref:System.Windows.Controls.ContextMenu>。  本主题介绍 <xref:System.Windows.Controls.ContextMenu> 元素，并提供有关如何在[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 和代码中使用该元素的示例。  
  
   
  
<a name="contextmenu_control"></a>   
## ContextMenu 控件  
 <xref:System.Windows.Controls.ContextMenu> 附加到特定的控件。  使用 <xref:System.Windows.Controls.ContextMenu> 元素可以向用户呈现一个项列表，这些项指定与特定控件（例如 <xref:System.Windows.Controls.Button>）相关联的命令或选项。  用户通过右击该控件可以显示菜单。  通常，单击 <xref:System.Windows.Controls.MenuItem> 将打开一个子菜单或者导致应用程序执行相应的命令。  
  
<a name="creating_contextmenus"></a>   
## 创建 ContextMenu  
 下面的示例演示如何创建包含子菜单的 <xref:System.Windows.Controls.ContextMenu>。  <xref:System.Windows.Controls.ContextMenu> 控件附加到按钮控件。  
  
 [!code-xml[ContextMenu#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ContextMenu/CSharp/Pane1.xaml#1)]  
  
 [!code-csharp[ContextMenu#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ContextMenu/CSharp/Pane1.xaml.cs#2)]
 [!code-vb[ContextMenu#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ContextMenu/VisualBasic/Pane1.xaml.vb#2)]  
  
<a name="applying_styles_to_contextmenu"></a>   
## 对 ContextMenu 应用样式  
 通过使用控件 <xref:System.Windows.Style>，无需编写自定义控件就可以显著改变 <xref:System.Windows.Controls.ContextMenu> 的外观和行为。  除了设置可视化属性以外，还可以对控件的各个部分应用样式。  例如，可以使用属性更改控件各个部分的行为，也可以向 <xref:System.Windows.Controls.ContextMenu> 中添加新的部分或更改其布局。  下面的示例演示向 <xref:System.Windows.Controls.ContextMenu> 控件添加样式的几种方法。  
  
 第一个示例定义一个名为 `SimpleSysResources` 的样式，它演示如何在您的样式中使用当前的系统设置。  该示例指定 <xref:System.Windows.SystemColors.MenuHighlightBrushKey%2A> 作为 <xref:System.Windows.Controls.ContextMenu> 的 <xref:System.Windows.Controls.Control.Background%2A> 颜色，指定 <xref:System.Windows.SystemColors.MenuTextBrushKey%2A> 作为其 <xref:System.Windows.Controls.Control.Foreground%2A> 颜色。  
  
```  
<Style x:Key="SimpleSysResources" TargetType="{x:Type MenuItem}">  
  <Setter Property = "Background" Value=   
    "{DynamicResource {x:Static SystemColors.MenuHighlightBrushKey}}"/>  
  <Setter Property = "Foreground" Value=   
    "{DynamicResource {x:Static SystemColors.MenuTextBrushKey}}"/>  
</Style>  
```  
  
 下面的示例使用 <xref:System.Windows.Trigger> 元素来更改 <xref:System.Windows.Controls.Menu> 的外观，以响应 <xref:System.Windows.Controls.ContextMenu> 上引发的事件。  当用户将鼠标移动到菜单上时，<xref:System.Windows.Controls.ContextMenu> 项的外观将随之更改。  
  
```  
<Style x:Key="Triggers" TargetType="{x:Type MenuItem}">  
  <Style.Triggers>  
    <Trigger Property="MenuItem.IsMouseOver" Value="true">  
      <Setter Property = "FontSize" Value="16"/>  
      <Setter Property = "FontStyle" Value="Italic"/>  
      <Setter Property = "Foreground" Value="Red"/>  
    </Trigger>  
  </Style.Triggers>  
</Style>  
```  
  
## 请参阅  
 <xref:System.Windows.Controls.ContextMenu>   
 <xref:System.Windows.Style>   
 <xref:System.Windows.Controls.Menu>   
 <xref:System.Windows.Controls.MenuItem>   
 [ContextMenu](../../../../docs/framework/wpf/controls/contextmenu.md)   
 [ContextMenu 样式和模板](../../../../docs/framework/wpf/controls/contextmenu-styles-and-templates.md)   
 [WPF Controls Gallery Sample](http://go.microsoft.com/fwlink/?LinkID=160053)