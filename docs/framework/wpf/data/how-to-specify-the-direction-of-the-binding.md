---
title: "如何：指定绑定的方向 | Microsoft Docs"
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
  - "绑定方向"
  - "Data Binding — 数据绑定, 绑定的方向"
  - "绑定的方向"
ms.assetid: 37334478-028b-4514-86c9-1420709f4818
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 20
---
# 如何：指定绑定的方向
此示例演示如何指定绑定是仅更新[绑定目标](GTMT)（目标）属性或[绑定源](GTMT)（源）属性，还是同时更新目标属性和源属性。  
  
## 示例  
 使用 <xref:System.Windows.Data.Binding.Mode%2A> 属性指定绑定的方向。  以下枚举列表列出了可供绑定更新的选项：  
  
-   无论是目标属性还是源属性，只要发生了更改，<xref:System.Windows.Data.BindingMode> 就会更新目标属性或源属性。  
  
-   <xref:System.Windows.Data.BindingMode> 仅当源属性发生更改时更新目标属性。  
  
-   <xref:System.Windows.Data.BindingMode> 仅当应用程序启动时或 <xref:System.Windows.FrameworkElement.DataContext%2A> 进行更改时更新目标属性。  
  
-   <xref:System.Windows.Data.BindingMode> 在目标属性更改时更新源属性。  
  
-   <xref:System.Windows.Data.BindingMode>：使用目标属性的默认 <xref:System.Windows.Data.Binding.Mode%2A> 值。  
  
 有关更多信息，请参见 <xref:System.Windows.Data.BindingMode>。  
  
 下面的示例演示如何设置 <xref:System.Windows.Data.Binding.Mode%2A> 属性。  
  
 [!code-xml[DirectionalBinding#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DirectionalBinding/CSharp/Page1.xaml#4)]  
  
 若要检测源更改（适用于 <xref:System.Windows.Data.BindingMode> 和 <xref:System.Windows.Data.BindingMode> 绑定），则源必须实现一种合适的属性更改通知机制（如 <xref:System.ComponentModel.INotifyPropertyChanged>）。  有关 <xref:System.ComponentModel.INotifyPropertyChanged> 实现的示例，请参见[实现属性更改通知](../../../../docs/framework/wpf/data/how-to-implement-property-change-notification.md)。  
  
 对于 <xref:System.Windows.Data.BindingMode> 或 <xref:System.Windows.Data.BindingMode> 绑定，可以通过设置 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 属性来控制源更新计时。  有关更多信息，请参见 <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A>。  
  
## 请参阅  
 <xref:System.Windows.Data.Binding>   
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)