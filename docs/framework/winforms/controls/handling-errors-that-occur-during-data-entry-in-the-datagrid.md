---
title: "演练：处理在 Windows 窗体 DataGridView 控件中输入数据时发生的错误 | Microsoft Docs"
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
  - "数据输入, 错误处理"
  - "数据网格, 错误处理"
  - "DataGridView 控件 [Windows 窗体], 错误处理"
  - "错误处理, 数据输入"
  - "错误处理, DataGridView 控件"
  - "演练 [Windows 窗体], DataGridView 控件"
ms.assetid: 30a68b85-d3af-4946-83c1-1e2d010d0511
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# 演练：处理在 Windows 窗体 DataGridView 控件中输入数据时发生的错误
处理基础数据存储区中的错误是数据输入应用程序所必备的功能。  Windows 窗体 <xref:System.Windows.Forms.DataGridView> 控件通过公开 <xref:System.Windows.Forms.DataGridView.DataError> 事件来轻松实现此类错误的处理；当数据存储区检测到约束冲突或违反业务规则时将引发该事件。  
  
 在本演练中，将从 Northwind 示例数据库的 `Customers` 表中检索行，并将检索到的行显示在 <xref:System.Windows.Forms.DataGridView> 控件中。  当在新行或编辑的现有行中检测到重复的 `CustomerID` 值时，将发生 <xref:System.Windows.Forms.DataGridView.DataError> 事件，并通过显示一个描述该异常的 <xref:System.Windows.Forms.MessageBox> 对此事件进行处理。  
  
 若要以单个列表的形式复制本主题中的代码，请参见 [如何：处理在 Windows 窗体 DataGridView 控件中输入数据时发生的错误](../../../../docs/framework/winforms/controls/handle-errors-that-occur-during-data-entry-in-the-datagrid.md)。  
  
## 系统必备  
 若要完成本演练，您需要：  
  
-   对 Northwind SQL Server 示例数据库所在的服务器的访问权限。  
  
## 创建窗体  
  
#### 在 DataGridView 控件中处理数据输入错误  
  
