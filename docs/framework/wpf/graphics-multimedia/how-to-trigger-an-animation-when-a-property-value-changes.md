---
title: "如何：在属性值更改时触发动画 | Microsoft Docs"
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
  - "动画, 在属性值更改时启动"
  - "情节提要, 在属性值更改时启动"
  - "触发动画"
ms.assetid: 12399c21-0300-4f4f-9e3a-d92d9907e5f5
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：在属性值更改时触发动画
本示例演示属性值更改时如何使用 <xref:System.Windows.Trigger> 来启动 <xref:System.Windows.Media.Animation.Storyboard>。  您可以在 <xref:System.Windows.Style>、<xref:System.Windows.Controls.ControlTemplate> 或 <xref:System.Windows.DataTemplate> 中使用 <xref:System.Windows.Trigger>。  
  
## 示例  
 下面的示例在当 <xref:System.Windows.Controls.Button> 的 <xref:System.Windows.UIElement.IsMouseOver%2A> 属性成为 `true` 时使用 <xref:System.Windows.Trigger> 对该按钮的 <xref:System.Windows.UIElement.Opacity%2A> 进行动画处理。  
  
 [!code-xml[AnimatePropertyStoryboards#PropertyTriggerExample](../../../../samples/snippets/xaml/VS_Snippets_Wpf/AnimatePropertyStoryboards/XAML/PropertyTriggerExample.xaml#propertytriggerexample)]  
  
 属性 <xref:System.Windows.Trigger> 对象所应用的动画的行为比 <xref:System.Windows.EventTrigger> 动画或使用 <xref:System.Windows.Media.Animation.Storyboard> 方法启动的动画的行为更复杂一些。  它们在“提交”时使用的是其他 <xref:System.Windows.Trigger> 对象定义的动画，但是在编写时使用 <xref:System.Windows.EventTrigger> 和方法触发的动画。  
  
## 请参阅  
 <xref:System.Windows.Trigger>   
 [属性动画技术概述](../../../../docs/framework/wpf/graphics-multimedia/property-animation-techniques-overview.md)   
 [演示图板概述](../../../../docs/framework/wpf/graphics-multimedia/storyboards-overview.md)