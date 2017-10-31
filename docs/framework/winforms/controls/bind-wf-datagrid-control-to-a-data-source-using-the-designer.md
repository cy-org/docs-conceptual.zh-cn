---
title: "如何：使用设计器将 Windows 窗体 DataGrid 控件绑定到数据源 | Microsoft Docs"
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
  - "绑定控件"
  - "绑定控件, DataGrid 控件"
  - "数据绑定, DataGrid 控件"
  - "数据绑定控件, DataGrid"
  - "DataGrid 控件 [Windows 窗体], 数据绑定"
  - "数据集 [Windows 窗体], 绑定到 DataGrid 控件"
  - "Windows 窗体控件, 数据绑定"
ms.assetid: 4e96e3d0-b1cc-4de1-8774-bc9970ec4554
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：使用设计器将 Windows 窗体 DataGrid 控件绑定到数据源
> [!NOTE]
>  <xref:System.Windows.Forms.DataGridView> 控件取代了 <xref:System.Windows.Forms.DataGrid> 控件并添加了功能；但是，可以选择保留 <xref:System.Windows.Forms.DataGrid> 控件以实现向后兼容并供将来使用。  有关更多信息，请参见 [Windows 窗体 DataGridView 控件和 DataGrid 控件之间的区别](../../../../docs/framework/winforms/controls/differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)。  
  
 Windows 窗体 <xref:System.Windows.Forms.DataGrid> 控件是专为显示来自数据源的信息而设计的。  可以在设计时通过设置 <xref:System.Windows.Forms.DataGrid.DataSource%2A> 和 <xref:System.Windows.Forms.DataGrid.DataMember%2A> 属性来绑定该控件，或在运行时通过调用 <xref:System.Windows.Forms.DataGrid.SetDataBinding%2A> 方法来绑定该控件。  虽然可以显示来自各种数据源的数据，但最常见的数据源是数据集和数据视图。  
  
 如果数据源在设计时可用（例如，窗体包含数据集或数据视图的实例时），则可以在设计时将该网格绑定到数据源。  然后可以预览数据在网格中的显示情况。  
  
 也可以在运行时以编程方式绑定网格。  当您希望依据在运行时获得的信息来设置数据源时，采用这种方式很有用。  例如，应用程序可能让用户指定要查看的表的名称。  在设计时不存在数据源的情况下，也有必要采用这种方式。  这包括诸如数组、集合、非类型化数据集和数据阅读器之类的数据源。  
  
 下面的过程需要一个**“Windows 应用程序”**项目，该项目拥有一个包含 <xref:System.Windows.Forms.DataGrid> 控件的窗体。  有关设置此类项目的信息，请参见[How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)和[如何：向 Windows 窗体添加控件](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)。  在 [!INCLUDE[vsprvslong](../../../../includes/vsprvslong-md.md)] 中，默认情况下，<xref:System.Windows.Forms.DataGrid> 控件不在**“工具箱”**中。  有关添加该控件的信息，请参见[How to: Add Items to the Toolbox](http://msdn.microsoft.com/zh-cn/458e119e-17fe-450b-b889-e31c128bd7e0)。  另外，在 [!INCLUDE[vsprvslong](../../../../includes/vsprvslong-md.md)] 中，可以使用**“数据源”**窗口来进行设计时数据绑定。  有关更多信息，请参见[在 Visual Studio 中将控件绑定到数据](../Topic/Bind%20controls%20to%20data%20in%20Visual%20Studio.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 在设计器中将 DataGrid 控件数据绑定到单个表  
  
1.  将该控件的 <xref:System.Windows.Forms.DataGrid.DataSource%2A> 属性设置为包含您要绑定到的数据项的对象。  
  
2.  如果数据源是数据集，应将 <xref:System.Windows.Forms.DataGrid.DataMember%2A> 属性设置为要绑定到的表的名称。  
  
3.  如果数据源是数据集或基于数据集表的数据视图，请向窗体添加代码来填充数据集。  
  
     所使用的确切代码取决于数据集从何处获取数据。  如果要从数据库中直接填充数据集，通常可以调用数据适配器的 `Fill` 方法，如下面的代码示例（它填充名为 `DsCategories1` 的数据集）所示：  
  
    ```vb  
    sqlDataAdapter1.Fill(DsCategories1)  
  
    ```  
  
    ```csharp  
    sqlDataAdapter1.Fill(DsCategories1);  
  
    ```  
  
    ```cpp  
    sqlDataAdapter1->Fill(dsCategories1);  
    ```  
  
4.  （可选）将适当的表样式和列样式添加到网格中。  
  
     如果没有表样式，您将看见该表，但其格式设置很少，且所有列均可见。  
  
### 在设计器中将 DataGrid 控件数据绑定到数据集中的多个表  
  
1.  将该控件的 <xref:System.Windows.Forms.DataGrid.DataSource%2A> 属性设置为包含您要绑定到的数据项的对象。  
  
2.  如果数据集包含相关表（即，如果它包含关系对象），请将 <xref:System.Windows.Forms.DataGrid.DataMember%2A> 属性设置为父表的名称。  
  
3.  编写代码来填充数据集。  
  
## 请参阅  
 [DataGrid 控件概述](../../../../docs/framework/winforms/controls/datagrid-control-overview-windows-forms.md)   
 [如何：向 Windows 窗体 DataGrid 控件添加表和列](../../../../docs/framework/winforms/controls/how-to-add-tables-and-columns-to-the-windows-forms-datagrid-control.md)   
 [DataGrid 控件](../../../../docs/framework/winforms/controls/datagrid-control-windows-forms.md)   
 [Windows 窗体数据绑定](../../../../docs/framework/winforms/windows-forms-data-binding.md)   
 [在 Visual Studio 中访问数据](../Topic/Accessing%20data%20in%20Visual%20Studio.md)