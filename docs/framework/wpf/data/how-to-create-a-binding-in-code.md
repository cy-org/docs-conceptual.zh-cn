---
title: "如何：在代码中创建绑定 | Microsoft Docs"
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
  - "绑定数据, 创建"
  - "Data Binding — 数据绑定, 创建"
ms.assetid: 1a606db9-cf5f-42ed-a1c5-9e4722ec77a0
caps.latest.revision: 22
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 22
---
# 如何：在代码中创建绑定
此示例演示如何在代码中创建和设置 <xref:System.Windows.Data.Binding>。  
  
## 示例  
 <xref:System.Windows.FrameworkElement> 类和 <xref:System.Windows.FrameworkContentElement> 类都公开 `SetBinding` 方法。  如果您要绑定一个继承这些类之一的元素，则可以直接调用 <xref:System.Windows.FrameworkElement.SetBinding%2A> 方法。  
  
 下面的示例创建一个名为 `MyData` 的类，该类包含一个名为 `MyDataProperty` 的属性。  
  
 [!code-csharp[CodeOnlyBinding#DataObject](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CodeOnlyBinding/CSharp/MyData.cs#dataobject)]
 [!code-vb[CodeOnlyBinding#DataObject](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CodeOnlyBinding/VisualBasic/MyData.vb#dataobject)]  
  
 下面的示例演示如何创建绑定对象以设置绑定源。  该示例使用 <xref:System.Windows.FrameworkElement.SetBinding%2A> 将 `myText`（它是一个 <xref:System.Windows.Controls.TextBlock> 控件）的 <xref:System.Windows.Controls.TextBlock.Text%2A> 属性绑定到 `MyDataProperty`。  
  
 [!code-csharp[CodeOnlyBinding#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CodeOnlyBinding/CSharp/binding.cs#1)]
 [!code-vb[CodeOnlyBinding#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CodeOnlyBinding/VisualBasic/App.vb#1)]  
  
 有关完整代码示例，请参见[Code\-only Binding Sample](http://msdn.microsoft.com/zh-cn/764aaf0b-2216-4941-9548-9c98da18d1a6)。  
  
 您可以使用 <xref:System.Windows.Data.BindingOperations> 类的 <xref:System.Windows.Data.BindingOperations.SetBinding%2A> 静态方法，而不是调用 <xref:System.Windows.FrameworkElement.SetBinding%2A>。  下面的示例调用 <xref:System.Windows.Data.BindingOperations.SetBinding%2A?displayProperty=fullName>（而不是 <xref:System.Windows.FrameworkElement.SetBinding%2A?displayProperty=fullName>），以将 `myText` 绑定到 `myDataProperty`。  
  
 [!code-csharp[CodeOnlyBinding#BOSetBinding](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CodeOnlyBinding/CSharp/binding.cs#bosetbinding)]
 [!code-vb[CodeOnlyBinding#BOSetBinding](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CodeOnlyBinding/VisualBasic/App.vb#bosetbinding)]  
  
## 请参阅  
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)