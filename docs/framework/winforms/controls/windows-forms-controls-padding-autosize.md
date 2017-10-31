---
title: "演练：使用 Padding、Margins 和 AutoSize 属性对 Windows 窗体控件进行布局 | Microsoft Docs"
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
  - "Margin.Bottom"
  - "Margin.Left"
  - "Margin.Top"
  - "Margin.All"
  - "Margin.Right"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "AutoSize 属性, 演练"
  - "布局 [Windows 窗体], 边距和填充"
  - "Margin 属性 [Windows 窗体], 演练"
  - "Padding 属性 [Windows 窗体], 演练"
  - "演练 [Windows 窗体], 布局"
  - "Windows 窗体, 布局"
ms.assetid: f8ae2a6b-db13-4630-8e25-d104091205c7
caps.latest.revision: 28
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 28
---
# 演练：使用 Padding、Margins 和 AutoSize 属性对 Windows 窗体控件进行布局
对许多应用程序而言，在窗体上精确地放置控件是一项需要优先考虑的任务。  **“Windows 窗体设计器”**提供了很多用于完成此任务的工具。  其中最重要的三个为 <xref:System.Windows.Forms.Control.Margin%2A>、<xref:System.Windows.Forms.Control.Padding%2A> 和 <xref:System.Windows.Forms.Control.AutoSize%2A> 属性，所有 Windows 窗体控件都具有这三个属性。  
  
 <xref:System.Windows.Forms.Control.Margin%2A> 属性定义控件周围的空白，以使其他控件与该控件的边界保持指定的距离。  
  
 <xref:System.Windows.Forms.Control.Padding%2A> 属性定义控件内部的空白，使控件中的内容（例如它的 <xref:System.Windows.Forms.Control.Text%2A> 属性的值）与控件的边界保持指定的距离。  
  
 下面的图解演示了控件的 <xref:System.Windows.Forms.Control.Padding%2A> 和 <xref:System.Windows.Forms.Control.Margin%2A> 属性。  
  
 ![Windows 窗体控件的填充和边距](../../../../docs/framework/winforms/controls/media/vs-winformpadmargin.gif "VS\_WinFormPadMargin")  
  
 <xref:System.Windows.Forms.Control.AutoSize%2A> 属性让控件自动调整大小以适合其内容。  它不会将自身大小调整到小于其原始 <xref:System.Windows.Forms.Control.Size%2A> 属性的值，它将体现其 <xref:System.Windows.Forms.Control.Padding%2A> 属性的值。  
  
 本演练涉及以下任务：  
  
-   创建 Windows 窗体项目  
  
-   设置控件的边距  
  
-   设置控件的填充  
  
-   自动调整控件大小  
  
 完成本演练后，您将对这些重要的布局功能所扮演的角色有所了解。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
## 系统必备  
 若要完成本演练，您需要：  
  
-   足够的权限，以便能够在安装 Visual Studio 的计算机上创建和运行 Windows 窗体应用程序项目。  
  
## 创建项目  
 第一步是创建项目并设置窗体。  
  
#### 创建项目  
  
1.  创建一个名为 `LayoutExample` 的**“Windows 应用程序”**项目。  有关更多信息，请参见[How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)。  
  
2.  在**“Windows 窗体设计器”**中选择窗体。  
  
## 设置控件的边距  
 可使用 <xref:System.Windows.Forms.Control.Margin%2A> 属性设置控件之间的默认距离。  当移动一个控件使之足够靠近另一控件时，您将看到一条显示两个控件边距的对齐线。  所移动的控件也将在边距所定义的距离处对齐。  
  
#### 使用 Margin 属性排列窗体上的控件  
  
1.  从**“工具箱”**中将两个 <xref:System.Windows.Forms.Button> 控件拖到窗体上。  
  
2.  选择 <xref:System.Windows.Forms.Button> 控件之一并将其移近另一个，直到两个控件几乎接触为止。  
  
     观察两者之间的对齐线。  此距离是两个控件的 <xref:System.Windows.Forms.Control.Margin%2A> 值之和。  您所移动的控件在此距离处对齐。  有关详细信息，请参见 [演练：使用对齐线在 Windows 窗体上排列控件](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-snaplines.md)。  
  
