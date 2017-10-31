---
title: "Windows 窗体 DataGridView 控件中的数据格式设置 | Microsoft Docs"
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
  - "数据 [Windows 窗体], 网格中的格式设置"
  - "数据网格, 格式化数据"
  - "DataGridView 控件 [Windows 窗体], 格式化数据"
ms.assetid: 07bf558d-3748-42ba-8ba0-37fdef924081
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Windows 窗体 DataGridView 控件中的数据格式设置
<xref:System.Windows.Forms.DataGridView> 控件提供了单元格值与父列所显示的数据类型之间的自动转换。  例如，文本框列显示表示日期、时间、数字和枚举值的字符串，并将用户输入的字符串值转换为数据存储区所需的类型。  
  
## 使用 DataGridViewCellStyle 类设置格式  
 <xref:System.Windows.Forms.DataGridView> 控件通过 <xref:System.Windows.Forms.DataGridViewCellStyle> 类提供了单元格值的基本数据格式设置。  可以使用 <xref:System.Windows.Forms.DataGridViewCellStyle.Format%2A> 属性通过 [格式化类型](../../../../docs/standard/base-types/formatting-types.md) 中所描述的格式说明符针对当前默认区域性设置日期、时间、数字和枚举值。  还可以使用 <xref:System.Windows.Forms.DataGridViewCellStyle.FormatProvider%2A> 属性针对特定区域性设置这些值的格式。  所指定的格式既用来显示数据，又用来分析用户以指定格式输入的数据。  
  
 <xref:System.Windows.Forms.DataGridViewCellStyle> 类为换行、文本对齐和数据库空值的自定义显示提供了附加格式设置属性。  有关更多信息，请参见 [如何：设置 Windows 窗体 DataGridView 控件中的数据格式](../../../../docs/framework/winforms/controls/how-to-format-data-in-the-windows-forms-datagridview-control.md)。  
  
## 使用 CellFormatting 事件设置格式  
 如果基本格式设置不能满足您的需要，可以在 <xref:System.Windows.Forms.DataGridView.CellFormatting?displayProperty=fullName> 事件的处理程序中提供自定义数据格式设置。  传递给该处理程序的 <xref:System.Windows.Forms.DataGridViewCellFormattingEventArgs> 有一个 <xref:System.Windows.Forms.ConvertEventArgs.Value%2A> 属性，其中最初包含单元格的值。  通常，此值被自动转换成显示类型。  若要自行转换该值，请将 <xref:System.Windows.Forms.ConvertEventArgs.Value%2A> 属性设置为显示类型的值。  
  
> [!NOTE]
>  如果格式字符串对该单元格有效，则它将重写您对 <xref:System.Windows.Forms.ConvertEventArgs.Value%2A> 属性值的更新，除非将 <xref:System.Windows.Forms.DataGridViewCellFormattingEventArgs.FormattingApplied%2A> 属性设置为 `true`。  
  
 如果要根据各单元格的值为它们设置 <xref:System.Windows.Forms.DataGridViewCellStyle> 属性，则 <xref:System.Windows.Forms.DataGridView.CellFormatting> 事件也很有用。  有关更多信息，请参见[如何：自定义 Windows 窗体 DataGridView 控件中的数据格式设置](../../../../docs/framework/winforms/controls/how-to-customize-data-formatting-in-the-windows-forms-datagridview-control.md)。  
  
 如果对用户指定的值的默认分析不能满足需要，可以处理 <xref:System.Windows.Forms.DataGridView> 控件的 <xref:System.Windows.Forms.DataGridView.CellParsing> 事件来提供自定义分析。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridViewCellStyle>   
 [在 Windows 窗体 DataGridView 控件中显示数据](../../../../docs/framework/winforms/controls/displaying-data-in-the-windows-forms-datagridview-control.md)   
 [Windows 窗体 DataGridView 控件中的单元格样式](../../../../docs/framework/winforms/controls/cell-styles-in-the-windows-forms-datagridview-control.md)   
 [如何：设置 Windows 窗体 DataGridView 控件中的数据格式](../../../../docs/framework/winforms/controls/how-to-format-data-in-the-windows-forms-datagridview-control.md)   
 [如何：自定义 Windows 窗体 DataGridView 控件中的数据格式设置](../../../../docs/framework/winforms/controls/how-to-customize-data-formatting-in-the-windows-forms-datagridview-control.md)