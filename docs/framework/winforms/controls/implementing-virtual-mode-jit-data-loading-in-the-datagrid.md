---
title: "在 Windows 窗体 DataGridView 控件中实现实时数据加载的虚拟模式 | Microsoft Docs"
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
  - "数据 [Windows 窗体], 管理大型数据集"
  - "DataGridView 控件 [Windows 窗体], 大型数据集"
  - "DataGridView 控件 [Windows 窗体], 虚拟模式"
  - "示例 [Windows 窗体], 实时数据加载"
  - "实时数据加载"
  - "虚拟模式, 实时数据加载"
ms.assetid: c2a052b9-423c-4ff7-91dc-d8c7c79345f6
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 在 Windows 窗体 DataGridView 控件中实现实时数据加载的虚拟模式
在 <xref:System.Windows.Forms.DataGridView> 控件中实现虚拟模式的一个原因是为了只在需要时才检索数据。  这称为“实时数据加载”。  
  
 例如，如果您正在使用远程数据库中的一个非常大的表，您可能希望只检索显示所需的数据，而且只在用户将新行滚动到视图中时才检索额外的数据，从而避免启动延迟。  如果运行您的应用程序的客户端计算机只有少量内存可供存储数据使用，则您可能还希望在从数据库中检索新值时丢弃无用的数据。  
  
 下面的部分描述如何配合使用 <xref:System.Windows.Forms.DataGridView> 控件与实时缓存。  
  
 若要将本主题中的代码作为一个单独的列表进行复制，请参见 [如何：在 Windows 窗体 DataGridView 控件中实现实时数据加载的虚拟模式](../../../../docs/framework/winforms/controls/virtual-mode-with-just-in-time-data-loading-in-the-datagrid.md)。  
  
## 窗体  
 下面的代码示例定义了一个包含只读 <xref:System.Windows.Forms.DataGridView> 控件的窗体，该控件通过 <xref:System.Windows.Forms.DataGridView.CellValueNeeded> 事件处理程序与 `Cache` 对象进行交互。  `Cache` 对象管理本地存储的值，并使用 `DataRetriever` 对象从 Northwind 示例数据库的 Orders 表中检索值。  `DataRetriever` 对象（实现 `Cache` 类所需要的 `IDataPageRetriever` 接口）还用于初始化 <xref:System.Windows.Forms.DataGridView> 控件的行和列。  
  
 `IDataPageRetriever`、`DataRetriever` 和 `Cache` 类型在本主题的稍后部分予以介绍。  
  