3.  通过展开**“属性”**窗口中的 <xref:System.Windows.Forms.Control.Margin%2A> 项并将 <xref:System.Windows.Forms.Padding.All%2A> 属性设置为 20 来更改其中一个控件的 <xref:System.Windows.Forms.Control.Margin%2A> 属性。  
  
4.  选择 <xref:System.Windows.Forms.Button> 控件之一并将其移近另一个。  
  
     定义边距值之和的对齐线变长，该控件对齐时与另一控件之间的距离变大。  
  
5.  通过展开**“属性”**窗口中的 <xref:System.Windows.Forms.Control.Margin%2A> 项并将 <xref:System.Windows.Forms.Padding.Top%2A> 属性设置为 5 来更改选定控件的 <xref:System.Windows.Forms.Control.Margin%2A> 属性。  
  
6.  将选定控件移动到另一控件之下，可观察到对齐线变短。  将选定控件移动到另一控件的左侧，可观察到对齐线保持为第 4 步中所观察的值。  
  
7.  可将 <xref:System.Windows.Forms.Control.Margin%2A> 属性、<xref:System.Windows.Forms.Padding.Left%2A>、<xref:System.Windows.Forms.Padding.Top%2A>、<xref:System.Windows.Forms.Padding.Right%2A>、<xref:System.Windows.Forms.Padding.Bottom%2A> 的每一方面设置为不同的值，也可通过 <xref:System.Windows.Forms.Padding.All%2A> 属性将其全部设置为相同的值。  
  
## 设置控件的填充  
 为了达到应用程序所要求的精确布局，控件中通常要包含子控件。  若要指定子控件边界与父控件边界之间的接近程度，可结合使用父控件的 <xref:System.Windows.Forms.Control.Padding%2A> 属性和子控件的 <xref:System.Windows.Forms.Control.Margin%2A> 属性。  <xref:System.Windows.Forms.Control.Padding%2A> 属性也可用于控制控件的内容（如 <xref:System.Windows.Forms.Button> 控件的 <xref:System.Windows.Forms.Control.Text%2A> 属性）与该控件边界的接近程度。  
  
#### 使用填充排列窗体上的控件  
  
1.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.Button> 控件拖到窗体上。  
  
2.  将 <xref:System.Windows.Forms.Button> 控件的 <xref:System.Windows.Forms.Control.AutoSize%2A> 属性值更改为 `true`。  
  
3.  通过展开**“属性”**窗口中的 <xref:System.Windows.Forms.Control.Padding%2A> 项并将 <xref:System.Windows.Forms.Padding.All%2A> 属性设置为 5 来更改 <xref:System.Windows.Forms.Control.Padding%2A> 属性。  
  
     控件将扩大以便为新的填充提供空间。  
  
4.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.GroupBox> 控件拖到窗体上。  从**“工具箱”**中将一个 <xref:System.Windows.Forms.Button> 控件拖到 <xref:System.Windows.Forms.GroupBox> 控件中。  定位 <xref:System.Windows.Forms.Button> 控件，使之与 <xref:System.Windows.Forms.GroupBox> 控件的右下角齐平。  
  
     观察在 <xref:System.Windows.Forms.Button> 控件接近 <xref:System.Windows.Forms.GroupBox> 控件的右边界和底部边界时出现的对齐线。  这些对齐线对应于 <xref:System.Windows.Forms.Button> 的 <xref:System.Windows.Forms.Control.Margin%2A> 属性。  
  
5.  通过展开**“属性”**窗口中的 <xref:System.Windows.Forms.Control.Padding%2A> 项并将 <xref:System.Windows.Forms.Padding.All%2A> 属性设置为 20 来更改 <xref:System.Windows.Forms.GroupBox> 控件的 <xref:System.Windows.Forms.Control.Padding%2A> 属性。  
  
