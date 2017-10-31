---
title: "Windows 窗体 DataGridView 控件中的单元格样式 | Microsoft Docs"
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
  - "单元格, 样式"
  - "数据网格, 单元格样式"
  - "DataGridView 控件 [Windows 窗体], 单元格样式"
ms.assetid: dbb75ed6-8804-4232-8382-f9920c2e380c
caps.latest.revision: 33
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 33
---
# Windows 窗体 DataGridView 控件中的单元格样式
<xref:System.Windows.Forms.DataGridView> 控件内的每个单元格都可以有自己的样式，如文本格式、背景色、前景色和字体。  但是，多个单元格通常会共享特定的样式特征。  
  
 共享样式的单元格组可能包含特定行或列内的所有单元格、包含特定值的所有单元格或控件内的所有单元格。  由于这些单元格组是重叠的，因此，每个单元格都可以从多处获取其样式信息。  例如，您可能希望 <xref:System.Windows.Forms.DataGridView> 控件中的每个单元格都使用相同字体，只有货币列的单元格使用货币格式，并且只有带负数的货币单元格使用红色前景色。  
  
## DataGridViewCellStyle 类  
 <xref:System.Windows.Forms.DataGridViewCellStyle> 类包含与视觉样式相关的下列属性：  
  
-   <xref:System.Windows.Forms.DataGridViewCellStyle.BackColor%2A> 和 <xref:System.Windows.Forms.DataGridViewCellStyle.ForeColor%2A>  
  
-   <xref:System.Windows.Forms.DataGridViewCellStyle.SelectionBackColor%2A> 和 <xref:System.Windows.Forms.DataGridViewCellStyle.SelectionForeColor%2A>  
  
-   <xref:System.Windows.Forms.DataGridViewCellStyle.Font%2A>  
  
 此类还包含与格式设置相关的下列属性：  
  
-   <xref:System.Windows.Forms.DataGridViewCellStyle.Format%2A> 和 <xref:System.Windows.Forms.DataGridViewCellStyle.FormatProvider%2A>  
  
-   <xref:System.Windows.Forms.DataGridViewCellStyle.NullValue%2A> 和 <xref:System.Windows.Forms.DataGridViewCellStyle.DataSourceNullValue%2A>  
  
-   <xref:System.Windows.Forms.DataGridViewCellStyle.WrapMode%2A>  
  
-   <xref:System.Windows.Forms.DataGridViewCellStyle.Alignment%2A>  
  
-   <xref:System.Windows.Forms.DataGridViewCellStyle.Padding%2A>  
  
 有关这些属性和其他单元格样式属性的更多信息，请参见 <xref:System.Windows.Forms.DataGridViewCellStyle> 参考文档和下面“请参见”部分列出的主题。  
  
## 使用 DataGridViewCellStyle 对象  
 可以从 <xref:System.Windows.Forms.DataGridView>、<xref:System.Windows.Forms.DataGridViewColumn>、<xref:System.Windows.Forms.DataGridViewRow> 和 <xref:System.Windows.Forms.DataGridViewCell> 类及其派生类的各个属性中检索 <xref:System.Windows.Forms.DataGridViewCellStyle> 对象。  如果这些属性中有一个尚未设置，则检索该属性的值将新建 <xref:System.Windows.Forms.DataGridViewCellStyle> 对象。  您还可以实例化自己的 <xref:System.Windows.Forms.DataGridViewCellStyle> 对象，并将这些对象分配给以上属性。  
  
 在多个 <xref:System.Windows.Forms.DataGridView> 元素间共享 <xref:System.Windows.Forms.DataGridViewCellStyle> 对象可以避免不必要地重复样式信息。  由于在控件、列和行三个级别设置的样式从每个级别向下筛选直到单元格级别，因此，在每个级别上仅设置与其上面的级别不同的那些样式属性，也可以避免样式重复。  相关内容在后面的“样式继承”部分有更详细的说明。  
  
 下表列出获取或设置 <xref:System.Windows.Forms.DataGridViewCellStyle> 对象的主要属性。  
  
