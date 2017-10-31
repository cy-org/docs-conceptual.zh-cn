---
title: "具有内置所有者描述支持的控件 | Microsoft Docs"
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
  - "绘图，所有者"
  - "绘制自定义"
  - "更改外观的控件 [Windows 窗体]"
  - "自定义绘制"
  - "所有者描述"
ms.assetid: 3823d01e-9610-43e6-864d-99f9b7c2b351
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 具有内置所有者描述支持的控件
所有者描述在 Windows 窗体，这是也称为自定义绘图，是一种更改某些控件的可视外观的技术。  
  
> [!NOTE]
>  本主题中的"控件"一词用于表示从派生的类<xref:System.Windows.Forms.Control>或<xref:System.ComponentModel.Component>。  
  
 通常情况下，Windows 绘制自动处理通过使用属性设置，例如<xref:System.Windows.Forms.Control.BackColor%2A>来确定控件的外观。 使用所有者描述，您可以接管绘制过程，更改通过使用属性不可用的元素的外观。 例如，许多控件都允许您设置将显示的文本的颜色，但仅限于一种颜色。 所有者描述可以执行某些操作，如在黑色和中红色部分中显示文本的一部分。  
  
 在实践中，所有者描述相当于窗体上绘制图形。 例如，你可以使用图形方法的处理中窗体的<xref:System.Windows.Forms.Control.Paint>事件，以模拟`ListBox`控件，但你必须编写您自己的代码以处理所有用户交互。 使用所有者描述，该控件使用您的代码来绘制其内容，但仍保留其内部的所有功能。 可以使用图形方法来绘制控件中的每一项或自定义每个项目的某些方面，而对于每个项的其他方面使用的默认外观。  
  
## <a name="owner-drawing-in-windows-forms-controls"></a>所有者描述在 Windows 窗体控件  
 若要执行所有者描述支持它的控件中，通常将设置一个属性并处理一个或多个事件。  
  
 大多数控件都具有该支持所有者描述`OwnerDraw`或`DrawMode`属性，它指示控件是否会引发其绘制相关的事件或事件时对该对象本身来绘制。  
  
 没有控件`OwnerDraw`或`DrawMode`属性包含`DataGridView`控件，它提供了图形事件，会自动执行，与`ToolStrip`控件，它使用具有其自己绘制相关的事件的外部呈现类绘制。  
  
 有许多不同类型的绘制事件，但典型的绘制事件是为了绘制控件内的单个项。 事件处理程序接收`EventArgs`对象，它包含有关所绘制项的信息和工具可用于绘制它。 例如，此对象通常包含在其父集合中的项的索引号<xref:System.Drawing.Rectangle>，该值指示项的显示边界，和一个<xref:System.Drawing.Graphics>用于调用绘制方法的对象。 对于某些事件，`EventArgs`对象提供有关可以调用来绘制项的某些方面，默认情况下，例如背景或聚焦框的方法和项的其他信息。  
  
 若要创建包含所有者描述的自定义项的可重用控件，创建派生自支持所有者描述的控件类的新类。 而不是绘制事件进行处理，所有者描述中包含代码，并重写相应`On` *EventName*方法或新的类中的方法。 请确保调用基类`On` *EventName*方法或方法在此情况下，以便可以处理所有者描述事件并提供其他自定义控件的用户。  
  
 Windows 窗体控件支持所有者描述.NET Framework 的所有版本中︰  
  
-   <xref:System.Windows.Forms.ListBox>  
  
-   <xref:System.Windows.Forms.ComboBox>  
  
-   <xref:System.Windows.Forms.MenuItem> (使用<xref:System.Windows.Forms.MainMenu>和<xref:System.Windows.Forms.ContextMenu>)  
  
-   <xref:System.Windows.Forms.TabControl>  
  
 以下控件支持所有者描述仅在[!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)]:  
  
-   <xref:System.Windows.Forms.ToolTip>  
  
-   <xref:System.Windows.Forms.ListView>  
  
-   <xref:System.Windows.Forms.TreeView>  
  
 以下控件支持所有者描述，并在新[!INCLUDE[dnprdnext](../../../../includes/dnprdnext-md.md)]:  
  
-   <xref:System.Windows.Forms.DataGridView>  
  
-   <xref:System.Windows.Forms.ToolStrip>  
  
 以下各节提供有关上述每个控件的其他详细信息。  
  
