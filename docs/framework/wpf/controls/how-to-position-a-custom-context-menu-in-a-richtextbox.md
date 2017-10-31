---
title: "如何：在 RichTextBox 中定位自定义上下文菜单 | Microsoft Docs"
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
  - "自定义上下文菜单定位"
  - "定位自定义上下文菜单"
  - "RichTextBox 控件中，定位自定义上下文菜单"
  - "上下文菜单定位"
ms.assetid: bf77c930-a546-4573-9a56-9af345ba189a
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：在 RichTextBox 中定位自定义上下文菜单
此示例演示如何定位自定义上下文菜单的<xref:System.Windows.Controls.RichTextBox>。  
  
 当您实现的自定义上下文菜单**RichTextBox**，您负责进行处理的上下文菜单的位置。  默认情况下，自定义上下文菜单打开的中心**RichTextBox**。  
  
## <a name="example"></a>示例  
 若要重写默认放置行为，将添加的侦听程序<xref:System.Windows.FrameworkContentElement.ContextMenuOpening>事件。  下面的示例演示如何以编程方式执行此操作。  
  
 [!code-csharp[RichTextBox_ContextMenu#_AddListener](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RichTextBox_ContextMenu/CSharp/app.xaml.cs#_addlistener)]
 [!code-vb[RichTextBox_ContextMenu#_AddListener](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/RichTextBox_ContextMenu/VisualBasic/app.xaml.vb#_addlistener)]  
  
## <a name="example"></a>示例  
 下面的示例演示一个实现相应<xref:System.Windows.FrameworkContentElement.ContextMenuOpening>事件侦听器。  
  
 [!code-csharp[RichTextBox_ContextMenu#_ListenerBody](../../../../samples/snippets/csharp/VS_Snippets_Wpf/RichTextBox_ContextMenu/CSharp/app.xaml.cs#_listenerbody)]
 [!code-vb[RichTextBox_ContextMenu#_ListenerBody](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/RichTextBox_ContextMenu/VisualBasic/app.xaml.vb#_listenerbody)]  
  
## <a name="see-also"></a>另请参阅  
 [RichTextBox 概述](../../../../docs/framework/wpf/controls/richtextbox-overview.md)   
 [TextBox 概述](../../../../docs/framework/wpf/controls/textbox-overview.md)