|属性|类|说明|  
|--------|-------|--------|  
|`DefaultCellStyle`|<xref:System.Windows.Forms.DataGridView>、<xref:System.Windows.Forms.DataGridViewColumn>、<xref:System.Windows.Forms.DataGridViewRow> 和派生类|获取或设置整个控件（包括标头单元格）、一列或一行中所有单元格使用的默认样式。|  
|<xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A>|<xref:System.Windows.Forms.DataGridView>|获取或设置控件中所有行使用的默认单元格样式。  不包括标头单元格。|  
|<xref:System.Windows.Forms.DataGridView.AlternatingRowsDefaultCellStyle%2A>|<xref:System.Windows.Forms.DataGridView>|获取或设置控件中交替行使用的默认单元格样式。  用于创建帐目型的效果。|  
|<xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle%2A>|<xref:System.Windows.Forms.DataGridView>|获取或设置控件的行标头使用的默认单元格样式。  如果启用视觉样式，则用当前主题进行重写。|  
|<xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle%2A>|<xref:System.Windows.Forms.DataGridView>|获取或设置控件的列标头使用的默认单元格样式。  如果启用视觉样式，则用当前主题进行重写。|  
|<xref:System.Windows.Forms.DataGridViewCell.Style%2A>|<xref:System.Windows.Forms.DataGridViewCell> 和派生类|获取或设置在单元格级别指定的样式。  这些样式将重写那些从较高级别继承的样式。|  
|`InheritedStyle`|<xref:System.Windows.Forms.DataGridViewCell>、<xref:System.Windows.Forms.DataGridViewRow>、<xref:System.Windows.Forms.DataGridViewColumn> 和派生类|获取当前应用于单元格、行或列的所有样式，包括从较高级别继承的样式。|  
  
 如上所述，如果以前没有设置过样式属性，则获取样式属性值将自动实例化新的 <xref:System.Windows.Forms.DataGridViewCellStyle> 对象。  为了避免不必要地创建这些对象，行类和列类具有 <xref:System.Windows.Forms.DataGridViewBand.HasDefaultCellStyle%2A> 属性，您可以检查该属性以确定是否设置了 <xref:System.Windows.Forms.DataGridViewBand.DefaultCellStyle%2A> 属性。  同样，单元格类具有 <xref:System.Windows.Forms.DataGridViewCell.HasStyle%2A> 属性，该属性指示是否设置了 <xref:System.Windows.Forms.DataGridViewCell.Style%2A> 属性。  
  
 每个样式属性在 <xref:System.Windows.Forms.DataGridView> 控件上都有一个对应的*属性名称*`Changed` 事件。  对于行、列和单元格属性，该事件的名称分别以“`Row`”、“`Column`”或“`Cell`”（例如，<xref:System.Windows.Forms.DataGridView.RowDefaultCellStyleChanged>）开头。  如果将对应的样式属性设置为不同的 <xref:System.Windows.Forms.DataGridViewCellStyle> 对象，则这些事件中的每个事件都会发生；  如果在样式属性中检索 <xref:System.Windows.Forms.DataGridViewCellStyle> 对象并更改其属性值，则这些事件不会发生。  若要响应对单元格样式对象本身的更改，可以对 <xref:System.Windows.Forms.DataGridView.CellStyleContentChanged> 事件进行处理。  
  
## 样式继承  
 每个 <xref:System.Windows.Forms.DataGridViewCell> 从其 <xref:System.Windows.Forms.DataGridViewCell.InheritedStyle%2A> 属性获取外观。  此属性返回的 <xref:System.Windows.Forms.DataGridViewCellStyle> 对象从类型 <xref:System.Windows.Forms.DataGridViewCellStyle> 的属性层次结构继承其属性值。  下面按非标头单元格的 <xref:System.Windows.Forms.DataGridViewCell.InheritedStyle%2A> 获取其值的顺序列出这些属性。  
  
1.  <xref:System.Windows.Forms.DataGridViewCell.Style%2A?displayProperty=fullName>  
  
2.  <xref:System.Windows.Forms.DataGridViewRow.DefaultCellStyle%2A?displayProperty=fullName>  
  
3.  <xref:System.Windows.Forms.DataGridView.AlternatingRowsDefaultCellStyle%2A?displayProperty=fullName>（仅限于索引号为奇数的行中的单元格）  
  
4.  <xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A?displayProperty=fullName>  
  
5.  <xref:System.Windows.Forms.DataGridViewColumn.DefaultCellStyle%2A?displayProperty=fullName>  
  
6.  <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=fullName>  
  
 对于行和列标头单元格，用以下列表中的值填充 <xref:System.Windows.Forms.DataGridViewCell.InheritedStyle%2A> 属性，该列表列出给定顺序的源属性。  
  
1.  <xref:System.Windows.Forms.DataGridViewCell.Style%2A?displayProperty=fullName>  
  
2.  <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle%2A?displayProperty=fullName> 或 <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle%2A?displayProperty=fullName>  
  
