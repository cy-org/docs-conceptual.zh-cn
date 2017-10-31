---
title: "演练：对用户控件启用拖放功能 | Microsoft Docs"
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
  - "拖放 [WPF], 演练"
  - "演练 [WPF], 拖放"
ms.assetid: cc844419-1a77-4906-95d9-060d79107fc7
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# 演练：对用户控件启用拖放功能
本演练演示如何创建可在 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 中参与拖放数据传输的自定义用户控件。  
  
 在本演练中，将创建一个表示圆形的自定义 WPF <xref:System.Windows.Controls.UserControl>。  您将在该控件上实现可通过拖放进行数据传输的功能。  例如，如果从一个圆形控件拖到另一个圆形控件，则会将填充颜色从源圆形复制到目标圆形。  如果从圆形控件拖到 <xref:System.Windows.Controls.TextBox>，则填充颜色的字符串表示形式将复制到 <xref:System.Windows.Controls.TextBox>。  您还将创建一个小应用程序，该应用程序包含两个面板控件和一个 <xref:System.Windows.Controls.TextBox>，以测试拖放功能。  您将编写可使面板能够处理放置的圆形数据的代码，这样就可以将圆形从一个面板的 Children 集合移动或复制到其他面板。  
  
 本演练阐释了以下任务：  
  
-   创建自定义用户控件。  
  
-   使用户控件成为拖动源。  
  
-   使用户控件成为放置目标。  
  
-   使面板能够接收从用户控件放置的数据。  
  
## 必备组件  
 您需要以下组件来完成本演练：  
  
-   Visual Studio 2010  
  
## 创建应用程序项目  
 在本节中，您将创建应用程序基础结构，其中包括一个具有两个面板和一个 <xref:System.Windows.Controls.TextBox> 的主页。  
  
### 创建项目  
  
1.  在 Visual Basic 或 Visual C\# 中创建名为 `DragDropExample` 的新 WPF 应用程序项目。  有关更多信息，请参见[如何：创建新的 WPF 应用程序项目](http://msdn.microsoft.com/zh-cn/1f6aea7a-33e1-4d3f-8555-1daa42e95d82)。  
  
2.  打开 MainWindow.xaml。  
  
