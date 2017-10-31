---
title: "如何：使用设计器冻结 Windows 窗体 DataGridView 控件中的列 | Microsoft Docs"
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
  - "列 [Windows 窗体], 冻结"
  - "数据 [Windows 窗体], 显示"
  - "DataGridView 控件 [Windows 窗体], 列冻结"
  - "Windows 窗体, 列"
ms.assetid: 87412dd2-478f-4751-af87-dafc591fc215
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# 如何：使用设计器冻结 Windows 窗体 DataGridView 控件中的列
用户在查看 Windows 窗体 <xref:System.Windows.Forms.DataGridView> 控件中显示的数据时，有时需要频繁参考一列或若干列。  例如，显示包含多列的用户信息表时，始终显示用户名称而使其他列在可视区域以外滚动会很有用。  
  
 要实现此行为，可以冻结控件中的列。  冻结一列后，其左侧（在从右到左的字符集中为右侧）的所有列也被冻结。  冻结的列保持不动，而其他所有列可以滚动。  如果允许对列进行重新排序，则将冻结的列视为一组，以区别于未冻结的列。  用户可重新调整冻结和未冻结这两个组中列的位置，但不能将其中一组中的列移动到另一组。  
  
 下面的过程需要一个**“Windows 应用程序”**项目，项目中应有一个包含 <xref:System.Windows.Forms.DataGridView> 控件的窗体。  有关设置此类项目的信息，请参见[How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)和[如何：向 Windows 窗体添加控件](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 使用设计器冻结列  
  
1.  单击 <xref:System.Windows.Forms.DataGridView> 控件右上角的智能标记标志符号 \(![智能标记标志符号](../../../../docs/framework/winforms/controls/media/vs-winformsmttagglyph.png "VS\_WinFormSmtTagGlyph")\)，然后选择**“编辑列”**。  
  
2.  从**“选定的列”**列表中选择一列。  
  
3.  在**“列属性”**网格中，将 <xref:System.Windows.Forms.DataGridViewColumn.Frozen%2A> 属性设置为 `true`。  
  
    > [!NOTE]
    >  还可通过选择**“添加列”**对话框中的**“已冻结”**冻结一列。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridViewColumn.Frozen%2A?displayProperty=fullName>   
 [如何：使用设计器添加和移除 Windows 窗体 DataGridView 控件中的列](../../../../docs/framework/winforms/controls/add-and-remove-columns-in-the-datagrid-using-the-designer.md)   
 [如何：使用设计器在 Windows 窗体的 DataGridView 控件中启用列重新排序](../../../../docs/framework/winforms/controls/enable-column-reordering-in-the-datagrid-using-the-designer.md)   
 [How to: Display Right\-to\-Left Text in Windows Forms for Globalization](http://msdn.microsoft.com/zh-cn/f0663385-2354-4c65-8676-706422283b14)   
 [How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)   
 [如何：向 Windows 窗体添加控件](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)