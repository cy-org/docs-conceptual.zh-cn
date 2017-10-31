---
title: "演练：使用 TableLayoutPanel 在 Windows 窗体上排列控件 | Microsoft Docs"
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
  - "控件 [Windows 窗体], 使用 TableLayoutPanel 排列"
  - "TableLayoutPanel 控件 [Windows 窗体], 演练"
  - "Windows 窗体控件, 排列"
ms.assetid: d474885e-12cc-4ab7-b997-2a23a643049b
caps.latest.revision: 28
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 28
---
# 演练：使用 TableLayoutPanel 在 Windows 窗体上排列控件
某些应用程序要求窗体布局在窗体调整大小或其内容大小更改时能够对窗体自身进行适当地排列。  当您需要进行动态布局，但并不希望在代码中显式处理 <xref:System.Windows.Forms.Control.Layout> 事件时，可以考虑使用布局面板。  
  
 <xref:System.Windows.Forms.FlowLayoutPanel> 控件和 <xref:System.Windows.Forms.TableLayoutPanel> 控件为在窗体上排列控件提供了两种直观的方式。  这两个控件为其中包含的子控件的相对位置提供了自动的、可配置的控制功能，并且都能在运行时提供动态布局特性，因此，在父窗体的尺寸更改时，它们能够调整子控件的大小和位置。  可在布局面板内嵌套布局面板，从而实现复杂的用户界面。  
  
 <xref:System.Windows.Forms.FlowLayoutPanel> 按特定流方向（水平或垂直）来排列其内容。  其内容可从一行换到下一行，或者从一列换到下一列。  另一种情况是不换行，而是将其内容截掉。  有关更多信息，请参见 [演练：使用 FlowLayoutPanel 在 Windows 窗体上排列控件](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-flowlayoutpanel.md)。  
  
 <xref:System.Windows.Forms.TableLayoutPanel> 在网格中排列其内容，提供了类似 HTML 中 \<table\> 元素的功能。  <xref:System.Windows.Forms.TableLayoutPanel> 控件允许您将控件放置于网格布局中，而无需精确指定每个单独控件的位置。  其单元格按行和列的方式排列，各行各列的尺寸可以不同。  单元格可以跨行跨列合并。  单元格可以包含窗体所能包含的任何内容，并且其行为在大多数其他方面与容器类似。  
  
 <xref:System.Windows.Forms.TableLayoutPanel> 控件还提供在运行时按比例调整大小的功能，因此窗体调整大小时，布局可以平滑地相应发生更改。  这使得 <xref:System.Windows.Forms.TableLayoutPanel> 控件非常适合用于数据输入窗体和本地化的应用程序等目的。  有关更多信息，请参见[Walkthrough: Creating a Resizable Windows Form for Data Entry](http://msdn.microsoft.com/zh-cn/e193b4fc-912a-4917-b036-b76c7a6f58ab)和[Walkthrough: Creating a Localizable Windows Form](http://msdn.microsoft.com/zh-cn/c5240b6e-aaca-4286-9bae-778a416edb9c)。  
  
 一般而言，不应将 <xref:System.Windows.Forms.TableLayoutPanel> 控件用作整体布局的容器。  而是使用 <xref:System.Windows.Forms.TableLayoutPanel> 控件为布局的各部分提供按比例调整大小的功能。  
  
 本演练涉及以下任务：  
  
-   创建 Windows 窗体项目  
  
-   按行和列排列控件  
  
-   设置行属性和列属性  
  
-   控件跨行和跨列  
  
-   自动处理溢出  
  
-   通过在工具箱中双击控件来插入控件  
  
-   通过绘制控件轮廓来插入控件  
  
-   将现有控件重新分配给不同的父控件  
  
 完成本演练后，您将对这些重要的布局功能所扮演的角色有所了解。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
## 创建项目  
 第一步是创建项目并设置窗体。  
  
#### 创建项目  
  
1.  创建名为“TableLayoutPanelExample”的 Windows 应用程序项目。  有关更多信息，请参见[How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)。  
  
2.  在**“Windows 窗体设计器”**中选择窗体。  
  
## 按行和列排列控件  
 <xref:System.Windows.Forms.TableLayoutPanel> 控件允许您轻松地按行和列来排列控件。  
  
#### 使用 TableLayoutPanel 按行和列来排列控件  
  
1.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.TableLayoutPanel> 控件拖到窗体上。  注意，在默认情况下，<xref:System.Windows.Forms.TableLayoutPanel> 控件有四个单元格。  
  
2.  将 <xref:System.Windows.Forms.Button> 控件从**“工具箱”**拖到 <xref:System.Windows.Forms.TableLayoutPanel> 控件的其中一个单元格中。  注意，将在选定的单元格中创建 <xref:System.Windows.Forms.Button> 控件。  
  
3.  再将三个 <xref:System.Windows.Forms.Button> 控件从**“工具箱”**拖到 <xref:System.Windows.Forms.TableLayoutPanel> 控件中，这样，每个单元格中都包含一个按钮。  
  
4.  抓住两列之间的垂直尺寸调整手柄，并向左移动。  注意，第一列中的 <xref:System.Windows.Forms.Button> 控件的大小将调整为较小的宽度，而第二列中的 <xref:System.Windows.Forms.Button> 控件的大小将保持不变。  
  
5.  抓住两列之间的垂直尺寸调整手柄，并向右移动。  注意，第一列中的 <xref:System.Windows.Forms.Button> 控件将恢复原始大小，而第二列中的 <xref:System.Windows.Forms.Button> 控件将向右移动。  
  
6.  上下移动水平尺寸柄以查看它对面板中的控件的影响。  
  
## 使用停靠和锚定在单元格内定位控件  
 <xref:System.Windows.Forms.TableLayoutPanel> 中子控件的锚定行为与其他容器控件中的行为不同。  子控件的停靠行为则与其他容器控件的相同。  
  
#### 在单元格内定位控件  
  
1.  选择第一个 <xref:System.Windows.Forms.Button> 控件。  将其 <xref:System.Windows.Forms.Control.Dock%2A> 属性的值更改为 <xref:System.Windows.Forms.DockStyle>。  注意，<xref:System.Windows.Forms.Button> 控件将扩展以填充单元格。  
  
2.  请选择其他 <xref:System.Windows.Forms.Button> 控件之一。  将其 <xref:System.Windows.Forms.Control.Anchor%2A> 属性的值更改为 <xref:System.Windows.Forms.AnchorStyles>。  注意，它就会被移动，使其右边框靠近单元格的右边框。  边框之间的间距是 <xref:System.Windows.Forms.Button> 控件的 <xref:System.Windows.Forms.Control.Margin%2A> 属性和面板的 <xref:System.Windows.Forms.Control.Padding%2A> 属性之和。  
  
3.  将 <xref:System.Windows.Forms.Button> 控件的 <xref:System.Windows.Forms.Control.Anchor%2A> 属性的值更改为 <xref:System.Windows.Forms.AnchorStyles> 和 <xref:System.Windows.Forms.AnchorStyles>。  注意，控件的大小会调整为单元格的宽度，并会考虑 <xref:System.Windows.Forms.Control.Margin%2A> 和 <xref:System.Windows.Forms.Control.Padding%2A> 值。  
  
4.  对 <xref:System.Windows.Forms.AnchorStyles> 和 <xref:System.Windows.Forms.AnchorStyles> 样式重复第 2 步和第 3 步。  
  
## 设置行属性和列属性  
 可以使用 <xref:System.Windows.Forms.TableLayoutPanel.RowStyles%2A> 和 <xref:System.Windows.Forms.TableLayoutPanel.ColumnStyles%2A> 集合分别设置行属性和列属性。  
  
#### 设置行属性和列属性  
  
1.  在**“Windows 窗体设计器”**中选择 <xref:System.Windows.Forms.TableLayoutPanel> 控件。  
  
2.  在**“属性”**窗口，通过单击**“列”**项旁边的省略号 \(![VisualStudioEllipsesButton 屏幕快照](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) 按钮，打开 <xref:System.Windows.Forms.TableLayoutPanel.ColumnStyles%2A> 集合。  
  
3.  选择第一列并将其 <xref:System.Windows.Forms.TableLayoutStyle.SizeType%2A> 属性的值更改为 <xref:System.Windows.Forms.SizeType>。  单击**“确定”**接受更改。  注意，第一列的宽度会缩小，以适合 <xref:System.Windows.Forms.Button> 控件。  另外请注意，该列的宽度的不是大小可调的。  
  
4.  在**“属性”**窗口中打开 <xref:System.Windows.Forms.TableLayoutPanel.ColumnStyles%2A> 集合并选择第一列。  将其 <xref:System.Windows.Forms.TableLayoutStyle.SizeType%2A> 属性的值更改为 <xref:System.Windows.Forms.SizeType>。  单击**“确定”**接受更改。  将 <xref:System.Windows.Forms.TableLayoutPanel> 控件的大小调整为较大的宽度。注意，第一列的宽度将扩展。  将 <xref:System.Windows.Forms.TableLayoutPanel> 控件的大小调整为较小的宽度。注意，第一列中的按钮将调整大小，以适合单元格。  另外请注意，该列的宽度是大小可调的。  
  
5.  在**“属性”**窗口中打开 <xref:System.Windows.Forms.TableLayoutPanel.ColumnStyles%2A> 集合并选择列出的所有列。  将每个 <xref:System.Windows.Forms.TableLayoutStyle.SizeType%2A> 属性的值设置为 <xref:System.Windows.Forms.SizeType>。  单击**“确定”**接受更改。  对 <xref:System.Windows.Forms.TableLayoutPanel.RowStyles%2A> 集合重复上一过程。  
  
6.  抓住角大小调整手柄之一，调整 <xref:System.Windows.Forms.TableLayoutPanel> 控件的宽度和高度的大小。  注意，当 <xref:System.Windows.Forms.TableLayoutPanel> 控件的大小更改时，行和列的大小也会调整。  另外请注意，行和列的大小可以通过水平和垂直大小调整手柄进行调整。  
  
## 控件跨行和跨列  
 <xref:System.Windows.Forms.TableLayoutPanel> 控件在设计时为控件添加了几个新属性。  其中两个属性就是 `RowSpan` 和 `ColumnSpan`。  可以使用这些属性使控件跨多个行或多个列。  
  
#### 控件跨行和跨列  
  
1.  选择第一行第一列中的 <xref:System.Windows.Forms.Button> 控件。  
  
2.  在**“属性”**窗口中将 `ColumnSpan` 属性的值更改为 2。  注意，<xref:System.Windows.Forms.Button> 控件填充第一列和第二列。  还请注意，已为适应此更改额外添加了一行。  
  
3.  对 `RowSpan` 属性重复第 2 步。  
  
## 通过在工具箱中双击控件来插入控件  
 可通过在**“工具箱”**中双击控件来填充 <xref:System.Windows.Forms.TableLayoutPanel> 控件。  
  
#### 通过在工具箱中双击来插入控件  
  
1.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.TableLayoutPanel> 控件拖到窗体上。  
  
2.  双击**“工具箱”**中的 <xref:System.Windows.Forms.Button> 控件图标。  请注意，一个新的按钮控件会出现在 <xref:System.Windows.Forms.TableLayoutPanel> 控件的第一个单元格中。  
  
3.  在**“工具箱”**中双击更多控件。  注意，在 <xref:System.Windows.Forms.TableLayoutPanel> 控件的未填充单元格中将连续出现几个新控件。  另外请注意，如果没有空的单元格可用，<xref:System.Windows.Forms.TableLayoutPanel> 控件将扩展以容纳新的控件。  
  
## 自动处理溢出  
 在向 <xref:System.Windows.Forms.TableLayoutPanel> 控件中插入控件时，可能会用完空的单元格，而无法插入新的控件。  <xref:System.Windows.Forms.TableLayoutPanel> 控件会通过增加单元格数目来自动处理这种情况。  
  
#### 观察溢出的自动处理  
  
1.  如果 <xref:System.Windows.Forms.TableLayoutPanel> 控件中还有空的单元格，请继续插入新的 <xref:System.Windows.Forms.Button> 控件，直至填满 <xref:System.Windows.Forms.TableLayoutPanel> 控件。  
  
2.  填满 <xref:System.Windows.Forms.TableLayoutPanel> 控件以后，在**“工具箱”**中双击 <xref:System.Windows.Forms.Button> 图标，插入另一个 <xref:System.Windows.Forms.Button> 控件。  注意，<xref:System.Windows.Forms.TableLayoutPanel> 控件将创建新的单元格以容纳新的控件。  再插入几个控件并观察调整大小的行为。  
  
3.  将 <xref:System.Windows.Forms.TableLayoutPanel> 控件的 <xref:System.Windows.Forms.TableLayoutPanel.GrowStyle%2A> 属性的值更改为 <xref:System.Windows.Forms.TableLayoutPanelGrowStyle>。  在**“工具箱”**中双击 <xref:System.Windows.Forms.Button> 图标，插入 <xref:System.Windows.Forms.Button> 控件，直至填满 <xref:System.Windows.Forms.TableLayoutPanel> 控件。  在**“工具箱”**上再次双击 <xref:System.Windows.Forms.Button> 图标。  注意，您将从**“Windows 窗体设计器”**收到一条错误信息，通知您无法创建附加的行和列。  
  
## 通过绘制控件轮廓来插入控件  
 可以通过在单元格中绘制控件轮廓来在 <xref:System.Windows.Forms.TableLayoutPanel> 控件中插入一个控件，并指定其大小。  
  
#### 通过绘制控件轮廓来插入控件  
  
1.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.TableLayoutPanel> 控件拖到窗体上。  
  
2.  在**“工具箱”**中单击 <xref:System.Windows.Forms.Button> 控件图标。  不要将其拖到窗体上。  
  
3.  将鼠标指针移到 <xref:System.Windows.Forms.TableLayoutPanel> 控件上方。  请留意附加了 <xref:System.Windows.Forms.Button> 控件图标的鼠标会变为十字线。  
  
4.  单击并按住鼠标按钮。  
  
5.  拖动鼠标指针绘制 <xref:System.Windows.Forms.Button> 控件的轮廓。  对大小感到满意后松开鼠标按钮。  注意，在您绘制控件轮廓的单元格内将创建一个 <xref:System.Windows.Forms.Button> 控件。  
  
## 单元格内不允许有多个控件  
 <xref:System.Windows.Forms.TableLayoutPanel> 控件在每个单元格中只能包含一个子控件。  
  
#### 演示在单元格内不允许有多个控件  
  
-   将 <xref:System.Windows.Forms.Button> 控件从**“工具箱”**拖到 <xref:System.Windows.Forms.TableLayoutPanel> 控件的其中一个已占用的单元格中。  注意，<xref:System.Windows.Forms.TableLayoutPanel> 控件不允许将 <xref:System.Windows.Forms.Button> 控件拖放到已占用的单元格中。  
  
## 交换控件  
 <xref:System.Windows.Forms.TableLayoutPanel> 允许您交换占用两个不同单元格的控件。  
  
#### 交换控件  
  
-   将 <xref:System.Windows.Forms.Button> 控件之一从一个占用的单元格拖到另一个占用的单元格中。  注意，这两个控件将从一个单元格移动到另一个单元格中。  
  
## 后续步骤  
 可以使用布局面板和控件的组合来实现复杂布局。  建议研究的其他方面包括：  
  
-   请尝试将 <xref:System.Windows.Forms.Button> 控件之一的大小调整为较大尺寸，并注意它对布局的影响。  
  
-   将选定的多个控件粘贴到 <xref:System.Windows.Forms.TableLayoutPanel> 控件中并注意这些控件是如何插入的。  
  
-   布局面板可以包含其他布局面板。  请试着将一个 <xref:System.Windows.Forms.TableLayoutPanel> 控件拖到现有控件中。  
  
-   将 <xref:System.Windows.Forms.TableLayoutPanel> 控件停靠到父窗体上。  调整窗体大小并注意这对布局的影响。  
  
## 请参阅  
 <xref:System.Windows.Forms.FlowLayoutPanel>   
 <xref:System.Windows.Forms.TableLayoutPanel>   
 [演练：使用 FlowLayoutPanel 在 Windows 窗体上排列控件](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-flowlayoutpanel.md)   
 [演练：使用对齐线在 Windows 窗体上排列控件](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-snaplines.md)   
 [Microsoft Windows User Experience, Official Guidelines for User Interface Developers and Designers.Redmond, WA: Microsoft Press, 1999. \(USBN: 0\-7356\-0566\-1\)](http://www.microsoft.com/mspress/southpacific/books/book11588.htm)   
 [Walkthrough: Creating a Resizable Windows Form for Data Entry](http://msdn.microsoft.com/zh-cn/e193b4fc-912a-4917-b036-b76c7a6f58ab)   
 [Walkthrough: Creating a Localizable Windows Form](http://msdn.microsoft.com/zh-cn/c5240b6e-aaca-4286-9bae-778a416edb9c)   
 [TableLayoutPanel 控件的最佳做法](../../../../docs/framework/winforms/controls/best-practices-for-the-tablelayoutpanel-control.md)   
 [AutoSize 属性概述](../../../../docs/framework/winforms/controls/autosize-property-overview.md)   
 [如何：在 Windows 窗体上停靠控件](../../../../docs/framework/winforms/controls/how-to-dock-controls-on-windows-forms.md)   
 [如何：在 Windows 窗体上锚定控件](../../../../docs/framework/winforms/controls/how-to-anchor-controls-on-windows-forms.md)   
 [演练：使用 Padding、Margins 和 AutoSize 属性对 Windows 窗体控件进行布局](../../../../docs/framework/winforms/controls/windows-forms-controls-padding-autosize.md)