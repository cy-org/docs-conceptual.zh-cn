---
title: "BindingNavigator 控件概述（Windows 窗体） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "DataNavigator"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "BindingNavigator 控件 [Windows 窗体], 关于 BindingNavigator 控件"
  - "数据 [Windows 窗体], 导航"
  - "数据导航"
  - "记录, 在窗体上导航"
ms.assetid: 4423eede-f8d1-4d02-822f-5bf8432680d0
caps.latest.revision: 26
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 26
---
# BindingNavigator 控件概述（Windows 窗体）
你可以使用 <xref:System.Windows.Forms.BindingNavigator> 控件来创建标准化的方法，以便用户搜索和更改 Windows 窗体上的数据。  频繁对 <xref:System.Windows.Forms.BindingSource> 组件使用 <xref:System.Windows.Forms.BindingNavigator>，以便用户能够在窗体上数据记录之间移动并与记录进行交互。  
  
## BindingNavigator 的工作原理  
 <xref:System.Windows.Forms.BindingNavigator> 控件由包含一系列 <xref:System.Windows.Forms.ToolStripItem> 对象的 <xref:System.Windows.Forms.ToolStrip> 组成，以执行大部分常见的与数据相关的操作：添加数据、删除数据，以及在数据中导航。  默认情况下，<xref:System.Windows.Forms.BindingNavigator> 控件包含这些标准按钮。  以下屏幕快照显示窗体上的 <xref:System.Windows.Forms.BindingNavigator> 控件。  
  
 ![BindingNavigator 控件](../../../../docs/framework/winforms/controls/media/cpdatacontainerctrl.gif "cpDataContainerCtrl")  
  
 下表列出了该控件并介绍了其功能。  
  
|控件|函数|  
|--------|--------|  
|<xref:System.Windows.Forms.BindingNavigator.AddNewItem%2A> 按钮|将新行插入到基础数据源。|  
|<xref:System.Windows.Forms.BindingNavigator.DeleteItem%2A> 按钮|从基础数据源中删除当前行。|  
|<xref:System.Windows.Forms.BindingNavigator.MoveFirstItem%2A> 按钮|移动到基础数据源中的第一项。|  
|<xref:System.Windows.Forms.BindingNavigator.MoveLastItem%2A> 按钮|移动到基础数据源中的最后一项。|  
|<xref:System.Windows.Forms.BindingNavigator.MoveNextItem%2A> 按钮|移动到基础数据源中的下一项。|  
|<xref:System.Windows.Forms.BindingNavigator.MovePreviousItem%2A> 按钮|移动到基础数据源中的上一项。|  
|<xref:System.Windows.Forms.BindingNavigator.PositionItem%2A> 文本框|返回基础数据源中的当前位置。|  
|<xref:System.Windows.Forms.BindingNavigator.CountItem%2A> 文本框|返回基础数据源中的总项数。|  
  
 对于此集合中每个控件，都有相应的以编程方式提供相同功能的 <xref:System.Windows.Forms.BindingSource> 组件成员。  例如，<xref:System.Windows.Forms.BindingNavigator.MoveFirstItem%2A> 按钮对应 <xref:System.Windows.Forms.BindingSource> 组件的 <xref:System.Windows.Forms.BindingSource.MoveFirst%2A> 方法，<xref:System.Windows.Forms.BindingNavigator.DeleteItem%2A> 按钮对应 <xref:System.Windows.Forms.BindingSource.RemoveCurrent%2A> 方法，依次类推。  
  
 如果默认按钮不适合你的应用程序，或者如果你需要其他按钮来支持其他类型的功能，则可以提供你自己的 <xref:System.Windows.Forms.ToolStrip> 按钮。  另请参阅[如何：向 Windows 窗体 BindingNavigator 控件添加“加载”、“保存”和“取消”按钮](../../../../docs/framework/winforms/controls/load-save-and-cancel-bindingnavigator.md)。  
  
## 请参阅  
 <xref:System.Windows.Forms.BindingNavigator>   
 <xref:System.Windows.Forms.BindingSource>   
 [BindingNavigator 控件](../../../../docs/framework/winforms/controls/bindingnavigator-control-windows-forms.md)