> [!NOTE]
>  将敏感信息（如密码）存储在连接字符串中可能会影响您的应用程序的安全性。  若要控制对数据库的访问，一种较为安全的方法是使用 Windows 身份验证（也称为集成安全性）。  有关更多信息，请参见[保护连接信息](../../../../docs/framework/data/adonet/protecting-connection-information.md)。  
  
 [!code-csharp[System.Windows.Forms.DataGridView.Virtual_lazyloading#100](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.Virtual_lazyloading/CS/lazyloading.cs#100)]
 [!code-vb[System.Windows.Forms.DataGridView.Virtual_lazyloading#100](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.Virtual_lazyloading/VB/lazyloading.vb#100)]  
  
## IDataPageRetriever 接口  
 下面的代码示例定义 `IDataPageRetriever` 接口，该接口由 `DataRetriever` 类实现。  此接口中唯一声明的方法是 `SupplyPageOfData` 方法，它需要提供一个初始行索引以及单个数据页中的行数。  实施者使用这些值来从数据源中检索一个数据子集。  
  
 `Cache` 对象在构造期间使用此接口的实现来加载两页初始数据。  每当需要未缓存的值时，该缓存将丢弃这两页中的一页，然后从 `IDataPageRetriever` 那里请求一个包含值的新页。  
  
 [!code-csharp[System.Windows.Forms.DataGridView.Virtual_lazyloading#201](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.Virtual_lazyloading/CS/lazyloading.cs#201)]
 [!code-vb[System.Windows.Forms.DataGridView.Virtual_lazyloading#201](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.Virtual_lazyloading/VB/lazyloading.vb#201)]  
  
## DataRetriever 类  
 下面的代码示例定义了 `DataRetriever` 类，该类实现了从服务器检索数据页的 `IDataPageRetriever` 接口。  `DataRetriever` 类还提供了 `Columns` 和 `RowCount` 属性，<xref:System.Windows.Forms.DataGridView> 控件使用这两个属性来创建必要的列，以及将适当数量的空行添加到 <xref:System.Windows.Forms.DataGridView.Rows%2A> 集合。  添加空行是必要的，这样该控件就看似包含了表中的所有数据。  这意味着滚动条中的滚动框将具有适当的大小，并且用户将能够访问表中的任何行。  只有将这些行滚动到视图中时，它们才会由 <xref:System.Windows.Forms.DataGridView.CellValueNeeded> 事件处理程序填充。  
  
 [!code-csharp[System.Windows.Forms.DataGridView.Virtual_lazyloading#200](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.Virtual_lazyloading/CS/lazyloading.cs#200)]
 [!code-vb[System.Windows.Forms.DataGridView.Virtual_lazyloading#200](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.Virtual_lazyloading/VB/lazyloading.vb#200)]  
  
## Cache 类  
 下面的代码示例定义 `Cache` 类，它管理通过 `IDataPageRetriever` 实现填充的两个数据页。  `Cache` 类定义了一个 `DataPage` 内部结构，该结构包含一个 <xref:System.Data.DataTable> 以存储单个缓存页中的值，并且计算表示页的上限和下限的行索引。  
  
 `Cache` 类在构造时加载两个数据页。  每当 <xref:System.Windows.Forms.DataGridView.CellValueNeeded> 事件请求值时，`Cache` 对象确定该值是否存在于其两个数据页的其中一页中，如果存在，则返回该值。  如果本地不存在该值，则 `Cache` 对象确定它的两个数据页中哪一页距离当前显示的行最远，然后用包含请求值的新页替换该页，随后返回该请求值。  
  
 假如数据页中的行数与屏幕一次可以显示的行数相同，则此模型可以使对表进行分页的用户有效地返回到最近查看过的页。  
  
 [!code-csharp[System.Windows.Forms.DataGridView.Virtual_lazyloading#300](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.Virtual_lazyloading/CS/lazyloading.cs#300)]
 [!code-vb[System.Windows.Forms.DataGridView.Virtual_lazyloading#300](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.Virtual_lazyloading/VB/lazyloading.vb#300)]  
  
## 附加注意事项  
 上面的代码示例是作为实时数据加载的演示提供的。  您需要根据自己的需要修改该代码以获得最大效率。  至少，您需要为缓存中每个数据页的行数选择一个适当的值。  此值将传入 `Cache` 构造函数。  每页的行数应该不小于 <xref:System.Windows.Forms.DataGridView> 控件中可同时显示的行数。  
  
 为了取得最佳效果，您需要进行性能测试和可用性测试以确定系统和用户需求。  您需要考虑多种因素，包括运行您的应用程序的客户端计算机中的内存量、所用网络连接的可用带宽以及所用服务器的延迟。  带宽和延迟应在使用高峰期确定。  
  
 若要提高应用程序的滚动性能，可增加本地存储的数据量。  但是，若要减少启动时间，则必须避免最初加载过多数据。  您可能需要修改 `Cache` 类以增加它所能存储的数据页的页数。  使用更多的数据页可提高滚动效率，但是您需要根据可用带宽和服务器延迟确定一个数据页的理想行数。  对于较小的页，对服务器的访问将更加频繁，但同时返回请求数据所用的时间也更少。  如果延迟比带宽更重要，则可能需要使用较大的数据页。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.VirtualMode%2A>   
 [Windows 窗体 DataGridView 控件中的性能优化](../../../../docs/framework/winforms/controls/performance-tuning-in-the-windows-forms-datagridview-control.md)   
 [缩放 Windows 窗体 DataGridView 控件的最佳做法](../../../../docs/framework/winforms/controls/best-practices-for-scaling-the-windows-forms-datagridview-control.md)   
 [Windows 窗体 DataGridView 控件中的虚拟模式](../../../../docs/framework/winforms/controls/virtual-mode-in-the-windows-forms-datagridview-control.md)   
 [演练：在 Windows 窗体 DataGridView 控件中实现虚拟模式](../../../../docs/framework/winforms/controls/implementing-virtual-mode-wf-datagridview-control.md)   
 [如何：在 Windows 窗体 DataGridView 控件中实现实时数据加载的虚拟模式](../../../../docs/framework/winforms/controls/virtual-mode-with-just-in-time-data-loading-in-the-datagrid.md)