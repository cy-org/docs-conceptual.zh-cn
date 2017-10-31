---
title: "如何：向 Windows 窗体 DataGrid 控件添加表和列 | Microsoft Docs"
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
  - "列 [Windows 窗体], 添加到 DataGrid 控件"
  - "DataGrid 控件 [Windows 窗体], 添加表和列"
  - "表 [Windows 窗体], 添加到 DataGrid 控件"
ms.assetid: 2fe661b9-aa06-49b9-a314-a0d3cbfdcb4d
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：向 Windows 窗体 DataGrid 控件添加表和列
> [!NOTE]
>  <xref:System.Windows.Forms.DataGridView> 控件取代了 <xref:System.Windows.Forms.DataGrid> 控件并添加了功能；但是，可以选择保留 <xref:System.Windows.Forms.DataGrid> 控件以实现向后兼容并供将来使用。  有关更多信息，请参见 [Windows 窗体 DataGridView 控件和 DataGrid 控件之间的区别](../../../../docs/framework/winforms/controls/differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)。  
  
 通过创建 **DataGridTableStyle** 对象，并将其添加到 **GridTableStylesCollection** 对象（通过 <xref:System.Windows.Forms.DataGrid> 控件的 **TableStyles** 属性访问），可以用表和列的形式在 Windows 窗体 <xref:System.Windows.Forms.DataGrid> 控件中显示数据。  每个表样式显示在 **DataGridTableStyle** 对象的 **MappingName** 属性中指定的任意数据表的内容。  默认情况下，未指定列样式的表样式将显示该数据表中的所有列。  通过将 **DataGridColumnStyle** 对象添加到 **GridColumnStylesCollection** 对象（通过各 **DataGridTableStyle** 对象的 **GridColumnStyles** 属性访问），可以限制所显示的表中的列。  
  
### 以编程方式向 DataGrid 添加表和列  
  
1.  为在表中显示数据，必须首先将 <xref:System.Windows.Forms.DataGrid> 控件绑定到数据集。  有关更多信息，请参见[如何：将 Windows 窗体 DataGrid 控件绑定到数据源](../../../../docs/framework/winforms/controls/how-to-bind-the-windows-forms-datagrid-control-to-a-data-source.md)。  
  
    > [!CAUTION]
    >  当以编程方式指定列样式时，在向 **GridTableStylesCollection** 对象添加 **DataGridTableStyle** 对象之前，请始终先创建 **DataGridColumnStyle** 对象并将其添加到 **GridColumnStylesCollection** 对象中。  当将空的 **DataGridTableStyle** 对象添加到集合时，会自动生成 **DataGridColumnStyle** 对象。  因此，如果尝试向 **GridColumnStylesCollection** 对象添加具有重复的 **MappingName** 值的新 **DataGridColumnStyle** 对象，则会引发异常。  
  
2.  声明新的表样式并设置其映射名称。  
  
    ```vb  
    Dim ts1 As New DataGridTableStyle()  
    ts1.MappingName = "Customers"  
  
    ```  
  
    ```csharp  
    DataGridTableStyle ts1 = new DataGridTableStyle();  
    ts1.MappingName = "Customers";  
  
    ```  
  
    ```cpp  
    DataGridTableStyle* ts1 = new DataGridTableStyle();  
    ts1->MappingName = S"Customers";  
    ```  
  
3.  声明新的列样式并设置其映射名称及其他属性。  
  
    ```vb  
    Dim myDataCol As New DataGridBoolColumn()  
    myDataCol.HeaderText = "My New Column"  
    myDataCol.MappingName = "Current"  
  
    ```  
  
    ```csharp  
    DataGridBoolColumn myDataCol = new DataGridBoolColumn();  
    myDataCol.HeaderText = "My New Column";  
    myDataCol.MappingName = "Current";  
  
    ```  
  
    ```cpp  
    DataGridBoolColumn^ myDataCol = gcnew DataGridBoolColumn();  
    myDataCol->HeaderText = "My New Column";  
    myDataCol->MappingName = "Current";  
    ```  
  
4.  调用 **GridColumnStylesCollection** 对象的 **Add** 方法以将该列添加到表样式中  
  
    ```vb  
    ts1.GridColumnStyles.Add(myDataCol)  
  
    ```  
  
    ```csharp  
    ts1.GridColumnStyles.Add(myDataCol);  
  
    ```  
  
    ```cpp  
    ts1->GridColumnStyles->Add(myDataCol);  
    ```  
  
5.  调用 **GridTableStylesCollection** 对象的 **Add** 方法以将表样式添加到数据网格中。  
  
    ```vb  
    DataGrid1.TableStyles.Add(ts1)  
  
    ```  
  
    ```csharp  
    dataGrid1.TableStyles.Add(ts1);  
  
    ```  
  
    ```cpp  
    dataGrid1->TableStyles->Add(ts1);  
    ```  
  
## 请参阅  
 [DataGrid 控件](../../../../docs/framework/winforms/controls/datagrid-control-windows-forms.md)   
 [如何：在 Windows 窗体 DataGrid 控件中删除或隐藏列](../../../../docs/framework/winforms/controls/how-to-delete-or-hide-columns-in-the-windows-forms-datagrid-control.md)