---
title: "如何：在运行时更改 Windows 窗体 DataGrid 控件中显示的数据 | Microsoft Docs"
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
  - "单元格, 更改 DataGrid 单元格值"
  - "DataGrid 控件 [Windows 窗体], 数据绑定"
  - "DataGrid 控件 [Windows 窗体], 在运行时动态地更改"
ms.assetid: 0c7a6d00-30de-416e-8223-0a81ddb4c1f8
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 如何：在运行时更改 Windows 窗体 DataGrid 控件中显示的数据
> [!NOTE]
>  <xref:System.Windows.Forms.DataGridView> 控件取代了 <xref:System.Windows.Forms.DataGrid> 控件并添加了功能；但是，可以选择保留 <xref:System.Windows.Forms.DataGrid> 控件以实现向后兼容并供将来使用。  有关更多信息，请参见 [Windows 窗体 DataGridView 控件和 DataGrid 控件之间的区别](../../../../docs/framework/winforms/controls/differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)。  
  
 使用设计时功能创建了 Windows 窗体 <xref:System.Windows.Forms.DataGrid> 后，可能还需要在运行时动态更改网格的 <xref:System.Data.DataSet> 对象的元素。  这可以包括对表的各个值的更改，也可以包括对绑定到 <xref:System.Windows.Forms.DataGrid> 控件的数据源的更改。  对各个值的更改是通过 <xref:System.Data.DataSet> 对象而不是 <xref:System.Windows.Forms.DataGrid> 控件来完成的。  
  
### 以编程方式更改数据  
  
1.  从 <xref:System.Data.DataSet> 对象中指定所需的表，然后从该表中指定所需的行和字段，并将单元格设置为等于新值。  
  
    > [!NOTE]
    >  若要指定 <xref:System.Data.DataSet> 的第一个表或表的第一行，请使用 0。  
  
     下面的示例演示了如何通过单击 `Button1` 更改数据集中第一个表的第一行中的第二项。  <xref:System.Data.DataSet> \(`ds`\) 和表（`0`  和 `1`）已预先创建好。  
  
    ```vb  
    Protected Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click  
       ds.tables(0).rows(0)(1) = "NewEntry"  
    End Sub  
  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)  
    {  
       ds.Tables[0].Rows[0][1]="NewEntry";  
    }  
  
    ```  
  
    ```cpp  
    private:   
       void button1_Click(System::Object^ sender, System::EventArgs^ e)  
       {  
          dataSet1->Tables[0]->Rows[0][1] = "NewEntry";  
       }  
    ```  
  
     （[!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 和 [!INCLUDE[vcprvc](../../../../includes/vcprvc-md.md)]）在窗体的构造函数中放置以下代码以注册事件处理程序。  
  
    ```csharp  
    this.button1.Click += new System.EventHandler(this.button1_Click);  
  
    ```  
  
    ```cpp  
    this->button1->Click +=  
       gcnew System::EventHandler(this, &Form1::button1_Click);  
    ```  
  
     在运行时可以使用 <xref:System.Windows.Forms.DataGrid.SetDataBinding%2A> 方法将 <xref:System.Windows.Forms.DataGrid> 控件绑定到另一个数据源上。  例如，可以有几个 [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] 数据控件，每个控件都连接到不同的数据库。  
  
### 以编程方式更改数据源  
  
1.  将 <xref:System.Windows.Forms.DataGrid.SetDataBinding%2A> 方法设置为要绑定的数据源和表的名称。  
  
     下面的示例演示如何使用 <xref:System.Windows.Forms.DataGrid.SetDataBinding%2A> 方法将数据源更改为一个 [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] 数据控件 \(adoPubsAuthors\)，此数据控件连接到 Pubs 数据库中的 Authors 表。  
  
    ```vb  
    Private Sub ResetSource()  
       DataGrid1.SetDataBinding(adoPubsAuthors, "Authors")  
    End Sub  
  
    ```  
  
    ```csharp  
    private void ResetSource()  
    {  
       DataGrid1.SetDataBinding(adoPubsAuthors, "Authors");  
    }  
  
    ```  
  
    ```cpp  
    private:  
       void ResetSource()  
       {  
          dataGrid1->SetDataBinding(adoPubsAuthors, "Authors");  
       }  
    ```  
  
## 请参阅  
 [ADO.NET DataSet](../../../../docs/framework/data/adonet/ado-net-datasets.md)   
 [如何：在 Windows 窗体 DataGrid 控件中删除或隐藏列](../../../../docs/framework/winforms/controls/how-to-delete-or-hide-columns-in-the-windows-forms-datagrid-control.md)   
 [如何：向 Windows 窗体 DataGrid 控件添加表和列](../../../../docs/framework/winforms/controls/how-to-add-tables-and-columns-to-the-windows-forms-datagrid-control.md)   
 [如何：将 Windows 窗体 DataGrid 控件绑定到数据源](../../../../docs/framework/winforms/controls/how-to-bind-the-windows-forms-datagrid-control-to-a-data-source.md)