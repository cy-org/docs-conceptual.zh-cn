---
title: "GridView 概述 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "控件, ListView"
  - "GridView 视图模式"
  - "ListView 控件, GridView 视图模式"
ms.assetid: b2d02267-32b3-40ce-8e9f-06972d8749d9
caps.latest.revision: 26
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 25
---
# GridView 概述
<xref:System.Windows.Controls.GridView> 视图模式是 <xref:System.Windows.Controls.ListView> 控件的视图模式之一。  使用 <xref:System.Windows.Controls.GridView> 类及其支持类，您以及您的用户可以查看以表的形式呈现的项集合，该表通常使用按钮作为交互式列标题。  本主题介绍 <xref:System.Windows.Controls.GridView> 类并概述它的使用。  
  
   
  
<a name="DefiningaListViewthatusesGridViewView"></a>   
## 什么是 GridView 视图？  
 <xref:System.Windows.Controls.GridView> 视图模式通过将数据字段绑定到列以及显示用于标识字段的列标题来显示数据项列表。  默认 <xref:System.Windows.Controls.GridView> 样式将按钮作为列标题实现。  通过对列标题使用按钮，可以实现重要的用户交互功能；例如，用户可以单击列标题来根据特定列的内容对 <xref:System.Windows.Controls.GridView> 数据进行排序。  
  
