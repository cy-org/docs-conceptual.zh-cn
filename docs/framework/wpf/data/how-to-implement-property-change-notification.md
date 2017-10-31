---
title: "如何：实现属性更改通知 | Microsoft Docs"
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
  - "更改通知"
  - "Data Binding — 数据绑定, 属性更改通知"
  - "更改通知"
  - "属性, 更改通知"
ms.assetid: 30b59d9e-8c3a-4349-aa82-4be837e841cf
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：实现属性更改通知
若要支持 <xref:System.Windows.Data.BindingMode> 或 <xref:System.Windows.Data.BindingMode> 绑定，从而使[绑定目标](GTMT)属性能够自动反映[绑定源](GTMT)的动态更改（例如，用户编辑窗体后，预览窗格会自动更新），类需要提供相应的属性更改通知。  此示例介绍了如何创建实现 <xref:System.ComponentModel.INotifyPropertyChanged> 的类。  
  
## 示例  
 若要实现 <xref:System.ComponentModel.INotifyPropertyChanged>，需要声明 <xref:System.ComponentModel.INotifyPropertyChanged.PropertyChanged> 事件并创建 `OnPropertyChanged` 方法。  然后，对于每个需要更改通知的属性，只要进行了更新，就可以调用 `OnPropertyChanged`。  
  
 [!code-csharp[SimpleBinding#PersonClass](../../../../samples/snippets/csharp/VS_Snippets_Wpf/SimpleBinding/CSharp/Person.cs#personclass)]
 [!code-vb[SimpleBinding#PersonClass](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleBinding/VisualBasic/Person.vb#personclass)]  
  
 有关 `Person` 类如何可用于支持 <xref:System.Windows.Data.BindingMode> 绑定的示例，请参见[控制文本框文本更新源的时间](../../../../docs/framework/wpf/data/how-to-control-when-the-textbox-text-updates-the-source.md)。  
  
## 请参阅  
 [绑定源概述](../../../../docs/framework/wpf/data/binding-sources-overview.md)   
 [数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)   
 [帮助主题](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)