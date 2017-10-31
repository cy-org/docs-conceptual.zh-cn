---
title: "演练：绑定到混合应用程序中的数据 | Microsoft Docs"
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
  - "数据绑定 [WPF 互操作性]"
  - "混合应用程序 [WPF 互操作性]"
ms.assetid: 18997e71-745a-4425-9c69-2cbce1d8669e
caps.latest.revision: 39
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 36
---
# 演练：绑定到混合应用程序中的数据
无论您使用的是 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]还是 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]，将数据源绑定到控件都是向用户提供基础数据访问所必需的。  本演练演示如何在同时包括 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]和 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件的混合应用程序中使用数据绑定。  
  
 本演练涉及以下任务：  
  
-   创建项目。  
  
-   定义数据模板。  
  
-   指定窗体布局。  
  
-   指定数据绑定。  
  
-   使用互操作功能来显示数据。  
  
-   向项目添加数据源。  
  
-   绑定到数据源。  
  
 有关本演练中所阐释任务的完整代码清单，请参见 [Data Binding in Hybrid Applications Sample](http://go.microsoft.com/fwlink/?LinkID=159983)（混合应用程序中的数据绑定示例）。  
  
 在完成本演练后，您将对混合应用程序中的数据绑定功能有了一定了解。  
  
## 系统必备  
 您需要以下组件来完成本演练：  
  
-   [!INCLUDE[vs_dev10_long](../../../../includes/vs-dev10-long-md.md)].  
  
-   对 Microsoft SQL Server 上运行的 Northwind 示例数据库的访问权限。  
  
## 创建项目  
  
#### 创建和设置项目  
  
1.  创建一个名为 `WPFWithWFAndDatabinding` 的 WPF 应用程序项目。  
  
2.  在解决方案资源管理器中，添加对以下程序集的引用。  
  
    -   WindowsFormsIntegration  
  
    -   System.Windows.Forms  
  
3.  在 [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)]中打开 MainWindow.xaml。  
  
4.  在 <xref:System.Windows.Window> 元素中，添加以下 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]命名空间映射。  
  
    ```xaml  
    xmlns:wf="clr-namespace:System.Windows.Forms;assembly=System.Windows.Forms"  
    ```  
  
