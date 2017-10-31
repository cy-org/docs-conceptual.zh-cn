---
title: "如何：使用 Windows 窗体 ErrorProvider 组件查看数据集中的错误 | Microsoft Docs"
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
  - "错误信息, 在数据集中查看"
  - "ErrorProvider 组件 [Windows 窗体], 数据集错误"
  - "错误 [Windows 窗体], 数据集错误"
ms.assetid: cbae023f-d651-4210-bdea-bcc5f037e321
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：使用 Windows 窗体 ErrorProvider 组件查看数据集中的错误
可以使用 Windows 窗体 <xref:System.Windows.Forms.ErrorProvider> 组件查看数据集或其他数据源中的列错误。  <xref:System.Windows.Forms.ErrorProvider> 组件可以在窗体上显示数据错误，因此，该组件不必与控件直接关联。  绑定到数据源后，该控件就可以在绑定到同一数据源的任何控件旁显示错误图标。  
  
> [!NOTE]
>  如果在运行时更改错误提供程序的 <xref:System.Windows.Forms.ErrorProvider.DataSource%2A> 和 <xref:System.Windows.Forms.ErrorProvider.DataMember%2A> 属性，应该使用 <xref:System.Windows.Forms.ErrorProvider.BindToDataAndErrors%2A> 方法避免冲突。  
  
### 显示数据错误  
  
1.  将该组件绑定到数据表内的特定列。  
  
    ```vb  
    ' Assumes existence of DataSet1, DataTable1  
    TextBox1.DataBindings.Add("Text", DataSet1, "Customers.Name")  
    ErrorProvider1.DataSource = DataSet1  
    ErrorProvider1.DataMember = "Customers"  
  
    ```  
  
    ```csharp  
    // Assumes existence of DataSet1, DataTable1  
    textBox1.DataBindings.Add("Text", DataSet1, "Customers.Name");  
    errorProvider1.DataSource = DataSet1;  
    errorProvider1.DataMember = "Customers";  
  
    ```  
  
2.  将 <xref:System.Windows.Forms.ErrorProvider.ContainerControl%2A> 属性设置为窗体。  
  
    ```vb  
    ErrorProvider1.ContainerControl = Me  
  
    ```  
  
    ```csharp  
    errorProvider1.ContainerControl = this;  
  
    ```  
  
3.  将当前记录的位置设置为包含列错误的行。  
  
    ```vb  
    DataTable1.Rows(5).SetColumnError("Name", "Bad data in this row.")  
    Me.BindingContext(DataTable1).Position = 5  
  
    ```  
  
    ```csharp  
    DataTable1.Rows[5].SetColumnError("Name", "Bad data in this row.");  
    this.BindingContext [DataTable1].Position = 5;  
  
    ```  
  
## 请参阅  
 [ErrorProvider 组件概述](../../../../docs/framework/winforms/controls/errorprovider-component-overview-windows-forms.md)   
 [如何：使用 Windows 窗体 ErrorProvider 组件显示窗体验证的错误图标](../../../../docs/framework/winforms/controls/display-error-icons-for-form-validation-with-wf-errorprovider.md)