### <a name="listbox-and-combobox-controls"></a>列表框和组合框控件  
 <xref:System.Windows.Forms.ListBox>和<xref:System.Windows.Forms.ComboBox>控件使您可以绘制控件都在一个大小，或采用不同的大小中的各个项。  
  
> [!NOTE]
>  尽管<xref:System.Windows.Forms.CheckedListBox>派生控件<xref:System.Windows.Forms.ListBox>控件，它不支持所有者描述。  
  
 若要绘制每个项的大小相同，请设置`DrawMode`属性设置为<xref:System.Windows.Forms.DrawMode>并处理`DrawItem`事件。  
  
 若要绘制每个项使用不同的大小，请设置`DrawMode`属性设置为<xref:System.Windows.Forms.DrawMode>和可以同时处理`MeasureItem`和`DrawItem`事件。 `MeasureItem`事件使您可以指示在之前的项的大小`DrawItem`该项发生的事件。  
  
 有关详细信息，包括代码示例，请参阅以下主题︰  
  
-   <xref:System.Windows.Forms.ListBox.DrawMode%2A?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.ListBox.MeasureItem?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.ListBox.DrawItem?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.ComboBox.DrawMode%2A?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.ComboBox.MeasureItem?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.ComboBox.DrawItem?displayProperty=fullName>  
  
-   [如何︰ 在 ComboBox 控件中创建大小可变的文本](../../../../docs/framework/winforms/controls/how-to-create-variable-sized-text-in-a-combobox-control.md)  
  
### <a name="menuitem-component"></a>MenuItem 组件  
 <xref:System.Windows.Forms.MenuItem>组件表示的单个菜单项<xref:System.Windows.Forms.MainMenu>或<xref:System.Windows.Forms.ContextMenu>组件。  
  
 若要绘制<xref:System.Windows.Forms.MenuItem>，请设置其`OwnerDraw`属性设置为`true`并处理其`DrawItem`事件。 若要自定义之前的菜单项大小`DrawItem`事件发生时，处理该项的`MeasureItem`事件。  
  
 有关详细信息，包括代码示例，请参阅以下参考主题︰  
  
-   <xref:System.Windows.Forms.MenuItem.OwnerDraw%2A?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.MenuItem.DrawItem?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.MenuItem.MeasureItem?displayProperty=fullName>  
  
### <a name="tabcontrol-control"></a>TabControl 控件  
 <xref:System.Windows.Forms.TabControl>控件，您可以在控件中绘制单独的选项卡。 所有者描述影响只有选项卡;<xref:System.Windows.Forms.TabPage>内容不会受到影响。  
  
 若要绘制每个选项卡中<xref:System.Windows.Forms.TabControl>，请设置`DrawMode`属性设置为<xref:System.Windows.Forms.TabDrawMode>并处理`DrawItem`事件。 此事件时发生一次每个选项卡仅选项卡控件中可见。  
  
 有关详细信息，包括代码示例，请参阅以下参考主题︰  
  
-   <xref:System.Windows.Forms.TabControl.DrawMode%2A?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.TabControl.DrawItem?displayProperty=fullName>  
  
### <a name="tooltip-component"></a>ToolTip 组件  
 <xref:System.Windows.Forms.ToolTip>组件，您可以绘制整个工具提示显示时。  
  
 若要绘制<xref:System.Windows.Forms.ToolTip>，请设置其`OwnerDraw`属性设置为`true`并处理其`Draw`事件。 若要自定义的大小<xref:System.Windows.Forms.ToolTip>之前`Draw`发生事件时，处理`Popup`事件并设置<xref:System.Windows.Forms.PopupEventArgs.ToolTipSize%2A>事件处理程序中的属性。  
  
 有关详细信息，包括代码示例，请参阅以下参考主题︰  
  
-   <xref:System.Windows.Forms.ToolTip.OwnerDraw%2A?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.ToolTip.Draw?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.ToolTip.Popup?displayProperty=fullName>  
  
### <a name="listview-control"></a>ListView 控件  
 <xref:System.Windows.Forms.ListView>控件，您可以绘制控件中的各个项、 子项和列标题。  
  
 若要启用所有者描述控件中，设置`OwnerDraw`属性设置为`true`。  
  
 若要在控件中绘制每个项，请处理`DrawItem`事件。  
  
 若要绘制控件中的每个子项或列的标头时<xref:System.Windows.Forms.ListView.View%2A>属性设置为<xref:System.Windows.Forms.View>，处理`DrawSubItem`和`DrawColumnHeader`事件。  
  
 有关详细信息，包括代码示例，请参阅以下参考主题︰  
  
