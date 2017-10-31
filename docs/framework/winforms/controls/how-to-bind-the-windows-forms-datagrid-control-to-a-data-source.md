---
title: "如何：将 Windows 窗体 DataGrid 控件绑定到数据源 | Microsoft Docs"
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
ms.assetid: 128cdb07-dfd3-4d60-9d6a-902847667c36
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# 如何：将 Windows 窗体 DataGrid 控件绑定到数据源
> [!NOTE]
>  <xref:System.Windows.Forms.DataGridView> 控件取代了 <xref:System.Windows.Forms.DataGrid> 控件并添加了功能；但是，可以选择保留 <xref:System.Windows.Forms.DataGrid> 控件以实现向后兼容并供将来使用。  有关更多信息，请参见 [Windows 窗体 DataGridView 控件和 DataGrid 控件之间的区别](../../../../docs/framework/winforms/controls/differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)。  
  
 Windows 窗体 <xref:System.Windows.Forms.DataGrid> 控件是专为显示来自数据源的信息而设计的。  通过调用 <xref:System.Windows.Forms.DataGrid.SetDataBinding%2A> 方法可以在运行时绑定控件。  虽然可以显示来自各种数据源的数据，但最常见的数据源是数据集和数据视图。  
  
### 以编程方式数据绑定 DataGrid 控件  
  
1.  编写代码来填充数据集。  
  
     如果数据源是数据集或基于数据集表的数据视图，请向窗体添加代码来填充数据集。  
  
     所使用的确切代码取决于数据集从何处获取数据。  如果要从数据库中直接填充数据集，通常可以调用数据适配器的 `Fill`  方法，如下面的示例所示（它填充名为 `DsCategories1` 的数据集）：  
  
    ```vb  
    sqlDataAdapter1.Fill(DsCategories1)  
  
    ```  
  
    ```csharp  
    sqlDataAdapter1.Fill(DsCategories1);  
  
    ```  
  
    ```cpp  
    sqlDataAdapter1->Fill(dsCategories1);  
    ```  
  
     如果要从 XML Web services 填充数据集，通常可以在代码中创建该服务的实例，然后调用其方法之一来返回数据集。  然后将 XML Web services 中的数据集并入本地的数据集。  下面的示例演示如何创建名为 `CategoriesService` 的 XML Web services 的实例，如何调用它的 `GetCategories` 方法，以及如何将生成的结果数据集合并到名为 `DsCategories1` 的本地数据集：  
  
    ```vb  
    Dim ws As New MyProject.localhost.CategoriesService()  
    ws.Credentials = System.Net.CredentialCache.DefaultCredentials  
    DsCategories1.Merge(ws.GetCategories())  
  
    ```  
  
    ```csharp  
    MyProject.localhost.CategoriesService ws = new MyProject.localhost.CategoriesService();  
    ws.Credentials = System.Net.CredentialCache.DefaultCredentials;  
    DsCategories1.Merge(ws.GetCategories());  
  
    ```  
  
    ```cpp  
    MyProject::localhost::CategoriesService^ ws =   
       new MyProject::localhost::CategoriesService();  
    ws->Credentials = System::Net::CredentialCache::DefaultCredentials;  
    dsCategories1->Merge(ws->GetCategories());  
    ```  
  
2.  调用 <xref:System.Windows.Forms.DataGrid> 控件的 <xref:System.Windows.Forms.DataGrid.SetDataBinding%2A> 方法，向其传递数据源和一个数据成员。  如果不需要显式传递一个数据成员，请传递一个空字符串。  
  
    > [!NOTE]
    >  如果是第一次绑定网格，可以设置控件的 <xref:System.Windows.Forms.DataGrid.DataSource%2A> 和 <xref:System.Windows.Forms.DataGrid.DataMember%2A> 属性。  但是，这些属性一经设置，便无法进行重置。  因此，建议您始终使用 <xref:System.Windows.Forms.DataGrid.SetDataBinding%2A> 方法。  
  
     下面的示例演示如何以编程方式绑定到 `DsCustomers1` 数据集中的 Customers 表：  
  
    ```vb  
    DataGrid1.SetDataBinding(DsCustomers1, "Customers")  
  
    ```  
  
    ```csharp  
    DataGrid1.SetDataBinding(DsCustomers1, "Customers");  
  
    ```  
  
    ```cpp  
    dataGrid1->SetDataBinding(dsCustomers1, "Customers");  
    ```  
  
     如果 Customers 表是数据集中唯一的表，也可以用下面的方法绑定网格：  
  
    ```vb  
    DataGrid1.SetDataBinding(DsCustomers1, "")  
  
    ```  
  
    ```csharp  
    DataGrid1.SetDataBinding(DsCustomers1, "");  
  
    ```  
  
    ```cpp  
    dataGrid1->SetDataBinding(dsCustomers1, "");  
    ```  
  
3.  （可选）将适当的表样式和列样式添加到网格中。  如果没有表样式，您将看见该表，但其格式设置很少，且所有列均可见。  
  
## 请参阅  
 [DataGrid 控件概述](../../../../docs/framework/winforms/controls/datagrid-control-overview-windows-forms.md)   
 [如何：向 Windows 窗体 DataGrid 控件添加表和列](../../../../docs/framework/winforms/controls/how-to-add-tables-and-columns-to-the-windows-forms-datagrid-control.md)   
 [DataGrid 控件](../../../../docs/framework/winforms/controls/datagrid-control-windows-forms.md)   
 [Windows 窗体数据绑定](../../../../docs/framework/winforms/windows-forms-data-binding.md)