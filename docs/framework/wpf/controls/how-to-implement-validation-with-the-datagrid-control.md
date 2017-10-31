---
title: "如何：用 DataGrid 控件实现验证 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "DataGrid [WPF], 验证"
  - "验证 [WPF], DataGrid"
ms.assetid: ec6078a8-1e42-4648-b414-f4348e81bda1
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：用 DataGrid 控件实现验证
利用 <xref:System.Windows.Controls.DataGrid> 控件，您既可以在单元格级别也可以在行级别执行验证。  通过单元格级别验证，将可在用户更新值时验证绑定数据对象的个别属性。  通过行级别验证，将可在用户提交对行的更改时验证整个数据对象。  您也可以为验证错误提供自定义的可视反馈，或使用 <xref:System.Windows.Controls.DataGrid> 控件提供的默认可视反馈。  
  
 以下过程介绍如何将验证规则应用于 <xref:System.Windows.Controls.DataGrid> 绑定，并自定义可视反馈。  
  
### 验证个别单元格值  
  
-   对用于列的绑定指定一条或多条验证规则。  这与在简单控件中验证数据类似，如[数据绑定概述](../../../../docs/framework/wpf/data/data-binding-overview.md)中所述。  
  
     下面的示例显示一个 <xref:System.Windows.Controls.DataGrid> 控件，其中包含绑定到业务对象的不同属性的四个列。  其中三个列通过将 <xref:System.Windows.Data.Binding.ValidatesOnExceptions%2A> 属性设置为 `true` 来指定 <xref:System.Windows.Controls.ExceptionValidationRule>。  
  
     [!code-xml[DataGrid_Validation#BasicXaml](../../../../samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/window1.xaml#basicxaml)]  
  
     当用户输入无效的值，例如在“Course ID”（课程 ID）列中输入非整数时，单元格周围将出现一个红色边框。  可以按照下面过程中所述的方式更改此默认验证反馈。  
  
### 自定义单元格验证反馈  
  
-   将列的 <xref:System.Windows.Controls.DataGridBoundColumn.EditingElementStyle%2A> 属性设置为适合于列的编辑控件的样式。  由于编辑控件是在运行时创建的，因此您无法像处理简单控件一样使用 <xref:System.Windows.Controls.Validation.ErrorTemplate%2A?displayProperty=fullName> 附加属性。  
  
     下面的示例通过添加由具有验证规则的三个列共享的错误样式来更新前面的示例。  当用户输入无效的值时，样式会更改单元格背景颜色，并添加一个工具提示。  请注意使用触发器来确定是否存在验证错误的做法。  这是必要的，因为当前没有专门用于单元格的错误模板。  
  
     [!code-xml[DataGrid_Validation#CellValidationXaml](../../../../samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml#cellvalidationxaml)]  
  
     可通过替换列使用的 <xref:System.Windows.Controls.DataGridColumn.CellStyle%2A> 来实现更广泛的自定义。  
  
### 验证单个行中的多个值  
  
1.  实现一个 <xref:System.Windows.Controls.ValidationRule> 子类，该子类将检查绑定的数据对象的多个属性。  在 <xref:System.Windows.Controls.ValidationRule.Validate%2A> 方法实现中，将 `value` 参数值强制转换为 <xref:System.Windows.Data.BindingGroup> 实例。  然后，即可通过 <xref:System.Windows.Data.BindingGroup.Items%2A> 属性访问数据对象。  
  
     下面的示例演示此过程，以验证 `Course` 对象的 `StartDate` 属性值是否早于其 `EndDate` 属性值。  
  
     [!code-csharp[DataGrid_Validation#CourseValidationRule](../../../../samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml.cs#coursevalidationrule)]
     [!code-vb[DataGrid_Validation#CourseValidationRule](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/datagrid_validation/vb/mainwindow.xaml.vb#coursevalidationrule)]  
  
2.  将验证规则添加到 <xref:System.Windows.Controls.DataGrid.RowValidationRules%2A?displayProperty=fullName> 集合。  <xref:System.Windows.Controls.DataGrid.RowValidationRules%2A> 属性提供对 <xref:System.Windows.Data.BindingGroup> 实例的 <xref:System.Windows.Data.BindingGroup.ValidationRules%2A> 属性的直接访问，该实例对控件使用的所有绑定进行分组。  
  
     下面的示例在 XAML 中设置 <xref:System.Windows.Controls.DataGrid.RowValidationRules%2A> 属性。  <xref:System.Windows.Controls.ValidationRule.ValidationStep%2A> 属性设置为 <xref:System.Windows.Controls.ValidationStep>，以使验证只会在更新了绑定数据对象之后进行。  
  
     [!code-xml[DataGrid_Validation#RowValidationRulesXaml](../../../../samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml#rowvalidationrulesxaml)]  
  
     当用户指定早于开始日期的结束日期时，行标题中将出现一个红色感叹号 \(\!\)。  可以按照下面过程中所述的方式更改此默认验证反馈。  
  
### 自定义行验证反馈  
  
-   设置 <xref:System.Windows.Controls.DataGrid.RowValidationErrorTemplate%2A?displayProperty=fullName> 属性。  利用此属性，您可以为个别 <xref:System.Windows.Controls.DataGrid> 控件自定义行验证反馈。  通过使用隐式行样式来设置 <xref:System.Windows.Controls.DataGridRow.ValidationErrorTemplate%2A?displayProperty=fullName> 属性，您也可以影响多个控件。  
  
     下面的示例将默认行验证反馈替换为更直观的指示符。  当用户输入无效的值时，行标题中将出现一个带有白色感叹号的红色圆圈。  对于行验证错误和单元格验证错误，都将发生此情况。  关联的错误消息显示在工具提示中。  
  
     [!code-xml[DataGrid_Validation#RowValidationFeedbackXaml](../../../../samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml#rowvalidationfeedbackxaml)]  
  
## 示例  
 下面的示例提供了单元格验证和行验证的完整演示。  `Course` 类提供了一个示例数据对象，该对象实现 <xref:System.ComponentModel.IEditableObject> 以支持事务。  <xref:System.Windows.Controls.DataGrid> 控件与 <xref:System.ComponentModel.IEditableObject> 交互，使用户能够通过按 Esc 来恢复更改。  
  
> [!NOTE]
>  如果使用的是 Visual Basic，请在 MainWindow.xaml 的第一行中将 `x:Class="DataGridValidation.MainWindow"` 替换为 `x:Class="MainWindow"`。  
  
 若要测试验证，请尝试以下操作：  
  
-   在“Course ID”（课程 ID）列中，输入一个非整数值。  
  
-   在“End Date”（结束日期）列中，输入一个早于开始日期的日期。  
  
-   删除“Course ID”（课程 ID）、“Start Date”（开始日期）或“End Date”（结束日期）中的值。  
  
-   若要撤消无效的单元格值，请将光标重新放在单元格中，并按 Esc 键。  
  
-   若要在当前单元格处于编辑模式中时撤消整行的更改，请按 Esc 键两次。  
  
-   发生验证错误时，将鼠标指针移到行标题中的指示符上即可看到关联的错误消息。  
  
 [!code-csharp[DataGrid_Validation#FullCode](../../../../samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml.cs#fullcode)]
 [!code-vb[DataGrid_Validation#FullCode](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/datagrid_validation/vb/mainwindow.xaml.vb#fullcode)]  
  
 [!code-xml[DataGrid_Validation#FullXaml](../../../../samples/snippets/csharp/VS_Snippets_Wpf/datagrid_validation/cs/mainwindow.xaml#fullxaml)]  
  
## 请参阅  
 <xref:System.Windows.Controls.DataGrid>   
 [DataGrid](../../../../docs/framework/wpf/controls/datagrid.md)   
 [数据绑定](../../../../docs/framework/wpf/data/data-binding-wpf.md)   
 [实现绑定验证](../../../../docs/framework/wpf/data/how-to-implement-binding-validation.md)   
 [在自定义对象上实现验证逻辑](../../../../docs/framework/wpf/data/how-to-implement-validation-logic-on-custom-objects.md)