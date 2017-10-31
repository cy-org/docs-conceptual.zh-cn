---
title: "演练：验证 Windows 窗体 DataGridView 控件中的数据 | Microsoft Docs"
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
  - "数据 [Windows 窗体], 验证"
  - "数据网格, 验证数据"
  - "数据验证, Windows 窗体"
  - "DataGridView 控件 [Windows 窗体], 数据验证"
  - "验证数据, Windows 窗体"
  - "演练 [Windows 窗体], DataGridView 控件"
ms.assetid: a4f1d015-2969-430c-8ea2-b612d179c290
caps.latest.revision: 22
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 22
---
# 演练：验证 Windows 窗体 DataGridView 控件中的数据
向用户显示数据输入功能时，必须频繁验证输入窗体中的数据。  <xref:System.Windows.Forms.DataGridView> 类提供了在将数据提交到数据存储区之前执行验证的便利方式。  可以通过处理 <xref:System.Windows.Forms.DataGridView.CellValidating> 事件来验证数据，该事件是在当前单元格发生更改时由 <xref:System.Windows.Forms.DataGridView> 引发的。  
  
 在本演练中，将从 Northwind 示例数据库的 `Customers` 表中检索行，并将检索到的行显示在 <xref:System.Windows.Forms.DataGridView> 控件中。  当用户编辑 `CompanyName` 列中的单元格后尝试离开该单元格时，<xref:System.Windows.Forms.DataGridView.CellValidating> 事件处理程序将检查新的公司名称字符串，以确保它不为空；如果新的值是空字符串，则 <xref:System.Windows.Forms.DataGridView> 阻止用户的光标离开该单元格，直到用户输入非空的字符串。  
  
 若要以单个列表的形式复制本主题中的代码，请参见 [如何：验证 Windows 窗体 DataGridView 控件中的数据](../../../../docs/framework/winforms/controls/how-to-validate-data-in-the-windows-forms-datagridview-control.md)。  
  
## 系统必备  
 若要完成本演练，您需要：  
  
-   对 Northwind SQL Server 示例数据库所在的服务器的访问权限。  
  
## 创建窗体  
  
#### 验证在 DataGridView 中输入的数据  
  
