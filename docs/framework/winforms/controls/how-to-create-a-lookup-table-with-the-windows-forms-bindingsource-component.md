---
title: "如何：使用 Windows 窗体 BindingSource 组件创建查找表 | Microsoft Docs"
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
  - "BindingSource 组件 [Windows 窗体], 创建查找表"
  - "BindingSource 组件 [Windows 窗体], 示例"
  - "查找表"
  - "表 [Windows 窗体], 创建查找表"
ms.assetid: 622fce80-879d-44be-abbf-8350ec22ca2b
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：使用 Windows 窗体 BindingSource 组件创建查找表
查找表是一种数据表，其中有一列显示另一个相关表的记录数据。  在以下过程中，<xref:System.Windows.Forms.ComboBox> 控件可用于显示具有从父表到子表的外键关系的字段。  
  
 为了帮助实现这两个表和这种关系的可视化，下面是一个父表和子表的示例：  
  
 CustomersTable（父表）  
  
|CustomerID|CustomerName|  
|----------------|------------------|  
|712|Paul Koch|  
|713|Tamara Johnston|  
  
 OrdersTable（子表）  
  
|OrderID|OrderDate|CustomerID|  
|-------------|---------------|----------------|  
|903|2004 年 2 月 12 日|712|  
|904|2004 年 2 月 13 日|713|  
  
 在这种情况下，表 CustomersTable 存储了想要显示和保存的实际信息。  但为了节省空间，此表省略了可增加清晰度的数据。  另一张表 OrdersTable 只包含有关哪个客户 ID 号等同于哪个订单日期和订单 ID 的表面相关信息。  并没有提及客户的名称。  
  
 在 [ComboBox 控件](../../../../docs/framework/winforms/controls/combobox-control-windows-forms.md) 控件上设置了 4 种重要属性来创建查找表。  
  
-   <xref:System.Windows.Forms.ComboBox.DataSource%2A> 属性包含查找表的名称。  
  
-   <xref:System.Windows.Forms.ListControl.DisplayMember%2A> 属性包含查找表中要作为控件文本（客户名称）显示的数据列。  
  
-   <xref:System.Windows.Forms.ListControl.ValueMember%2A> 属性包含查找表中具有存储信息（父表中的 ID 号）的数据列。  
  
-   <xref:System.Windows.Forms.ListControl.SelectedValue%2A> 属性根据 <xref:System.Windows.Forms.ListControl.ValueMember%2A> 为子表提供查找值。  
  
 下面的过程显示了如何将窗体布局设置为一个查找表，并将数据绑定到它上面的控件。  为了成功完成这些过程，必须像上面提到的一样有一个带有存在外键关系的父表和子表的数据源。  
  
### 创建用户界面  
  
1.  从**“工具箱”**中，将 <xref:System.Windows.Forms.ComboBox> 控件拖到窗体上。  
  
     此控件将显示父表的列。  
  
2.  拖动其他控件以显示子表的详细信息。  表中数据的格式决定了应当选择哪些控件。  有关详细信息，请参阅[根据功能列出的 Windows 窗体控件](../../../../docs/framework/winforms/controls/windows-forms-controls-by-function.md)。  
  
3.  将一个 <xref:System.Windows.Forms.BindingNavigator> 控件拖到窗体上；这将允许你导航子表中的数据。  
  
### 连接到数据并将其绑定到控件  
  
1.  选择 <xref:System.Windows.Forms.ComboBox> 并单击“智能任务”标志符号，以显示“智能任务”对话框。  
  
2.  选择**“使用数据绑定项”**。  
  
3.  单击**“数据源”**下拉框旁边的箭头。  如果以前已经为项目或窗体配置了数据源，将显示该数据源；否则，完成以下步骤（此示例使用 Northwind 示例数据库中的 Customers 表和 Orders 表，并在括号中引用它们）。  
  
    1.  单击**“添加项目数据源”**以连接到数据并创建一个数据源。  
  
    2.  在**“数据源配置向导”**欢迎页上，单击**“下一步”**。  
  
    3.  在**“选择数据源类型”**页面上选择**“数据库”**。  
  
    4.  从**“选择你的数据连接”**页面上的可用连接列表中选择一个数据连接。  如果所需的数据连接不可用，则选择**“新建连接”**以创建一个新的数据连接。  
  
    5.  单击**“是，保存连接”**以将连接字符串保存到应用程序配置文件中。  
  
    6.  选择要放置到应用程序中的数据库对象。  在这种情况下，选择具有外键关系的一个父表和一个子表（例如 Customers 和 Orders）。  
  
    7.  如果愿意，可以替换默认的数据集名称。  
  
    8.  单击**“完成”**。  
  
4.  在**“显示成员”**下拉框中，选择将在组合框中显示的列名（例如，ContactName）。  
  
5.  在**“值成员”**下拉框中，选择该列（例如，CustomerID）以在子表中执行查找操作。  
  
6.  在**“选定值”**下拉框中，导航到**“项目数据源”**和刚创建的包含父表和子表的数据集。  选择与父表的值成员相同的子表属性（例如，Orders.CustomerID）。  将创建适当的 <xref:System.Windows.Forms.BindingSource>、数据集和表适配器组件，并将其添加到窗体中。  
  
7.  将 <xref:System.Windows.Forms.BindingNavigator> 控件绑定到子表的 <xref:System.Windows.Forms.BindingSource>（例如，`OrdersBindingSource`）。  
  
8.  从想要显示的子表的 <xref:System.Windows.Forms.BindingSource>（例如，`OrdersBindingSource`）中，将除了 <xref:System.Windows.Forms.ComboBox> 和 <xref:System.Windows.Forms.BindingNavigator> 外的控件绑定到详细信息字段上。  
  
## 请参阅  
 <xref:System.Windows.Forms.BindingSource>   
 [BindingSource 组件](../../../../docs/framework/winforms/controls/bindingsource-component.md)   
 [ComboBox 控件](../../../../docs/framework/winforms/controls/combobox-control-windows-forms.md)   
 [在 Visual Studio 中将控件绑定到数据](../Topic/Bind%20controls%20to%20data%20in%20Visual%20Studio.md)