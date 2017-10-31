---
title: "如何：设置 ToolBar 上的控件的样式 | Microsoft Docs"
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
  - "自定义工具栏上的控件"
  - "设置工具栏上的控件样式"
  - "工具栏"
ms.assetid: ba6ae056-d6a9-4c24-90f8-467ab0bc0b1a
caps.latest.revision: 4
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 4
---
# 如何：设置 ToolBar 上的控件的样式
<xref:System.Windows.Controls.ToolBar> 定义 <xref:System.Windows.ResourceKey> 对象以指定 <xref:System.Windows.Controls.ToolBar> 内的控件的样式。  要设置 <xref:System.Windows.Controls.ToolBar> 中的控件的样式，请将样式的 `x:key` 特性设置为 <xref:System.Windows.Controls.ToolBar> 中定义的 <xref:System.Windows.ResourceKey>。  
  
 <xref:System.Windows.Controls.ToolBar> 定义以下 <xref:System.Windows.ResourceKey> 对象：  
  
-   <xref:System.Windows.Controls.ToolBar.ButtonStyleKey%2A>  
  
-   <xref:System.Windows.Controls.ToolBar.CheckBoxStyleKey%2A>  
  
-   <xref:System.Windows.Controls.ToolBar.ComboBoxStyleKey%2A>  
  
-   <xref:System.Windows.Controls.ToolBar.MenuStyleKey%2A>  
  
-   <xref:System.Windows.Controls.ToolBar.RadioButtonStyleKey%2A>  
  
-   <xref:System.Windows.Controls.ToolBar.SeparatorStyleKey%2A>  
  
-   <xref:System.Windows.Controls.ToolBar.TextBoxStyleKey%2A>  
  
-   <xref:System.Windows.Controls.ToolBar.ToggleButtonStyleKey%2A>  
  
## 示例  
 下面的示例定义 <xref:System.Windows.Controls.ToolBar> 中的控件的样式。  
  
 [!code-xml[ToolBar_snip#ToolBarAllStyles](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolBar_snip/CS/pane1.xaml#toolbarallstyles)]  
[!code-xml[ToolBar_snip#ToolBar](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ToolBar_snip/CS/pane1.xaml#toolbar)]  
  
## 请参阅  
 [样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)