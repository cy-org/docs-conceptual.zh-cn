---
title: "如何：在 TableLayoutPanel 控件中对齐和拉伸控件 | Microsoft Docs"
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
  - "net.ComponentModel.StyleCollectionEditor.TLP.AlignStretchCtrl"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "控件 [Windows 窗体], 对齐"
  - "控件 [Windows 窗体], 拉伸"
  - "TableLayoutPanel 控件 [Windows 窗体], 拉伸控件"
ms.assetid: 7dc1a157-6fee-4995-8ebc-b65bdc0909a8
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：在 TableLayoutPanel 控件中对齐和拉伸控件
可通过 <xref:System.Windows.Forms.Control.Anchor%2A> 和 <xref:System.Windows.Forms.Control.Dock%2A> 属性在 <xref:System.Windows.Forms.TableLayoutPanel> 中对齐和拉伸控件。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 对齐和拉伸控件  
  
1.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.TableLayoutPanel> 控件拖到窗体上。  
  
2.  将 <xref:System.Windows.Forms.Button> 控件从**“工具箱”**拖到 <xref:System.Windows.Forms.TableLayoutPanel> 控件的左上单元格中。  <xref:System.Windows.Forms.Button> 在单元格中居中。  
  
3.  将 <xref:System.Windows.Forms.Button> 控件的 <xref:System.Windows.Forms.Control.Anchor%2A> 属性值设置为 `Left,Right`。  <xref:System.Windows.Forms.Button> 控件将拉伸到与单元格的宽度相符。  
  
4.  将 <xref:System.Windows.Forms.Button> 控件的 <xref:System.Windows.Forms.Control.Anchor%2A> 属性的值设置为 `Top,Bottom`。  <xref:System.Windows.Forms.Button> 控件将拉伸到与单元格的高度相符。  
  
5.  将 <xref:System.Windows.Forms.Button> 控件的 <xref:System.Windows.Forms.Control.Dock%2A> 属性值设置为 <xref:System.Windows.Forms.DockStyle>。  <xref:System.Windows.Forms.Button> 控件将扩展到填满单元格。  
  
6.  将 <xref:System.Windows.Forms.Button> 控件的 <xref:System.Windows.Forms.Control.Dock%2A> 属性值设置为 <xref:System.Windows.Forms.DockStyle>。  <xref:System.Windows.Forms.Button> 控件将恢复到原始大小并移动到单元格的左上角。  **“Windows 窗体设计器”** 已将 <xref:System.Windows.Forms.Control.Anchor%2A> 属性设置为 `Top, Left`。  
  
7.  将 <xref:System.Windows.Forms.Button> 控件的 <xref:System.Windows.Forms.Control.Anchor%2A> 属性值设置为 `Bottom,Right`。  <xref:System.Windows.Forms.Button> 控件将移动到单元格的右下角。  
  
8.  将 <xref:System.Windows.Forms.Button> 控件的 <xref:System.Windows.Forms.Control.Anchor%2A> 属性值设置为 <xref:System.Windows.Forms.AnchorStyles>。  <xref:System.Windows.Forms.Button> 控件将移动到单元格的中心。  
  
## 请参阅  
 [TableLayoutPanel 控件](../../../../docs/framework/winforms/controls/tablelayoutpanel-control-windows-forms.md)