---
title: "如何：在 Windows 窗体 DataGrid 控件中删除或隐藏列 | Microsoft Docs"
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
  - "列 [Windows 窗体], 在数据网格中删除"
  - "列 [Windows 窗体], 隐藏"
  - "数据网格, 删除列"
  - "数据网格, 隐藏列"
  - "DataGrid 控件 [Windows 窗体], 删除列"
  - "DataGrid 控件 [Windows 窗体], 隐藏列"
ms.assetid: bcd0dd96-6687-4c48-b0e1-d5287b93ac91
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：在 Windows 窗体 DataGrid 控件中删除或隐藏列
> [!NOTE]
>  <xref:System.Windows.Forms.DataGridView> 控件取代了 <xref:System.Windows.Forms.DataGrid> 控件并添加了功能；但是，可以选择保留 <xref:System.Windows.Forms.DataGrid> 控件以实现向后兼容并供将来使用。  有关更多信息，请参见 [Windows 窗体 DataGridView 控件和 DataGrid 控件之间的区别](../../../../docs/framework/winforms/controls/differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)。  
  
 使用 <xref:System.Windows.Forms.GridColumnStylesCollection> 和 <xref:System.Windows.Forms.DataGridColumnStyle> 对象（属于 <xref:System.Windows.Forms.DataGridTableStyle> 类的成员）的属性和方法，可以通过编程方式删除或隐藏 Windows 窗体 <xref:System.Windows.Forms.DataGrid> 控件中的列。  
  
 已删除或隐藏的列仍存在于网格绑定到的数据源中，而且仍然可以通过编程方式访问。  只是在数据网格中无法再看到它们。  
  
> [!NOTE]
>  如果您的应用程序不访问某些数据列，而且您不希望在数据网格中显示它们，那么，一开始就不必将它们包括在数据源中。  
  
### 以编程方式从 DataGrid 中删除列  
  
1.  在窗体的声明区域中声明 <xref:System.Windows.Forms.DataGridTableStyle> 类的新实例。  
  
2.  将 <xref:System.Windows.Forms.DataGridTableStyle.MappingName%2A?displayProperty=fullName> 属性设置为希望应用样式的数据源中的表。  下面的示例使用 <xref:System.Windows.Forms.DataGrid.DataMember%2A?displayProperty=fullName> 属性（假设已经设置了它）。  
  
3.  向数据网格的表样式集合中添加新的 <xref:System.Windows.Forms.DataGridTableStyle> 对象。  
  
4.  调用 <xref:System.Windows.Forms.DataGrid> 的 <xref:System.Windows.Forms.DataGridTableStyle.GridColumnStyles%2A> 集合的 <xref:System.Windows.Forms.GridColumnStylesCollection.RemoveAt%2A> 方法，指定要删除列的列索引。  
  
    ```vb  
    ' Declare a new DataGridTableStyle in the  
    ' declarations area of your form.  
    Dim ts As DataGridTableStyle = New DataGridTableStyle()  
  
    Sub DeleteColumn()  
       ' Set the DataGridTableStyle.MappingName property  
       ' to the table in the data source to map to.  
       ts.MappingName = DataGrid1.DataMember  
  
       ' Add it to the datagrid's TableStyles collection  
       DataGrid1.TableStyles.Add(ts)  
  
       ' Delete the first column (index 0)  
       DataGrid1.TableStyles(0).GridColumnStyles.RemoveAt(0)  
    End Sub  
  
    ```  
  
    ```csharp  
    // Declare a new DataGridTableStyle in the  
    // declarations area of your form.  
    DataGridTableStyle ts = new DataGridTableStyle();  
  
    private void deleteColumn()  
    {  
       // Set the DataGridTableStyle.MappingName property  
       // to the table in the data source to map to.  
       ts.MappingName = dataGrid1.DataMember;  
  
       // Add it to the datagrid's TableStyles collection  
       dataGrid1.TableStyles.Add(ts);  
  
       // Delete the first column (index 0)  
       dataGrid1.TableStyles[0].GridColumnStyles.RemoveAt(0);  
    }  
    ```  
  
### 以编程方式隐藏数据网格中的列  
  
1.  在窗体的声明区域中声明 <xref:System.Windows.Forms.DataGridTableStyle> 类的新实例。  
  
2.  将 <xref:System.Windows.Forms.DataGridTableStyle> 的 <xref:System.Windows.Forms.DataGridTableStyle.MappingName%2A> 属性设置为希望应用样式的数据源中的表。  下面的代码示例使用 <xref:System.Windows.Forms.DataGrid.DataMember%2A?displayProperty=fullName> 属性（假设已经设置了它）。  
  
3.  向数据网格的表样式集合中添加新的 <xref:System.Windows.Forms.DataGridTableStyle> 对象。  
  
4.  通过将列的 `Width`  属性设置为 0，并指定要隐藏的列的列索引来隐藏列。  
  
    ```vb  
    ' Declare a new DataGridTableStyle in the  
    ' declarations area of your form.  
    Dim ts As DataGridTableStyle = New DataGridTableStyle()  
  
    Sub HideColumn()  
       ' Set the DataGridTableStyle.MappingName property  
       ' to the table in the data source to map to.  
       ts.MappingName = DataGrid1.DataMember  
  
       ' Add it to the datagrid's TableStyles collection  
       DataGrid1.TableStyles.Add(ts)  
  
       ' Hide the first column (index 0)  
       DataGrid1.TableStyles(0).GridColumnStyles(0).Width = 0  
    End Sub  
  
    ```  
  
    ```csharp  
    // Declare a new DataGridTableStyle in the  
    // declarations area of your form.  
    DataGridTableStyle ts = new DataGridTableStyle();  
  
    private void hideColumn()  
    {  
       // Set the DataGridTableStyle.MappingName property  
       // to the table in the data source to map to.  
       ts.MappingName = dataGrid1.DataMember;  
  
       // Add it to the datagrid's TableStyles collection  
       dataGrid1.TableStyles.Add(ts);  
  
       // Hide the first column (index 0)  
       dataGrid1.TableStyles[0].GridColumnStyles[0].Width = 0;  
    }  
    ```  
  
## 请参阅  
 [如何：在运行时更改 Windows 窗体 DataGrid 控件中显示的数据](../../../../docs/framework/winforms/controls/change-displayed-data-at-run-time-wf-datagrid-control.md)   
 [如何：向 Windows 窗体 DataGrid 控件添加表和列](../../../../docs/framework/winforms/controls/how-to-add-tables-and-columns-to-the-windows-forms-datagrid-control.md)