3.  <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=fullName>  
  
 下图阐释此过程。  
  
 ![类型 DataGridViewCellStyle 的属性](../../../../docs/framework/winforms/controls/media/datagridviewcells1.png "DataGridViewCells1")  
  
 还可以访问由特定的行和列继承的样式。  列 <xref:System.Windows.Forms.DataGridViewColumn.InheritedStyle%2A> 属性从下列属性继承其属性值。  
  
1.  <xref:System.Windows.Forms.DataGridViewColumn.DefaultCellStyle%2A?displayProperty=fullName>  
  
2.  <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=fullName>  
  
 行 <xref:System.Windows.Forms.DataGridViewRow.InheritedStyle%2A> 属性从下列属性继承其属性值。  
  
1.  <xref:System.Windows.Forms.DataGridViewRow.DefaultCellStyle%2A?displayProperty=fullName>  
  
2.  <xref:System.Windows.Forms.DataGridView.AlternatingRowsDefaultCellStyle%2A?displayProperty=fullName>（仅限于索引号为奇数的行中的单元格）  
  
3.  <xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A?displayProperty=fullName>  
  
4.  <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=fullName>  
  
 对于 `InheritedStyle` 属性返回的 <xref:System.Windows.Forms.DataGridViewCellStyle> 对象中的每个属性，均从相应列表中的第一个单元格样式获得其属性值，该列表中对应的属性被设置为 <xref:System.Windows.Forms.DataGridViewCellStyle> 类默认值以外的值。  
  
 下表阐释如何从包含示例单元格的列继承该单元格的 <xref:System.Windows.Forms.DataGridViewCellStyle.ForeColor%2A> 属性值。  
  
