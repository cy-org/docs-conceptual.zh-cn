---
title: "如何：使用设计器设置 Windows 窗体 DataGrid 控件的格式 | Microsoft Docs"
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
  - "颜色, 应用于 DataGrid 控件"
  - "列 [Windows 窗体], DataGrid 控件"
  - "DataGrid 控件 [Windows 窗体], 默认样式"
  - "DataGrid 控件 [Windows 窗体], 格式化"
  - "格式设置 [Windows 窗体]"
  - "表 [Windows 窗体], DataGrid 控件中的格式设置"
ms.assetid: 533b9814-6124-49dc-9fda-085f1502609f
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：使用设计器设置 Windows 窗体 DataGrid 控件的格式
> [!NOTE]
>  <xref:System.Windows.Forms.DataGridView> 控件取代了 <xref:System.Windows.Forms.DataGrid> 控件并添加了功能；但是，可以选择保留 <xref:System.Windows.Forms.DataGrid> 控件以实现向后兼容并供将来使用。  有关更多信息，请参见 [Windows 窗体 DataGridView 控件和 DataGrid 控件之间的区别](../../../../docs/framework/winforms/controls/differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)。  
  
 对 <xref:System.Windows.Forms.DataGrid> 控件的不同部分应用不同颜色可使得该控件中的信息更加易于阅读和解释。  颜色可以应用于行和列。  您还可以自行决定隐藏还是显示行和列。  
  
 设置 <xref:System.Windows.Forms.DataGrid> 控件的格式涉及三个基本方面：  
  
-   您可以设置属性来建立显示数据的默认样式。  
  
-   以此为基础，接着可以自定义某些表在运行时的显示方式。  
  
