---
title: "如何：绑定两个控件的属性 | Microsoft Docs"
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
  - "绑定两个控件的属性"
  - "控件, 绑定属性"
  - "Data Binding — 数据绑定, 绑定两个控件的属性"
ms.assetid: 06318fac-6afd-4c7d-a277-6d7ef50f47bc
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：绑定两个控件的属性
此示例演示如何使用 <xref:System.Windows.Data.Binding.ElementName%2A> 属性将一个已实例化的控件的属性绑定到另一个控件的属性。  
  
## 示例  
 下例演示如何将 <xref:System.Windows.Controls.Canvas> 的 <xref:System.Windows.Controls.Panel.Background%2A> 属性绑定到 <xref:System.Windows.Controls.ComboBox> 的 <xref:System.Windows.Controls.Primitives.Selector.SelectedItem%2A>.<xref:System.Windows.Controls.ContentControl.Content%2A> 属性：  
  
 [!code-xml[BindDptoDp#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BindDPtoDP/CS/Window1.xaml#1)]  
  
 当此示例呈现时，应如下所示：  
  
 ![具有绿色背景的画布](../../../../docs/framework/wpf/data/media/databindingbindingdpssample.png "DataBindingBindingDPsSample")  
  
 **注意** [绑定目标](GTMT)属性（在本示例中是 <xref:System.Windows.Controls.Panel.Background%2A> 属性）必须是一个[依赖项属性](GTMT)。  有关更多信息，请参见[数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)。  
  
## 请参阅  
 [指定绑定源](../../../../docs/framework/wpf/data/how-to-specify-the-binding-source.md)   
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)