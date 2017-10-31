---
title: "Windows 窗体 DataGridView 控件中的性能优化 | Microsoft Docs"
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
  - "DataGridView 控件 [Windows 窗体], 性能优化"
  - "性能优化, 数据网格"
  - "性能, DataGridView 控件"
ms.assetid: 6ccbff28-a0ff-41e4-b601-61b31b61851d
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Windows 窗体 DataGridView 控件中的性能优化
当处理大量数据时，除非谨慎地使用 `DataGridView` 控件，否则该控件可能占用大量内存，从而增加系统开销。  在具有有限内存的客户端上，可以避免使用具有高内存成本的功能，从而避免一定的系统开销。  还可以使用虚拟模式来自己管理部分或全部数据维护和检索任务，这样您便可以根据具体的情况来自定义内存使用。  
  
## 本节内容  
 [缩放 Windows 窗体 DataGridView 控件的最佳做法](../../../../docs/framework/winforms/controls/best-practices-for-scaling-the-windows-forms-datagridview-control.md)  
 描述在处理大量数据时，如何正确使用 `DataGridView` 控件，以避免不必要的内存使用和性能影响。  
  
 [Windows 窗体 DataGridView 控件中的虚拟模式](../../../../docs/framework/winforms/controls/virtual-mode-in-the-windows-forms-datagridview-control.md)  
 描述如何使用虚拟模式来补充或取代标准数据绑定机制。  
  
 [演练：在 Windows 窗体 DataGridView 控件中实现虚拟模式](../../../../docs/framework/winforms/controls/implementing-virtual-mode-wf-datagridview-control.md)  
 描述如何实现几个虚拟模式事件的处理程序。  还演示如何实现用户编辑的行级回滚和提交。  
  
 [在 Windows 窗体 DataGridView 控件中实现实时数据加载的虚拟模式](../../../../docs/framework/winforms/controls/implementing-virtual-mode-jit-data-loading-in-the-datagrid.md)  
 描述如何按需加载数据，当要显示的数据比可用客户端内存可以存储的数据多时，按需加载非常有用。  
  
## 参考  
 <xref:System.Windows.Forms.DataGridView>  
 提供 <xref:System.Windows.Forms.DataGridView> 控件的参考文档。  
  
 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A>  
 提供 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A> 属性的参考文档。  
  
## 请参阅  
 [DataGridView 控件](../../../../docs/framework/winforms/controls/datagridview-control-windows-forms.md)   
 [Windows 窗体 DataGridView 控件中的数据显示模式](../../../../docs/framework/winforms/controls/data-display-modes-in-the-windows-forms-datagridview-control.md)