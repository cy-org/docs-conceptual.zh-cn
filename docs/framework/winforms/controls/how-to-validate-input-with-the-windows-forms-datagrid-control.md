---
title: "如何：用 Windows 窗体 DataGrid 控件验证输入 | Microsoft Docs"
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
  - "DataGrid 控件 [Windows 窗体], 示例"
  - "DataGrid 控件 [Windows 窗体], 验证输入"
  - "示例 [Windows 窗体], DataGrid 控件"
  - "用户输入, 验证"
  - "验证, 用户输入"
ms.assetid: f1e9c3a0-d0a1-4893-a615-b4b0db046c63
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：用 Windows 窗体 DataGrid 控件验证输入
> [!NOTE]
>  <xref:System.Windows.Forms.DataGridView> 控件取代了 <xref:System.Windows.Forms.DataGrid> 控件并添加了功能；但是，可以选择保留 <xref:System.Windows.Forms.DataGrid> 控件以实现向后兼容并供将来使用。  有关更多信息，请参见 [Windows 窗体 DataGridView 控件和 DataGrid 控件之间的区别](../../../../docs/framework/winforms/controls/differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)。  
  
 Windows 窗体 <xref:System.Windows.Forms.DataGrid> 控件有两种可用的输入验证类型。  如果用户尝试输入一个值，而该值具有单元格不可接受的数据类型（例如，向需要整数的单元格中输入一个字符串），则新的无效值将替换为旧值。  这种输入验证是自动完成的，不能进行自定义。  
  
 另一种输入验证类型可用于拒绝任何不可接受的数据。例如，在必须大于或等于 1 的字段中输入 0 就属于不可接受的数据。此外，不合适的字符串也是不可接受的数据。  这是在数据集中通过编写 <xref:System.Data.DataTable.ColumnChanging> 或 <xref:System.Data.DataTable.RowChanging> 事件的事件处理程序来完成的。  下面的示例使用 <xref:System.Data.DataTable.ColumnChanging> 事件，因为“Product”列不接受不允许的值。  可以使用 <xref:System.Data.DataTable.RowChanging> 事件来检查“End Date”列的值是否晚于同一行中“Start Date”列的值。  
  
### 验证用户输入  
  
1.  编写代码以处理相应表的 <xref:System.Data.DataTable.ColumnChanging> 事件。  当检测到不适当的输入时，调用 <xref:System.Data.DataRow> 对象的 <xref:System.Data.DataRow.SetColumnError%2A> 方法。  
  
    ```vb  
    Private Sub Customers_ColumnChanging(ByVal sender As Object, _  
    ByVal e As System.Data.DataColumnChangeEventArgs)  
       ' Only check for errors in the Product column  
       If (e.Column.ColumnName.Equals("Product")) Then  
          ' Do not allow "Automobile" as a product.  
          If CType(e.ProposedValue, String) = "Automobile" Then  
             Dim badValue As Object = e.ProposedValue  
             e.ProposedValue = "Bad Data"  
             e.Row.RowError = "The Product column contians an error"  
             e.Row.SetColumnError(e.Column, "Product cannot be " & _  
             CType(badValue, String))  
          End If  
       End If  
    End Sub  
  
    ```  
  
    ```csharp  
    //Handle column changing events on the Customers table  
    private void Customers_ColumnChanging(object sender, System.Data.DataColumnChangeEventArgs e) {  
  
       //Only check for errors in the Product column  
       if (e.Column.ColumnName.Equals("Product")) {  
  
          //Do not allow "Automobile" as a product  
          if (e.ProposedValue.Equals("Automobile")) {  
             object badValue = e.ProposedValue;  
             e.ProposedValue = "Bad Data";  
             e.Row.RowError = "The Product column contains an error";  
             e.Row.SetColumnError(e.Column, "Product cannot be " + badValue);  
          }  
       }  
    }  
  
    ```  
  
2.  将事件处理程序连接到事件。  
  
     将下面的代码置于窗体的 <xref:System.Windows.Forms.Form.Load> 事件或其构造函数内。  
  
    ```vb  
    ' Assumes the grid is bound to a dataset called customersDataSet1  
    ' with a table called Customers.  
    ' Put this code in the form's Load event or its constructor.  
    AddHandler customersDataSet1.Tables("Customers").ColumnChanging, AddressOf Customers_ColumnChanging  
  
    ```  
  
    ```csharp  
    // Assumes the grid is bound to a dataset called customersDataSet1  
    // with a table called Customers.  
    // Put this code in the form's Load event or its constructor.  
    customersDataSet1.Tables["Customers"].ColumnChanging += new DataColumnChangeEventHandler(this.Customers_ColumnChanging);  
  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGrid>   
 <xref:System.Data.DataTable.ColumnChanging>   
 <xref:System.Data.DataRow.SetColumnError%2A>   
 [DataGrid 控件](../../../../docs/framework/winforms/controls/datagrid-control-windows-forms.md)