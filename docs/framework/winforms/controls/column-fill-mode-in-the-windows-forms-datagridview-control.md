---
title: "Windows 窗体 DataGridView 控件中的列填充模式 | Microsoft Docs"
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
  - "数据网格, 自动调整列大小"
  - "数据网格, 列填充模式"
  - "DataGridView 控件 [Windows 窗体], 列填充模式"
ms.assetid: b4ef7411-ebf4-4e26-bb33-aecec90de80c
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Windows 窗体 DataGridView 控件中的列填充模式
在列填充模式中，<xref:System.Windows.Forms.DataGridView> 控件自动调整其列的大小，以便它们可填充可用显示区域的宽度。  该控件不显示水平滚动条，除非有必要使每列的宽度等于或大于其 <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A> 属性值。  
  
 每列的大小调整行为取决于其 <xref:System.Windows.Forms.DataGridViewColumn.InheritedAutoSizeMode%2A> 属性。  如果列值为 <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode>（默认值），则此属性的值继承自列的 <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A> 属性或控件的 <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A> 属性。  
  
 每列都可有不同的大小模式，但具有 <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode> 大小模式的任何列将共享其他列未使用的显示区域宽度。  将根据列的 <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> 属性值在填充模式列间按比例划分宽度。  例如，如果两个列的 <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> 值为 100 和 200，则第一列的宽度将为第二列的一半。  
  
## 填充模式中的用户大小调整  
 不同于基于单元格内容的大小进行调整的调整模式，填充模式不会阻止用户调整 <xref:System.Windows.Forms.DataGridViewColumn.Resizable%2A> 属性值为 `true` 的列。  当用户调整填充模式列的大小时，也将对已调整列之后的任何填充模式列（如果 <xref:System.Windows.Forms.Control.RightToLeft%2A> 是 `false`，则向右；否则向左）的大小进行调整，以弥补可用宽度的更改。  如果在已调整列之后没有填充模式列，则调整控件中的所有其他填充模式列的大小以进行补偿。  如果控件中没有其他的填充模式列，则忽略大小调整。  如果调整了非填充模式的列大小，那么控件中的所有填充模式列都更改大小以便进行补偿。  
  
 调整填充模式列的大小后，也将按比例调整更改的所有列的 <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> 值。  例如，如果四个填充模式列的 <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> 值为 100，将第二列的宽度调整为其原始宽度的一半，将导致 <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> 值为 100、50、125 和 125。  调整非填充模式中列的大小不会更改任何 <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> 值，因为填充模式列只需在保留相同比例的情况下调整大小以进行补偿。  
  
## 基于内容的 FillWeight 调整  
 可以使用 <xref:System.Windows.Forms.DataGridView> 自动调整大小的方法（如 <xref:System.Windows.Forms.DataGridView.AutoResizeColumns%2A> 方法）初始化填充模式列的 <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> 值。  此方法首先计算列所需的宽度以显示其内容。  接下来，该控件调整所有填充模式列的 <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> 值，以便其比例匹配计算的宽度的比例。  最后，该控件使用新的 <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> 比例调整填充模式列的大小，以便控件中的所有列都填充可用的水平空间。  
  
## 示例  
  
### 描述  
 通过使用 <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A>、<xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A>、<xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> 和 <xref:System.Windows.Forms.DataGridViewColumn.Resizable%2A> 属性的适当值，可为多种不同方案自定义列的大小调整行为。  
  
 下面的演示代码使你能够试验不同列的 <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A>、<xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> 和 <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A> 属性的不同值。  在此示例中，<xref:System.Windows.Forms.DataGridView> 控件绑定到其自身的 <xref:System.Windows.Forms.DataGridView.Columns%2A> 集合，并且有一列绑定到 <xref:System.Windows.Forms.DataGridViewColumn.HeaderText%2A>、<xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A>、<xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A>、<xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A> 和 <xref:System.Windows.Forms.DataGridViewColumn.Width%2A> 各属性。  每列也可由控件中的行表示，更改行的值将更新对应列的属性，这样你可以看到值如何进行交互。  
  
### 代码  
 [!code-csharp[System.Windows.Forms.DataGridViewFillColumnsDemo#00](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewFillColumnsDemo/CS/fillcolumns.cs#00)]
 [!code-vb[System.Windows.Forms.DataGridViewFillColumnsDemo#00](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewFillColumnsDemo/vb/fillcolumns.vb#00)]  
  
### 注释  
 使用此演示应用程序：  
  
-   更改窗体大小。  观察列如何更改宽度并同时保留由 <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> 属性值指示的比例。  
  
-   通过使用鼠标拖动列分隔线，更改列的大小。  观察 <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> 值如何进行更改。  
  
-   更改某一列的 <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A> 值，然后拖动以调整窗体大小。  当将窗体调整到足够小时，观察如何让 <xref:System.Windows.Forms.DataGridViewColumn.Width%2A> 值不低于 <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A> 值。  
  
-   将所有列的 <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A> 值变大，以便组合值超过控件的宽度。  观察水平滚动条的显示方式。  
  
-   更改某些列的 <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A> 值。  当调整列或窗体的大小时，观察效果。  
  
## 编译代码  
 此示例需要：  
  
-   对 System、System.Drawing 和 System.Windows.Forms 程序集的引用。  
  
 有关从 [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] 或 [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 命令行生成此示例的信息，请参阅[从命令行生成](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) 或[在命令行上使用 csc.exe 生成](../../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)。  还可以通过将代码粘贴到新项目，在 [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] 中生成此示例。  另请参阅[如何：使用 Visual Studio 编译和运行完整的 Windows 窗体代码示例](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\))。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridView.AutoResizeColumns%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewAutoSizeColumnsMode>   
 <xref:System.Windows.Forms.DataGridViewColumn>   
 <xref:System.Windows.Forms.DataGridViewColumn.InheritedAutoSizeMode%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode>   
 <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewColumn.Width%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewColumn.Resizable%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.Control.RightToLeft%2A?displayProperty=fullName>   
 [调整 Windows 窗体 DataGridView 控件中列和行的大小](../../../../docs/framework/winforms/controls/resizing-columns-and-rows-in-the-windows-forms-datagridview-control.md)