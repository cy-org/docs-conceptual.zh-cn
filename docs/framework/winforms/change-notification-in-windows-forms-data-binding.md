---
title: "Windows 窗体数据绑定中的更改通知 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "Windows 窗体, 为数据绑定添加更改通知"
  - "Windows 窗体, 数据绑定"
ms.assetid: b5b10f90-0585-41d9-a377-409835262a92
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# Windows 窗体数据绑定中的更改通知
Windows 窗体数据绑定的最重要的概念之一是“更改通知”。  为了确保数据源及绑定控件总是具有最新的数据，必须为数据绑定添加更改通知。  具体地说，您希望确保绑定控件收到对其数据源所做更改的通知，并希望数据源收到对控件的绑定属性所做更改的通知。  
  
 根据数据绑定类型的不同，存在不同类型的更改通知：  
  
-   简单绑定，即单个控件属性绑定到单个对象实例。  
  
-   基于列表的绑定，既可以包括绑定到列表中某一项的属性的单个控件属性，也可以包括绑定到对象列表的控件属性。  
  
 此外，如果要创建希望用于数据绑定的 Windows 窗体控件，则必须将*属性名称*Changed 模式应用于这些控件，以便将对控件的绑定属性进行的更改传播到数据源。  
  
## 简单绑定的更改通知  
 对于简单绑定，当绑定属性的值发生更改时，业务对象必须提供更改通知。  通过为业务对象的每个属性公开*属性名称*Changed 事件，并使用 <xref:System.Windows.Forms.BindingSource> 或使用首选方法（在该方法中，业务对象实现 <xref:System.ComponentModel.INotifyPropertyChanged> 接口，并在属性值发生更改时引发 <xref:System.ComponentModel.INotifyPropertyChanged.PropertyChanged> 事件）将业务对象绑定到控件，可以实现此目的。  有关更多信息，请参见[如何：实现 INotifyPropertyChanged 接口](../../../docs/framework/winforms/how-to-implement-the-inotifypropertychanged-interface.md)。  当使用实现 <xref:System.ComponentModel.INotifyPropertyChanged> 接口的对象时，不必使用 <xref:System.Windows.Forms.BindingSource> 将对象绑定到控件，而是推荐使用 <xref:System.Windows.Forms.BindingSource>。  
  
## 基于列表的绑定的更改通知  
 Windows 窗体根据绑定列表，向绑定控件提供属性更改（列表项属性值的更改）和列表更改（删除项或向列表添加项）信息。  因此，用于数据绑定的列表必须实现 <xref:System.ComponentModel.IBindingList>，该接口提供两种类型的更改通知。  <xref:System.ComponentModel.BindingList%601> 是 <xref:System.ComponentModel.IBindingList> 的泛型实现，专用于 Windows 窗体数据绑定。  可以创建一个 <xref:System.ComponentModel.BindingList%601>，其中包含实现 <xref:System.ComponentModel.INotifyPropertyChanged> 的业务对象类型，该列表自动将 <xref:System.ComponentModel.INotifyPropertyChanged.PropertyChanged> 事件转换为 <xref:System.ComponentModel.IBindingList.ListChanged> 事件。  如果绑定列表不是 <xref:System.ComponentModel.IBindingList>，则必须使用 <xref:System.Windows.Forms.BindingSource> 组件将对象列表绑定到 Windows 窗体控件。  <xref:System.Windows.Forms.BindingSource> 组件将提供与 <xref:System.ComponentModel.BindingList%601> 的属性到列表的转换类似的属性到列表的转换。  有关更多信息，请参见 [如何：使用 BindingSource 和 INotifyPropertyChanged 接口引发更改通知](../../../docs/framework/winforms/controls/raise-change-notifications--bindingsource.md)。  
  
## 自定义控件的更改通知  
 最后，在控件方面，必须为设计用于绑定到数据的每个属性公开*属性名称*Changed 事件。  对控件属性的更改然后将传播到绑定的数据源。  有关更多信息，请参见 [如何：应用 PropertyNameChanged 模式](../../../docs/framework/winforms/how-to-apply-the-propertynamechanged-pattern.md)  
  
## 请参阅  
 <xref:System.Windows.Forms.BindingSource>   
 <xref:System.ComponentModel.INotifyPropertyChanged>   
 <xref:System.ComponentModel.BindingList%601>   
 [Windows 窗体数据绑定](../../../docs/framework/winforms/windows-forms-data-binding.md)   
 [Windows 窗体支持的数据源](../../../docs/framework/winforms/data-sources-supported-by-windows-forms.md)   
 [数据绑定和 Windows 窗体](../../../docs/framework/winforms/data-binding-and-windows-forms.md)