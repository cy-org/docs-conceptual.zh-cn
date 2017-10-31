---
title: "如何：使用 ColumnDefinitionsCollection 和 RowDefinitionsCollection 来操作列和行 | Microsoft Docs"
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
  - "类, ColumnDefinitionCollection"
  - "类, RowDefinitionCollection"
  - "ColumnDefinitionCollection 类"
  - "控件, Grid 类"
  - "Grid 控件, ColumnDefinitionCollection 类"
  - "Grid 控件, RowDefinitionCollection 类"
  - "RowDefinitionCollection 类"
ms.assetid: bfc7160a-45f2-4e17-9961-df414dfb13c5
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：使用 ColumnDefinitionsCollection 和 RowDefinitionsCollection 来操作列和行
此示例演示如何在 <xref:System.Windows.Controls.ColumnDefinitionCollection> 和 <xref:System.Windows.Controls.RowDefinitionCollection> 类中使用方法来执行像添加、清除或计数行或列内容这样的操作。  例如，您可以对 <xref:System.Windows.Controls.ColumnDefinition> 或 <xref:System.Windows.Controls.RowDefinition> 中包括的项执行 <xref:System.Windows.Controls.ColumnDefinitionCollection.Add%2A>、<xref:System.Windows.Controls.ColumnDefinitionCollection.Clear%2A> 或 <xref:System.Windows.Controls.ColumnDefinitionCollection.Count%2A> 方法。  
  
## 示例  
 下面的示例创建了一个 <xref:System.Windows.Controls.Grid> 元素，其 <xref:System.Windows.FrameworkElement.Name%2A> 为 `grid1`。  <xref:System.Windows.Controls.Grid> 包含保存 <xref:System.Windows.Controls.Button> 元素（每个元素都由不同的集合方法进行控制）的 <xref:System.Windows.Controls.StackPanel>。  单击 <xref:System.Windows.Controls.Button> 时，它将在代码隐藏文件中激活一个方法调用。  
  
 [!code-xml[ColumnDefinitionsGrid#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ColumnDefinitionsGrid/CSharp/Window1.xaml#1)]  
  
 此示例定义了一系列自定义方法，每种自定义方法都与 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 文件中的一个 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件相对应。  您可以用多种方法来更改 <xref:System.Windows.Controls.Grid> 中的列数和行数，包括添加或删除行和列以及计算行和列的总数。  若要防止出现 <xref:System.ArgumentOutOfRangeException> 和 <xref:System.ArgumentException> 异常，可以使用 <xref:System.Windows.Controls.ColumnDefinitionCollection.RemoveRange%2A> 方法提供的错误检查功能。  
  
 [!code-csharp[ColumnDefinitionsGrid#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ColumnDefinitionsGrid/CSharp/Window1.xaml.cs#2)]
 [!code-vb[ColumnDefinitionsGrid#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ColumnDefinitionsGrid/VisualBasic/Window1.xaml.vb#2)]  
  
## 请参阅  
 <xref:System.Windows.Controls.Grid>   
 <xref:System.Windows.Controls.ColumnDefinitionCollection>   
 <xref:System.Windows.Controls.RowDefinitionCollection>