-   <xref:System.Windows.Forms.ListView.OwnerDraw%2A?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.ListView.DrawItem?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.ListView.DrawSubItem?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.ListView.DrawColumnHeader?displayProperty=fullName>  
  
### <a name="treeview-control"></a>TreeView 控件  
 <xref:System.Windows.Forms.TreeView>控件，您可以在控件中绘制单独的节点。  
  
 若要绘制只会在每个节点中显示的文本，请设置`DrawMode`属性设置为<xref:System.Windows.Forms.TreeViewDrawMode>并处理`DrawNode`用于绘制文本的事件。  
  
 若要绘制的每个节点的所有元素，将设置`DrawMode`属性设置为<xref:System.Windows.Forms.TreeViewDrawMode>并处理`DrawNode`事件以便都绘制您的需要如文本、 图标、 复选框，加号和减号情况下，并连接节点的线的任何一个元素。  
  
 有关详细信息，包括代码示例，请参阅以下参考主题︰  
  
-   <xref:System.Windows.Forms.TreeView.DrawMode%2A?displayProperty=fullName>  
  
-   <xref:System.Windows.Forms.TreeView.DrawNode?displayProperty=fullName>  
  
### <a name="datagridview-control"></a>DataGridView 控件  
 <xref:System.Windows.Forms.DataGridView>控件，您可以绘制控件中的单个单元格和行。  
  
 若要绘制单个单元格，处理`CellPainting`事件。  
  
 若要绘制单个行的元素，处理一个或两个`RowPrePaint`和`RowPostPaint`事件。 `RowPrePaint`事件发生前绘制行中的单元格，与`RowPostPaint`事件发生后会绘制的单元格。 您可以处理这两个事件和`CellPainting`事件以分别，绘制行背景、 各个单元格和行前景或您可以提供特定的自定义需要它们的行的其他元素使用的默认显示。  
  
 有关详细信息，包括代码示例，请参阅以下主题︰  
  
-   <xref:System.Windows.Forms.DataGridView.CellPainting>  
  
-   <xref:System.Windows.Forms.DataGridView.RowPrePaint>  
  
-   <xref:System.Windows.Forms.DataGridView.RowPostPaint>  
  
-   [如何︰ 自定义 Windows 窗体 DataGridView 控件中的单元格的外观](../../../../docs/framework/winforms/controls/customize-the-appearance-of-cells-in-the-datagrid.md)  
  
-   [如何︰ 自定义 Windows 窗体 DataGridView 控件中行的外观](../../../../docs/framework/winforms/controls/customize-the-appearance-of-rows-in-the-datagrid.md)  
  
### <a name="toolstrip-control"></a>ToolStrip 控件  
 <xref:System.Windows.Forms.ToolStrip>和派生的控件，您可以自定义其外观任何方面。  
  
 若要提供自定义呈现<xref:System.Windows.Forms.ToolStrip>控件中，设置`Renderer`属性<xref:System.Windows.Forms.ToolStrip>， <xref:System.Windows.Forms.ToolStripManager>， <xref:System.Windows.Forms.ToolStripPanel>，或<xref:System.Windows.Forms.ToolStripContentPanel>到`ToolStripRenderer`对象，然后处理一个或多个由提供的许多绘图事件`ToolStripRenderer`类。 或者，设置`Renderer`指向您自己的类的实例的属性派生自`ToolStripRenderer`， <xref:System.Windows.Forms.ToolStripProfessionalRenderer>，或<xref:System.Windows.Forms.ToolStripSystemRenderer> ，实现或重写特定`On` *EventName*方法。  
  
 有关详细信息，包括代码示例，请参阅以下主题︰  
  
-   <xref:System.Windows.Forms.ToolStripRenderer>  
  
-   [如何︰ 创建和设置自定义呈现器 ToolStrip 控件在 Windows 窗体](../../../../docs/framework/winforms/controls/create-and-set-a-custom-renderer-for-the-toolstrip-control-in-wf.md)  
  
-   [如何︰ 自定义绘制 ToolStrip 控件](../../../../docs/framework/winforms/controls/how-to-custom-draw-a-toolstrip-control.md)  
  
## <a name="see-also"></a>另请参阅  
 [Windows 窗体上使用的控件](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)