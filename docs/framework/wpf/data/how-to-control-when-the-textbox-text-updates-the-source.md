---
title: "如何：控制文本框文本更新源的时间 | Microsoft Docs"
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
  - "Data Binding — 数据绑定, 源更新的计时"
  - "源代码更新, 计时"
  - "源更新的计时"
ms.assetid: ffb7b96a-351d-4c68-81e7-054033781c64
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：控制文本框文本更新源的时间
本主题描述如何使用 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 属性控制[绑定源](GTMT)更新的执行时间。  本主题使用 <xref:System.Windows.Controls.TextBox> 控件作为示例。  
  
## 示例  
 <xref:System.Windows.Controls.TextBox>.<xref:System.Windows.Controls.TextBox.Text%2A> 属性的默认 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 值为 <xref:System.Windows.Data.UpdateSourceTrigger>。  这意味着如果应用程序的 <xref:System.Windows.Controls.TextBox> 包含数据绑定 <xref:System.Windows.Controls.TextBox>.<xref:System.Windows.Controls.TextBox.Text%2A> 属性，则直到 <xref:System.Windows.Controls.TextBox> 失去焦点（例如，将鼠标移到 <xref:System.Windows.Controls.TextBox> 外单击时），键入到 <xref:System.Windows.Controls.TextBox> 中的文本才能更新源。  
  
 如果希望在键入过程中更新源，请将该绑定的 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 设置为 <xref:System.Windows.Data.UpdateSourceTrigger>。  在下面的示例中，<xref:System.Windows.Controls.TextBox> 和 <xref:System.Windows.Controls.TextBlock> 的 `Text` 属性都绑定到同一源属性。  将 <xref:System.Windows.Controls.TextBox> 绑定的 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 属性设置为 <xref:System.Windows.Data.UpdateSourceTrigger>。  
  
 [!code-xml[SimpleBinding#USTHowTo](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleBinding/VisualBasic/Page1.xaml#usthowto)]  
  
 因此，<xref:System.Windows.Controls.TextBlock> 所显示的文本将与用户输入到 <xref:System.Windows.Controls.TextBox> 中的文本相同（因为源发生更改），如该示例的以下屏幕快照所示：  
  
 ![简单数据绑定示例屏幕快照](../../../../docs/framework/wpf/data/media/databindingsimplebindingsample2.png "DataBindingSimpleBindingSample2")  
  
 如果您具有一个对话框或用户可编辑的窗体，并且希望将源更新延迟到用户完成字段编辑并单击“确定”之后，则可以将绑定的 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 值设置为 <xref:System.Windows.Data.UpdateSourceTrigger>，如下面的示例所示：  
  
 [!code-xml[UpdateSource#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/UpdateSource/CSharp/Window1.xaml#2)]  
  
 如果将 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 值设置为 <xref:System.Windows.Data.UpdateSourceTrigger>，则仅当应用程序调用 <xref:System.Windows.Data.BindingExpression.UpdateSource%2A> 方法时，该源值才会发生更改。  下面的示例演示如何为 `itemNameTextBox` 调用 <xref:System.Windows.Data.BindingExpression.UpdateSource%2A>：  
  
 [!code-csharp[UpdateSource#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/UpdateSource/CSharp/Window1.xaml.cs#1)]
 [!code-vb[UpdateSource#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UpdateSource/VisualBasic/Window1.xaml.vb#1)]  
  
> [!NOTE]
>  此方法可用于其他控件的属性，但请记住，其他大多数属性的默认 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 值为 <xref:System.Windows.Data.UpdateSourceTrigger>。  有关更多信息，请参见 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 属性页。  
  
> [!NOTE]
>  <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 属性用于处理源更新，因此仅适用于 <xref:System.Windows.Data.BindingMode> 或 <xref:System.Windows.Data.BindingMode> 绑定。  若要使 <xref:System.Windows.Data.BindingMode> 和 <xref:System.Windows.Data.BindingMode> 绑定生效，源对象需要提供属性更改通知。  有关更多信息，可以参见本主题中引用的示例。  此外，也可以参见[实现属性更改通知](../../../../docs/framework/wpf/data/how-to-implement-property-change-notification.md)。  
  
## 请参阅  
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)