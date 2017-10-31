---
title: "演练：使用对齐线在 Windows 窗体上排列控件 | Microsoft Docs"
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
  - "控件 [Windows 窗体], 使用对齐线排列"
  - "SnapLine 类, 演练"
  - "对齐线, 排列 Windows 窗体控件"
  - "Windows 窗体控件, 排列"
ms.assetid: d5c9edc7-cf30-4a97-8ebe-201d569340f8
caps.latest.revision: 24
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 24
---
# 演练：使用对齐线在 Windows 窗体上排列控件
对许多应用程序而言，在窗体上精确地放置控件是一项需要优先考虑的任务。  “Windows 窗体设计器”提供了很多用于完成此任务的工具。  在这些工具中，最重要的一个就是 <xref:System.Windows.Forms.Design.Behavior.SnapLine> 功能。  
  
 对齐线为您精确地指示使控件相互对齐的位置。  它们还会根据 Windows 用户界面指南的规定，显示出建议在控件边缘之间留出的距离。  有关详细信息，请参见 [User Interface Design and Development](http://go.microsoft.com/FWLink/?LinkId=83878)（用户界面设计和开发）。  
  
 使用对齐线，您可以方便轻松地对齐控件，获得简洁、专业的外观和效果（视觉体验）。  
  
 本演练涉及以下任务：  
  
-   创建 Windows 窗体项目  
  
-   使用对齐线调整间距并对齐控件  
  
-   与窗体和容器的边缘对齐  
  
-   对齐一组控件  
  
-   通过勾画控件轮廓来使用对齐线放置控件  
  
-   在从工具箱中拖动控件时使用对齐线  
  
-   使用对齐线调整控件大小  
  
-   使标签与控件文本对齐  
  
-   配合键盘导航来使用对齐线  
  
-   对齐线和布局面板  
  
-   禁用对齐线  
  
 完成上述任务之后，您将对对齐线所发挥的布局作用有所了解。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
## 创建项目  
 第一步是创建项目并设置窗体。  
  
#### 创建项目  
  
1.  创建一个名为“SnaplineExample”的基于 Windows 的应用程序项目。  有关详细信息，请参见[How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)。  
  
2.  在“窗体设计器”中选择窗体。  
  
## 使用对齐线调整间距并对齐控件  
 对齐线为在窗体上对齐控件创造了一种准确而直观的方式。  当您在一个需要与一个（或一组）控件对齐的位置附近移动另一个（或一组）选定控件时，对齐线就会出现。  当您将选定控件移过其他控件时，选定控件就会“贴合”到建议的位置。  
  
#### 使用对齐线排列控件  
  
1.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.Button> 控件拖到窗体上。  
  
2.  将 <xref:System.Windows.Forms.Button> 控件移动到窗体的右下角。  当 <xref:System.Windows.Forms.Button> 控件接近窗体的底部和右边框时，请注意随之出现的对齐线。  这些对齐线会显示控件边框和窗体边框之间的推荐距离。  
  
3.  在窗体边框附近移动 <xref:System.Windows.Forms.Button> 控件，留意对齐线出现的位置。  完成之后，将 <xref:System.Windows.Forms.Button> 控件移到窗体的中心附近。  
  
4.  从**“工具箱”**中将另一个 <xref:System.Windows.Forms.Button> 控件拖到窗体上。  
  
5.  移动第二个 <xref:System.Windows.Forms.Button> 控件，使之差不多与第一个控件平齐。  请留意出现在两个按钮的文本基线处的对齐线，您会发现所移动的控件会贴合到与另一个控件完全平齐的位置。  
  
6.  移动第二个 <xref:System.Windows.Forms.Button> 控件，使之位于第一个控件的正上方。  请留意出现在两个按钮左右两边的对齐线，您会发现所移动的控件会贴合到与另一个控件完全对齐的位置。  
  
7.  选择 <xref:System.Windows.Forms.Button> 控件之一并将其移近另一个，直到两个控件几乎接触为止。  留意它们之间的对齐线。  此距离就是控件边框之间的推荐距离。  另外，还请注意您所移动的控件会按此位置对齐。  
  
8.  从**“工具箱”**中将两个 <xref:System.Windows.Forms.Panel> 控件拖到窗体上。  
  
9. 移动一个 <xref:System.Windows.Forms.Panel> 控件，使之差不多与第一个控件平齐。  请留意出现在两个控件上下两边的对齐线，您会发现所移动的控件会贴合到与另一个控件完全平齐的位置。  
  
## 与窗体和容器的边缘对齐  
 对齐线会帮助您以统一的风格将控件与窗体和容器的边缘对齐。  
  
#### 将控件沿窗体和容器边缘对齐  
  
1.  选择一个 <xref:System.Windows.Forms.Button> 控件，将其朝靠近窗体右边框的方向移动，直到出现对齐线。  对齐线与右边框之间的距离等于控件的 <xref:System.Windows.Forms.Control.Margin%2A> 属性和窗体的 <xref:System.Windows.Forms.Control.Padding%2A> 属性值之和。  
  
> [!NOTE]
>  如果窗体的 <xref:System.Windows.Forms.Control.Padding%2A> 属性设置为 0,0,0,0，则 Windows 窗体设计器将为窗体指定隐藏的 <xref:System.Windows.Forms.Control.Padding%2A> 值 9,9,9,9。  为避免此行为，请指定一个 0,0,0,0 以外的值。  
  
1.  更改 <xref:System.Windows.Forms.Button> 控件的 <xref:System.Windows.Forms.Control.Margin%2A> 属性值，方法是在**“属性”**窗口中展开 <xref:System.Windows.Forms.Control.Margin%2A> 项，将 <xref:System.Windows.Forms.Padding.All%2A> 属性设置为 0。  有关详细信息，请参见[演练：使用 Padding、Margins 和 AutoSize 属性对 Windows 窗体控件进行布局](../../../../docs/framework/winforms/controls/windows-forms-controls-padding-autosize.md)。  
  
2.  将 <xref:System.Windows.Forms.Button> 控件朝靠近窗体右边框的方向移动，直到出现对齐线。  现在，此距离与窗体的 <xref:System.Windows.Forms.Control.Padding%2A> 属性值相等。  
  
3.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.GroupBox> 控件拖到窗体上。  
  
4.  更改 <xref:System.Windows.Forms.GroupBox> 控件的 <xref:System.Windows.Forms.Control.Padding%2A> 属性值，方法是在**“属性”**窗口中展开 <xref:System.Windows.Forms.Control.Padding%2A> 项，将 <xref:System.Windows.Forms.Padding.All%2A> 属性设置为 10。  
  
5.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.Button> 控件拖到 <xref:System.Windows.Forms.GroupBox> 控件中。  
  
6.  将 <xref:System.Windows.Forms.Button> 控件朝靠近 <xref:System.Windows.Forms.GroupBox> 控件右边框的方向移动，直到出现对齐线。  在 <xref:System.Windows.Forms.GroupBox> 控件内移动 <xref:System.Windows.Forms.Button> 控件，留意对齐线出现的位置。  
  
## 对齐一组控件  
 使用对齐线，您可以对齐一组控件，以及 <xref:System.Windows.Forms.GroupBox> 控件内部的控件。  
  
#### 对齐一组控件  
  
1.  从您的窗体上选择两个控件。  移动选定控件，同时留意在选定控件和其他控件之间出现的对齐线。  
  
2.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.GroupBox> 控件拖到窗体上。  
  
3.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.Button> 控件拖到 <xref:System.Windows.Forms.GroupBox> 控件中。  
  
4.  选择一个 <xref:System.Windows.Forms.Button> 控件，在 <xref:System.Windows.Forms.GroupBox> 控件附近移动。  留意 <xref:System.Windows.Forms.GroupBox> 控件边缘的对齐线。  同时留意位于 <xref:System.Windows.Forms.GroupBox> 控件内部的 <xref:System.Windows.Forms.Button> 控件边缘的对齐线。  容器控件的子控件也支持对齐线。  
  
## 通过勾画控件轮廓来使用对齐线放置控件  
 当您第一次在窗体上放置控件时，对齐线会帮助您使控件对齐。  
  
#### 通过勾画控件轮廓来使用对齐线放置控件  
  
1.  在**“工具箱”**中单击 <xref:System.Windows.Forms.Button> 控件图标。  不要将其拖到窗体上。  
  
2.  将鼠标指针移动到窗体的设计图面上方。  请留意附加了 <xref:System.Windows.Forms.Button> 控件图标的鼠标会变为十字线。  还请注意建议 <xref:System.Windows.Forms.Button> 控件的对齐位置的对齐线。  
  
3.  单击并按住鼠标按钮。  
  
4.  围绕窗体拖动鼠标指针。  此时会绘制出一条轮廓线，它指示控件的位置和大小。  
  
5.  拖动指针，使之与窗体上的另一个控件对齐。  此时会出现一条对齐线来指示对齐位置。  
  
6.  释放鼠标按钮。  系统会按照轮廓线指示的位置和大小创建控件。  
  
## 在从工具箱中拖动控件时使用对齐线  
 当您从**“工具箱”**中将控件拖到窗体上时，对齐线会帮助您对齐控件。  
  
#### 在从工具箱中拖动控件时使用对齐线  
  
1.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.Button> 控件拖到窗体上，但不要释放鼠标按钮。  
  
2.  将鼠标指针移动到窗体的设计图面上方。  您会注意到指针会随即更改，以指示新的 <xref:System.Windows.Forms.Button> 控件将在哪个位置创建。  
  
3.  围绕窗体拖动鼠标指针。  请留意建议 <xref:System.Windows.Forms.Button> 控件的对齐位置的对齐线。  找到一个可以与其他控件对齐的位置。  
  
4.  释放鼠标按钮。  系统会按照对齐线指示的位置创建控件。  
  
## 使用对齐线调整控件大小  
 对齐线会帮助您在调整控件大小的同时使控件对齐。  
  
#### 使用对齐线调整控件大小  
  
1.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.Button> 控件拖到窗体上。  
  
2.  调整 <xref:System.Windows.Forms.Button> 控件的大小，方法是抓住某个角尺寸柄并拖动它。  有关详细信息，请参见 [如何：调整 Windows 窗体上控件的大小](../../../../docs/framework/winforms/controls/how-to-resize-controls-on-windows-forms.md)。  
  
3.  拖动尺寸柄，使 <xref:System.Windows.Forms.Button> 控件的某个边框与另一个控件对齐。  请留意此时出现的对齐线。  还请留意，尺寸柄会按照对齐线所提示的位置对齐。  
  
4.  沿不同的方向调整 <xref:System.Windows.Forms.Button> 控件的大小，使尺寸柄与不同的控件对齐。  请注意，对齐线会在不同方向上的显示以指示对其位置。  
  
## 使标签与控件文本对齐  
 某些控件会提供一条对齐线，以便其他控件与显示的文本对齐。  
  
#### 使标签与控件文本对齐  
  
1.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.TextBox> 控件拖到窗体上。  当您将 <xref:System.Windows.Forms.TextBox> 控件放到窗体上时，单击智能标记标志符号并选择**“将文本设置为 textBox1”**选项。  有关详细信息，请参见[演练：使用 Windows 窗体控件上的智能标记执行常规任务](../../../../docs/framework/winforms/controls/performing-common-tasks-using-smart-tags-on-wf-controls.md)。  
  
2.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.Label> 控件拖到窗体上。  
  
3.  将 <xref:System.Windows.Forms.Label> 控件的 <xref:System.Windows.Forms.Control.AutoSize%2A> 属性的值更改为 `true`。  请注意控件的边框会为了适应显示文本而进行相应的调整。  
  
4.  将 <xref:System.Windows.Forms.Label> 控件移动到 <xref:System.Windows.Forms.TextBox> 控件的左侧，使之与 <xref:System.Windows.Forms.TextBox> 控件的底部边缘对齐。  留意两个控件底部边缘处的对齐线。  
  
5.  将 <xref:System.Windows.Forms.Label>控件略微向上移动，使 <xref:System.Windows.Forms.Label>文本与 <xref:System.Windows.Forms.TextBox> 文本对齐。  您会发现，此时对齐线的样式有所不同，这表明正在将两个控件的文本字段对齐。  
  
## 配合键盘导航来使用对齐线  
 对齐线会帮助您借助键盘的箭头键来对齐控件。  
  
#### 配合键盘导航来使用对齐线  
  
1.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.Button> 控件拖到窗体上。  将其置于窗体的左上角。  
  
2.  按 Ctrl\+向下键。  注意，控件会沿窗体向下移动到第一个可用的水平对齐位置。  
  
3.  按 Ctrl\+向下键，将控件移到窗体的底部。  注意，控件在沿窗体向下移动的过程中所占用的位置。  
  
4.  按 Ctrl\+向右键。  注意，控件会沿窗体水平移动到第一个可用的垂直对齐位置。  
  
5.  按 Ctrl\+向右键，将控件移到窗体的右侧。  注意，控件在沿窗体水平移动的过程中所占用的位置。  
  
6.  借助组合箭头键在窗体中移动控件。  请留意控件占用的位置以及伴随它们出现的对齐线。  
  
7.  按 Shift\+任意箭头键，以一个像素为增量调整 <xref:System.Windows.Forms.Button> 控件的大小。  
  
8.  按 Ctrl\+Shift\+任意箭头键，以对齐线为增量调整 <xref:System.Windows.Forms.Button> 控件的大小。  
  
## 对齐线和布局面板  
 在布局面板内，对齐线是禁用的。  
  
#### 选择性地禁用对齐线  
  
1.  从**“工具箱”**中将一个 <xref:System.Windows.Forms.TableLayoutPanel> 控件拖到窗体上。  
  
2.  双击**“工具箱”**中的 <xref:System.Windows.Forms.Button> 控件图标。  请注意，一个新的按钮控件会出现在 <xref:System.Windows.Forms.TableLayoutPanel> 控件的第一个单元格中。  
  
3.  再次双击**“工具箱”**中的 <xref:System.Windows.Forms.Button> 控件图标。  这样会在 <xref:System.Windows.Forms.TableLayoutPanel> 控件中留下一个空单元格。  
  
4.  从**“工具箱”**中，将一个 <xref:System.Windows.Forms.Button> 控件拖到 <xref:System.Windows.Forms.TableLayoutPanel> 控件的空单元格中。  请注意此时不会出现对齐线。  
  
5.  将 <xref:System.Windows.Forms.Button> 控件从 <xref:System.Windows.Forms.TableLayoutPanel> 控件中拖动出来，然后在 <xref:System.Windows.Forms.TableLayoutPanel> 控件周围移动它。  请注意此时会再次出现对齐线。  
  
## 禁用对齐线  
 默认情况下，对齐线功能是打开的。  您可以选择性地禁用对齐线，也可以在设计环境中禁用它们。  
  
#### 选择性地禁用对齐线  
  
-   按 Alt 键，同时在窗体上移动一个控件。  
  
     请注意此时不会出现对齐线，而且控件不会沿任何可能的对齐位置对齐。  
  
#### 在设计环境中禁用对齐线  
  
1.  从**“工具”**菜单中，打开**“选项”**对话框。  打开“Windows 窗体设计器”对话框。  有关详细信息，请参见 [General, Windows Forms Designer, Options Dialog Box](http://msdn.microsoft.com/zh-cn/8dd170af-72f0-4212-b04b-034ceee92834)。  
  
2.  选择**“常规”**节点。  在**“布局模式”**区域中，将选项从**“对齐线”**改为**“网格线对齐”**。  
  
3.  单击“确定”应用设置。  
  
4.  在窗体上选择一个控件，在其他控件周围移动它。  请注意此时不会出现对齐线。  
  
## 后续步骤  
 对齐线为您在窗体上对齐控件提供了一种直观的方式。  建议研究的其他方面包括：  
  
-   尝试将一个 <xref:System.Windows.Forms.GroupBox> 控件嵌套在另一个 <xref:System.Windows.Forms.GroupBox> 控件中。  将一个 <xref:System.Windows.Forms.Button> 控件放置在子级 <xref:System.Windows.Forms.GroupBox> 控件中，将另一个控件放置在父级 <xref:System.Windows.Forms.GroupBox> 控件中。  四处移动 <xref:System.Windows.Forms.Button> 控件，观察对齐线跨越容器边界的方式。  
  
-   创建一列 <xref:System.Windows.Forms.TextBox> 控件以及一列相应的 <xref:System.Windows.Forms.Label> 控件。  将 <xref:System.Windows.Forms.Label>控件的 <xref:System.Windows.Forms.Control.AutoSize%2A> 属性的值设置为 `true`。  使用对齐线移动 <xref:System.Windows.Forms.Label>控件，使它们的显示文本与 <xref:System.Windows.Forms.TextBox> 控件中的文本对齐。  
  
 有关 Windows 用户界面设计的信息，请参见 Microsoft Windows User Experience, Official Guidelines for User Interface Developers and Designers Redmond, WA: Microsoft Press, 1999. \(USBN: 0\-7356\-0566\-1\)（《Microsoft Windows 用户体验：用户界面开发人员和设计人员官方指南》）  一书。  
  
## 请参阅  
 <xref:System.Windows.Forms.Design.Behavior.SnapLine>   
 [演练：使用 FlowLayoutPanel 在 Windows 窗体上排列控件](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-flowlayoutpanel.md)   
 [演练：使用 TableLayoutPanel 在 Windows 窗体上排列控件](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel.md)   
 [演练：使用 Padding、Margins 和 AutoSize 属性对 Windows 窗体控件进行布局](../../../../docs/framework/winforms/controls/windows-forms-controls-padding-autosize.md)   
 [排列 Windows 窗体上的控件](../../../../docs/framework/winforms/controls/arranging-controls-on-windows-forms.md)