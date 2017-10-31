---
title: "如何：自定义 Windows 窗体 DataGridView 控件中行的外观 | Microsoft Docs"
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
  - "数据网格, 自定义行"
  - "DataGridView 控件 [Windows 窗体], 自定义行"
  - "行, 在 DataGridView 控件中自定义"
ms.assetid: d40b53d2-7e7c-48c5-8570-6e79d15c3bbb
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：自定义 Windows 窗体 DataGridView 控件中行的外观
通过处理 <xref:System.Windows.Forms.DataGridView.RowPrePaint?displayProperty=fullName> 和 <xref:System.Windows.Forms.DataGridView.RowPostPaint?displayProperty=fullName> 事件之一或两者同时处理，可以控制 <xref:System.Windows.Forms.DataGridView> 行的外观。  这些事件设计用于使你可以仅绘制想绘制的内容，同时使 <xref:System.Windows.Forms.DataGridView> 控件绘制其余内容。  例如，如果要绘制自定义背景，则可以处理 <xref:System.Windows.Forms.DataGridView.RowPrePaint?displayProperty=fullName> 事件并让各个单元格自行绘制自己的前景内容。  或者，还可以让单元格自行绘制，并在 <xref:System.Windows.Forms.DataGridView.RowPostPaint?displayProperty=fullName> 事件的处理程序中添加自定义前景内容。  此外，还可以禁用单元格绘制，并在 <xref:System.Windows.Forms.DataGridView.RowPrePaint?displayProperty=fullName> 事件处理程序中亲自绘制所有内容。  
  
 下面的代码示例实现两个事件的处理程序，以便提供渐变选区背景和某些跨多个列的自定义前景内容。  
  
## 示例  
 [!code-csharp[System.Windows.Forms.DataGridViewRowPainting#00](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewRowPainting/CS/datagridviewrowpainting.cs#00)]
 [!code-vb[System.Windows.Forms.DataGridViewRowPainting#00](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewRowPainting/VB/datagridviewrowpainting.vb#00)]  
  
## 编译代码  
 此示例需要：  
  
-   对 System、System.Drawing 和 System.Windows.Forms 程序集的引用。  
  
 有关从 [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] 或 [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 命令行生成此示例的信息，请参阅[从命令行生成](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) 或[在命令行上使用 csc.exe 生成](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)。  还可以通过将代码粘贴到新项目，在 [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] 中生成此示例。  另请参阅[如何：使用 Visual Studio 编译和运行完整的 Windows 窗体代码示例](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\))。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.RowPrePaint?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.RowPostPaint?displayProperty=fullName>   
 [自定义 Windows 窗体 DataGridView 控件](../../../../docs/framework/winforms/controls/customizing-the-windows-forms-datagridview-control.md)   
 [DataGridView 控件体系结构](../../../../docs/framework/winforms/controls/datagridview-control-architecture-windows-forms.md)