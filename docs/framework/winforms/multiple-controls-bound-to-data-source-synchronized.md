---
title: "如何：确保绑定到同一数据源的多个控件保持同步 | Microsoft Docs"
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
  - "控件 [Windows 窗体], 绑定多个"
  - "控件 [Windows 窗体], 与数据源同步"
ms.assetid: c2f0ecc6-11e6-4c2c-a1ca-0759630c451e
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：确保绑定到同一数据源的多个控件保持同步
在 Windows 窗体中使用数据绑定时，经常有多个控件被绑定到同一数据源。  在某些情况下，可能有必要采取额外步骤，以确保控件的绑定属性彼此之间保持同步，并且与数据源保持同步。  在两种情况下，这些步骤是必要的：  
  
-   如果数据源未实现 <xref:System.ComponentModel.IBindingList>，并因此生成类型 <xref:System.ComponentModel.ListChangedType> 的 <xref:System.ComponentModel.IBindingList.ListChanged> 事件。  
  
-   如果数据源实现 <xref:System.ComponentModel.IEditableObject>。  
  
 在前一种情况下，可使用 <xref:System.Windows.Forms.BindingSource> 将数据源绑定到控件。  在后一种情况下，应使用 <xref:System.Windows.Forms.BindingSource> 并处理 <xref:System.Windows.Forms.BindingSource.BindingComplete> 事件，然后对关联的 <xref:System.Windows.Forms.BindingManagerBase> 调用 <xref:System.Windows.Forms.BindingManagerBase.EndCurrentEdit%2A>。  
  
## 示例  
 下面的代码示例演示如何使用 <xref:System.Windows.Forms.BindingSource> 组件，将三个控件（两个文本框控件和一个 <xref:System.Windows.Forms.DataGridView> 控件）绑定到 <xref:System.Data.DataSet> 中的同一列。  该示例演示如何处理 <xref:System.Windows.Forms.BindingSource.BindingComplete> 事件，并确保当一个文本框的文本值更改时，会用正确的值更新其他文本框和 <xref:System.Windows.Forms.DataGridView> 控件。  
  
 该示例使用 <xref:System.Windows.Forms.BindingSource> 来绑定数据源和控件。  或者，可以直接将控件绑定到数据源，并从窗体的 <xref:System.Windows.Forms.Control.BindingContext%2A> 检索用于绑定的 <xref:System.Windows.Forms.BindingManagerBase>，然后为 <xref:System.Windows.Forms.BindingManagerBase> 处理 <xref:System.Windows.Forms.BindingManagerBase.BindingComplete> 事件。  有关如何进行此操作的示例，请参见 <xref:System.Windows.Forms.BindingManagerBase> 的 <xref:System.Windows.Forms.BindingManagerBase.BindingComplete> 事件的相关帮助页。  
  
 [!code-csharp[System.Windows.Forms.BindingSourceMultipleControls#1](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.BindingSourceMultipleControls/CS/Form1.cs#1)]
 [!code-vb[System.Windows.Forms.BindingSourceMultipleControls#1](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.BindingSourceMultipleControls/VB/Form1.vb#1)]  
  
## 编译代码  
  
-   此代码示例需要  
  
-   对 <xref:System>、<xref:System.Windows.Forms> 和 <xref:System.Drawing> 程序集的引用。  
  
-   一个处理了 <xref:System.Windows.Forms.Form.Load> 事件的窗体，以及从窗体的 <xref:System.Windows.Forms.Form.Load> 事件处理程序对示例中的 `InitializeControlsAndDataSource` 方法的调用。  
  
## 请参阅  
 [如何：使用 BindingSource 组件跨窗体共享绑定数据](../../../docs/framework/winforms/controls/how-to-share-bound-data-across-forms-using-the-bindingsource-component.md)   
 [Windows 窗体数据绑定中的更改通知](../../../docs/framework/winforms/change-notification-in-windows-forms-data-binding.md)   
 [与数据绑定相关的接口](../../../docs/framework/winforms/interfaces-related-to-data-binding.md)   
 [Windows 窗体数据绑定](../../../docs/framework/winforms/windows-forms-data-binding.md)