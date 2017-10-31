---
title: "如何：对控件应用 FocusVisualStyle | Microsoft Docs"
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
  - "FocusVisualStyle 属性"
  - "属性, FocusVisualStyle"
ms.assetid: 363de99e-8ecc-438c-ac4a-f9147432ebd6
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：对控件应用 FocusVisualStyle
此示例演示如何使用 <xref:System.Windows.FrameworkElement.FocusVisualStyle%2A> 属性在资源中创建一个焦点视觉样式，并将该样式应用于某个控件。  
  
## 示例  
 下面的示例定义一个样式，该样式创建其他控件合成，只有当该控件是[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 中的键盘焦点时，才应用该控件合成。  这是通过使用 <xref:System.Windows.Controls.ControlTemplate> 定义一个样式，然后在设置 <xref:System.Windows.FrameworkElement.FocusVisualStyle%2A> 属性时将该样式作为一个资源进行引用来实现的。  
  
 一个类似于边框的外部矩形放置在矩形区域之外。  除非进行了修改，否则样式使用应用了焦点视觉样式的矩形控件的 <xref:System.Windows.FrameworkElement.ActualHeight%2A> 和 <xref:System.Windows.FrameworkElement.ActualWidth%2A> 来调整大小。  本示例为 <xref:System.Windows.FrameworkElement.Margin%2A> 设置了负值，以使边框稍微出现在焦点控件的外部。  
  
 [!code-xml[FEFocusVisualStyle#XAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/FEFocusVisualStyle/CS/page1.xaml#xaml)]  
  
 <xref:System.Windows.FrameworkElement.FocusVisualStyle%2A> 是对显式样式或主题样式附带的任何控件模板样式的补充；控件的主要样式仍然可以使用 <xref:System.Windows.Controls.ControlTemplate> 并将该样式设置为 <xref:System.Windows.FrameworkElement.Style%2A> 属性来创建。  
  
 一个主题或 UI 中应统一使用焦点可视化样式，而不是为每个可设定焦点的元素使用不同的样式。  有关详细信息，请参见[为控件中的焦点设置样式以及 FocusVisualStyle](../../../../docs/framework/wpf/advanced/styling-for-focus-in-controls-and-focusvisualstyle.md)。  
  
## 请参阅  
 <xref:System.Windows.FrameworkElement.FocusVisualStyle%2A>   
 [样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)   
 [为控件中的焦点设置样式以及 FocusVisualStyle](../../../../docs/framework/wpf/advanced/styling-for-focus-in-controls-and-focusvisualstyle.md)