1.  创建一个从 <xref:System.Windows.Forms.Form> 派生的类，该类包含一个 <xref:System.Windows.Forms.DataGridView> 控件和一个 <xref:System.Windows.Forms.BindingSource> 组件。  
  
     下面的代码示例提供了基本的初始化功能，并包含一个 `Main` 方法。  
  
     [!code-csharp[System.Windows.Forms.DataGridView.DataError#01](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/CS/errorhandling.cs#01)]
     [!code-vb[System.Windows.Forms.DataGridView.DataError#01](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/VB/errorhandling.vb#01)]  
    [!code-csharp[System.Windows.Forms.DataGridView.DataError#02](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/CS/errorhandling.cs#02)]
    [!code-vb[System.Windows.Forms.DataGridView.DataError#02](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/VB/errorhandling.vb#02)]  
  
2.  在窗体的类定义中实现一个方法，用于处理有关与数据库的连接的详细信息。  
  
     此代码示例使用 `GetData` 方法，该方法返回填充的 <xref:System.Data.DataTable> 对象。  请确保将 `connectionString` 变量设置为适用于您的数据库的值。  
  
    > [!IMPORTANT]
    >  将敏感信息（如密码）存储在连接字符串中可能会影响您的应用程序的安全性。  若要控制对数据库的访问，一种较为安全的方法是使用 Windows 身份验证（也称为集成安全性）。  有关更多信息，请参见[保护连接信息](../../../../docs/framework/data/adonet/protecting-connection-information.md)。  
  
     [!code-csharp[System.Windows.Forms.DataGridView.DataError#30](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/CS/errorhandling.cs#30)]
     [!code-vb[System.Windows.Forms.DataGridView.DataError#30](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/VB/errorhandling.vb#30)]  
  
3.  为窗体的 <xref:System.Windows.Forms.Form.Load> 事件实现一个处理程序，该事件初始化 <xref:System.Windows.Forms.DataGridView> 和 <xref:System.Windows.Forms.BindingSource> 并设置数据绑定。  
  
     [!code-csharp[System.Windows.Forms.DataGridView.DataError#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/CS/errorhandling.cs#10)]
     [!code-vb[System.Windows.Forms.DataGridView.DataError#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/VB/errorhandling.vb#10)]  
  
4.  在 <xref:System.Windows.Forms.DataGridView> 中处理 <xref:System.Windows.Forms.DataGridView.DataError> 事件。  
  
     如果错误发生在提交操作过程中，则在 <xref:System.Windows.Forms.MessageBox> 中显示该错误。  
  
     [!code-csharp[System.Windows.Forms.DataGridView.DataError#20](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/CS/errorhandling.cs#20)]
     [!code-vb[System.Windows.Forms.DataGridView.DataError#20](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridView.DataError/VB/errorhandling.vb#20)]  
  
## 测试应用程序  
 现在可以测试窗体，以确保其行为与预期相同。  
  
#### 测试窗体  
  
-   按 F5 运行该应用程序。  
  
     您将看到一个用 Customers 表中的数据填充的 <xref:System.Windows.Forms.DataGridView> 控件。  如果为 `CustomerID` 输入重复的值并提交编辑结果，则该单元格的值将自动恢复为原来的值，您将看到一个显示数据输入错误的 <xref:System.Windows.Forms.MessageBox>。  
  
## 后续步骤  
 此应用程序使您对 <xref:System.Windows.Forms.DataGridView> 控件的功能有一个基本了解。  您可以通过以下几种方法来自定义 <xref:System.Windows.Forms.DataGridView> 控件的外观和行为：  
  
-   更改边框和标题样式。  有关更多信息，请参见 [如何：更改 Windows 窗体 DataGridView 控件中的边框和网格线的样式](../../../../docs/framework/winforms/controls/change-the-border-and-gridline-styles-in-the-datagrid.md)。  
  
-   允许或限制用户向 <xref:System.Windows.Forms.DataGridView> 控件中输入数据。  有关更多信息，请参见[如何：防止在 Windows 窗体 DataGridView 控件中添加和删除行](../../../../docs/framework/winforms/controls/prevent-row-addition-and-deletion-datagridview.md)和[如何：使 Windows 窗体 DataGridView 控件中的列只读](../../../../docs/framework/winforms/controls/how-to-make-columns-read-only-in-the-windows-forms-datagridview-control.md)。  
  
-   对用户在 <xref:System.Windows.Forms.DataGridView> 控件中输入的数据进行验证。  有关更多信息，请参见 [演练：验证 Windows 窗体 DataGridView 控件中的数据](../../../../docs/framework/winforms/controls/walkthrough-validating-data-in-the-windows-forms-datagridview-control.md)。  
  
-   使用虚拟模式处理特大数据集。  有关更多信息，请参见 [演练：在 Windows 窗体 DataGridView 控件中实现虚拟模式](../../../../docs/framework/winforms/controls/implementing-virtual-mode-wf-datagridview-control.md)。  
  
-   自定义单元格的外观。  有关更多信息，请参见 [如何：自定义 Windows 窗体 DataGridView 控件中单元格的外观](../../../../docs/framework/winforms/controls/customize-the-appearance-of-cells-in-the-datagrid.md) 和 [如何：设置 Windows 窗体 DataGridView 控件的默认单元格样式](../../../../docs/framework/winforms/controls/how-to-set-default-cell-styles-for-the-windows-forms-datagridview-control.md)。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.BindingSource>   
 [Windows 窗体 DataGridView 控件中的数据输入](../../../../docs/framework/winforms/controls/data-entry-in-the-windows-forms-datagridview-control.md)   
 [如何：处理在 Windows 窗体 DataGridView 控件中输入数据时发生的错误](../../../../docs/framework/winforms/controls/handle-errors-that-occur-during-data-entry-in-the-datagrid.md)   
 [演练：验证 Windows 窗体 DataGridView 控件中的数据](../../../../docs/framework/winforms/controls/walkthrough-validating-data-in-the-windows-forms-datagridview-control.md)   
 [保护连接信息](../../../../docs/framework/data/adonet/protecting-connection-information.md)