---
title: "如何：绑定到枚举 | Microsoft Docs"
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
  - "绑定数据, 枚举"
  - "数据绑定, 枚举"
  - "枚举"
ms.assetid: b9091eba-1119-424e-868b-d1a4168b3732
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：绑定到枚举
本示例演示如何通过绑定到枚举的 GetValues 方法来绑定到该枚举。  
  
## 示例  
 在下面的示例中，<xref:System.Windows.Controls.ListBox> 通过数据绑定显示 <xref:System.Windows.HorizontalAlignment> 枚举值的列表。  <xref:System.Windows.Controls.ListBox> 和 <xref:System.Windows.Controls.Button> 绑定，这样，您可以通过在 <xref:System.Windows.Controls.ListBox> 中选择一个值来更改 <xref:System.Windows.Controls.Button> 的 <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> 属性值。  
  
 [!code-xml[BindToEnum#BindToEnum](../../../../samples/snippets/csharp/VS_Snippets_Wpf/BindToEnum/CS/Window1.xaml#bindtoenum)]  
  
## 请参阅  
 [绑定到方法](../../../../docs/framework/wpf/data/how-to-bind-to-a-method.md)   
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)