-   最后，您可以修改在数据网格中显示哪些列以及显示哪些颜色和其他格式设置。  
  
 设置数据网格的格式时，首先可以设置 <xref:System.Windows.Forms.DataGrid> 本身的属性。  以这些颜色和格式选择为基础，您可以根据显示的数据表和列进行更改。  
  
 下面的过程需要一个**“Windows 应用程序”**项目，该项目拥有一个包含 <xref:System.Windows.Forms.DataGrid> 控件的窗体。  有关设置此类项目的信息，请参见[How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)和[如何：向 Windows 窗体添加控件](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)。  在 [!INCLUDE[vsprvslong](../../../../includes/vsprvslong-md.md)] 中，默认情况下，<xref:System.Windows.Forms.DataGrid> 控件不在**“工具箱”**中。  有关更多信息，请参见[How to: Add Items to the Toolbox](http://msdn.microsoft.com/zh-cn/458e119e-17fe-450b-b889-e31c128bd7e0)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 为 DataGrid 控件创建默认样式  
  
1.  选择 <xref:System.Windows.Forms.DataGrid> 控件。  
  
2.  在**“属性”**窗口中，根据需要设置下列属性。  
  
    |属性|说明|  
    |--------|--------|  
    |<xref:System.Windows.Forms.DataGrid.AlternatingBackColor%2A>|`BackColor` 属性定义网格偶数行的颜色。  在将 <xref:System.Windows.Forms.DataGrid.AlternatingBackColor%2A> 属性设置为另一种颜色时，间隔行（第 1 行、第 3 行、第 5 行，等等）将设置为此新颜色。|  
    |<xref:System.Windows.Forms.DataGrid.BackColor%2A>|网格偶数行（第 0 行、第 2 行、第 4 行、第 6 行，等等）的背景色。|  
    |<xref:System.Windows.Forms.DataGrid.BackgroundColor%2A>|<xref:System.Windows.Forms.DataGrid.BackColor%2A> 和 <xref:System.Windows.Forms.DataGrid.AlternatingBackColor%2A> 属性确定网格行的颜色，<xref:System.Windows.Forms.DataGrid.BackgroundColor%2A> 属性确定非行区域（只有在网格滚动到底部或网格中只包含少数几行时，才能看到该区域）的颜色。|  
    |<xref:System.Windows.Forms.DataGrid.BorderStyle%2A>|网格的边框样式，<xref:System.Windows.Forms.BorderStyle> 枚举值之一。|  
    |<xref:System.Windows.Forms.DataGrid.CaptionBackColor%2A>|网格正上方网格窗口标题的背景色。|  
    |<xref:System.Windows.Forms.DataGrid.CaptionFont%2A>|网格顶部标题的字体。|  
    |<xref:System.Windows.Forms.DataGrid.CaptionForeColor%2A>|网格的窗口标题的背景色。|  
    |<xref:System.Windows.Forms.Control.Font%2A>|用于显示网格中文本的字体。|  
    |<xref:System.Windows.Forms.DataGrid.ForeColor%2A>|数据网格行中的数据所显示的字体颜色。|  
    |<xref:System.Windows.Forms.DataGrid.GridLineColor%2A>|数据网格的网格线的颜色。|  
    |<xref:System.Windows.Forms.DataGrid.GridLineStyle%2A>|网格单元格分隔线的样式，<xref:System.Windows.Forms.DataGridLineStyle> 枚举值之一。|  
    |<xref:System.Windows.Forms.DataGrid.HeaderBackColor%2A>|行标头和列标头的背景色。|  
    |<xref:System.Windows.Forms.DataGrid.HeaderFont%2A>|用于列标头的字体。|  
    |<xref:System.Windows.Forms.DataGrid.HeaderForeColor%2A>|网格的列标头的前景色，包括列标头文本以及加号 \(\+\) 和减号 \(\-\) 的标志符号（用于在显示多个相关的表时展开和折叠行）。|  
    |<xref:System.Windows.Forms.DataGrid.LinkColor%2A>|数据网格中所有链接的文本颜色，包括指向子表的链接、关系名称，等等。|  
    |<xref:System.Windows.Forms.DataGrid.ParentRowsBackColor%2A>|在子表中，这是父行的背景色。|  
    |<xref:System.Windows.Forms.DataGrid.ParentRowsForeColor%2A>|在子表中，这是父行的前景色。|  
    |<xref:System.Windows.Forms.DataGrid.ParentRowsLabelStyle%2A>|通过 <xref:System.Windows.Forms.DataGridParentRowsLabelStyle> 枚举确定父行中是否显示表名和列名。|  
    |<xref:System.Windows.Forms.DataGrid.PreferredColumnWidth%2A>|网格中列的默认宽度（以像素为单位）。  请在重置 <xref:System.Windows.Forms.DataGrid.DataSource%2A> 和 <xref:System.Windows.Forms.DataGrid.DataMember%2A> 属性（单独进行设置，或者通过 <xref:System.Windows.Forms.DataGrid.SetDataBinding%2A> 方法设置）之前设置此属性，否则此属性将无效。<br /><br /> 该属性不能设置为小于 0 的值。|  
    |<xref:System.Windows.Forms.DataGrid.PreferredRowHeight%2A>|网格中行的行高（以像素为单位）。  请在重置 <xref:System.Windows.Forms.DataGrid.DataSource%2A> 和 <xref:System.Windows.Forms.DataGrid.DataMember%2A> 属性（单独进行设置，或者通过 <xref:System.Windows.Forms.DataGrid.SetDataBinding%2A> 方法设置）之前设置此属性，否则此属性将无效。<br /><br /> 该属性不能设置为小于 0 的值。|  
    |<xref:System.Windows.Forms.DataGrid.RowHeaderWidth%2A>|网格的行标头的宽度。|  
    |<xref:System.Windows.Forms.DataGrid.SelectionBackColor%2A>|在选中行或单元格时，这是背景色。|  
    |<xref:System.Windows.Forms.DataGrid.SelectionForeColor%2A>|在选中行或单元格时，这是前景色。|  
  
    > [!NOTE]
    >  在自定义控件颜色时，颜色选择不当（例如，红色和绿色）有可能导致无法访问控件。  要避免此问题，请使用**“系统颜色”**调色板提供的颜色。  
  
     下面的过程需要一个绑定到数据表的 <xref:System.Windows.Forms.DataGrid> 控件。  有关更多信息，请参见[如何：将 Windows 窗体 DataGrid 控件绑定到数据源](../../../../docs/framework/winforms/controls/how-to-bind-the-windows-forms-datagrid-control-to-a-data-source.md)。  
  
### 在设计时设置数据表的表样式和列样式  
  
1.  选择窗体上的 <xref:System.Windows.Forms.DataGrid> 控件。  
  
2.  在**“属性”**窗口中，选择 <xref:System.Windows.Forms.DataGrid.TableStyles%2A> 属性并单击**“省略号”**\(![VisualStudioEllipsesButton 屏幕快照](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) 按钮。  
  
3.  在**“DataGridTableStyle 集合编辑器”**对话框中，单击**“添加”**向集合中添加一个表样式。  
  
     通过**“DataGridTableStyle 集合编辑器”**，您可以添加或移除表样式，设置显示和布局属性，并可以为表样式设置映射名称。  
  
4.  对于每个表样式，将 <xref:System.Windows.Forms.DataGridTableStyle.MappingName%2A> 属性设置为它的映射名称。  
  
     映射名称用于指定哪个表应该使用哪种表样式。  
  
5.  在**“DataGridTableStyle 集合编辑器”**中，选择 <xref:System.Windows.Forms.DataGridTableStyle.GridColumnStyles%2A> 属性并单击省略号按钮 \(![VisualStudioEllipsesButton 屏幕快照](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\)。  
  
6.  在**“DataGridColumnStyle 集合编辑器”**对话框中，向您创建的表样式添加列样式。  
  
     通过**“DataGridColumnStyle 集合编辑器”**，您可以添加或移除列样式，设置显示和布局属性，并可以为数据列设置映射名称和格式设置字符串。  
  
    > [!NOTE]
    >  有关格式设置字符串的更多信息，请参见[格式化类型](../../../../docs/standard/base-types/formatting-types.md)。  
  
## 请参阅  
 <xref:System.Windows.Forms.GridTableStylesCollection>   
 <xref:System.Windows.Forms.GridColumnStylesCollection>   
 <xref:System.Windows.Forms.DataGrid>   
 [如何：在 Windows 窗体 DataGrid 控件中删除或隐藏列](../../../../docs/framework/winforms/controls/how-to-delete-or-hide-columns-in-the-windows-forms-datagrid-control.md)   
 [DataGrid 控件](../../../../docs/framework/winforms/controls/datagrid-control-windows-forms.md)