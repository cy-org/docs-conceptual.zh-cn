---
title: "如何：使用 Windows 窗体 DataGrid 控件创建主/从列表 | Microsoft Docs"
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
ms.assetid: 20388c6a-94f9-4d96-be18-8c200491247f
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：使用 Windows 窗体 DataGrid 控件创建主/从列表
> [!NOTE]
>  <xref:System.Windows.Forms.DataGridView> 控件取代了 <xref:System.Windows.Forms.DataGrid> 控件并添加了功能；但是，可以选择保留 <xref:System.Windows.Forms.DataGrid> 控件以实现向后兼容并供将来使用。  有关更多信息，请参见 [Windows 窗体 DataGridView 控件和 DataGrid 控件之间的区别](../../../../docs/framework/winforms/controls/differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)。  
  
 如果 <xref:System.Data.DataSet> 包含一系列相关表，则可以使用两个 <xref:System.Windows.Forms.DataGrid> 控件以主\/从格式显示数据。  一个 <xref:System.Windows.Forms.DataGrid> 被指定为主网格，另一个被指定为详细信息网格。  当在主列表中选择某项时，所有相关的子项都显示在详细信息列表中。  例如，如果 <xref:System.Data.DataSet> 包含 Customers 表和相关的 Orders 表，则您可将 Customers 表指定为主网格，而将 Orders 表指定为详细信息网格。  当从主网格中选择某个客户时，Orders 表中与该客户关联的所有订单都将显示在详细信息网格中。  
  
### 以编程方式设置主\/从关系  
  
1.  新建两个 <xref:System.Windows.Forms.DataGrid> 控件并设置它们的属性。  
  
2.  向数据集添加表。  
  
3.  声明一个类型为 <xref:System.Data.DataRelation> 的变量来表示您要创建的关系。  
  
4.  通过指定关系的名称和指定表、列以及将关联这两个表的项来实例化关系。  
  
5.  将此关系添加到 <xref:System.Data.DataSet> 对象的 <xref:System.Data.DataSet.Relations%2A> 集合中。  
  
6.  使用 <xref:System.Windows.Forms.DataGrid> 的 <xref:System.Windows.Forms.DataGrid.SetDataBinding%2A> 方法将每个网格绑定到 <xref:System.Data.DataSet>。  
  
     下面的示例演示如何在以前生成的 <xref:System.Data.DataSet> \(`ds`\) 中设置 Customers 表与 Orders 表之间的主\/从关系。  
  
    ```vb  
    Dim myDataRelation As DataRelation  
    myDataRelation = New DataRelation _  
       ("CustOrd", ds.Tables("Customers").Columns("CustomerID"), _  
       ds.Tables("Orders").Columns("CustomerID"))  
    ' Add the relation to the DataSet.  
    ds.Relations.Add(myDataRelation)  
    GridOrders.SetDataBinding(ds, "Customers")  
    GridDetails.SetDataBinding(ds, "Customers.CustOrd")  
  
    ```  
  
    ```csharp  
    DataRelation myDataRelation;  
    myDataRelation = new DataRelation("CustOrd", ds.Tables["Customers"].Columns["CustomerID"], ds.Tables["Orders"].Columns["CustomerID"]);  
    // Add the relation to the DataSet.  
    ds.Relations.Add(myDataRelation);  
    GridOrders.SetDataBinding(ds,"Customers");  
    GridDetails.SetDataBinding(ds,"Customers.CustOrd");  
  
    ```  
  
    ```cpp  
    DataRelation^ myDataRelation;  
    myDataRelation = gcnew DataRelation("CustOrd",  
       ds->Tables["Customers"]->Columns["CustomerID"],  
       ds->Tables["Orders"]->Columns["CustomerID"]);  
    // Add the relation to the DataSet.  
    ds->Relations->Add(myDataRelation);  
    GridOrders->SetDataBinding(ds, "Customers");  
    GridDetails->SetDataBinding(ds, "Customers.CustOrd");  
    ```  
  
## 请参阅  
 [DataGrid 控件](../../../../docs/framework/winforms/controls/datagrid-control-windows-forms.md)   
 [DataGrid 控件概述](../../../../docs/framework/winforms/controls/datagrid-control-overview-windows-forms.md)   
 [如何：将 Windows 窗体 DataGrid 控件绑定到数据源](../../../../docs/framework/winforms/controls/how-to-bind-the-windows-forms-datagrid-control-to-a-data-source.md)