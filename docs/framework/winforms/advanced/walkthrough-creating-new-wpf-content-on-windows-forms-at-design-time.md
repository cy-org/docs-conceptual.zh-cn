---
title: "演练：设计时在 Windows 窗体上创建新的 WPF 内容 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "ElementHost 控件"
  - "在 Windows 窗体中承载 WPF 内容"
  - "互操作性, WPF 和 Windows 窗体"
  - "WPF 内容, 在 Windows 窗体中承载"
  - "WPF 用户控件, 在 Windows 窗体中承载"
ms.assetid: 2e92d8e8-f0e4-4df7-9f07-2acf35cd798c
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 20
---
# 演练：设计时在 Windows 窗体上创建新的 WPF 内容
本主题显示如何创建 Windows Presentation Foundation \(WPF\) 控件，以便在基于 Windows 窗体的应用程序中使用。  
  
 在本演练中，你将要执行以下任务：  
  
-   创建项目。  
  
-   创建一个新的 WPF 控件。  
  
-   将新的 WPF 控件添加到 Windows 窗体。  WPF 控件承载在 <xref:System.Windows.Forms.Integration.ElementHost> 控件中。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关详细信息，请参阅 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
## 系统必备  
 你需要以下组件来完成本演练：  
  
-   [!INCLUDE[vs_orcas_long](../../../../includes/vs-orcas-long-md.md)]。  
  
## 创建项目  
 第一步是创建 Windows 窗体项目。  
  
> [!NOTE]
>  承载 WPF 内容时，仅支持 C\# 和 Visual Basic 项目。  
  
#### 创建项目  
  
-   在 Visual Basic 或 Visual C\# 中创建名为 `HostingWpf` 的新 Windows 窗体应用程序项目。  
  
## 创建新的 WPF 控件  
 创建新的 WPF 控件并将其添加到你的项目中，这与将任何其他项添加到你的项目中一样容易。  Windows 窗体设计器使用名为*复合控件*，或*用户控件*的特定类型控件。  有关 WPF 用户控件的详细信息，请参阅 <xref:System.Windows.Controls.UserControl>。  
  
> [!NOTE]
>  WPF 的 <xref:System.Windows.Controls.UserControl?displayProperty=fullName> 类型不同于 Windows 窗体提供的用户控件类型（也称为 <xref:System.Windows.Forms.UserControl?displayProperty=fullName>）。  
  
#### 创建新的 WPF 控件  
  
1.  在**解决方案资源管理器**中，将新的 **WPF 用户控件库**项目添加到解决方案中。  使用控件库默认名称 `WpfControlLibrary1`。  默认控件名称是 `UserControl1.xaml`。  
  
     添加新控件将产生以下影响。  
  
    -   添加文件 UserControl1.xaml。  
  
    -   添加文件 UserControl1.xaml.cs 或 UserControl1.xaml.vb。  此文件包含事件处理程序和其他实现的代码隐藏。  
  
    -   添加对 WPF 程序集的引用。  
  
    -   文件 UserControl1.xaml 在 [!INCLUDE[wpfdesigner_current_long](../../../../includes/wpfdesigner-current-long-md.md)] 中打开。  
  
2.  在设计视图中，请确保已选中 `UserControl1`。  有关详细信息，请参阅[如何：在设计图面上选择和移动元素](http://msdn.microsoft.com/zh-cn/54cb70b6-b35b-46e4-a0cc-65189399c474)。  
  
3.  在“属性”窗口中，将 <xref:System.Windows.FrameworkElement.Width%2A> 和 <xref:System.Windows.FrameworkElement.Height%2A> 属性的值设置为 `200`。  
  
4.  在“工具箱”中，将 <xref:System.Windows.Controls.TextBox?displayProperty=fullName> 控件拖到设计图面上。  
  
5.  在“属性”窗口中，将 <xref:System.Windows.Controls.TextBox.Text%2A> 属性的值设置为“承载的内容”。  
  
    > [!NOTE]
    >  一般情况下，你应承载更复杂的 WPF 内容。  此处，<xref:System.Windows.Controls.TextBox?displayProperty=fullName> 控件仅为了便于说明。  
  
6.  生成项目。  
  
## 将 WPF 控件添加到 Windows 窗体  
 新的 WPF 控件可供在窗体上使用。  Windows 窗体使用 <xref:System.Windows.Forms.Integration.ElementHost> 控件承载 WPF 内容  
  
#### 将 WPF 控件添加到 Windows 窗体  
  
1.  在 Windows 窗体设计器中打开 `Form1`。  
  
2.  在“工具箱”中，找到标记为“WPFUserControlLibrary WPF 用户控件”的选项卡。  
  
3.  将 `UserControl1` 的实例拖到窗体上。  
  
    -   在窗体上自动创建 <xref:System.Windows.Forms.Integration.ElementHost> 控件以承载 WPF 控件。  
  
    -   <xref:System.Windows.Forms.Integration.ElementHost> 控件被命名为 `elementHost1`，并且在“属性”窗口中，可以看到其 <xref:System.Windows.Forms.Integration.ElementHost.Child%2A> 属性被设置为 **UserControl1**。  
  
    -   将对 WPF 程序集的引用添加到项目。  
  
    -   `elementHost1` 控件具有显示可用承载选项的智能标记面板。  
  
4.  在“ElementHost 任务”智能标记面板中，选择“在父容器中停靠”。  
  
5.  按 F5 生成并运行该应用程序。  
  
## 后续步骤  
 Windows 窗体和 WPF 是不同的技术，但它们设计为可以密切地互操作。  若要在你的应用程序中提供更丰富的外观和行为，请尝试以下操作。  
  
-   在 WPF 页中承载 Windows 窗体控件。  有关详细信息，请参阅[演练：在 WPF 中承载 Windows 窗体控件](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-windows-forms-control-in-wpf.md)。  
  
-   将 Windows 窗体的视觉样式应用于你的 WPF 内容。  有关详细信息，请参阅[如何：在混合应用程序中启用视觉样式](../../../../docs/framework/wpf/advanced/how-to-enable-visual-styles-in-a-hybrid-application.md)。  
  
-   更改 WPF 内容的样式。  有关详细信息，请参阅[演练：设置 WPF 内容的样式](../../../../docs/framework/winforms/advanced/walkthrough-styling-wpf-content.md)。  
  
## 请参阅  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [迁移和互操作性](../../../../docs/framework/wpf/advanced/migration-and-interoperability.md)   
 [使用 WPF 控件](../../../../docs/framework/winforms/advanced/using-wpf-controls.md)   
 [WPF 设计器](http://msdn.microsoft.com/zh-cn/c6c65214-8411-4e16-b254-163ed4099c26)