---
title: "如何：使用设计器更改 Windows 窗体 DataGridView 列的类型 | Microsoft Docs"
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
  - "列 [Windows 窗体], 类型"
  - "数据 [Windows 窗体], 显示"
  - "DataGridView 控件 [Windows 窗体], 更改列类型"
  - "Windows 窗体, 列"
ms.assetid: 7f994d45-600d-4190-a187-35803214b40c
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：使用设计器更改 Windows 窗体 DataGridView 列的类型
有时，对于已经添加到 Windows 窗体 <xref:System.Windows.Forms.DataGridView> 控件中的列，您需要更改列的类型。  例如，将该控件绑定到数据源时，可能需要更改某些自动生成的列的类型。  如果所显示的表的某些列包含到相关表中行的外键，这会很有用。  在这种情况下，可能需要用组合框列来取代显示这些外键的文本框列，这些组合框列用于显示相关表中更有意义的值。  
  
 下面的过程需要一个**“Windows 应用程序”**项目，项目中应有一个包含 <xref:System.Windows.Forms.DataGridView> 控件的窗体。  有关设置此类项目的信息，请参见[How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)和[如何：向 Windows 窗体添加控件](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 使用设计器更改列的类型  
  
1.  单击 <xref:System.Windows.Forms.DataGridView> 控件右上角的智能标记标志符号 \(![智能标记标志符号](../../../../docs/framework/winforms/controls/media/vs-winformsmttagglyph.png "VS\_WinFormSmtTagGlyph")\)，然后选择**“编辑列”**。  
  
2.  从**“选定的列”**列表中选择一列。  
  
3.  在**“列属性”**网格中，将 `ColumnType` 属性设置为新的列类型。  
  
    > [!NOTE]
    >  `ColumnType` 属性是一个“仅用于设计时”属性，它指示的类表示列类型。  它不是列类中定义的实际属性。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridViewColumn>   
 [How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)   
 [如何：向 Windows 窗体添加控件](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)