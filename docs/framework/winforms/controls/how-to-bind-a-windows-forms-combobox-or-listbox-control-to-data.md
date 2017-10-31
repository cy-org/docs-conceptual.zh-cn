---
title: "如何：将 Windows 窗体 ComboBox 控件或 ListBox 控件绑定到数据 | Microsoft Docs"
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
  - "绑定控件, 组合框"
  - "组合框, 数据绑定"
  - "ComboBox 控件 [Windows 窗体], 数据绑定"
  - "数据 [Windows 窗体], 绑定到控件"
  - "数据绑定, 组合框"
  - "数据绑定控件, Windows 窗体"
  - "列表框, 数据绑定"
  - "ListBox 控件 [Windows 窗体], 数据绑定"
  - "Windows 窗体控件, 数据绑定"
ms.assetid: dfd7f081-8bea-4a41-86a3-86a1934828ef
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：将 Windows 窗体 ComboBox 控件或 ListBox 控件绑定到数据
可以将 <xref:System.Windows.Forms.ComboBox> 和 <xref:System.Windows.Forms.ListBox> 绑定到数据，以便执行诸如浏览数据库中的数据、输入新数据或编辑现有数据等任务。  
  
### 绑定 ComboBox 控件或 ListBox 控件  
  
1.  将 `DataSource`  属性设置为数据源对象。  可能的数据源包括被绑定到数据、数据表、数据视图、数据集、数据视图管理器、数组或实现了 <xref:System.Collections.IList> 接口的任何类的 <xref:System.Windows.Forms.BindingSource>。  有关更多信息，请参见 [Windows 窗体支持的数据源](../../../../docs/framework/winforms/data-sources-supported-by-windows-forms.md)。  
  
2.  如果绑定到表，请将`DisplayMember` 属性设置为数据源中的列的名称。  
  
     \- 或 \-  
  
     如果绑定到 <xref:System.Collections.IList>，请将显示成员设置为列表中的类型的公用属性。  
  
    ```vb  
    Private Sub BindComboBox()  
      ComboBox1.DataSource = DataSet1.Tables("Suppliers")  
      ComboBox1.DisplayMember = "ProductName"  
    End Sub  
  
    ```  
  
    ```csharp  
    private void BindComboBox()  
    {  
      comboBox1.DataSource = dataSet1.Tables["Suppliers"];  
      comboBox1.DisplayMember = "ProductName";  
    }  
  
    ```  
  
    > [!NOTE]
    >  如果绑定到未实现 <xref:System.ComponentModel.IBindingList> 接口的数据源（例如，<xref:System.Collections.ArrayList>），则在数据源更新时，将不会更新绑定控件的数据。  例如，如果将组合框绑定到 <xref:System.Collections.ArrayList>，并将数据添加到 <xref:System.Collections.ArrayList> 中，则这些新项将不会出现在组合框中。  但是，您可以通过调用控件绑定到的 <xref:System.Windows.Forms.BindingContext> 类的实例上的 <xref:System.Windows.Forms.BindingManagerBase.SuspendBinding%2A> 和 <xref:System.Windows.Forms.BindingManagerBase.ResumeBinding%2A> 方法来强制更新组合框。  
  
## 请参阅  
 <xref:System.Windows.Forms.ComboBox>   
 <xref:System.Windows.Forms.ListBox>   
 [Windows 窗体数据绑定](../../../../docs/framework/winforms/windows-forms-data-binding.md)   
 [数据绑定和 Windows 窗体](../../../../docs/framework/winforms/data-binding-and-windows-forms.md)   
 [用于列出选项的 Windows 窗体控件](../../../../docs/framework/winforms/controls/windows-forms-controls-used-to-list-options.md)