6.  选择 <xref:System.Windows.Forms.GroupBox> 控件内的 <xref:System.Windows.Forms.Button> 控件，并将其移向 <xref:System.Windows.Forms.GroupBox> 的中心。  
  
     对齐线出现在了距 <xref:System.Windows.Forms.GroupBox> 控件边界更远的地方。  该距离是 <xref:System.Windows.Forms.Button> 控件的 <xref:System.Windows.Forms.Control.Margin%2A> 属性与 <xref:System.Windows.Forms.GroupBox> 控件的 <xref:System.Windows.Forms.Control.Padding%2A> 属性之和。  
  
## 自动调整控件大小  
 在一些应用程序中，控件的大小在运行时与设计时不同。  例如，<xref:System.Windows.Forms.Button> 控件的文本可能来自数据库，不能预先知道其长度。  
  
 将 <xref:System.Windows.Forms.Control.AutoSize%2A> 属性设置为 `true` 时，控件将自行调整大小以适合其内容。  有关更多信息，请参见 [AutoSize 属性概述](../../../../docs/framework/winforms/controls/autosize-property-overview.md)。  
  
#### 使用 AutoSize 属性排列窗体上的控件  
  
1.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.Button> 控件拖到窗体上。  
  
2.  将 <xref:System.Windows.Forms.Button> 控件的 <xref:System.Windows.Forms.Control.AutoSize%2A> 属性值更改为 `true`。  
  
3.  将 <xref:System.Windows.Forms.Button> 控件的 <xref:System.Windows.Forms.Control.Text%2A> 属性更改为“此按钮的‘Text’属性是一个长字符串”。  
  
     提交更改后，<xref:System.Windows.Forms.Button> 控件会自行调整大小以适合新的文本。  
  
4.  从**“工具箱”**中将另一个 <xref:System.Windows.Forms.Button> 控件拖到窗体上。  
  
5.  将 <xref:System.Windows.Forms.Button> 控件的 <xref:System.Windows.Forms.Control.Text%2A> 属性更改为“此按钮的‘Text’属性是一个长字符串”。  
  
     提交更改后，<xref:System.Windows.Forms.Button> 控件不会自行调整大小，文本会在控件的右边界处截断。  
  
6.  通过展开**“属性”**窗口中的 <xref:System.Windows.Forms.Control.Padding%2A> 项并将 <xref:System.Windows.Forms.Padding.All%2A> 属性设置为 5 来更改 <xref:System.Windows.Forms.Control.Padding%2A> 属性。  
  
     控件内部的文本在四面都被截断。  
  
7.  将 <xref:System.Windows.Forms.Button> 控件的 <xref:System.Windows.Forms.Control.AutoSize%2A> 属性更改为 `true`。  
  
     <xref:System.Windows.Forms.Button> 控件将自行调整以容纳整个字符串。  另外，文本周围还加上了填充，使得 <xref:System.Windows.Forms.Button> 控件在四个方向都进行了扩展。  
  
8.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.Button> 控件拖到窗体上。  将其定位在窗体的右下角。  
  
9. 将 <xref:System.Windows.Forms.Button> 控件的 <xref:System.Windows.Forms.Control.AutoSize%2A> 属性值更改为 `true`。  
  
10. 将 <xref:System.Windows.Forms.Button> 控件的 <xref:System.Windows.Forms.Control.Anchor%2A> 属性设置为 <xref:System.Windows.Forms.AnchorStyles>，<xref:System.Windows.Forms.AnchorStyles>。  
  
11. 将 <xref:System.Windows.Forms.Button> 控件的 <xref:System.Windows.Forms.Control.Text%2A> 属性更改为“此按钮的‘Text’属性是一个长字符串”。  
  
     提交更改后，<xref:System.Windows.Forms.Button> 控件会向左方自行调整大小。  通常，自动大小调整功能会使控件的大小在与其 <xref:System.Windows.Forms.Control.Anchor%2A> 属性设置相反的方向上增加。  
  
## AutoSize 和 AutoSizeMode 属性  
 一些控件支持 `AutoSizeMode` 属性，利用该属性可以对控件的自动调整大小行为进行更精细的控制。  
  
#### 使用 AutoSizeMode 属性  
  
