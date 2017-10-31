---
title: "如何：在 TableLayoutPanel 控件中编辑行和列 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "net.ComponentModel.StyleCollectionEditor"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "列 [Windows 窗体], 编辑"
  - "行 [Windows 窗体], 编辑"
  - "TableLayoutPanel 控件 [Windows 窗体], 编辑"
ms.assetid: c367ed43-40dc-49eb-9e0f-ba70e83dfec0
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：在 TableLayoutPanel 控件中编辑行和列
可以使用 <xref:System.Windows.Forms.TableLayoutPanel> 控件的集合编辑器（称作**“列和行样式”**对话框）来编辑控件的行和列。  
  
> [!NOTE]
>  如果您希望控件跨多个行或多个列，可设置控件上的 `RowSpan` 和 `ColumnSpan` 属性。  有关更多信息，请参见 [演练：使用 TableLayoutPanel 在 Windows 窗体上排列控件](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)。  
>   
>  若要在单元格中对齐控件，或在单元格内拉伸控件，请使用控件的 <xref:System.Windows.Forms.Control.Anchor%2A> 属性。  有关更多信息，请参见 [演练：使用 TableLayoutPanel 在 Windows 窗体上排列控件](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)。  
>   
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 编辑行和列  
  
1.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.TableLayoutPanel> 控件拖到窗体上。  
  
2.  单击 <xref:System.Windows.Forms.TableLayoutPanel> 控件的智能标记标志符号 \(![智能标记标志符号](../../../../docs/framework/winforms/controls/media/vs-winformsmttagglyph.png "VS\_WinFormSmtTagGlyph")\)，并选择**“编辑行和列”**来打开**“列和行样式”**对话框。  还可右击 <xref:System.Windows.Forms.TableLayoutPanel> 控件并从快捷菜单中选择**“编辑行和列”**。  
  
3.  若要添加或移除列，请从**“成员类型”**下拉列表框中选择**“列”**。  
  
4.  若要添加或移除行，请从**“成员类型”**下拉列表框中选择**“行”**。  
  
5.  单击**“添加”**按钮可将一行或一列添加到**“成员”**列表的末尾。  
  
6.  单击**“插入”**按钮可将一行或一列添加到列表中当前选定项之前。  
  
7.  如果要添加一行或一列，请为新行或新列选择**“大小类型”**。  有关更多信息，请参见 <xref:System.Windows.Forms.SizeType>。  
  
8.  若要移除一行或一列，请单击**“移除”**按钮删除**“成员”**列表中的当前选定项。  
  
## 请参阅  
 <xref:System.Windows.Forms.SizeType>   
 [TableLayoutPanel 控件](../../../../docs/framework/winforms/controls/tablelayoutpanel-control-windows-forms.md)