3.  在开始和结束 <xref:System.Windows.Controls.Grid> 标记之间添加以下标记。  
  
     此标记将创建测试应用程序的用户界面。  
  
     [!code-xml[DragDropWalkthrough#PanelsStep1XAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/SnippetWindow.xaml#panelsstep1xaml)]  
  
## 向项目中添加新用户控件  
 在本节中，您将向项目中添加一个新用户控件。  
  
### 添加新用户控件  
  
1.  在“项目”菜单中，选择**“添加用户控件”**。  
  
2.  在“添加新项”对话框中，将名称更改为 `Circle.xaml`，然后单击**“添加”**。  
  
     Circle.xaml 及其代码隐藏内容将添加到项目中。  
  
3.  打开 Circle.xaml。  
  
     此文件将包含用户控件的用户界面元素。  
  
4.  将以下标记添加到根 <xref:System.Windows.Controls.Grid>，以创建将一个蓝色圆形作为其 UI 的简单用户控件。  
  
     [!code-xml[DragDropWalkthrough#EllipseXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml#ellipsexaml)]  
  
5.  打开 Circle.xaml.cs 或 Circle.xaml.vb。  
  
6.  在 C\# 中，在默认构造函数的后面添加以下代码以创建复制构造函数。  在 Visual Basic 中，添加以下代码以创建默认构造函数和复制构造函数。  
  
     若要允许复制用户控件，需在代码隐藏文件中添加复制构造函数方法。  在简化的圆形用户控件中，您将仅复制该用户控件的填充和大小。  
  
     [!code-csharp[DragDropWalkthrough#CopyCtor](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#copyctor)]
     [!code-vb[DragDropWalkthrough#CopyCtor](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#copyctor)]  
  
### 向主窗口添加用户控件  
  
1.  打开 MainWindow.xaml。  
  
2.  将以下 XAML 添加到开始 <xref:System.Windows.Window> 标记以创建对当前应用程序的 XML 命名空间引用。  
  
    ```  
    xmlns:local="clr-namespace:DragDropExample"  
    ```  
  
3.  在第一个 <xref:System.Windows.Controls.StackPanel> 中，添加以下 XAML，以在第一个面板中创建圆形用户控件的两个实例。  
  
     [!code-xml[DragDropWalkthrough#CirclesXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/SnippetWindow.xaml#circlesxaml)]  
  
     该面板的完整 XAML 与下面类似。  
  
     [!code-xml[DragDropWalkthrough#PanelsStep2XAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/SnippetWindow.xaml#panelsstep2xaml)]  
  
## 在用户控件中实现拖动源事件  
 在本节中，您将重写 <xref:System.Windows.UIElement.OnMouseMove%2A> 方法并启动拖放操作。  
  
 如果已开始拖动（按下鼠标按钮并移动鼠标），则会将要传输的数据打包到 <xref:System.Windows.DataObject> 中。  在这种情况下，圆形控件将打包三个数据项：其填充颜色的字符串表示形式、其高度的双精度表示形式以及其自身的副本。  
  
### 启动拖放操作  
  
1.  打开 Circle.xaml.cs 或 Circle.xaml.vb。  
  
2.  添加以下 <xref:System.Windows.UIElement.OnMouseMove%2A> 重写，以便为 <xref:System.Windows.UIElement.MouseMove> 事件提供类处理。  
  
     [!code-csharp[DragDropWalkthrough#OnMouseMove](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#onmousemove)]
     [!code-vb[DragDropWalkthrough#OnMouseMove](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#onmousemove)]  
  
     此 <xref:System.Windows.UIElement.OnMouseMove%2A> 重写执行以下任务：  
  
    -   检查在鼠标移动时是否按下了鼠标左键。  
  
    -   将圆形数据打包到一个 <xref:System.Windows.DataObject> 中。  在这种情况下，圆形控件会打包三个数据项：其填充颜色的字符串表示形式、其高度的双精度表示形式以及其自身的副本。  
  
    -   调用静态 <xref:System.Windows.DragDrop.DoDragDrop%2A?displayProperty=fullName> 方法以启动拖放操作。  将以下三个参数传递给 <xref:System.Windows.DragDrop.DoDragDrop%2A> 方法：  
  
        -   `dragSource` – 对此控件的引用。  
  
        -   `data` – 在前面代码中创建的 <xref:System.Windows.DataObject>。  
  
        -   `allowedEffects` – 允许的拖放操作，即 <xref:System.Windows.DragDropEffects> 或 <xref:System.Windows.DragDropEffects>。  
  
3.  按 F5 生成并运行该应用程序。  
  
4.  单击一个圆形控件并将其拖到面板、另一个圆形和 <xref:System.Windows.Controls.TextBox> 上。  在拖到 <xref:System.Windows.Controls.TextBox> 上时，光标会更改，以指示移动。  
  
5.  在将圆形拖到 <xref:System.Windows.Controls.TextBox> 上时，按 Ctrl 键。  请注意光标是如何更改以指示复制的。  
  
6.  将一个圆形拖放到 <xref:System.Windows.Controls.TextBox> 上。  该圆形填充颜色的字符串表示形式会追加到 <xref:System.Windows.Controls.TextBox>。  
  
     ![圆的填充颜色的字符串表示形式](../../../../docs/framework/wpf/advanced/media/dragdrop-colorstring.png "DragDrop\_ColorString")  
  
 默认情况下，光标会在拖放操作过程中更改，以指示放置数据会产生的效果。  您可通过处理 <xref:System.Windows.UIElement.GiveFeedback> 事件并设置不同光标来自定义向用户提供的反馈。  
  
### 向用户提供反馈  
  
1.  打开 Circle.xaml.cs 或 Circle.xaml.vb。  
  
2.  添加以下 <xref:System.Windows.UIElement.OnGiveFeedback%2A> 重写，以便为 <xref:System.Windows.UIElement.GiveFeedback> 事件提供类处理。  
  
     [!code-csharp[DragDropWalkthrough#OnGiveFeedback](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ongivefeedback)]
     [!code-vb[DragDropWalkthrough#OnGiveFeedback](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ongivefeedback)]  
  
     此 <xref:System.Windows.UIElement.OnGiveFeedback%2A> 重写执行以下任务：  
  
    -   检查在放置目标的 <xref:System.Windows.UIElement.DragOver> 事件处理程序中设置的 <xref:System.Windows.GiveFeedbackEventArgs.Effects%2A> 值。  
  
    -   基于 <xref:System.Windows.GiveFeedbackEventArgs.Effects%2A> 值来设置自定义光标。  该光标旨在向用户提供关于放置数据所产生的效果的可视反馈。  
  
3.  按 F5 生成并运行该应用程序。  
  
4.  将一个圆形控件拖到面板、另一个圆形和 <xref:System.Windows.Controls.TextBox> 上。  请注意，现在的光标是在 <xref:System.Windows.UIElement.OnGiveFeedback%2A> 重写中指定的自定义光标。  
  
     ![使用自定义光标拖放](../../../../docs/framework/wpf/advanced/media/dragdrop-customcursor.png "DragDrop\_CustomCursor")  
  
5.  从 <xref:System.Windows.Controls.TextBox> 中选择文本 `green`。  
  
6.  将 `green` 文本拖到一个圆形控件。  请注意，将显示默认光标以指示拖放操作的效果。  反馈光标始终由拖动源设置。  
  
## 在用户控件中实现放置目标事件  
 在本节中，您将指定用户控件是放置目标，重写可使用户控件成为放置目标的方法，并处理放置在其上的数据。  
  
### 使用户控件成为放置目标  
  
1.  打开 Circle.xaml。  
  
2.  在开始 <xref:System.Windows.Controls.UserControl> 标记中，添加 <xref:System.Windows.UIElement.AllowDrop%2A> 属性并将其设置为 `true`。  
  
     [!code-xml[DragDropWalkthrough#UCTagXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml#uctagxaml)]  
  
 在 <xref:System.Windows.UIElement.AllowDrop%2A> 属性设置为 `true` 并将拖动源的数据放置在圆形用户控件上时，会调用 <xref:System.Windows.UIElement.OnDrop%2A> 方法。  在此方法中，您将处理已放置的数据，并将这些数据应用于圆形。  
  
### 处理放置的数据  
  
1.  打开 Circle.xaml.cs 或 Circle.xaml.vb。  
  
2.  添加以下 <xref:System.Windows.UIElement.OnDrop%2A> 重写，以便为 <xref:System.Windows.UIElement.Drop> 事件提供类处理。  
  
     [!code-csharp[DragDropWalkthrough#OnDrop](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ondrop)]
     [!code-vb[DragDropWalkthrough#OnDrop](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ondrop)]  
  
     此 <xref:System.Windows.UIElement.OnDrop%2A> 重写执行以下任务：  
  
    -   使用 <xref:System.Windows.DataObject.GetDataPresent%2A> 方法来检查拖动的数据是否包含字符串对象。  
  
    -   使用 <xref:System.Windows.DataObject.GetData%2A> 方法来提取字符串数据（如果存在）。  
  
    -   使用 <xref:System.Windows.Media.BrushConverter> 尝试将字符串转换为 <xref:System.Windows.Media.Brush>。  
  
    -   如果转换成功，则将画笔应用于提供圆形控件 UI 的 <xref:System.Windows.Shapes.Ellipse> 的 <xref:System.Windows.Shapes.Shape.Fill%2A>。  
  
    -   将 <xref:System.Windows.UIElement.Drop> 事件标记为已处理。  应将放置事件标记为已处理，以便接收此事件的其他元素知道圆形用户控件对其进行了处理。  
  
3.  按 F5 生成并运行该应用程序。  
  
4.  从 <xref:System.Windows.Controls.TextBox> 中选择文本 `green`。  
  
5.  将该文本拖放到一个圆形控件上。  该圆形会从蓝色变为绿色。  
  
     ![将字符串转换为画笔](../../../../docs/framework/wpf/advanced/media/dragdrop-dropgreentext.png "DragDrop\_DropGreenText")  
  
6.  在 <xref:System.Windows.Controls.TextBox> 中键入文本 `green`。  
  
7.  在 <xref:System.Windows.Controls.TextBox> 中选择文本 `gre`。  
  
8.  将其拖放到一个圆形控件上。  请注意，光标会更改以指示允许放置，但圆形的颜色未更改，因为 `gre` 不是有效颜色。  
  
9. 从绿色圆形控件拖放到蓝色圆形控件上。  该圆形会从蓝色变为绿色。  请注意，显示的光标取决于是 <xref:System.Windows.Controls.TextBox> 还是圆形作为拖动源。  
  
 若要使某个元素成为放置目标，只需将 <xref:System.Windows.UIElement.AllowDrop%2A> 属性设置为 `true` 并处理放置的数据。  但是，若要提供更佳的用户体验，则还应处理 <xref:System.Windows.UIElement.DragEnter>、<xref:System.Windows.UIElement.DragLeave> 和 <xref:System.Windows.UIElement.DragOver> 事件。  在这些事件中，您可以在放置数据前执行检查并向用户提供其他反馈。  
  
 将数据拖动到圆形用户控件上时，该控件应通知拖动源它是否可以处理所拖动的数据。  如果该控件不知道如何处理这些数据，则它应拒绝放置。  为此，您将处理 <xref:System.Windows.UIElement.DragOver> 事件并设置 <xref:System.Windows.DragEventArgs.Effects%2A> 属性。  
  
### 验证是否允许数据放置  
  
1.  打开 Circle.xaml.cs 或 Circle.xaml.vb。  
  
2.  添加以下 <xref:System.Windows.UIElement.OnDragOver%2A> 重写，以便为 <xref:System.Windows.UIElement.DragOver> 事件提供类处理。  
  
     [!code-csharp[DragDropWalkthrough#OnDragOver](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ondragover)]
     [!code-vb[DragDropWalkthrough#OnDragOver](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ondragover)]  
  
     此 <xref:System.Windows.UIElement.OnDragOver%2A> 重写执行以下任务：  
  
    -   将 <xref:System.Windows.DragEventArgs.Effects%2A> 属性设置为 <xref:System.Windows.DragDropEffects>。  
  
    -   执行在 <xref:System.Windows.UIElement.OnDrop%2A> 方法中执行的相同检查，以确定圆形用户控件是否可以处理拖动的数据。  
  
    -   如果该用户控件可以处理这些数据，则将 <xref:System.Windows.DragEventArgs.Effects%2A> 属性设置为 <xref:System.Windows.DragDropEffects> 或 <xref:System.Windows.DragDropEffects>。  
  
3.  按 F5 生成并运行该应用程序。  
  
4.  在 <xref:System.Windows.Controls.TextBox> 中选择文本 `gre`。  
  
5.  将该文本拖到一个圆形控件。  请注意，光标此时会更改以指示不允许放置，因为 `gre` 不是有效颜色。  
  
 您可通过应用放置操作的预览来进一步增强用户体验。  对于圆形用户控件，您将重写 <xref:System.Windows.UIElement.OnDragEnter%2A> 和 <xref:System.Windows.UIElement.OnDragLeave%2A> 方法。  在将数据拖动到该控件上时，当前背景 <xref:System.Windows.Shapes.Shape.Fill%2A> 会保存在一个占位符变量中。  随后字符串会转换为画笔并应用于提供圆形 UI 的 <xref:System.Windows.Shapes.Ellipse>。  如果将数据拖动出该圆形而没有放置，则原始 <xref:System.Windows.Shapes.Shape.Fill%2A> 值将重新应用于该圆形。  
  
### 预览拖放操作的效果  
  
1.  打开 Circle.xaml.cs 或 Circle.xaml.vb。  
  
2.  在圆形类中，可声明一个名为 `_previousFill` 的私有 <xref:System.Windows.Media.Brush> 变量，并将其初始化为 `null`。  
  
     [!code-csharp[DragDropWalkthrough#Brush](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#brush)]
     [!code-vb[DragDropWalkthrough#Brush](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#brush)]  
  
3.  添加以下 <xref:System.Windows.UIElement.OnDragEnter%2A> 重写，以便为 <xref:System.Windows.UIElement.DragEnter> 事件提供类处理。  
  
     [!code-csharp[DragDropWalkthrough#OnDragEnter](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ondragenter)]
     [!code-vb[DragDropWalkthrough#OnDragEnter](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ondragenter)]  
  
     此 <xref:System.Windows.UIElement.OnDragEnter%2A> 重写执行以下任务：  
  
    -   将 <xref:System.Windows.Shapes.Ellipse> 的 <xref:System.Windows.Shapes.Shape.Fill%2A> 属性保存在 `_previousFill` 变量中。  
  
    -   执行在 <xref:System.Windows.UIElement.OnDrop%2A> 方法中执行的相同检查，以确定是否可将数据转换为 <xref:System.Windows.Media.Brush>。  
  
    -   如果数据可转换为有效的 <xref:System.Windows.Media.Brush>，则将其应用于 <xref:System.Windows.Shapes.Ellipse> 的 <xref:System.Windows.Shapes.Shape.Fill%2A>。  
  
4.  添加以下 <xref:System.Windows.UIElement.OnDragLeave%2A> 重写，以便为 <xref:System.Windows.UIElement.DragLeave> 事件提供类处理。  
  
     [!code-csharp[DragDropWalkthrough#OnDragLeave](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ondragleave)]
     [!code-vb[DragDropWalkthrough#OnDragLeave](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ondragleave)]  
  
     此 <xref:System.Windows.UIElement.OnDragLeave%2A> 重写执行以下任务：  
  
    -   将保存在 `_previousFill` 变量中的 <xref:System.Windows.Media.Brush> 应用于提供圆形用户控件 UI 的 <xref:System.Windows.Shapes.Ellipse> 的 <xref:System.Windows.Shapes.Shape.Fill%2A>。  
  
5.  按 F5 生成并运行该应用程序。  
  
6.  从 <xref:System.Windows.Controls.TextBox> 中选择文本 `green`。  
  
7.  将该文本拖到一个圆形控件上而不放置。  该圆形会从蓝色变为绿色。  
  
     ![预览拖放操作的效果](../../../../docs/framework/wpf/advanced/media/dragdrop-previeweffects.png "DragDrop\_PreviewEffects")  
  
8.  将文本拖离该圆形控件。  该圆形会从绿色变回为蓝色。  
  
## 使面板能够接收放置的数据  
 在本节中，您将让承载圆形用户控件的面板充当拖动的圆形数据的放置目标。  您将实现的代码使您可以将圆形从一个面板移动到另一个面板，或通过在拖放圆形时按住 Ctrl 键来复制圆形控件。  
  
### 使面板成为放置目标  
  
1.  打开 MainWindow.xaml。  
  
2.  如以下 XAML 所示，在每个 <xref:System.Windows.Controls.StackPanel> 控件中，为 <xref:System.Windows.UIElement.DragOver> 和 <xref:System.Windows.UIElement.Drop> 事件添加处理程序。  将 <xref:System.Windows.UIElement.DragOver> 事件处理程序命名为 `panel_DragOver`，并将 <xref:System.Windows.UIElement.Drop> 事件处理程序命名为 `panel_Drop`。  
  
     [!code-xml[DragDropWalkthrough#PanelsXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/MainWindow.xaml#panelsxaml)]  
  
3.  打开 MainWindows.xaml.cs 或 MainWindow.xaml.vb。  
  
4.  为 <xref:System.Windows.UIElement.DragOver> 事件处理程序添加下面的代码。  
  
     [!code-csharp[DragDropWalkthrough#PanelDragOver](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/MainWindow.xaml.cs#paneldragover)]
     [!code-vb[DragDropWalkthrough#PanelDragOver](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/MainWindow.xaml.vb#paneldragover)]  
  
     此 <xref:System.Windows.UIElement.DragOver> 事件处理程序执行以下任务：  
  
    -   检查拖动的数据是否包含由圆形用户控件打包在 <xref:system.Windows.DataObject> 中并且在 <xref:System.Windows.DragDrop.DoDragDrop%2A> 调用中传递的“对象”数据。  
  
    -   如果存在“对象”数据，请检查是否按下了 Ctrl 键。  
  
    -   如果按下了 Ctrl 键，则将 <xref:System.Windows.DragEventArgs.Effects%2A> 属性设置为 <xref:System.Windows.DragDropEffects>。  否则，将 <xref:System.Windows.DragEventArgs.Effects%2A> 属性设置为 <xref:System.Windows.DragDropEffects>。  
  
5.  为 <xref:System.Windows.UIElement.Drop> 事件处理程序添加下面的代码。  
  
     [!code-csharp[DragDropWalkthrough#PanelDrop](../../../../samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/MainWindow.xaml.cs#paneldrop)]
     [!code-vb[DragDropWalkthrough#PanelDrop](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/MainWindow.xaml.vb#paneldrop)]  
  
     此 <xref:System.Windows.UIElement.Drop> 事件处理程序执行以下任务：  
  
    -   检查是否已处理 <xref:System.Windows.UIElement.Drop> 事件。  例如，如果将一个圆形放置在处理 <xref:System.Windows.UIElement.Drop> 事件的另一个圆形上，则无需让包含该圆形的面板也处理该事件。  
  
    -   如果未处理 <xref:System.Windows.UIElement.Drop> 事件，请检查是否按下了 Ctrl 键。  
  
    -   如果在发生 <xref:System.Windows.UIElement.Drop> 时按下了 Ctrl 键，则会创建圆形控件的副本并将其添加到 <xref:System.Windows.Controls.StackPanel> 的 <xref:System.Windows.Controls.Panel.Children%2A> 集合。  
  
    -   如果未按下 Ctrl 键，则将圆形从其父面板的 <xref:System.Windows.Controls.Panel.Children%2A> 集合移动到放置该圆形的面板的 <xref:System.Windows.Controls.Panel.Children%2A> 集合。  
  
    -   设置 <xref:System.Windows.DragEventArgs.Effects%2A> 属性以通知 <xref:System.Windows.DragDrop.DoDragDrop%2A> 方法是执行了移动还是复制操作。  
  
6.  按 F5 生成并运行该应用程序。  
  
7.  从 <xref:System.Windows.Controls.TextBox> 中选择文本 `green`。  
  
8.  将该文本拖放到一个圆形控件上。  
  
9. 将一个圆形控件从左面板拖放到右面板上。  该圆形将从左面板的 <xref:System.Windows.Controls.Panel.Children%2A> 结合中移除，并添加到右面板的 Children 集合中。  
  
10. 在按下 Ctrl 键的同时，将一个圆形控件从其所在的面板拖放到其他面板。  将复制该圆形并将副本添加到接收面板的 <xref:System.Windows.Controls.Panel.Children%2A> 集合中。  
  
     ![按住 Ctrl 键的同时拖动圆形](../../../../docs/framework/wpf/advanced/media/dragdrop-paneldrop.png "DragDrop\_PanelDrop")  
  
## 请参阅  
 [拖放概述](../../../../docs/framework/wpf/advanced/drag-and-drop-overview.md)