---
title: "演练：在 Windows 窗体中承载 WPF 复合控件 | Microsoft Docs"
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
  - "在 Windows 窗体中承载 WPF 内容"
ms.assetid: 0ac41286-4c1b-4b17-9196-d985cb844ce1
caps.latest.revision: 34
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 31
---
# 演练：在 Windows 窗体中承载 WPF 复合控件
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 提供用于创建应用程序的丰富环境。  但是，如果您在 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]代码上有大量投入，那么更有效的办法可能是用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 来扩展现有的 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]应用程序，而不是从头开始重新编写应用程序。  常见的方案是将用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 实现的一个或多个控件嵌入 [!INCLUDE[TLA2#tla_winforms](../../../../includes/tla2sharptla-winforms-md.md)]应用程序。  有关自定义 WPF 控件的更多信息，请参见[控件自定义](../../../../docs/framework/wpf/controls/control-customization.md)。  
  
 本演练引导您创建一个应用程序，该应用程序承载 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]复合控件以在 [!INCLUDE[TLA2#tla_winforms](../../../../includes/tla2sharptla-winforms-md.md)]应用程序程序中执行数据输入。  该复合控件打包到一个 DLL 中。  该一般过程可以扩展到更复杂的应用程序和控件。  本演练的设计在外观与功能上与[演练：在 WPF 中承载 Windows 窗体复合控件](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)几乎完全相同。  主要区别在于承载方案是相反的。  
  
 本演练分为两部分。  第一部分简要介绍 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]复合控件的实现。  第二部分详细讨论如何在 [!INCLUDE[TLA2#tla_winforms](../../../../includes/tla2sharptla-winforms-md.md)]应用程序中承载该复合控件、从该控件接收事件以及访问该控件的一些属性。  
  
 本演练涉及以下任务：  
  
-   实现 WPF 复合控件。  
  
-   实现 Windows 窗体宿主应用程序。  
  
 有关本演练中所阐释任务的完整代码清单，请参见 [Hosting a WPF Composite Control in Windows Forms Sample](http://go.microsoft.com/fwlink/?LinkID=159996)（在 Windows 窗体中承载 WPF 复合控件示例）。  
  
## 必备组件  
 您需要以下组件来完成本演练：  
  
-   [!INCLUDE[vs_dev10_long](../../../../includes/vs-dev10-long-md.md)].  
  
## 实现 WPF 复合控件  
 本示例中使用的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 复合控件是一个简单的数据输入窗体，它接受用户的姓名和地址。  当用户单击两个按钮之一来指示任务已完成时，该控件引发一个自定义事件，将该信息返回到主机。  下图演示呈现的控件。  
  
 ![简单的 WPF 控件](../../../../docs/framework/wpf/advanced/media/avaloncontrol.png "AvalonControl")  
WPF 复合控件  
  
### 创建项目  
 若要开始创建项目，请执行以下操作：  
  
1.  启动 [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)]，打开**“新建项目”**对话框。  
  
2.  在 Visual C\# 和 Windows 类别中，选择**“WPF 用户控件库”**模板。  
  
3.  将新项目命名为 `MyControls`。  
  
4.  为位置指定一个便于命名的顶级文件夹，如 `WindowsFormsHostingWpfControl`。  稍后会将宿主应用程序放入此文件夹中。  
  
5.  单击**“确定”**创建项目。  默认项目包含一个名为 `UserControl1` 的控件。  
  
6.  在解决方案资源管理器中，将 `UserControl1` 重命名为 `MyControl1`。  
  
 您的项目应当具有对以下系统 DLL 的引用。  如果其中有任何 DLL 默认情况下未包括在您的项目中，请将它添加到您的项目中。  
  
-   PresentationCore  
  
-   PresentationFramework  
  
-   系统  
  
-   WindowsBase  
  
### 创建用户界面  
 复合控件的[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 是通过[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 实现的。  复合控件 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 由五个 <xref:System.Windows.Controls.TextBox> 元素组成。  每个 <xref:System.Windows.Controls.TextBox> 元素都有一个充当标签的关联 <xref:System.Windows.Controls.TextBlock> 元素。  底部有两个 <xref:System.Windows.Controls.Button> 元素，它们是**“OK”（确定）**和**“Cancel”（取消）**。  当用户单击其中任何一个按钮时，控件将引发一个自定义事件，将该信息返回到主机。  
  
#### 基本布局  
 多个不同的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 元素包含在一个 <xref:System.Windows.Controls.Grid> 元素中。  可以使用 <xref:System.Windows.Controls.Grid> 排列复合控件的内容，此方式与使用 HTML 中的 `Table` 元素大致相同。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 还有一个 <xref:System.Windows.Documents.Table> 元素，但 <xref:System.Windows.Controls.Grid> 更小巧，因而更适于简单的布局任务。  
  
 下面的 XAML 显示了基本布局。  此 XAML 指定 <xref:System.Windows.Controls.Grid> 元素中的列数和行数，从而定义控件的整体结构。  
  
 在 MyControl1.xaml 中，将现有 XAML 替换为以下 XAML。  
  
 [!code-xml[WindowsFormsHostingWpfControl#101](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/MyControls/Page1.xaml#101)]  
[!code-xml[WindowsFormsHostingWpfControl#102](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/MyControls/Page1.xaml#102)]  
  
#### 向 Grid 中添加 TextBlock 和 TextBox 元素  
 在网格中放入一个 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 元素，并将该元素的 <xref:System.Windows.Controls.Grid.RowProperty> 特性和 <xref:System.Windows.Controls.Grid.ColumnProperty> 特性设置为适当的行号和列号。  请记住行号和列号是从零开始的。  通过设置元素的 <xref:System.Windows.Controls.Grid.ColumnSpanProperty> 特性，可以使该元素跨多列。  有关 <xref:System.Windows.Controls.Grid> 元素的更多信息，请参见[创建网格元素](../../../../docs/framework/wpf/controls/how-to-create-a-grid-element.md)。  
  
 下面的 XAML 演示复合控件的 <xref:System.Windows.Controls.TextBox> 和 <xref:System.Windows.Controls.TextBlock> 元素及其 <xref:System.Windows.Controls.Grid.RowProperty> 和 <xref:System.Windows.Controls.Grid.ColumnProperty> 特性（设置这些特性是为了使元素在网格中正确定位）。  
  
 在 MyControl1.xaml 中，将以下 XAML 添加到 <xref:System.Windows.Controls.Grid> 元素中。  
  
 [!code-xml[WindowsFormsHostingWpfControl#103](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/MyControls/Page1.xaml#103)]  
  
#### 设置 UI 元素的样式  
 数据输入窗体上的许多元素都有类似的外观，这意味着它们在几个属性的设置方面是完全相同的。  上面的 XAML 使用 <xref:System.Windows.Style> 元素定义元素类的标准属性设置，而不是分别设置每个元素的特性。  此方法降低了控件的复杂度，并使您可以通过一个样式特性改变多个元素的外观。  
  
 <xref:System.Windows.Style> 元素包含在 <xref:System.Windows.Controls.Grid> 元素的 <xref:System.Windows.FrameworkElement.Resources%2A> 属性中，因此可供控件中的所有元素使用。  如果对样式进行命名，则可通过添加一个设置为该样式的名称的 <xref:System.Windows.Style> 元素来将该样式应用于元素。  未命名的样式将成为元素的默认样式。  有关 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 样式的更多信息，请参见[样式设置和模板化](../../../../docs/framework/wpf/controls/styling-and-templating.md)。  
  
 下面的 XAML 演示复合控件的 <xref:System.Windows.Style> 元素。  若要查看样式是如何应用于元素的，请参见上面的 XAML。  例如，最后一个 <xref:System.Windows.Controls.TextBlock> 元素具有 `inlineText` 样式，最后一个 <xref:System.Windows.Controls.TextBox> 元素使用默认样式。  
  
 在 MyControl1.xaml 中的 <xref:System.Windows.Controls.Grid> 开始元素之后，紧接着添加以下 XAML。  
  
 [!code-xml[WindowsFormsHostingWpfControl#104](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/MyControls/Page1.xaml#104)]  
  
#### 添加“OK”（确定）和“Cancel”（取消）按钮  
 复合控件的最后两个元素是**“OK”（确定）**和**“Cancel”（取消）**<xref:System.Windows.Controls.Button> 元素，它们占据 <xref:System.Windows.Controls.Grid> 的最后一行的前两列。  这些元素使用常用事件处理程序 `ButtonClicked`，以及在前面的 XAML 中定义的默认 <xref:System.Windows.Controls.Button> 样式。  
  
 在 MyControl1.xaml 中的最后一个 <xref:System.Windows.Controls.TextBox> 元素之后，添加以下 XAML。  复合控件的 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 部分现已完成。  
  
 [!code-xml[WindowsFormsHostingWpfControl#105](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/MyControls/Page1.xaml#105)]  
  
### 实现代码隐藏文件  
 代码隐藏文件 MyControl1.xaml.cs 实现三个基本任务：  
  
1.  处理当用户单击某个按钮时发生的事件。  
  
2.  从 <xref:System.Windows.Controls.TextBox> 元素中检索数据，并将它们打包在一个自定义的事件参数对象中。  
  
3.  引发自定义的 `OnButtonClick` 事件，通知主机用户已完成并将数据传回主机。  
  
 该控件还公开许多颜色和字体属性，使您可以更改外观。  与用于承载 [!INCLUDE[TLA2#tla_winforms](../../../../includes/tla2sharptla-winforms-md.md)]控件的 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 类不同，<xref:System.Windows.Forms.Integration.ElementHost> 类仅公开控件的 <xref:System.Windows.Controls.Panel.Background%2A> 属性。  为了保持本代码示例与[演练：在 WPF 中承载 Windows 窗体复合控件](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)中讨论的示例的相似性，该控件直接公开其余的属性。  
  
#### 代码隐藏文件的基本结构  
 代码隐藏文件包含一个命名空间 `MyControls`，该命名空间包含两个类，即 `MyControl1` 和 `MyControlEventArgs`。  
  
```  
  
namespace MyControls  
{  
  public partial class MyControl1 : Grid  
  {  
    //...  
  }  
  public class MyControlEventArgs : EventArgs  
  {  
    //...  
  }  
}  
  
```  
  
 第一个类 `MyControl1` 是一个分部类，它包含实现在 MyControl1.xaml 中定义的 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 的功能的代码。  当分析 MyControl1.xaml 时，[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 会转换为相同的分部类，两个分部类会合并以组成编译后的控件。  因此，代码隐藏文件中的类名必须与分配给 MyControl1.xaml 的类名匹配，并且它必须继承自控件的根元素。  第二个类 `MyControlEventArgs` 是一个事件参数类，用于将数据发回主机。  
  
 打开 MyControl1.xaml.cs。  更改现有类声明，使其具有以下名称并从 <xref:System.Windows.Controls.Grid> 继承。  
  
 [!code-csharp[WindowsFormsHostingWpfControl#21](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/MyControls/Page1.xaml.cs#21)]  
  
#### 初始化控件  
 下面的代码实现几个基本任务：  
  
-   声明一个私有事件 `OnButtonClick` 以及它的关联委托 `MyControlEventHandler`。  
  
-   创建几个存储用户数据的私有全局变量。  这些数据是通过对应的属性公开的。  
  
-   为控件的 <xref:System.Windows.FrameworkElement.Loaded> 事件实现一个处理程序 `Init`。  此处理程序通过将 MyControl1.xaml 中定义的值赋给全局变量来初始化这些变量。  为此，它使用指定给典型 <xref:System.Windows.Controls.TextBlock> 元素 `nameLabel` 的 <xref:System.Windows.FrameworkElement.Name%2A> 来访问该元素的属性设置。  
  
 删除现有构造函数并向 `MyControl1` 类添加以下代码。  
  
 [!code-csharp[WindowsFormsHostingWpfControl#11](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/MyControls/Page1.xaml.cs#11)]  
  
#### 处理按钮的 Click 事件  
 用户通过单击**“OK”（确定）**按钮或**“Cancel”（取消）**按钮来指示数据输入任务已完成。  两个按钮使用相同的 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> 事件处理程序 `ButtonClicked`。  两个按钮均有一个名称，即 `btnOK` 或 `btnCancel`，这样处理程序就可以通过检查 `sender` 参数的值来确定单击的是哪个按钮。  处理程序执行以下操作：  
  
-   创建一个 `MyControlEventArgs` 对象，该对象包含来自于 <xref:System.Windows.Controls.TextBox> 元素的数据。  
  
-   如果用户单击**“Cancel”（取消）**按钮，将 `MyControlEventArgs` 对象的 `IsOK` 属性设置为 `false`。  
  
-   引发 `OnButtonClick` 事件，该事件通知主机用户已完成并传回所收集的数据。  
  
 在 `MyControl1` 类的 `Init` 方法后面添加下面的代码。  
  
 [!code-csharp[WindowsFormsHostingWpfControl#12](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/MyControls/Page1.xaml.cs#12)]  
  
#### 创建属性  
 该类的其余部分仅仅公开与前面讨论的全局变量对应的属性。  当属性更改时，set 访问器通过更改对应的元素属性并更新底层的全局变量来修改控件的外观。  
  
 将下面的代码添加到 `MyControl1` 类中。  
  
 [!code-csharp[WindowsFormsHostingWpfControl#13](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/MyControls/Page1.xaml.cs#13)]  
  
#### 将数据发回主机  
 文件中的最后一个组件是 `MyControlEventArgs` 类，它用于将所收集的数据发回主机。  
  
 将下面的代码添加到 `MyControls` 命名空间。  具体实现非常简单，不在这里进一步讨论。  
  
 [!code-csharp[WindowsFormsHostingWpfControl#14](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/MyControls/Page1.xaml.cs#14)]  
  
 生成解决方案。  此生成行为将生成一个名为 MyControls.dll 的 DLL。  
  
<a name="winforms_host_section"></a>   
## 实现 Windows 窗体宿主应用程序  
 [!INCLUDE[TLA2#tla_winforms](../../../../includes/tla2sharptla-winforms-md.md)]宿主应用程序使用 <xref:System.Windows.Forms.Integration.ElementHost> 对象承载 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 复合控件。  该应用程序处理 `OnButtonClick` 事件以接收来自复合控件的数据。  该应用程序还具有一组选项按钮，供您用来修改控件的外观。  下图显示了该应用程序。  
  
 ![Windows 窗体承载 Avalon 控件](../../../../docs/framework/wpf/advanced/media/wfhost.png "WFHost")  
在 Windows 窗体应用程序中承载的 WPF 复合控件  
  
### 创建项目  
 若要开始创建项目，请执行以下操作：  
  
1.  启动 [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)]，打开**“新建项目”**对话框。  
  
2.  在 Visual C\# 和 Windows 类别中，选择**“Windows 窗体应用程序”**模板。  
  
3.  将新项目命名为 `WFHost`。  
  
4.  为位置指定包含 MyControls 项目的同一顶级文件夹。  
  
5.  单击**“确定”**创建项目。  
  
 您还需要添加对包含 `MyControl1` 和其他程序集的 DLL 的引用。  
  
1.  在解决方案资源管理器中右击项目名称，然后选择**“添加引用”**。  
  
2.  单击**“浏览”**选项卡，然后浏览到包含 MyControls.dll 的文件夹。  对于本演练，该文件夹为 MyControls\\bin\\Debug。  
  
3.  选择 MyControls.dll，然后单击**“确定”**。  
  
4.  添加对下列程序集的引用。  
  
    -   PresentationCore  
  
    -   PresentationFramework  
  
    -   System.Xaml  
  
    -   WindowsBase  
  
    -   WindowsFormsIntegration  
  
### 实现应用程序的用户界面  
 Windows 窗体应用程序的 UI 包含几个用于与 WPF 复合控件交互的控件。  
  
1.  在 Windows 窗体设计器中打开 Form1。  
  
2.  扩展窗体以容纳控件。  
  
3.  在窗体的右上角添加一个 <xref:System.Windows.Forms.Panel?displayProperty=fullName> 控件以容纳 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 复合控件。  
  
4.  将以下 <xref:System.Windows.Forms.GroupBox?displayProperty=fullName> 控件添加到窗体中。  
  
    |名称|Text|  
    |--------|----------|  
    |groupBox1|Background Color|  
    |groupBox2|Foreground Color|  
    |groupBox3|Font Size|  
    |groupBox4|Font Family|  
    |groupBox5|Font Style|  
    |groupBox6|Font Weight|  
    |groupBox7|Data from control|  
  
5.  将以下 <xref:System.Windows.Forms.RadioButton?displayProperty=fullName> 控件添加到 <xref:System.Windows.Forms.GroupBox?displayProperty=fullName> 控件中。  
  
    |GroupBox|名称|Text|  
    |--------------|--------|----------|  
    |groupBox1|radioBackgroundOriginal|Original|  
    |groupBox1|radioBackgroundLightGreen|LightGreen|  
    |groupBox1|radioBackgroundLightSalmon|LightSalmon|  
    |groupBox2|radioForegroundOriginal|Original|  
    |groupBox2|radioForegroundRed|Red|  
    |groupBox2|radioForegroundYellow|Yellow|  
    |groupBox3|radioSizeOriginal|Original|  
    |groupBox3|radioSizeTen|10|  
    |groupBox3|radioSizeTwelve|12|  
    |groupBox4|radioFamilyOriginal|Original|  
    |groupBox4|radioFamilyTimes|Times New Roman|  
    |groupBox4|radioFamilyWingDings|WingDings|  
    |groupBox5|radioStyleOriginal|Normal|  
    |groupBox5|radioStyleItalic|Italic|  
    |groupBox6|radioWeightOriginal|Original|  
    |groupBox6|radioWeightBold|Bold|  
  
6.  将以下 <xref:System.Windows.Forms.Label?displayProperty=fullName> 控件添加到最后一个 <xref:System.Windows.Forms.GroupBox?displayProperty=fullName> 中。  这些控件显示 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 复合控件返回的数据。  
  
    |GroupBox|名称|Text|  
    |--------------|--------|----------|  
    |groupBox7|lblName|Name:|  
    |groupBox7|lblAddress|Street Address:|  
    |groupBox7|lblCity|City:|  
    |groupBox7|lblState|State:|  
    |groupBox7|lblZip|Zip:|  
  
### 初始化窗体  
 通常在窗体的 <xref:System.Windows.Forms.Form.Load> 事件处理程序中实现承载代码。  下面的代码演示 <xref:System.Windows.Forms.Form.Load> 事件处理程序（[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 复合控件的 <xref:System.Windows.FrameworkElement.Loaded> 事件的处理程序），以及后面使用的几个全局变量的声明。  
  
 在 Windows 窗体设计器中，双击窗体创建一个 <xref:System.Windows.Forms.Form.Load> 事件处理程序。  在 Form1.cs 顶部添加以下 `using` 语句。  
  
 [!code-csharp[WindowsFormsHostingWpfControl#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/WFHost/Form1.cs#10)]  
  
 用下面的代码替换现有 `Form1` 类的内容。  
  
 [!code-csharp[WindowsFormsHostingWpfControl#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/WFHost/Form1.cs#2)]  
  
 前面的代码中的 `Form1_Load` 方法演示了承载 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件的常规过程：  
  
1.  创建一个新的 <xref:System.Windows.Forms.Integration.ElementHost> 对象。  
  
2.  将控件的 <xref:System.Windows.Forms.Control.Dock%2A> 属性设置为 <xref:System.Windows.Forms.DockStyle?displayProperty=fullName>。  
  
3.  将 <xref:System.Windows.Forms.Integration.ElementHost> 控件添加到 <xref:System.Windows.Forms.Panel> 控件的 <xref:System.Windows.Forms.Control.Controls%2A> 集合。  
  
4.  创建 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件的一个实例。  
  
5.  在窗体中承载该复合控件，方法是：将该控件分配给 <xref:System.Windows.Forms.Integration.ElementHost> 控件的 <xref:System.Windows.Forms.Integration.ElementHost.Child%2A> 属性。  
  
 `Form1_Load` 方法中的余下两行向两个控件事件附加处理程序：  
  
-   `OnButtonClick` 是一个自定义事件，当用户单击**“OK”（确定）**或**“Cancel”（取消）**按钮时，复合控件将触发该事件。  您处理该事件，以获取用户响应并收集用户指定的任何数据。  
  
-   <xref:System.Windows.FrameworkElement.Loaded> 是一个标准事件，当 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件已完全加载时将引发该事件。  此处使用该事件是因为示例需要使用控件的属性初始化几个全局变量。  在窗体的 <xref:System.Windows.Forms.Form.Load> 事件发生时，控件未完全加载，这些值仍设置为 `null`。  您需要一直等到控件的 <xref:System.Windows.FrameworkElement.Loaded> 事件发生，然后才能访问这些属性。  
  
 <xref:System.Windows.FrameworkElement.Loaded> 事件处理程序显示在前面的代码中。  `OnButtonClick` 处理程序在下一节讨论。  
  
### 处理 OnButtonClick  
 当用户单击**“OK”（确定）**或**“Cancel”（取消）**按钮时，会发生 `OnButtonClick` 事件。  
  
 事件处理程序检查事件参数的 `IsOK` 字段，确定单击的是哪个按钮。  `lbl`*data* 变量与前面讨论的 <xref:System.Windows.Forms.Label> 控件对应。  如果用户单击**“OK”（确定）**按钮，来自该控件的 <xref:System.Windows.Controls.TextBox> 控件中的数据将分配给对应的 <xref:System.Windows.Forms.Label> 控件。  如果用户单击**“Cancel”（取消）**，则 <xref:System.Windows.Forms.Label.Text%2A> 值将设置为默认字符串。  
  
 将下面的按钮单击事件处理程序代码添加到 `Form1` 类。  
  
 [!code-csharp[WindowsFormsHostingWpfControl#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/WFHost/Form1.cs#3)]  
  
 生成并运行应用程序。  在 WPF 复合控件中添加一些文本，然后单击**“OK”（确定）**。  该文本会显示在标签中。  此时，尚未添加用于处理单选按钮的代码。  
  
### 修改控件外观  
 使用窗体上的 <xref:System.Windows.Forms.RadioButton> 控件，用户可以更改 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 复合控件的前景和背景颜色以及几个字体属性。  背景色由 <xref:System.Windows.Forms.Integration.ElementHost> 对象公开。  其余属性作为控件的自定义属性公开。  
  
 双击窗体上的每个 <xref:System.Windows.Forms.RadioButton> 控件以创建 <xref:System.Windows.Forms.RadioButton.CheckedChanged> 事件处理程序。  使用下面的代码替换 <xref:System.Windows.Forms.RadioButton.CheckedChanged> 事件处理程序。  
  
 [!code-csharp[WindowsFormsHostingWpfControl#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/WFHost/Form1.cs#4)]  
  
 生成并运行应用程序。  单击不同的单选按钮以查看对 WPF 复合控件的影响。  
  
## 请参阅  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [WPF 设计器](http://msdn.microsoft.com/zh-cn/c6c65214-8411-4e16-b254-163ed4099c26)   
 [演练：在 WPF 中承载 Windows 窗体复合控件](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)   
 [演练：在 Windows 窗体中承载 3\-D WPF 复合控件](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-3-d-wpf-composite-control-in-windows-forms.md)