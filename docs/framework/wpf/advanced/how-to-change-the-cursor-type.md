---
title: "如何：更改光标类型 | Microsoft Docs"
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
  - "光标（鼠标指针）"
  - "鼠标指针（光标）, 光标类型"
ms.assetid: 08c945a7-8ab0-4320-acf3-0b4955a344c2
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：更改光标类型
本示例演示如何针对特定元素和应用程序更改鼠标指针的 <xref:System.Windows.Input.Cursor>。  
  
 本示例包括一个[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 文件和一个代码隐藏文件。  
  
## 示例  
 创建用户界面，它包含一个用于选择所需的 <xref:System.Windows.Input.Cursor> 的 <xref:System.Windows.Controls.ComboBox>、一对用于确定光标更改是仅应用于单个元素还是应用于整个应用程序的 <xref:System.Windows.Controls.RadioButton> 对象以及一个 <xref:System.Windows.Controls.Border>（新光标将应用于的元素）。  
  
 [!code-xml[cursors#ChangeCursorsXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/cursors/CSharp/Window1.xaml#changecursorsxaml)]  
  
 下面的代码隐藏创建一个 <xref:System.Windows.Controls.Primitives.Selector.SelectionChanged> 事件处理程序，当 <xref:System.Windows.Controls.ComboBox> 中的光标类型发生变化时，将调用该处理程序。  switch 语句用于筛选光标名称，并设置名为 *DisplayArea* 的 <xref:System.Windows.Controls.Border> 上的 <xref:System.Windows.FrameworkElement.Cursor%2A> 属性。  
  
 如果光标更改设置为“Entire Application”（整个应用程序），则 <xref:System.Windows.Input.Mouse.OverrideCursor%2A> 属性将设置为 <xref:System.Windows.Controls.Border> 控件的 <xref:System.Windows.FrameworkElement.Cursor%2A> 属性。  这会强制为整个应用程序更改光标。  
  
 [!code-csharp[cursors#ChangeCursorsSample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/cursors/CSharp/Window1.xaml.cs#changecursorssample)]
 [!code-vb[cursors#ChangeCursorsSample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/cursors/VisualBasic/Window1.xaml.vb#changecursorssample)]  
  
## 请参阅  
 [输入概述](../../../../docs/framework/wpf/advanced/input-overview.md)