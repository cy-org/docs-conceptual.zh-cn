---
title: "如何：使用设计器用 Windows 窗体 DataGrid 控件创建主/详细信息列表 | Microsoft Docs"
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
  - "DataGrid 控件 [Windows 窗体], 主-详细信息列表"
  - "主-详细信息列表"
  - "相关表, 在 DataGrid 控件中显示"
ms.assetid: 19438ba2-f687-4417-a2fb-ab1cd69d4ded
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：使用设计器用 Windows 窗体 DataGrid 控件创建主/详细信息列表
> [!NOTE]
>  <xref:System.Windows.Forms.DataGridView> 控件取代了 <xref:System.Windows.Forms.DataGrid> 控件并添加了功能；但是，可以选择保留 <xref:System.Windows.Forms.DataGrid> 控件以实现向后兼容并供将来使用。  有关更多信息，请参见 [Windows 窗体 DataGridView 控件和 DataGrid 控件之间的区别](../../../../docs/framework/winforms/controls/differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)。  
  
 如果 <xref:System.Data.DataSet> 包含一系列相关表，则可以使用两个 <xref:System.Windows.Forms.DataGrid> 控件以主\/详细信息格式显示数据。  一个 <xref:System.Windows.Forms.DataGrid> 被指定为主网格，另一个被指定为详细信息网格。  当在主列表中选择某项时，所有相关的子项都显示在详细信息列表中。  例如，如果 <xref:System.Data.DataSet> 包含 Customers 表和相关的 Orders 表，则您可将 Customers 表指定为主网格，而将 Orders 表指定为详细信息网格。  当从主网格中选择某个客户时，Orders 表中与该客户关联的所有订单都将显示在详细信息网格中。  
  
 下面的过程需要一个**“Windows 应用程序”**项目。  有关设置此类项目的信息，请参见 [How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 在设计器中创建主\/详细信息列表  
  
1.  向窗体添加两个 <xref:System.Windows.Forms.DataGrid> 控件。  有关更多信息，请参见 [如何：向 Windows 窗体添加控件](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)。  在 [!INCLUDE[vsprvslong](../../../../includes/vsprvslong-md.md)] 中，默认情况下，<xref:System.Windows.Forms.DataGrid> 控件不在**“工具箱”**中。  有关更多信息，请参见[How to: Add Items to the Toolbox](http://msdn.microsoft.com/zh-cn/458e119e-17fe-450b-b889-e31c128bd7e0)。  
  
    > [!NOTE]
    >  下列步骤不适用于使用**“数据源”**窗口进行设计时数据绑定的 [!INCLUDE[vsprvslong](../../../../includes/vsprvslong-md.md)]。  有关更多信息，请参见[在 Visual Studio 中将控件绑定到数据](../Topic/Bind%20controls%20to%20data%20in%20Visual%20Studio.md)和[如何：在 Windows 窗体应用程序中显示相关数据](../Topic/How%20to:%20Display%20Related%20Data%20in%20a%20Windows%20Forms%20Application.md)。  
  
2.  将两个或多个表从**“服务器资源管理器”**拖到窗体上。  
  
3.  从**“数据”**菜单中选择**“生成数据集”**。  
  
4.  使用 XML 设计器设置表之间的关系。  有关详细信息，请参见 MSDN 上的“如何：在 XML 架构和数据集内创建一对多关系”。  
  
5.  通过从**“文件”**菜单选择**“全部保存”**来保存关系。  
  
6.  配置想要指定为主网格的 <xref:System.Windows.Forms.DataGrid> 控件，如下所示：  
  
    1.  从 <xref:System.Windows.Forms.DataGrid.DataSource%2A> 属性的下拉列表选择 <xref:System.Data.DataSet>。  
  
    2.  从 <xref:System.Windows.Forms.DataGrid.DataMember%2A> 属性的下拉列表中选择主表（例如“Customers”）。  
  
7.  配置想要指定为详细信息网格的 <xref:System.Windows.Forms.DataGrid> 控件，如下所示：  
  
    1.  从 <xref:System.Windows.Forms.DataGrid.DataSource%2A> 属性的下拉列表选择 <xref:System.Data.DataSet>。  
  
    2.  从 <xref:System.Windows.Forms.DataGrid.DataMember%2A> 属性的下拉列表中选择主表与详细信息表之间的关系（例如“Customers.CustOrd”）。  为了查看关系，请通过单击下拉列表中主表旁边的加号 \(**\+**\) 来展开节点。  
  
## 请参阅  
 [DataGrid 控件](../../../../docs/framework/winforms/controls/datagrid-control-windows-forms.md)   
 [DataGrid 控件概述](../../../../docs/framework/winforms/controls/datagrid-control-overview-windows-forms.md)   
 [如何：将 Windows 窗体 DataGrid 控件绑定到数据源](../../../../docs/framework/winforms/controls/how-to-bind-the-windows-forms-datagrid-control-to-a-data-source.md)   
 [在 Visual Studio 中将控件绑定到数据](../Topic/Bind%20controls%20to%20data%20in%20Visual%20Studio.md)