---
title: "如何：使用设计器更改 Windows 窗体 DataGridView 控件中列的顺序 | Microsoft Docs"
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
  - "列 [Windows 窗体], 顺序"
  - "数据 [Windows 窗体], 显示"
  - "DataGridView 控件 [Windows 窗体], 列顺序"
  - "Windows 窗体, 列"
ms.assetid: 7fe52a98-75d6-448c-97a5-65ca2c568c1a
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：使用设计器更改 Windows 窗体 DataGridView 控件中列的顺序
将 Windows 窗体 <xref:System.Windows.Forms.DataGridView> 控件绑定到数据源时，自动生成的列的显示顺序由数据源确定。  如果不希望以这种顺序显示，可使用设计器进行更改。  您可能还需要将未绑定的列添加到控件，并更改这些列的显示顺序。  有关如何以编程方式更改列顺序的更多信息，请参见[如何：更改 Windows 窗体 DataGridView 控件中列的顺序](../../../../docs/framework/winforms/controls/how-to-change-the-order-of-columns-in-the-windows-forms-datagridview-control.md)。  
  
 下面的过程需要一个**“Windows 应用程序”**项目，项目中应有一个包含 <xref:System.Windows.Forms.DataGridView> 控件的窗体。  有关设置此类项目的信息，请参见[How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)和[如何：向 Windows 窗体添加控件](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)  
  
### 使用设计器更改列顺序  
  
1.  单击 <xref:System.Windows.Forms.DataGridView> 控件右上角的智能标记标志符号 \(![智能标记标志符号](../../../../docs/framework/winforms/controls/media/vs-winformsmttagglyph.png "VS\_WinFormSmtTagGlyph")\)，然后选择**“编辑列”**。  
  
2.  从**“选定的列”**列表中选择一列。  
  
3.  单击**“选定的列”**列表右边的向上或向下箭头，直到选定的列位于所希望的位置。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 [如何：使用设计器添加和移除 Windows 窗体 DataGridView 控件中的列](../../../../docs/framework/winforms/controls/add-and-remove-columns-in-the-datagrid-using-the-designer.md)   
 [How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)   
 [如何：向 Windows 窗体添加控件](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)