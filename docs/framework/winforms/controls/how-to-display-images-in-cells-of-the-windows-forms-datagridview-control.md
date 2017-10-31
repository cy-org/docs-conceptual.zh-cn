---
title: "如何：在 Windows 窗体 DataGridView 控件的单元格中显示图像 | Microsoft Docs"
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
  - "单元格, 显示图像"
  - "数据网格, 在单元格中显示图像"
  - "数据网格, 在网格中显示"
  - "DataGridView 控件 [Windows 窗体], 显示图像"
ms.assetid: 53b13d31-1b56-476d-9ab4-18bfac138a22
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：在 Windows 窗体 DataGridView 控件的单元格中显示图像
图片或图形是可以在一行数据中显示的值之一。  这些图形通常采用雇员照片或公司徽标的形式。  
  
 当在 <xref:System.Windows.Forms.DataGridView> 控件内显示数据时，并入图片很简单。  <xref:System.Windows.Forms.DataGridView> 控件本身处理 <xref:System.Drawing.Image> 类支持的任何图像格式，以及一些数据库使用的 OLE 图片格式。  
  
 如果 <xref:System.Windows.Forms.DataGridView> 控件的数据源具有一列图像，则 <xref:System.Windows.Forms.DataGridView> 控件将自动显示它们。  
  
 下面的代码示例演示如何从嵌入式资源提取图标并将其转换为位图以便在图像列的每个单元格中显示。  有关将文本单元格值替换为相应图像的其他示例，请参见 [如何：自定义 Windows 窗体 DataGridView 控件中的数据格式设置](../../../../docs/framework/winforms/controls/how-to-customize-data-formatting-in-the-windows-forms-datagridview-control.md)。  
  
## 示例  
 [!code-csharp[System.Windows.Forms.DataGridViewMisc#050](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#050)]
 [!code-vb[System.Windows.Forms.DataGridViewMisc#050](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#050)]  
  
## 编译代码  
 此示例需要：  
  
-   名为 `dataGridView1` 的 <xref:System.Windows.Forms.DataGridView> 控件。  
  
-   名为 `tree.ico` 的嵌入式图标。  
  
-   对 <xref:System?displayProperty=fullName>、<xref:System.Windows.Forms?displayProperty=fullName> 和 <xref:System.Drawing?displayProperty=fullName> 程序集的引用。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 [Windows 窗体 DataGridView 控件中的基本列、行和单元格功能](../../../../docs/framework/winforms/controls/basic-column-row-and-cell-features-wf-datagridview-control.md)   
 [如何：自定义 Windows 窗体 DataGridView 控件中的数据格式设置](../../../../docs/framework/winforms/controls/how-to-customize-data-formatting-in-the-windows-forms-datagridview-control.md)