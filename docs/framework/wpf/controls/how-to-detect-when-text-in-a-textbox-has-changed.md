---
title: "如何：检测 TextBox 中的文本何时更改 | Microsoft Docs"
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
  - "检测文本更改"
  - "文本更改, 检测"
  - "TextBox 控件, 检测文本更改"
ms.assetid: 1c39ee14-e37f-49fb-a0d1-a9824ca13584
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：检测 TextBox 中的文本何时更改
使用本示例所演示的方法，可以在 <xref:System.Windows.Controls.TextBox> 控件中的文本发生更改时，使用 <xref:System.Windows.Controls.Primitives.TextBoxBase.TextChanged> 事件执行相应的方法。  
  
 在包含您要监视其是否发生更改的 <xref:System.Windows.Controls.TextBox> 控件的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 代码隐藏类中，插入一个要在 <xref:System.Windows.Controls.Primitives.TextBoxBase.TextChanged> 事件激发时调用的方法。  此方法必须具有一个与 <xref:System.Windows.Controls.TextChangedEventHandler> 委托所期望的签名相匹配的签名。  
  
 每当 <xref:System.Windows.Controls.TextBox> 控件的内容由用户更改或以编程方式更改时，都会调用该事件处理程序。  
  
 **注意：**当创建 <xref:System.Windows.Controls.TextBox> 控件并用文本最初填充它时，将激发此事件。  
  
## 示例  
 在用来定义 <xref:System.Windows.Controls.TextBox> 控件的[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 中，使用与事件处理程序方法名称相匹配的值来指定 <xref:System.Windows.Controls.Primitives.TextBoxBase.TextChanged> 特性。  
  
 [!code-xml[TextBox_MiscCode#_TextChangedXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml#_textchangedxaml)]  
  
## 示例  
 在包含您要监视其是否发生更改的 <xref:System.Windows.Controls.TextBox> 控件的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 代码隐藏类中，插入一个要在 <xref:System.Windows.Controls.Primitives.TextBoxBase.TextChanged> 事件激发时调用的方法。  此方法必须具有一个与 <xref:System.Windows.Controls.TextChangedEventHandler> 委托所期望的签名相匹配的签名。  
  
 [!code-csharp[TextBox_MiscCode#_TextChangedEventHandler](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml.cs#_textchangedeventhandler)]
 [!code-vb[TextBox_MiscCode#_TextChangedEventHandler](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/TextBox_MiscCode/VisualBasic/Window1.xaml.vb#_textchangedeventhandler)]  
  
 每当 <xref:System.Windows.Controls.TextBox> 控件的内容由用户更改或以编程方式更改时，都会调用该事件处理程序。  
  
 **注意：**当创建 <xref:System.Windows.Controls.TextBox> 控件并用文本最初填充它时，将激发此事件。  
  
 注释  
  
## 请参阅  
 <xref:System.Windows.Controls.TextChangedEventArgs>   
 [TextBox 概述](../../../../docs/framework/wpf/controls/textbox-overview.md)   
 [RichTextBox 概述](../../../../docs/framework/wpf/controls/richtextbox-overview.md)