1.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.Panel> 控件拖到窗体上。  
  
2.  将 <xref:System.Windows.Forms.Panel> 控件的 <xref:System.Windows.Forms.Control.AutoSize%2A> 属性值设置为 `true`。  
  
3.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.Button> 控件拖到 <xref:System.Windows.Forms.Panel> 控件中。  
  
4.  将 <xref:System.Windows.Forms.Button> 控件置于靠近 <xref:System.Windows.Forms.Panel> 控件右下角的地方。  
  
5.  选择 <xref:System.Windows.Forms.Panel> 控件并抓住右下角大小调整手柄。  将 <xref:System.Windows.Forms.Panel> 控件调大和调小。  
  
    > [!NOTE]
    >  可自由调整 <xref:System.Windows.Forms.Panel> 控件的大小，但无法将其调到小于 <xref:System.Windows.Forms.Button> 控件右下角的位置。  此行为由 `AutoSizeMode` 属性的默认值 <xref:System.Windows.Forms.AutoSizeMode> 指定。  
  
6.  将 <xref:System.Windows.Forms.Panel> 控件的 `AutoSizeMode` 属性值设置为 <xref:System.Windows.Forms.AutoSizeMode>。  
  
     <xref:System.Windows.Forms.Panel> 控件会自行调整大小以包围 <xref:System.Windows.Forms.Button> 控件。  不能调整 <xref:System.Windows.Forms.Panel> 控件的大小。  
  
7.  将 <xref:System.Windows.Forms.Button> 控件拖向 <xref:System.Windows.Forms.Panel> 控件的左上角。  
  
     <xref:System.Windows.Forms.Panel> 控件的大小会调整为 <xref:System.Windows.Forms.Button> 控件的新位置。  
  
## 后续步骤  
 可用于在 Windows 窗体应用程序中排列控件的布局功能还有许多。  您可以尝试使用下面的这些组合：  
  
-   使用 <xref:System.Windows.Forms.TableLayoutPanel> 控件设立窗体。  有关详细信息，请参见 [演练：使用 TableLayoutPanel 在 Windows 窗体上排列控件](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)。  尝试更改 <xref:System.Windows.Forms.TableLayoutPanel> 控件的 <xref:System.Windows.Forms.Control.Padding%2A> 属性的值以及其子控件的 <xref:System.Windows.Forms.Control.Margin%2A> 属性的值。  
  
-   使用 <xref:System.Windows.Forms.FlowLayoutPanel> 控件进行同样的试验。  有关详细信息，请参见 [演练：使用 FlowLayoutPanel 在 Windows 窗体上排列控件](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-flowlayoutpanel.md)。  
  
-   试验在 <xref:System.Windows.Forms.Panel> 控件中停靠子控件。  <xref:System.Windows.Forms.Control.Padding%2A> 属性是 <xref:System.Windows.Forms.ScrollableControl.DockPadding%2A> 属性的更常见的实现方式，通过将一个子控件放入 <xref:System.Windows.Forms.Panel> 控件并将该子控件的 <xref:System.Windows.Forms.Control.Dock%2A> 属性设置为 <xref:System.Windows.Forms.DockStyle>，您将满意地发现事实确实如此。  将 <xref:System.Windows.Forms.Panel> 控件的 <xref:System.Windows.Forms.Control.Padding%2A> 属性设置为各种值并注意效果。  
  
## 请参阅  
 <xref:System.Windows.Forms.Control.AutoSize%2A>   
 <xref:System.Windows.Forms.ScrollableControl.DockPadding%2A>   
 <xref:System.Windows.Forms.Control.Margin%2A>   
 <xref:System.Windows.Forms.Control.Padding%2A>   
 [AutoSize 属性概述](../../../../docs/framework/winforms/controls/autosize-property-overview.md)   
 [演练：使用 TableLayoutPanel 在 Windows 窗体上排列控件](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)   
 [演练：使用 FlowLayoutPanel 在 Windows 窗体上排列控件](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-flowlayoutpanel.md)   
 [演练：使用对齐线在 Windows 窗体上排列控件](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-snaplines.md)