1.  创建一个从 <xref:System.Windows.Forms.Form> 派生的类，该类包含一个 <xref:System.Windows.Forms.DataGridView> 控件和一个 <xref:System.Windows.Forms.BindingSource> 组件。  
  
     下面的代码示例提供了基本的初始化功能，并包含一个 `Main` 方法。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewDataValidation#01](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewDataValidation/CS/datavalidation.cs#01)]
     [!code-vb[System.Windows.Forms.DataGridViewDataValidation#01](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewDataValidation/VB/datavalidation.vb#01)]  
    [!code-csharp[System.Windows.Forms.DataGridViewDataValidation#02](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewDataValidation/CS/datavalidation.cs#02)]
    [!code-vb[System.Windows.Forms.DataGridViewDataValidation#02](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewDataValidation/VB/datavalidation.vb#02)]  
  
2.  在窗体的类定义中实现一个方法，用于处理有关与数据库的连接的详细信息。  
  
     此代码示例使用 `GetData` 方法，该方法返回填充的 <xref:System.Data.DataTable> 对象。  请确保将 `connectionString` 变量设置为适用于您的数据库的值。  
  
    > [!IMPORTANT]
    >  将敏感信息（如密码）存储在连接字符串中可能会影响您的应用程序的安全性。  若要控制对数据库的访问，一种较为安全的方法是使用 Windows 身份验证（也称为集成安全性）。  有关更多信息，请参见[保护连接信息](../../../../docs/framework/data/adonet/protecting-connection-information.md)。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewDataValidation#30](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewDataValidation/CS/datavalidation.cs#30)]
     [!code-vb[System.Windows.Forms.DataGridViewDataValidation#30](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewDataValidation/VB/datavalidation.vb#30)]  
  
3.  为窗体的 <xref:System.Windows.Forms.Form.Load> 事件实现一个处理程序，该事件初始化 <xref:System.Windows.Forms.DataGridView> 和 <xref:System.Windows.Forms.BindingSource> 并设置数据绑定。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewDataValidation#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewDataValidation/CS/datavalidation.cs#10)]
     [!code-vb[System.Windows.Forms.DataGridViewDataValidation#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewDataValidation/VB/datavalidation.vb#10)]  
  
4.  实现 <xref:System.Windows.Forms.DataGridView> 控件的 <xref:System.Windows.Forms.DataGridView.CellValidating> 和 <xref:System.Windows.Forms.DataGridView.CellEndEdit> 事件的处理程序。  
  
     可以在 <xref:System.Windows.Forms.DataGridView.CellValidating> 事件处理程序中确定 `CompanyName` 列中的单元格的值是否为空。  如果单元格值验证失败，请将 <xref:System.Windows.Forms.DataGridViewCellValidatingEventArgs?displayProperty=fullName> 类的 <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> 属性设置为 `true`。  这将导致 <xref:System.Windows.Forms.DataGridView> 控件阻止光标离开该单元格。  将该行的 <xref:System.Windows.Forms.DataGridViewRow.ErrorText%2A> 属性设置为解释性字符串。  这将显示错误图标，其工具提示将包含此错误文本。  在 <xref:System.Windows.Forms.DataGridView.CellEndEdit> 事件处理程序中，将该行的 <xref:System.Windows.Forms.DataGridViewRow.ErrorText%2A> 属性设置为空字符串。  只有当单元格退出编辑模式（如果验证失败，则不能退出单元格）时，才能发生 <xref:System.Windows.Forms.DataGridView.CellEndEdit> 事件。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewDataValidation#20](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewDataValidation/CS/datavalidation.cs#20)]
     [!code-vb[System.Windows.Forms.DataGridViewDataValidation#20](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewDataValidation/VB/datavalidation.vb#20)]  
  
## 测试应用程序  
 现在可以测试窗体，以确保其行为与预期相同。  
  
#### 测试窗体  
  
-   编译并运行应用程序。  
  
     您将看到一个用 `Customers` 表的数据填充的 <xref:System.Windows.Forms.DataGridView>。  双击 `CompanyName` 列中的单元格时，可以编辑该值。  如果删除所有字符，并按 Tab 键退出该单元格，则 <xref:System.Windows.Forms.DataGridView> 会阻止您退出。  在该单元格中键入非空字符串后，<xref:System.Windows.Forms.DataGridView> 控件将允许您退出此单元格。  
  
## 后续步骤  
 此应用程序使您对 <xref:System.Windows.Forms.DataGridView> 控件的功能有一个基本了解。  您可以通过以下几种方法来自定义 <xref:System.Windows.Forms.DataGridView> 控件的外观和行为：  
  
-   更改边框和标题样式。  有关更多信息，请参见 [如何：更改 Windows 窗体 DataGridView 控件中的边框和网格线的样式](../../../../docs/framework/winforms/controls/change-the-border-and-gridline-styles-in-the-datagrid.md)。  
  
-   允许或限制用户向 <xref:System.Windows.Forms.DataGridView> 控件中输入数据。  有关更多信息，请参见[如何：防止在 Windows 窗体 DataGridView 控件中添加和删除行](../../../../docs/framework/winforms/controls/prevent-row-addition-and-deletion-datagridview.md)和[如何：使 Windows 窗体 DataGridView 控件中的列只读](../../../../docs/framework/winforms/controls/how-to-make-columns-read-only-in-the-windows-forms-datagridview-control.md)。  
  
-   检查用户输入中是否有与数据库有关的错误。  有关更多信息，请参见 [演练：处理在 Windows 窗体 DataGridView 控件中输入数据时发生的错误](../../../../docs/framework/winforms/controls/handling-errors-that-occur-during-data-entry-in-the-datagrid.md)。  
  
-   使用虚拟模式处理特大数据集。  有关更多信息，请参见 [演练：在 Windows 窗体 DataGridView 控件中实现虚拟模式](../../../../docs/framework/winforms/controls/implementing-virtual-mode-wf-datagridview-control.md)。  
  
-   自定义单元格的外观。  有关更多信息，请参见 [如何：自定义 Windows 窗体 DataGridView 控件中单元格的外观](../../../../docs/framework/winforms/controls/customize-the-appearance-of-cells-in-the-datagrid.md) 和 [如何：设置 Windows 窗体 DataGridView 控件中的字体和颜色样式](../../../../docs/framework/winforms/controls/how-to-set-font-and-color-styles-in-the-windows-forms-datagridview-control.md)。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.BindingSource>   
 [Windows 窗体 DataGridView 控件中的数据输入](../../../../docs/framework/winforms/controls/data-entry-in-the-windows-forms-datagridview-control.md)   
 [如何：验证 Windows 窗体 DataGridView 控件中的数据](../../../../docs/framework/winforms/controls/how-to-validate-data-in-the-windows-forms-datagridview-control.md)   
 [演练：处理在 Windows 窗体 DataGridView 控件中输入数据时发生的错误](../../../../docs/framework/winforms/controls/handling-errors-that-occur-during-data-entry-in-the-datagrid.md)   
 [保护连接信息](../../../../docs/framework/data/adonet/protecting-connection-information.md)