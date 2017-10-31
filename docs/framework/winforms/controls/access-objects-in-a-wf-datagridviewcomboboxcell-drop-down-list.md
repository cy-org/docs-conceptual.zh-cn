---
title: "如何：访问 Windows 窗体 DataGridViewComboBoxCell 下拉列表中的对象 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "组合框, 访问 DataGridViewComboBoxCell 下拉列表中的对象"
  - "组合框, 在 DataGridView 控件中"
  - "DataGridView 控件 [Windows 窗体], 访问组合框单元格中的对象"
ms.assetid: bcbe794a-d1fa-47f8-b5a3-5f085b32097d
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# 如何：访问 Windows 窗体 DataGridViewComboBoxCell 下拉列表中的对象
与 <xref:System.Windows.Forms.ComboBox> 控件一样，<xref:System.Windows.Forms.DataGridViewComboBoxColumn> 和 <xref:System.Windows.Forms.DataGridViewComboBoxCell> 类型允许向其下拉列表添加任意对象。  使用此功能，可以在下拉列表中表示复杂的状态，而不必在单独集合中存储相应的对象。  
  
 与 <xref:System.Windows.Forms.ComboBox> 控件不同，<xref:System.Windows.Forms.DataGridView> 类型不具有用于检索当前所选对象的 <xref:System.Windows.Forms.ComboBox.SelectedItem%2A> 属性，  必须将 <xref:System.Windows.Forms.DataGridViewComboBoxColumn.ValueMember%2A?displayProperty=fullName> 或 <xref:System.Windows.Forms.DataGridViewComboBoxCell.ValueMember%2A?displayProperty=fullName> 属性设置为业务对象的属性名称。  当用户进行选择时，指示的业务对象属性将设置单元格 <xref:System.Windows.Forms.DataGridViewCell.Value%2A> 属性。  
  
 要通过单元格值检索业务对象，`ValueMember` 属性必须指示一个属性，该属性返回对业务对象本身的引用。  因此，如果业务对象的类型不受您的控制，您必须通过继承来扩展该类型，从而添加此类属性。  
  
 下面的过程演示如何用业务对象填充下拉列表并通过单元格 <xref:System.Windows.Forms.DataGridViewCell.Value%2A> 属性检索对象。  
  
### 向下拉列表添加业务对象  
  
1.  创建新的 <xref:System.Windows.Forms.DataGridViewComboBoxColumn> 并填充其 <xref:System.Windows.Forms.DataGridViewComboBoxColumn.Items%2A> 集合。  或者，可以将列 <xref:System.Windows.Forms.DataGridViewComboBoxColumn.DataSource%2A> 属性设置为业务对象的集合。  但在这种情况下，如果没有在集合中创建相应的业务对象，就不能向下拉列表添加“未赋值”。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewComboBoxObjectBinding#110](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/CS/form1.cs#110)]
     [!code-vb[System.Windows.Forms.DataGridViewComboBoxObjectBinding#110](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/vb/form1.vb#110)]  
  
2.  设置 <xref:System.Windows.Forms.DataGridViewComboBoxColumn.DisplayMember%2A> 和 <xref:System.Windows.Forms.DataGridViewComboBoxColumn.ValueMember%2A> 属性。  <xref:System.Windows.Forms.DataGridViewComboBoxColumn.DisplayMember%2A> 指示要显示在下拉列表中的业务对象的属性。  <xref:System.Windows.Forms.DataGridViewComboBoxColumn.ValueMember%2A> 指示返回对业务对象的引用的属性。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewComboBoxObjectBinding#115](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/CS/form1.cs#115)]
     [!code-vb[System.Windows.Forms.DataGridViewComboBoxObjectBinding#115](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/vb/form1.vb#115)]  
  
3.  确保业务对象类型包含一个属性，该属性返回对当前实例的引用。  此属性必须以上一步中分配给 <xref:System.Windows.Forms.DataGridViewComboBoxColumn.ValueMember%2A> 的值来命名。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewComboBoxObjectBinding#310](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/CS/form1.cs#310)]
     [!code-vb[System.Windows.Forms.DataGridViewComboBoxObjectBinding#310](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/vb/form1.vb#310)]  
  
### 检索当前所选的业务对象  
  
-   获取单元格 <xref:System.Windows.Forms.DataGridViewCell.Value%2A> 属性，将其强制转换为业务对象类型。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewComboBoxObjectBinding#120](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/CS/form1.cs#120)]
     [!code-vb[System.Windows.Forms.DataGridViewComboBoxObjectBinding#120](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/vb/form1.vb#120)]  
  
## 示例  
 整个示例演示了对下拉列表中业务对象的使用。  在此示例中，<xref:System.Windows.Forms.DataGridView> 控件被绑定到 `Task` 对象的集合。  每个 `Task` 对象都有一个 `AssignedTo` 属性，该属性指示当前分配给该任务的 `Employee` 对象。  `Assigned To` 列显示每个已分配员工的 `Name` 属性值；如果 `Task.AssignedTo` 属性值为 `null`，则显示“未赋值”。  
  
 要查看此示例的行为，请执行下列步骤：  
  
1.  从下拉列表选择不同的值，或在组合框单元格中按 CTRL\+0，从而更改 `Assigned To` 列中的赋值。  
  
2.  单击 `Generate Report` 以显示当前赋值。  此操作演示 `Assigned To` 列中的更改会自动更新 `tasks` 集合。  
  
3.  单击 `Request Status` 按钮，以便为该行调用当前 `Employee` 对象的 `RequestStatus` 方法。  此操作演示所选对象已检索成功。  
  
 [!code-csharp[System.Windows.Forms.DataGridViewComboBoxObjectBinding#000](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/CS/form1.cs#000)]
 [!code-vb[System.Windows.Forms.DataGridViewComboBoxObjectBinding#000](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewComboBoxObjectBinding/vb/form1.vb#000)]  
  
## 编译代码  
 此示例需要：  
  
-   对 System 和 System.Windows.Forms 程序集的引用。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridViewComboBoxColumn>   
 <xref:System.Windows.Forms.DataGridViewComboBoxColumn.Items%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewComboBoxColumn.DataSource%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewComboBoxColumn.ValueMember%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewComboBoxCell>   
 <xref:System.Windows.Forms.DataGridViewComboBoxCell.Items%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewComboBoxCell.DataSource%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewComboBoxCell.ValueMember%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewCell.Value%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.ComboBox>   
 [在 Windows 窗体 DataGridView 控件中显示数据](../../../../docs/framework/winforms/controls/displaying-data-in-the-windows-forms-datagridview-control.md)