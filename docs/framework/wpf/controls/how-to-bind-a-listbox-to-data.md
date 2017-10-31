---
title: "如何：将 ListBox 绑定到数据 | Microsoft Docs"
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
  - "绑定数据, 到 ListBox 控件"
  - "Data Binding — 数据绑定, ListBox 控件"
  - "ListBox 控件, 将数据绑定到"
ms.assetid: de93a907-709a-44a7-84bf-578b846a3d8b
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：将 ListBox 绑定到数据
应用程序开发人员可以创建 <xref:System.Windows.Controls.ListBox> 控件，而无需分别指定每个 <xref:System.Windows.Controls.ListBoxItem> 的内容。  可以使用数据绑定将数据绑定到各个项。  
  
 下面的示例演示如何创建 <xref:System.Windows.Controls.ListBox> 并通过将数据绑定到名为 *Colors* 的数据源来填充 <xref:System.Windows.Controls.ListBoxItem> 元素。  在此情况下，不必使用 <xref:System.Windows.Controls.ListBoxItem> 标记来指定各项的内容。  
  
## 示例  
 [!code-xml[ListBoxEvent#7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListBoxEvent/CSharp/Pane1.xaml#7)]  
[!code-xml[ListBoxEvent#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListBoxEvent/CSharp/Pane1.xaml#3)]  
  
## 请参阅  
 <xref:System.Windows.Controls.ListBox>   
 <xref:System.Windows.Controls.ListBoxItem>   
 [控件](../../../../docs/framework/wpf/advanced/optimizing-performance-controls.md)