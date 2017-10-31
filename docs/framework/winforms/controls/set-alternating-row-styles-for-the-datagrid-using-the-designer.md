---
title: "如何：使用设计器设置 Windows 窗体 DataGridView 控件的交替行样式 | Microsoft Docs"
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
  - "数据 [Windows 窗体], 显示"
  - "DataGridView 控件 [Windows 窗体], 行样式替换"
  - "类似分类帐的格式"
  - "行, 交替"
  - "Windows 窗体, 行"
ms.assetid: 02373442-bf94-4470-9f8a-e44c4a9d5b88
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：使用设计器设置 Windows 窗体 DataGridView 控件的交替行样式
表格数据通常以类似帐目的格式显示，其中各交替行的背景颜色不同。  这种格式便于用户判断每一行中有哪些单元格，特别是在表格很宽，有很多列的情况下。  
  
 对于 <xref:System.Windows.Forms.DataGridView> 控件，可以为交替行指定完整的样式信息。  除了背景颜色之外，还可以使用诸如前景颜色和字体等样式特性来区分交替行。  有关更多信息，请参见 [Windows 窗体 DataGridView 控件中的单元格样式](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md)。  
  
 下面的过程需要一个**“Windows 应用程序”**项目，项目中应有一个包含 <xref:System.Windows.Forms.DataGridView> 控件的窗体。  有关设置此类项目的信息，请参见[How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)和[如何：向 Windows 窗体添加控件](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 定义交替行样式  
  
1.  在设计器中选择 <xref:System.Windows.Forms.DataGridView> 控件。  
  
2.  在**“属性”**窗口中，单击 <xref:System.Windows.Forms.DataGridView.AlternatingRowsDefaultCellStyle%2A> 属性旁的省略号按钮 \(![VisualStudioEllipsesButton 屏幕快照](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\)。  
  
3.  在**“CellStyle 生成器”**对话框中，通过设置属性定义样式，再使用**“预览”**窗格确认选择。  您所指定的样式将用于控件中显示的每一个交替行（从第二行开始）。  
  
4.  若要定义其余各行的样式，请使用 <xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A> 属性重复步骤 2 和步骤 3。  
  
    > [!NOTE]
    >  将使用从多个属性继承的样式显示单元格。  有关样式继承的更多信息，请参见 [Windows 窗体 DataGridView 控件中的单元格样式](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md)。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 [Windows 窗体 DataGridView 控件中的单元格样式](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md)   
 [Windows 窗体 DataGridView 控件中的基本格式设置和样式设置](../../../../docs/framework/winforms/controls/basic-formatting-and-styling-in-the-windows-forms-datagridview-control.md)   
 [将设计器与 Windows 窗体 DataGridView 控件结合使用](../../../../docs/framework/winforms/controls/using-the-designer-with-the-windows-forms-datagridview-control.md)   
 [How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)   
 [如何：向 Windows 窗体添加控件](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)