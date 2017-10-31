---
title: "如何：检测何时按下 Enter 键 | Microsoft Docs"
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
  - "Enter 键, 检测"
  - "键, Enter"
ms.assetid: a66f39d2-ef4a-43a5-b454-a4ea0fe88655
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：检测何时按下 Enter 键
此示例演示如何检测何时按下键盘上的 <xref:System.Windows.Input.Key> 键。  
  
 本示例包括一个[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 文件和一个代码隐藏文件。  
  
## 示例  
 当用户在 <xref:System.Windows.Controls.TextBox> 中按下 <xref:System.Windows.Input.Key> 键时，文本框中的输入将显示在[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 的其他区域。  
  
 下面的 [!INCLUDE[TLA2#tla_titlexaml](../../../../includes/tla2sharptla-titlexaml-md.md)] 创建了用户界面，其中包括一个 <xref:System.Windows.Controls.StackPanel>、一个 <xref:System.Windows.Controls.TextBlock> 和一个 <xref:System.Windows.Controls.TextBox>。  
  
 [!code-xml[keydown#KeyDownUI](../../../../samples/snippets/csharp/VS_Snippets_Wpf/KeyDown/CSharp/Window1.xaml#keydownui)]  
  
 下面的代码隐藏创建 <xref:System.Windows.UIElement.KeyDown> 事件处理程序。  如果按下的键是 <xref:System.Windows.Input.Key> 键，则在 <xref:System.Windows.Controls.TextBlock> 中会显示一条消息。  
  
 [!code-csharp[keydown#KeyDownSample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/KeyDown/CSharp/Window1.xaml.cs#keydownsample)]
 [!code-vb[keydown#KeyDownSample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/KeyDown/VisualBasic/Window1.xaml.vb#keydownsample)]  
  
## 请参阅  
 [输入概述](../../../../docs/framework/wpf/advanced/input-overview.md)   
 [路由事件概述](../../../../docs/framework/wpf/advanced/routed-events-overview.md)