|类型 `DataGridViewCellStyle` 的属性|检索的对象的示例 `ForeColor` 值|  
|------------------------------------|----------------------------|  
|<xref:System.Windows.Forms.DataGridViewCell.Style%2A?displayProperty=fullName>|<xref:System.Drawing.Color.Empty?displayProperty=fullName>|  
|<xref:System.Windows.Forms.DataGridViewRow.DefaultCellStyle%2A?displayProperty=fullName>|<xref:System.Drawing.Color.Red%2A?displayProperty=fullName>|  
|<xref:System.Windows.Forms.DataGridView.AlternatingRowsDefaultCellStyle%2A?displayProperty=fullName>|<xref:System.Drawing.Color.Empty?displayProperty=fullName>|  
|<xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A?displayProperty=fullName>|<xref:System.Drawing.Color.Empty?displayProperty=fullName>|  
|<xref:System.Windows.Forms.DataGridViewColumn.DefaultCellStyle%2A?displayProperty=fullName>|<xref:System.Drawing.Color.DarkBlue%2A?displayProperty=fullName>|  
|<xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=fullName>|<xref:System.Drawing.Color.Black%2A?displayProperty=fullName>|  
  
 此时，单元格所在行的 <xref:System.Drawing.Color.Red%2A?displayProperty=fullName> 值是列表中的第一个实际值。  这个值作为单元格的 <xref:System.Windows.Forms.DataGridViewCell.InheritedStyle%2A> 的 <xref:System.Windows.Forms.DataGridViewCellStyle.ForeColor%2A> 属性值。  
  
 下图阐释不同的 <xref:System.Windows.Forms.DataGridViewCellStyle> 属性如何从不同的地方继承其属性值。  
  
 ![DataGridView 属性&#47;值继承](../../../../docs/framework/winforms/controls/media/datagridviewcells2.png "DataGridViewCells2")  
  
 可以利用样式继承为整个控件提供相应的样式，而不必在多处指定相同的信息。  
  
 如上所述，虽然标头单元格参与了样式继承，但是，<xref:System.Windows.Forms.DataGridView> 控件的 <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle%2A> 和 <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle%2A> 属性返回的对象具有以下的初始属性值，这些属性值将重写 <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A> 属性返回的对象的属性值。  对于 <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A> 属性返回的对象，如果要将为其设置的属性应用于行标头和列标头，则对于 <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle%2A> 和 <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle%2A> 属性返回的对象，必须将其对应的属性设置为为 <xref:System.Windows.Forms.DataGridViewCellStyle> 类指定的默认值。  
  
> [!NOTE]
>  如果启用了视觉样式，则行标头和列标头（<xref:System.Windows.Forms.DataGridView.TopLeftHeaderCell%2A> 除外）的样式将自动由当前主题设置，并重写由这些属性指定的任何样式。  
  
 <xref:System.Windows.Forms.DataGridViewButtonColumn>、<xref:System.Windows.Forms.DataGridViewImageColumn> 和 <xref:System.Windows.Forms.DataGridViewCheckBoxColumn> 类型还对以下对象的某些值进行初始化，该对象由列 <xref:System.Windows.Forms.DataGridViewColumn.DefaultCellStyle%2A> 属性返回。  有关更多信息，请参见这些类型的参考文档。  
  
## 动态设置样式  
 要使用特定值自定义单元格样式，需要实现 <xref:System.Windows.Forms.DataGridView.CellFormatting?displayProperty=fullName> 事件的处理程序。  此事件的处理程序接收 <xref:System.Windows.Forms.DataGridViewCellFormattingEventArgs> 类型的参数。  此对象包含的属性使您可以确定正进行格式设置的单元格的值，以及该值在 <xref:System.Windows.Forms.DataGridView> 控件中的位置。  此对象还包含 <xref:System.Windows.Forms.DataGridViewCellFormattingEventArgs.CellStyle%2A> 属性，该属性被初始化为正进行格式设置的单元格的 <xref:System.Windows.Forms.DataGridViewCell.InheritedStyle%2A> 属性的值。  可以修改单元格样式属性，以指定适合单元格值和位置的样式信息。  
  
> [!NOTE]
>  <xref:System.Windows.Forms.DataGridView.RowPrePaint> 和 <xref:System.Windows.Forms.DataGridView.RowPostPaint> 事件还接收事件数据中的 <xref:System.Windows.Forms.DataGridViewCellStyle> 对象，但在这种情况下，接收的对象是行 <xref:System.Windows.Forms.DataGridViewRow.InheritedStyle%2A> 属性的只读副本，并且对该对象所做的更改不会影响控件。  
  
 您还可以动态修改单个单元格的样式，以响应 <xref:System.Windows.Forms.DataGridView.CellMouseEnter?displayProperty=fullName> 和 <xref:System.Windows.Forms.DataGridView.CellMouseLeave> 等事件。  例如，在 <xref:System.Windows.Forms.DataGridView.CellMouseEnter> 事件的处理程序中，您可以存储单元格背景色的当前值（通过单元格的 <xref:System.Windows.Forms.DataGridViewCell.Style%2A> 属性检索），然后将这个当前值设置为一种新颜色，当鼠标悬停在单元格上时，这种新颜色就会突出显示相应的单元格。  然后，在 <xref:System.Windows.Forms.DataGridView.CellMouseLeave> 事件的处理程序中，您可以再将背景色还原为其原始值。  
  
> [!NOTE]
>  无论是否设置了特定的样式值，对单元格的 <xref:System.Windows.Forms.DataGridViewCell.Style%2A> 属性中存储的值进行缓存都很重要。  如果您临时替换了某个样式设置，则将该设置还原为其原始的“未设置”状态可以确保单元格追溯到较高的级别以继承样式设置。  如果需要确定单元格的实际样式（无论该样式是否是继承的），则使用单元格的 <xref:System.Windows.Forms.DataGridViewCell.InheritedStyle%2A> 属性。  
  
## 请参阅  
 <xref:System.Windows.Forms.DataGridView>   
 <xref:System.Windows.Forms.DataGridViewCellStyle>   
 <xref:System.Windows.Forms.DataGridView.AlternatingRowsDefaultCellStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.ColumnHeadersDefaultCellStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.DefaultCellStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.RowHeadersDefaultCellStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.RowsDefaultCellStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewBand.InheritedStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewRow.InheritedStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewColumn.InheritedStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewBand.DefaultCellStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewCell.InheritedStyle%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridViewCell.Style%2A?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.CellFormatting?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.CellStyleContentChanged?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.RowPrePaint?displayProperty=fullName>   
 <xref:System.Windows.Forms.DataGridView.RowPostPaint?displayProperty=fullName>   
 [Windows 窗体 DataGridView 控件中的基本格式设置和样式设置](../../../../docs/framework/winforms/controls/basic-formatting-and-styling-in-the-windows-forms-datagridview-control.md)   
 [如何：设置 Windows 窗体 DataGridView 控件的默认单元格样式](../../../../docs/framework/winforms/controls/how-to-set-default-cell-styles-for-the-windows-forms-datagridview-control.md)   
 [Windows 窗体 DataGridView 控件中的数据格式设置](../../../../docs/framework/winforms/controls/data-formatting-in-the-windows-forms-datagridview-control.md)