> [!NOTE]
>  <xref:System.Windows.Controls.GridView> 用于列标题的按钮控件是从 <xref:System.Windows.Controls.Primitives.ButtonBase> 派生的。  
  
 下图显示了 <xref:System.Windows.Controls.ListView> 内容的 <xref:System.Windows.Controls.GridView> 视图。  
  
 **ListView 内容的 GridView 视图**  
  
 ![带样式的 ListView](../../../../docs/framework/wpf/controls/media/styledlistview.png "StyledListView")  
  
 <xref:System.Windows.Controls.GridView> 列由 <xref:System.Windows.Controls.GridViewColumn> 对象表示，此类对象可以自动根据其内容来调整大小。  您也可以选择显式地将 <xref:System.Windows.Controls.GridViewColumn> 设置为一个特定宽度。  您可以通过拖动列标题之间的手柄来调整列的大小。  您还可以动态地添加、移除、替换列以及对列重新排序，因为此功能内置于 <xref:System.Windows.Controls.GridView> 中。  但是，<xref:System.Windows.Controls.GridView> 无法直接更新它显示的数据。  
  
 下面的示例演示如何定义显示员工数据的 <xref:System.Windows.Controls.GridView>。  在此示例中，<xref:System.Windows.Controls.ListView> 将 `EmployeeInfoDataSource` 定义为 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A>。  <xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A> 的属性定义将 <xref:System.Windows.Controls.GridViewColumn> 内容绑定到 `EmployeeInfoDataSource` 数据类别。  
  
 [!code-xml[ListViewCode#ListViewEmployee](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ListViewCode/CSharp/Window1.xaml#listviewemployee)]  
  
 下图显示了上一示例创建的表。  
  
 **显示 ItemsSource 中的数据的 GridView**  
  
 ![具有 GridView 输出的 ListView](../../../../docs/framework/wpf/controls/media/listviewgridview.png "ListViewGridView")  
  
<a name="GridViewLayoutandStyle"></a>   
## GridView 布局和样式  
 <xref:System.Windows.Controls.GridViewColumn> 的列单元格和列标题具有相同的宽度。  默认情况下，每一列都根据其内容来调整宽度。  您也可以选择将列设置为固定宽度。  
  
 相关的数据内容显示在水平行中。  例如，在上图中，每个员工的姓、名和 ID 号显示为一组，因为它们显示在一个水平行中。  
  
<a name="DefiningandStylingColumnsinaGridView"></a>   
### 在 GridView 中定义列以及设置列的样式  
 当定义要显示在 <xref:System.Windows.Controls.GridViewColumn> 中的数据字段时，应使用 <xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A>、<xref:System.Windows.Controls.GridViewColumn.CellTemplate%2A> 或 <xref:System.Windows.Controls.GridViewColumn.CellTemplateSelector%2A> 属性。  <xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A> 属性优先于任何一个模板属性。  
  
 若要指定 <xref:System.Windows.Controls.GridView> 的列中内容的对齐方式，请定义 <xref:System.Windows.Controls.GridViewColumn.CellTemplate%2A>。  不要为通过使用 <xref:System.Windows.Controls.GridView> 显示的 <xref:System.Windows.Controls.ListView> 内容使用 <xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A> 和 <xref:System.Windows.Controls.Control.VerticalContentAlignment%2A> 属性。  
  
 若要为列标题指定模板和样式属性，应使用 <xref:System.Windows.Controls.GridView>、<xref:System.Windows.Controls.GridViewColumn> 和 <xref:System.Windows.Controls.GridViewColumnHeader> 类。  有关更多信息，请参见 [GridView 列标题的样式和模板概述](../../../../docs/framework/wpf/controls/gridview-column-header-styles-and-templates-overview.md)。  
  
<a name="AddingVisualElementstoaGridViewView"></a>   
### 向 GridView 中添加可视元素  
 要向 <xref:System.Windows.Controls.GridView> 视图模式中添加可视元素（如 <xref:System.Windows.Controls.CheckBox> 和 <xref:System.Windows.Controls.Button> 控件），应使用模板或样式。  
  
 如果您显式地将一个可视元素定义为一个数据项，则它只能在 <xref:System.Windows.Controls.GridView> 中出现一次。  之所以存在此限制，是因为元素只能有一个父级，因此，只能在[可视化树](GTMT)中出现一次。  
  
<a name="StylingRowsinaGridViewView"></a>   
### 设置 GridView 中的行的样式  
 使用 <xref:System.Windows.Controls.GridViewRowPresenter> 和 <xref:System.Windows.Controls.GridViewHeaderRowPresenter> 类可以设置 <xref:System.Windows.Controls.GridView> 的行的格式并显示这些行。  有关演示如何设置 <xref:System.Windows.Controls.GridView> 视图模式中行的样式的示例，请参见[为实现 GridView 的 ListView 中的行设置样式](../../../../docs/framework/wpf/controls/how-to-style-a-row-in-a-listview-that-implements-a-gridview.md)。  
  
<a name="AlignmentIssuesWhenUsingItemContainerStyle"></a>   
### 使用 ItemContainerStyle 时的对齐问题  
 为了防止列标题与单元格之间的对齐问题，请不要在 <xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A> 中设置影响某一项的宽度的属性或者指定这样的模板。  例如，不要设置 <xref:System.Windows.FrameworkElement.Margin%2A> 属性，或者指定将 <xref:System.Windows.Controls.CheckBox> 添加到在 <xref:System.Windows.Controls.ListView> 控件上定义的 <xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A> 的 <xref:System.Windows.Controls.ControlTemplate>。  而是应直接在定义 <xref:System.Windows.Controls.GridView> 视图模式的类上指定影响列宽的属性和模板。  
  
 例如，若要向 <xref:System.Windows.Controls.GridView> 视图模式中的行添加 <xref:System.Windows.Controls.CheckBox>，应将 <xref:System.Windows.Controls.CheckBox> 添加到一个 <xref:System.Windows.DataTemplate> 中，然后将 <xref:System.Windows.Controls.GridViewColumn.CellTemplate%2A> 属性设置为该 <xref:System.Windows.DataTemplate>。  
  
<a name="InteractingwithaGridViewControl"></a>   
## 与 GridView 的用户交互  
 当您在应用程序中使用 <xref:System.Windows.Controls.GridView> 时，用户可以与 <xref:System.Windows.Controls.GridView> 交互并修改它的格式。  例如，用户可以对列重新排序、调整列的大小、选择表中的项以及滚动查看内容。  您还可以定义当用户单击列标题按钮时进行响应的事件处理程序。  事件处理程序可以执行一些操作，例如，根据一列的内容对 <xref:System.Windows.Controls.GridView> 中显示的数据进行排序。  
  
 下表更详细地讨论了使用 <xref:System.Windows.Controls.GridView> 来进行用户交互的能力：  
  
-   **使用拖放方法对列重新排序。**  
  
     用户可以通过在列标题上按鼠标左键，然后将该列拖动到新的位置，来对 <xref:System.Windows.Controls.GridView> 中的列重新排序。  当用户拖动列标题时，会显示标题的浮动版本，以及显示列的插入位置的黑色实线。  
  
     如果您希望修改标题的浮动版本的默认样式，请为 <xref:System.Windows.Controls.GridViewColumnHeader> 类型指定一个 <xref:System.Windows.Controls.ControlTemplate>，当 <xref:System.Windows.Controls.GridViewColumnHeader.Role%2A> 属性设置为 <xref:System.Windows.Controls.GridViewColumnHeaderRole> 时会触发该类型。  有关更多信息，请参见[为拖动的 GridView 列标题创建样式](../../../../docs/framework/wpf/controls/how-to-create-a-style-for-a-dragged-gridview-column-header.md)。  
  
-   **调整列的大小使之适合其内容。**  
  
     用户可以双击列标题右侧的手柄来调整列的大小使之适合其内容。  
  
    > [!NOTE]
    >  将 <xref:System.Windows.Controls.GridViewColumn.Width%2A> 属性设置为 `Double.NaN` 可以产生同样的效果。  
  
-   **选择行项。**  
  
     用户可以选择 <xref:System.Windows.Controls.GridView> 中的一个或多个项。  
  
     如果您要更改选定项的 <xref:System.Windows.Style>，请参见[使用触发器为 ListView 中的选定项设置样式](../../../../docs/framework/wpf/controls/how-to-use-triggers-to-style-selected-items-in-a-listview.md)。  
  
-   **滚动查看最初未显示在屏幕上的内容。**  
  
     如果 <xref:System.Windows.Controls.GridView> 的大小不足以显示所有项，则用户可以使用滚动条来水平或垂直滚动查看，滚动条由 <xref:System.Windows.Controls.ScrollViewer> 控件提供。  如果内容在某个特定方向是全部可见的，则 <xref:System.Windows.Controls.Primitives.ScrollBar> 隐藏。  列标题不会随着垂直滚动条滚动，但可以水平滚动。  
  
-   **通过单击列标题按钮与列交互。**  
  
     如果您提供了排序算法，则当用户单击列标题按钮时，可以对列中显示的数据进行排序。  
  
     您可以处理列标题按钮的 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件，来提供诸如排序算法这样的功能。  若要处理单个列标题的 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件，应在 <xref:System.Windows.Controls.GridViewColumnHeader> 上设置事件处理程序。  若要设置处理所有列标题的 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件的事件处理程序，应在 <xref:System.Windows.Controls.ListView> 控件上设置处理程序。  
  
<a name="Obtaining_Other_Custom_Views"></a>   
## 获取其他自定义视图  
 从 <xref:System.Windows.Controls.ViewBase> 抽象类派生的 <xref:System.Windows.Controls.GridView> 类仅仅是 <xref:System.Windows.Controls.ListView> 类的可能视图模式中的一个。  您可以通过从 <xref:System.Windows.Controls.ViewBase> 类派生来为 <xref:System.Windows.Controls.ListView> 创建其他自定义视图。  有关自定义视图模式的示例，请参见[为 ListView 创建自定义视图模式](../../../../docs/framework/wpf/controls/how-to-create-a-custom-view-mode-for-a-listview.md)。  
  
<a name="GridViewSupportingClasses"></a>   
## GridView 支持类  
 下面的类支持 <xref:System.Windows.Controls.GridView> 视图模式。  
  
-   <xref:System.Windows.Controls.GridViewColumn>  
  
-   <xref:System.Windows.Controls.GridViewColumnHeader>  
  
-   <xref:System.Windows.Controls.GridViewRowPresenter>  
  
-   <xref:System.Windows.Controls.GridViewHeaderRowPresenter>  
  
-   <xref:System.Windows.Controls.GridViewColumnCollection>  
  
-   <xref:System.Windows.Controls.GridViewColumnHeaderRole>  
  
## 请参阅  
 <xref:System.Windows.Controls.ListView>   
 <xref:System.Windows.Controls.ListViewItem>   
 <xref:System.Windows.Controls.GridViewColumn>   
 <xref:System.Windows.Controls.GridViewColumnHeader>   
 <xref:System.Windows.Controls.GridViewRowPresenter>   
 <xref:System.Windows.Controls.GridViewHeaderRowPresenter>   
 <xref:System.Windows.Controls.ViewBase>   
 [ListView 概述](../../../../docs/framework/wpf/controls/listview-overview.md)   
 [在单击标题时对 GridView 列进行排序](../../../../docs/framework/wpf/controls/how-to-sort-a-gridview-column-when-a-header-is-clicked.md)   
 [帮助主题](../../../../docs/framework/wpf/controls/listview-how-to-topics.md)