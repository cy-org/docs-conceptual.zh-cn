---
title: "如何：为拖动的 GridView 列标题创建样式 | Microsoft Docs"
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
  - "ListView 控件, 样式设置"
ms.assetid: 0b999645-0313-4b33-80b9-19ece08b5459
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：为拖动的 GridView 列标题创建样式
下面的示例演示当用户更改列的位置时，所拖动的 <xref:System.Windows.Controls.GridViewColumnHeader> 的外观如何发生变化。  
  
## 示例  
 在使用 <xref:System.Windows.Controls.GridView> 作为其视图模式的 <xref:System.Windows.Controls.ListView> 中，当您将某个列标题移到另一个位置时，该列将移到新的位置。  当您拖动列标题时，除了原始标题以外，还会出现该标题的浮动副本。  <xref:System.Windows.Controls.GridView> 中的列标题由 <xref:System.Windows.Controls.GridViewColumnHeader> 对象来表示。  
  
 若要同时对浮动标题和原始标题的外观进行自定义，可以设置 <xref:System.Windows.Controls.ControlTemplate.Triggers%2A> 以修改 <xref:System.Windows.Controls.GridViewColumnHeader> <xref:System.Windows.Style>。  如果 <xref:System.Windows.Controls.Primitives.ButtonBase.IsPressed%2A> 属性值为 `true`，并且 <xref:System.Windows.Controls.GridViewColumnHeader.Role%2A> 属性值为 <xref:System.Windows.Controls.GridViewColumnHeaderRole>，则会应用这些 <xref:System.Windows.Controls.ControlTemplate.Triggers%2A>。  
  
 当鼠标悬停在 <xref:System.Windows.Controls.GridViewColumnHeader> 上时，如果用户按住鼠标按钮，则 <xref:System.Windows.Controls.Primitives.ButtonBase.IsPressed%2A> 属性值会更改为 `true`。  同样，当用户开始执行拖动操作时，<xref:System.Windows.Controls.GridViewColumnHeader.Role%2A> 属性会更改为 <xref:System.Windows.Controls.GridViewColumnHeaderRole>。  
  
 下面的示例演示如何设置 <xref:System.Windows.Controls.ControlTemplate.Triggers%2A>，使用户将列拖到新位置时，原始标题和浮动标题的 <xref:System.Windows.Controls.Control.Foreground%2A> 和 <xref:System.Windows.Controls.Control.Background%2A> 颜色发生变化。  
  
 [!code-xml[ListViewHeaderRoleStyle#GVCHControlTemplateStart](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewHeaderRoleStyle/CS/Window1.xaml#gvchcontroltemplatestart)]  
[!code-xml[ListViewHeaderRoleStyle#ControlTemplateTriggersStart](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewHeaderRoleStyle/CS/Window1.xaml#controltemplatetriggersstart)]  
[!code-xml[ListViewHeaderRoleStyle#IsPressed](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewHeaderRoleStyle/CS/Window1.xaml#ispressed)]  
[!code-xml[ListViewHeaderRoleStyle#Floating](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewHeaderRoleStyle/CS/Window1.xaml#floating)]  
[!code-xml[ListViewHeaderRoleStyle#ControlTemplateTriggersEnd](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewHeaderRoleStyle/CS/Window1.xaml#controltemplatetriggersend)]  
[!code-xml[ListViewHeaderRoleStyle#GVCHControlTemplateEnd](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewHeaderRoleStyle/CS/Window1.xaml#gvchcontroltemplateend)]  
  
## 请参阅  
 <xref:System.Windows.Controls.GridViewColumnHeader>   
 <xref:System.Windows.Controls.GridViewColumnHeaderRole>   
 <xref:System.Windows.Controls.ListView>   
 <xref:System.Windows.Controls.GridView>   
 [帮助主题](../../../../docs/framework/wpf/controls/listview-how-to-topics.md)   
 [ListView 概述](../../../../docs/framework/wpf/controls/listview-overview.md)   
 [GridView 概述](../../../../docs/framework/wpf/controls/gridview-overview.md)