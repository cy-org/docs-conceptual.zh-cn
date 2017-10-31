---
title: "如何：在 TableLayoutPanel 控件中跨行和跨列 | Microsoft Docs"
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
  - "net.ComponentModel.StyleCollectionEditor.TLP.SpanRowsColumns"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "单元格, 合并"
  - "列 [Windows 窗体], 跨越"
  - "合并单元格"
  - "行 [Windows 窗体], 跨越"
  - "TableLayoutPanel 控件 [Windows 窗体], 跨越行和列"
ms.assetid: a8a2fdd3-a848-48b0-a4cd-4e85ebded87e
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：在 TableLayoutPanel 控件中跨行和跨列
<xref:System.Windows.Forms.TableLayoutPanel> 控件中的控件可以跨相邻的行和列。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 跨行和跨列  
  
1.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.TableLayoutPanel> 控件拖到窗体上。  
  
2.  将 <xref:System.Windows.Forms.Button> 控件从**“工具箱”**拖到 <xref:System.Windows.Forms.TableLayoutPanel> 控件的左上单元格中。  
  
3.  将 <xref:System.Windows.Forms.Button> 控件的**“ColumnSpan”**属性设置为 2。  注意，<xref:System.Windows.Forms.Button> 控件将跨越第一列和第二列。  
  
4.  将 <xref:System.Windows.Forms.Button> 控件的**“RowSpan”**属性设置为 2。  注意，<xref:System.Windows.Forms.Button> 控件将跨越第一列和第二列。  
  
5.  将 <xref:System.Windows.Forms.Button> 控件的**“ColumnSpan”**属性设置为 1。  注意，<xref:System.Windows.Forms.Button> 控件将移到第一列并跨越第一行和第二行。  
  
## 请参阅  
 [TableLayoutPanel 控件](../../../../docs/framework/winforms/controls/tablelayoutpanel-control-windows-forms.md)