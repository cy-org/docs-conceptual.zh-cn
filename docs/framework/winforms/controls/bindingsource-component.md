---
title: "BindingSource 组件 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "BindingSource 组件 [Windows 窗体]"
  - "数据绑定, Windows 窗体"
  - "Windows 窗体, 数据绑定控件"
ms.assetid: 3e2faf4c-f5b8-4fa6-9fbc-f59c37ec2fb9
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 20
---
# BindingSource 组件
Encapsulates a data source for binding to controls.  
  
 <xref:System.Windows.Forms.BindingSource> 组件有两个用途。  首先，将一个窗体的控件绑定到数据时，该组件会提供一个间接层。  这是通过将 <xref:System.Windows.Forms.BindingSource> 组件与你的数据源绑定，然后将窗体上的控件绑定到 <xref:System.Windows.Forms.BindingSource> 组件完成的。  与数据的所有进一步交互（包括导航、排序、筛选和更新）都是通过调用 <xref:System.Windows.Forms.BindingSource> 组件来完成的。  
  
 第二，<xref:System.Windows.Forms.BindingSource> 组件可以充当强类型的数据源。  通过使用 <xref:System.Windows.Forms.BindingSource.Add%2A> 方法向 <xref:System.Windows.Forms.BindingSource> 组件添加一个类型来创建该类型的列表。  
  
## 本节内容  
 [BindingSource 组件概述](../../../../docs/framework/winforms/controls/bindingsource-component-overview.md)  
 介绍 <xref:System.Windows.Forms.BindingSource> 组件的一般概念，这些概念使你能将数据源绑定到控件。  
  
 [如何：将 Windows 窗体控件绑定到 DBNull 数据库值](../../../../docs/framework/winforms/controls/how-to-bind-windows-forms-controls-to-dbnull-database-values.md)  
 演示如何使用 <xref:System.Windows.Forms.BindingSource> 组件处理数据源的 <xref:System.DBNull>值。  
  
 [如何：使用 Windows 窗体 BindingSource 组件对 ADO.NET 数据进行排序和筛选](../../../../docs/framework/winforms/controls/sort-and-filter-ado-net-data-with-wf-bindingsource-component.md)  
 演示如何使用 <xref:System.Windows.Forms.BindingSource> 组件将排序和筛选应用到显示的数据上。  
  
 [如何：使用 Windows 窗体 BindingSource 绑定到 Web 服务](../../../../docs/framework/winforms/controls/how-to-bind-to-a-web-service-using-the-windows-forms-bindingsource.md)  
 演示如何使用 <xref:System.Windows.Forms.BindingSource> 组件绑定到 Web 服务。  
  
 [如何：处理因数据绑定而发生的错误和异常](../../../../docs/framework/winforms/controls/how-to-handle-errors-and-exceptions-that-occur-with-databinding.md)  
 演示如何使用 <xref:System.Windows.Forms.BindingSource> 组件妥善处理数据在绑定操作中发生的错误。  
  
 [如何：将 Windows 窗体控件绑定到类型](../../../../docs/framework/winforms/controls/how-to-bind-a-windows-forms-control-to-a-type.md)  
 演示如何使用 <xref:System.Windows.Forms.BindingSource> 组件绑定到一种类型。  
  
 [如何：将 Windows 窗体控件绑定到 Factory 对象](../../../../docs/framework/winforms/controls/how-to-bind-a-windows-forms-control-to-a-factory-object.md)  
 演示如何使用 <xref:System.Windows.Forms.BindingSource> 组件绑定到 Factory 对象或方法。  
  
 [如何：使用 Windows 窗体 BindingSource 自定义项添加](../../../../docs/framework/winforms/controls/how-to-customize-item-addition-with-the-windows-forms-bindingsource.md)  
 演示如何使用 <xref:System.Windows.Forms.BindingSource> 组件创建新项并将它们添加到数据源。  
  
 [如何：使用 BindingSource ResetItem 方法引发更改通知](../../../../docs/framework/winforms/controls/how-to-raise-change-notifications-using-the-bindingsource-resetitem-method.md)  
 演示如何使用 <xref:System.Windows.Forms.BindingSource> 组件引发对不支持更改通知的数据源的更改通知事件。  
  
 [如何：使用 BindingSource 和 INotifyPropertyChanged 接口引发更改通知](../../../../docs/framework/winforms/controls/raise-change-notifications--bindingsource.md)  
 演示如何将继承自 <xref:System.ComponentModel.INotifyPropertyChanged> 的类型用于 <xref:System.Windows.Forms.BindingSource> 控件。  
  
 [如何：使用 BindingSource 在 Windows 窗体控件中反映数据源更新](../../../../docs/framework/winforms/controls/reflect-data-source-updates-in-a-wf-control-with-the-bindingsource.md)  
 演示如何使用 <xref:System.Windows.Forms.BindingSource> 组件响应数据源中的更改。  
  
 [如何：使用 BindingSource 组件跨窗体共享绑定数据](../../../../docs/framework/winforms/controls/how-to-share-bound-data-across-forms-using-the-bindingsource-component.md)  
 演示如何使用 <xref:System.Windows.Forms.BindingSource> 将多个窗体绑定到相同的数据源。  
  
## 参考  
 <xref:System.Windows.Forms.BindingSource>  
 提供关于 <xref:System.Windows.Forms.BindingSource> 组件的参考文档。  
  
 <xref:System.Windows.Forms.BindingNavigator>  
 提供关于 <xref:System.Windows.Forms.BindingNavigator> 控件的参考文档。  
  
## 相关章节  
 [Windows 窗体数据绑定](../../../../docs/framework/winforms/windows-forms-data-binding.md)  
 包含描述 Windows 窗体数据绑定体系结构的主题链接。  
  
 另请参阅[在 Visual Studio 中将控件绑定到数据](../Topic/Bind%20controls%20to%20data%20in%20Visual%20Studio.md)。