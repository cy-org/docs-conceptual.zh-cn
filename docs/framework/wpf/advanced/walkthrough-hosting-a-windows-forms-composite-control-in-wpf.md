---
title: "演练：在 WPF 中承载 Windows 窗体复合控件 | Microsoft Docs"
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
  - "复合控件, 在 WPF 中承载"
  - "在 WPF 中承载 Windows 窗体控件"
ms.assetid: 96fcd78d-1c77-4206-8928-3a0579476ef4
caps.latest.revision: 33
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 30
---
# 演练：在 WPF 中承载 Windows 窗体复合控件
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 提供用于创建应用程序的丰富环境。  但是，如果您对 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]代码的投入较大，那么更有效的办法是在您的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序中至少重用该代码的一部分，而不是从头开始重新编写应用程序。  最常见的情况是您有现有的 [!INCLUDE[TLA2#tla_winforms](../../../../includes/tla2sharptla-winforms-md.md)]控件。  在某些情况下，您可能甚至没有对这些控件的源代码的访问权。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 提供了一个在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序中承载此类控件的简单过程。  例如，您可以在承载专用的 <xref:System.Windows.Forms.DataGridView> 控件时，将 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 用于大多数编程。  
  
 本演练引导您创建一个应用程序，该应用程序承载 [!INCLUDE[TLA2#tla_winforms](../../../../includes/tla2sharptla-winforms-md.md)]复合控件以在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序程序中执行数据输入。  该复合控件打包到一个 DLL 中。  该一般过程可以扩展到更复杂的应用程序和控件。  本演练的设计在外观与功能上与[演练：在 Windows 窗体中承载 WPF 复合控件](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)几乎完全相同。  主要区别在于承载方案是相反的。  
  
 本演练分为两部分。  第一部分简要介绍 [!INCLUDE[TLA2#tla_winforms](../../../../includes/tla2sharptla-winforms-md.md)]复合控件的实现。  第二部分详细讨论如何在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序中承载该复合控件、从该控件接收事件以及访问该控件的一些属性。  
  
 本演练涉及以下任务：  
  
-   实现 Windows 窗体复合控件。  
  
-   实现 WPF 宿主应用程序。  
  
 有关本演练中所阐释任务的完整代码清单，请参见 [Hosting a Windows Forms Composite Control in WPF Sample](http://go.microsoft.com/fwlink/?LinkID=159999)（在 WPF 中承载 Windows 窗体复合控件示例）。  
  
## 必备组件  
 您需要以下组件来完成本演练：  
  
-   [!INCLUDE[vs_dev10_long](../../../../includes/vs-dev10-long-md.md)].  
  
## 实现 Windows 窗体复合控件  
 本示例中使用的 [!INCLUDE[TLA2#tla_winforms](../../../../includes/tla2sharptla-winforms-md.md)]复合控件是一个简单的数据输入窗体。  该窗体接受用户的名称和地址，然后使用自定义事件将此信息返回到宿主。  下图演示呈现的控件。  
  
 ![简单的 Windows 窗体控件](../../../../docs/framework/wpf/advanced/media/wfcontrol.png "WFControl")  
Windows 窗体复合控件  
  
### 创建项目  
 若要开始创建项目，请执行以下操作：  
  
1.  启动 [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)]，打开**“新建项目”**对话框。  
  
2.  在窗口类别中，选择**“Windows 窗体控件库”**模板。  
  
3.  将新项目命名为 `MyControls`。  
  
4.  为位置指定一个便于命名的顶级文件夹，如 `WpfHostingWindowsFormsControl`。  稍后会将宿主应用程序放入此文件夹中。  
  
5.  单击**“确定”**创建项目。  默认项目包含一个名为 `UserControl1` 的控件。  
  
6.  在解决方案资源管理器中，将 `UserControl1` 重命名为 `MyControl1`。  
  
 您的项目应当具有对以下系统 DLL 的引用。  如果默认情况下未包括其中任何一个 DLL，请将它添加到项目中。  
  
-   系统  
  
-   System.Data  
  
-   System.Drawing  
  
-   System.Windows.Forms  
  
-   System.Xml  
  
### 向窗体添加控件  
 向窗体添加控件：  
  
-   在设计器中打开 `MyControl1`。  
  
 在窗体中添加五个 <xref:System.Windows.Forms.Label> 控件及其相应的 <xref:System.Windows.Forms.TextBox> 控件，这些控件的大小和排列方式如前面的图中所示。  在此示例中，<xref:System.Windows.Forms.TextBox> 控件命名为：  
  
-   `txtName`  
  
-   `txtAddress`  
  
-   `txtCity`  
  
-   `txtState`  
  
-   `txtZip`  
  
 添加两个标有**“OK”（确定）**和**“Cancel”（取消）**的 <xref:System.Windows.Forms.Button> 控件。  在此示例中，按钮名称分别为 `btnOK` 和 `btnCancel`。  
  
### 实现支持代码  
 在代码视图中打开窗体。  控件通过引发自定义 `OnButtonClick` 事件向其宿主返回所收集的数据。  这些数据包含在事件参数对象中。  下面的代码演示事件和委托声明。  
  
 向 `MyControl1` 类添加下面的代码。  
  
 [!code-csharp[WpfHostingWindowsFormsControl#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/MyControls/MyControl1.cs#2)]
 [!code-vb[WpfHostingWindowsFormsControl#2](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/VisualBasic/MyControls/MyControl1.vb#2)]  
  
 `MyControlEventArgs` 类包含要返回到宿主的信息。  
  
 向窗体添加以下类。  
  
 [!code-csharp[WpfHostingWindowsFormsControl#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/MyControls/MyControl1.cs#3)]
 [!code-vb[WpfHostingWindowsFormsControl#3](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/VisualBasic/MyControls/MyControl1.vb#3)]  
  
 用户单击**“OK”（确定）**或**“Cancel”（取消）**按钮时，<xref:System.Windows.Forms.Control.Click> 事件处理程序创建一个 `MyControlEventArgs` 对象，该对象包含这些数据并引发 `OnButtonClick` 事件。  两个处理程序的唯一区别在于事件参数的 `IsOK` 属性。  通过该属性，宿主可以确定单击了哪个按钮。  对于**“OK”（确定）**按钮，它设置为 `true`，对于**“Cancel”（取消）**按钮，则设置为 `false`。  下面的代码演示两个按钮处理程序。  
  
 向 `MyControl1` 类添加下面的代码。  
  
 [!code-csharp[WpfHostingWindowsFormsControl#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/MyControls/MyControl1.cs#4)]
 [!code-vb[WpfHostingWindowsFormsControl#4](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/VisualBasic/MyControls/MyControl1.vb#4)]  
  
### 为程序集赋予强名称并生成该程序集  
 若要使 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序引用该程序集，该程序集必须具有强名称。  若要创建强名称，请使用 Sn.exe 创建一个密钥文件并将其添加到项目中。  
  
1.  打开 [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)] 命令提示窗口。  为此，请单击**“开始”**菜单，然后依次选择**“所有程序”\/“Microsoft Visual Studio 2010”\/“Visual Studio 工具”\/“Visual Studio 命令提示”**。  这将启动一个控制台窗口，该窗口带有自定义的环境变量。  
  
2.  在命令提示符处，使用 `cd` 命令转至您的项目文件夹。  
  
3.  运行以下命令以生成一个名为 MyControls.snk 的密钥文件。  
  
    ```  
    Sn.exe -k MyControls.snk  
    ```  
  
4.  若要将密钥文件包括在项目中，请在解决方案资源管理器中右击项目名称，然后单击**“属性”**。  在项目设计器中，单击**“签名”**选项卡，选中**“为程序集签名”**复选框，然后浏览至您的密钥文件。  
  
5.  生成解决方案。  此生成行为将生成一个名为 MyControls.dll 的 DLL。  
  
## 实现 WPF 宿主应用程序  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 宿主应用程序使用 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 控件来承载 `MyControl1`。  该应用程序处理 `OnButtonClick` 事件以接收来自控件的数据。  它还具有选项按钮集合，可用于从 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序更改控件的一些属性。  下图演示已完成的应用程序。  
  
 ![嵌入在 WPF 页中的控件](../../../../docs/framework/wpf/advanced/media/avalonhost.png "AvalonHost")  
显示嵌入在 WPF 应用程序中的控件的完整应用程序  
  
### 创建项目  
 若要开始创建项目，请执行以下操作：  
  
1.  打开 [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)]，并选择**“新建项目”**。  
  
2.  在窗口类别中，选择**“WPF 应用程序”**模板。  
  
3.  将新项目命名为 `WpfHost`。  
  
4.  为位置指定包含 MyControls 项目的同一顶级文件夹。  
  
5.  单击**“确定”**创建项目。  
  
 您还需要添加对包含 `MyControl1` 和其他程序集的 DLL 的引用。  
  
1.  在解决方案资源管理器中右击项目名称，然后选择**“添加引用”**。  
  
2.  单击**“浏览”**选项卡，然后浏览到包含 MyControls.dll 的文件夹。  对于本演练，该文件夹为 MyControls\\bin\\Debug。  
  
3.  选择 MyControls.dll，然后单击**“确定”**。  
  
4.  添加一个对名为 WindowsFormsIntegration.dll 的 WindowsFormsIntegration 程序集的引用。  
  
### 实现基本布局  
 宿主应用程序的[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 在 MainWindow.xaml 中实现。  此文件包含定义布局并承载 [!INCLUDE[TLA2#tla_winforms](../../../../includes/tla2sharptla-winforms-md.md)]控件的[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 标记。  应用程序分为三个区域：  
  
-   **“控件属性”**面板，该面板包含可用于修改所承载控件的各个属性的选项按钮集合。  
  
-   **“来自控件的数据”**面板，该面板包含若干显示从所承载控件返回的数据的 <xref:System.Windows.Controls.TextBlock> 元素。  
  
-   所承载的控件自身。  
  
 下面的 XAML 显示了基本布局。  此示例省略了承载 `MyControl1` 所需的标记，但后面将对其进行讨论。  
  
 用以下内容替换 MainWindow.xaml 中的 XAML。  如果使用的是 Visual Basic，则将类更改为 `x:Class="MainWindow"`。  
  
 [!code-xml[WpfHostingWindowsFormsControl#100](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/WpfHost/Page1.xaml#100)]  
  
 第一个 <xref:System.Windows.Controls.StackPanel> 元素包含若干 <xref:System.Windows.Controls.RadioButton> 控件集，使用这些控件可以修改所承载控件的各个默认属性。  该元素之后是 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素，此元素承载 `MyControl1`。  最后的 <xref:System.Windows.Controls.StackPanel> 元素包含若干显示从所承载控件返回的数据的 <xref:System.Windows.Controls.TextBlock> 元素。  这些元素的排序以及 <xref:System.Windows.Controls.DockPanel.Dock%2A> 和 <xref:System.Windows.FrameworkElement.Height%2A> 特性设置无间隙并且不失真地将所承载的控件嵌入到窗口中。  
  
#### 承载控件  
 下面是上一个 XAML 的已编辑版本，重点说明承载 `MyControl1` 所需的元素。  
  
 [!code-xml[WpfHostingWindowsFormsControl#101](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/WpfHost/Page1.xaml#101)]  
[!code-xml[WpfHostingWindowsFormsControl#102](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/WpfHost/Page1.xaml#102)]  
  
 `xmlns` 命名空间映射特性创建一个对包含所承载控件的 `MyControls` 命名空间的引用。  通过该映射，可以在 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 中将 `MyControl1` 表示为 `<mcl:MyControl1>`。  
  
 此 XAML 中的以下两个元素处理承载：  
  
-   `WindowsFormsHost` 表示 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素，通过该元素可以在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序中承载 [!INCLUDE[TLA2#tla_winforms](../../../../includes/tla2sharptla-winforms-md.md)]控件。  
  
-   `mcl:MyControl1`，表示 `MyControl1`，它被添加到 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素的子集合。  因此，此 [!INCLUDE[TLA2#tla_winforms](../../../../includes/tla2sharptla-winforms-md.md)]控件呈现为 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 窗口的一部分，并且您可以从该应用程序与此控件通信。  
  
### 实现代码隐藏文件  
 代码隐藏文件 MainWindow.xaml.vb 或 MainWindow.xaml.cs 包含用于实现上一节中所述的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 功能的程序代码。  主要任务是：  
  
-   将一个事件处理程序附加到 `MyControl1` 的 `OnButtonClick` 事件。  
  
-   基于选项按钮集合的设置方式修改 `MyControl1` 的各个属性。  
  
-   显示由控件收集的数据。  
  
#### 初始化应用程序  
 初始化代码包含在窗口的 <xref:System.Windows.FrameworkElement.Loaded> 事件的事件处理程序中，并将事件处理程序附加到控件的 `OnButtonClick` 事件。  
  
 在 MainWindow.xaml.vb 或 MainWindow.xaml.cs 中，向 `MainWindow` 类添加以下代码。  
  
 [!code-csharp[WpfHostingWindowsFormsControl#11](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/WpfHost/Page1.xaml.cs#11)]
 [!code-vb[WpfHostingWindowsFormsControl#11](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/VisualBasic/WpfHost/Page1.xaml.vb#11)]  
  
 由于前面讨论的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 将 `MyControl1` 添加到了 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素的子元素集合中，因此您可以强制转换 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素的 <xref:System.Windows.Forms.Integration.WindowsFormsHost.Child%2A>，以获取对 `MyControl1` 的引用。  然后，可以使用该引用将事件处理程序附加到 `OnButtonClick`。  
  
 除了提供对控件自身的引用之外，<xref:System.Windows.Forms.Integration.WindowsFormsHost> 还公开控件的许多属性，您可以从该应用程序来操作这些属性。  初始化代码将这些值分配给私有全局变量，以便以后在应用程序中使用。  
  
 这样您就可以方便地访问 `MyControls` DLL 中的类型，将以下 `Imports` 或 `using` 语句添加到文件的顶部。  
  
```vb  
Imports MyControls  
```  
  
```csharp  
using MyControls;  
```  
  
#### 处理 OnButtonClick 事件  
 当用户单击控件的任何一个按钮时，`MyControl1` 将引发 `OnButtonClick` 事件。  
  
 向 `MainWindow` 类添加下面的代码。  
  
 [!code-csharp[WpfHostingWindowsFormsControl#12](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/WpfHost/Page1.xaml.cs#12)]
 [!code-vb[WpfHostingWindowsFormsControl#12](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/VisualBasic/WpfHost/Page1.xaml.vb#12)]  
  
 文本框中的数据将被打包到 `MyControlEventArgs` 对象中。  如果用户单击**“OK”（确定）**按钮，事件处理程序将提取数据，并在 `MyControl1` 下面的面板中显示这些数据。  
  
#### 修改控件的属性  
 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 元素公开所承载控件的若干默认属性。  因此，您可以更改控件的外观，以便与应用程序的样式更加匹配。  使用左侧面板中的选项按钮集合，可以修改若干颜色和字体属性。  每个按钮集合都有用于 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件的处理程序，该处理程序将检测用户的选项按钮选择，并更改控件上的相应属性。  
  
 向 `MainWindow` 类添加下面的代码。  
  
 [!code-csharp[WpfHostingWindowsFormsControl#13](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/WpfHost/Page1.xaml.cs#13)]
 [!code-vb[WpfHostingWindowsFormsControl#13](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/VisualBasic/WpfHost/Page1.xaml.vb#13)]  
  
 生成并运行应用程序。  在 Windows 窗体复合控件中添加一些文本，然后单击**“确定”**。  该文本会显示在标签中。  单击不同的单选按钮以查看对控件的效果。  
  
## 请参阅  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [WPF 设计器](http://msdn.microsoft.com/zh-cn/c6c65214-8411-4e16-b254-163ed4099c26)   
 [演练：在 WPF 中承载 Windows 窗体控件](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-windows-forms-control-in-wpf.md)   
 [演练：在 Windows 窗体中承载 WPF 复合控件](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)