5.  通过分配 <xref:System.Windows.FrameworkElement.Name%2A> 属性来将默认的 <xref:System.Windows.Controls.Grid> 元素命名为 `mainGrid`。  
  
     [!code-xml[WPFWithWFAndDatabinding#8](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml#8)]  
  
## 定义数据模板  
 客户的主列表显示在 <xref:System.Windows.Controls.ListBox> 控件中。  下面的代码示例定义一个名为 `ListItemsTemplate` 的 <xref:System.Windows.DataTemplate> 对象，该对象控制 <xref:System.Windows.Controls.ListBox> 控件的可视化树。  这个 <xref:System.Windows.DataTemplate> 分配给 <xref:System.Windows.Controls.ListBox> 控件的 <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> 属性。  
  
#### 定义数据模板  
  
-   将下面的 XAML 复制到 <xref:System.Windows.Controls.Grid> 元素的声明中。  
  
     [!code-xml[WPFWithWFAndDatabinding#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml#3)]  
  
## 指定窗体布局  
 窗体的布局由一个包含三行和三列的网格来定义。  <xref:System.Windows.Controls.Label> 控件旨在标识 Customers 表中的每一列。  
  
#### 设置网格布局  
  
-   将下面的 XAML 复制到 <xref:System.Windows.Controls.Grid> 元素的声明中。  
  
     [!code-xml[WPFWithWFAndDatabinding#4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml#4)]  
  
#### 设置 Label 控件  
  
-   将下面的 XAML 复制到 <xref:System.Windows.Controls.Grid> 元素的声明中。  
  
     [!code-xml[WPFWithWFAndDatabinding#5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml#5)]  
  
## 指定数据绑定  
 客户的主列表显示在 <xref:System.Windows.Controls.ListBox> 控件中。  所附加的 `ListItemsTemplate` 将 <xref:System.Windows.Controls.TextBlock> 控件绑定到数据库中的 `ContactName` 字段。  
  
 每个客户记录的详细信息都显示在多个 <xref:System.Windows.Controls.TextBox> 控件中。  
  
#### 指定数据绑定  
  
-   将下面的 XAML 复制到 <xref:System.Windows.Controls.Grid> 元素的声明中。  
  
     <xref:System.Windows.Data.Binding> 类将 <xref:System.Windows.Controls.TextBox> 控件绑定到数据库中的相应字段。  
  
     [!code-xml[WPFWithWFAndDatabinding#6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml#6)]  
  
## 使用互操作功能来显示数据  
 与选定客户相对应的订单显示在一个名为 `dataGridView1` 的 <xref:System.Windows.Forms.DataGridView?displayProperty=fullName> 控件中。  `dataGridView1` 控件绑定到代码隐藏文件中的数据源。  <xref:System.Windows.Forms.Integration.WindowsFormsHost> 控件是这个 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件的父级。  
  
#### 在 DataGridView 控件中显示数据  
  
-   将下面的 XAML 复制到 <xref:System.Windows.Controls.Grid> 元素的声明中。  
  
     [!code-xml[WPFWithWFAndDatabinding#7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml#7)]  
  
## 向项目添加数据源  
 使用 [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)]，可以方便地向项目中添加数据源。  此过程会向项目中添加一个强类型数据集，  还将添加其他多个支持类（如面向每个所选表的表适配器）。  
  
#### 添加数据源  
  
1.  从**“数据”**菜单中，选择**“添加新数据源”**。  
  
2.  在**“数据源配置向导”**中，使用数据集创建到 Northwind 数据库的连接。  有关更多信息，请参见[如何：连接到数据库中的数据](../Topic/How%20to:%20Connect%20to%20Data%20in%20a%20Database.md)。  
  
3.  在收到**“数据源配置向导”**的提示时，请将连接字符串另存为 `NorthwindConnectionString`。  
  
4.  当提示您选择数据库对象时，选择 `Customers` 和 `Orders` 表，并将生成的数据集命名为 `NorthwindDataSet`。  
  
## 绑定到数据源  
 <xref:System.Windows.Forms.BindingSource?displayProperty=fullName> 组件为应用程序的数据源提供了一个统一接口。  到数据源的绑定是在代码隐藏文件中实现的。  
  
#### 绑定到数据源  
  
1.  打开名为 MainWindow.xaml.vb 或 MainWindow.xaml.cs 的代码隐藏文件。  
  
2.  将下面的代码复制到 `MainWindow` 类定义中。  
  
     此代码声明 <xref:System.Windows.Forms.BindingSource> 组件以及连接到此数据库并与该组件相关联的帮助器类。  
  
     [!code-csharp[WPFWithWFAndDatabinding#11](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml.cs#11)]
     [!code-vb[WPFWithWFAndDatabinding#11](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFWithWFAndDatabinding/VisualBasic/WPFWithWFAndDatabinding/Window1.xaml.vb#11)]  
  
3.  将下面的代码复制到构造函数中。  
  
     此代码创建并初始化 <xref:System.Windows.Forms.BindingSource> 组件。  
  
     [!code-csharp[WPFWithWFAndDatabinding#12](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml.cs#12)]
     [!code-vb[WPFWithWFAndDatabinding#12](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFWithWFAndDatabinding/VisualBasic/WPFWithWFAndDatabinding/Window1.xaml.vb#12)]  
  
4.  打开 MainWindow.xaml。  
  
5.  在设计视图或 XAML 视图中，选择 <xref:System.Windows.Window> 元素。  
  
6.  在“属性”窗口中，单击**“事件”**选项卡。  
  
7.  双击 <xref:System.Windows.FrameworkElement.Loaded> 事件。  
  
8.  将下面的代码复制到 <xref:System.Windows.FrameworkElement.Loaded> 事件处理程序中。  
  
     此代码将 <xref:System.Windows.Forms.BindingSource> 组件作为数据上下文进行分配并填充 `Customers` 和 `Orders` 适配器对象。  
  
     [!code-csharp[WPFWithWFAndDatabinding#13](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml.cs#13)]
     [!code-vb[WPFWithWFAndDatabinding#13](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFWithWFAndDatabinding/VisualBasic/WPFWithWFAndDatabinding/Window1.xaml.vb#13)]  
  
9. 将下面的代码复制到 `MainWindow` 类定义中。  
  
     此方法处理 <xref:System.Windows.Data.CollectionView.CurrentChanged> 事件并更新数据绑定的当前项。  
  
     [!code-csharp[WPFWithWFAndDatabinding#14](../../../../samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml.cs#14)]
     [!code-vb[WPFWithWFAndDatabinding#14](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/WPFWithWFAndDatabinding/VisualBasic/WPFWithWFAndDatabinding/Window1.xaml.vb#14)]  
  
10. 按 F5 生成并运行该应用程序。  
  
## 请参阅  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [WPF 设计器](http://msdn.microsoft.com/zh-cn/c6c65214-8411-4e16-b254-163ed4099c26)   
 [Data Binding in Hybrid Applications Sample](http://go.microsoft.com/fwlink/?LinkID=159983)   
 [演练：在 WPF 中承载 Windows 窗体复合控件](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)   
 [演练：在 Windows 窗体中承载 WPF 复合控件](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)