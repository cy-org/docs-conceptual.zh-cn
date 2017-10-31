---
title: "如何：设置绑定更新的通知 | Microsoft Docs"
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
  - "绑定, 更新, 通知"
  - "Data Binding — 数据绑定, 绑定更新的通知"
  - "通知, 绑定更新"
ms.assetid: 5673073e-dbe1-49da-980a-484a88f9595a
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：设置绑定更新的通知
此示例演示如何设置当绑定的[绑定目标](GTMT)（目标）或[绑定源](GTMT)（源）属性更新时收到通知。  
  
## 示例  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 在每次更新绑定源或目标时都会引发数据更新事件。  在内部，此事件用于通知[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]：它应该更新，因为绑定数据已更改。  请注意，若要让这些事件起作用，并让单向或双向绑定正常工作，您需要使用 <xref:System.ComponentModel.INotifyPropertyChanged> 接口实现您的数据类。  有关更多信息，请参见[实现属性更改通知](../../../../docs/framework/wpf/data/how-to-implement-property-change-notification.md)。  
  
 将绑定中的 <xref:System.Windows.Data.Binding.NotifyOnTargetUpdated%2A> 或 <xref:System.Windows.Data.Binding.NotifyOnSourceUpdated%2A> 属性（或两者）设置为 `true`。  您提供的用于侦听此事件的处理程序必须直接附加到您希望收到更改通知的元素，或者如果您希望在上下文中的任何内容发生变化时得到通知，则附加到整个数据上下文。  
  
 下面的示例演示如何设置当目标属性更新时收到通知。  
  
 [!code-xml[DirectionalBinding#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DirectionalBinding/CSharp/Page1.xaml#2)]  
  
 然后您可以根据 EventHandler\<T\> 委托（在本示例中为 *OnTargetUpdated*）分配处理程序来处理该事件：  
  
 [!code-csharp[DirectionalBinding#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DirectionalBinding/CSharp/Page1.xaml.cs#3)]  
[!code-csharp[DirectionalBinding#EndEvent](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DirectionalBinding/CSharp/Page1.xaml.cs#endevent)]  
  
 事件的参数可用于确定已更改属性的详细信息（例如，类型或特定元素信息，如果同一处理程序附加到多个元素），如果在单个元素上有多个绑定属性，则这些详细信息很有用。  
  
## 请参阅  
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)