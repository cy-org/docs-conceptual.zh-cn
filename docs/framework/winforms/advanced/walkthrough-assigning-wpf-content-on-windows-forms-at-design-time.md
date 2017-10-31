---
title: "演练：设计时在 Windows 窗体上分配 WPF 内容 | Microsoft Docs"
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
  - "ElementHost 控件, 在设计时分配 WPF 内容"
  - "互操作性 [WPF]"
  - "Windows 窗体, 内容分配"
  - "WPF 内容 [Windows 窗体], 在设计时分配"
  - "WPF 用户控件, 在 Windows 窗体中承载"
ms.assetid: b3e9ef93-7e0f-4a2f-8f1e-3437609a1eb7
caps.latest.revision: 18
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 18
---
# 演练：设计时在 Windows 窗体上分配 WPF 内容
本演练展示了如何选择要在窗体上显示的 Windows Presentation Foundation \(WPF\) 控件类型。  可选择项目中包含的任何 WPF 控件类型。  
  
 在本演练中，你将要执行以下任务：  
  
-   创建项目。  
  
-   创建 WPF 控件类型。  
  
-   选择 WPF 控件。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关详细信息，请参阅 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
## 系统必备  
 你需要以下组件来完成本演练：  
  
-   [!INCLUDE[vs_dev11_long](../../../../includes/vs-dev11-long-md.md)]。  
  
## 创建项目  
 第一步是创建 Windows 窗体项目。  
  
> [!NOTE]
>  承载 WPF 内容时，仅支持 C\# 和 Visual Basic 项目。  
  
#### 创建项目  
  
-   在 Visual Basic 或 Visual C\# 中创建名为 `SelectingWpfContent` 的新 Windows 窗体应用程序项目。  
  
## 创建 WPF 控件类型  
 将 WPF 控件类型添加到项目后，可将其托管到不同的 <xref:System.Windows.Forms.Integration.ElementHost> 控件。  
  
#### 创建 WPF 控件类型  
  
1.  将新的 WPF <xref:System.Windows.Controls.UserControl> 项目添加到解决方案。  使用控件类型的默认名称，`UserControl1.xaml`。  有关详细信息，请参阅[演练：设计时在 Windows 窗体上创建新的 WPF 内容](../../../../docs/framework/winforms/advanced/walkthrough-creating-new-wpf-content-on-windows-forms-at-design-time.md)。  
  
2.  在设计视图中，请确保已选中 `UserControl1`。  有关详细信息，请参阅[如何：在设计图面上选择和移动元素](http://msdn.microsoft.com/zh-cn/54cb70b6-b35b-46e4-a0cc-65189399c474)。  
  
3.  在“属性”窗口中，将 <xref:System.Windows.FrameworkElement.Width%2A> 和 <xref:System.Windows.FrameworkElement.Height%2A> 属性的值设置为 `200`。  
  
4.  将 <xref:System.Windows.Controls.TextBox?displayProperty=fullName> 控件添加到 <xref:System.Windows.Controls.UserControl>，并将 <xref:System.Windows.Controls.TextBox.Text%2A> 属性的值设置为“所承载的内容”。  
  
5.  将第二个 WPF <xref:System.Windows.Controls.UserControl> 添加到项目。  使用控件类型的默认名称，`UserControl2.xaml`。  
  
6.  在“属性”窗口中，将 <xref:System.Windows.FrameworkElement.Width%2A> 和 <xref:System.Windows.FrameworkElement.Height%2A> 属性的值设置为 `200`。  
  
7.  将 <xref:System.Windows.Controls.TextBox?displayProperty=fullName> 控件添加到 <xref:System.Windows.Controls.UserControl>，并将 <xref:System.Windows.Controls.TextBox.Text%2A> 属性的值设置为“所承载的内容 2”。  
  
 **注意** 一般情况下，你应承载更复杂的 WPF 内容。  此处，<xref:System.Windows.Controls.TextBox?displayProperty=fullName> 控件仅为了便于说明。  
  
1.  生成项目。  
  
## 选择 WPF 控件  
 可将不同的 WPF 内容分配到 <xref:System.Windows.Forms.Integration.ElementHost> 控件，该控件现已承载内容。  
  
#### 选择 WPF 控件  
  
1.  在 Windows 窗体设计器中打开 `Form1`。  
  
2.  在“工具箱”中，双击 `UserControl1` 在窗体上创建 `UserControl1` 的实例。  
  
     `UserControl1` 的实例托管在名为 `elementHost1` 的新 <xref:System.Windows.Forms.Integration.ElementHost> 控件中。  
  
3.  在 `elementHost1` 的智能标记面板中，打开**选择承载的内容**下拉列表。  
  
4.  从下拉列表框中选择 **UserControl2**。  
  
     `elementHost1` 控件现承载 `UserControl2` 类型的实例。  
  
5.  在**属性**窗口中，请确认将 <xref:System.Windows.Forms.Integration.ElementHost.Child%2A> 属性设置为 **UserControl2**。  
  
6.  在“工具箱”中，请在“WPF 互操作性”组中，将 <xref:System.Windows.Forms.Integration.ElementHost> 控件拖放到窗体上。  
  
     新控件的默认名称是 `elementHost2`。  
  
7.  在 `elementHost2` 的智能标记面板中，打开**选择承载的内容**下拉列表。  
  
8.  从下拉列表中选择 **UserControl1**。  
  
9. `elementHost2` 控件现承载 `UserControl1` 类型的实例。  
  
## 请参阅  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [迁移和互操作性](../../../../docs/framework/wpf/advanced/migration-and-interoperability.md)   
 [使用 WPF 控件](../../../../docs/framework/winforms/advanced/using-wpf-controls.md)   
 [WPF 设计器](http://msdn.microsoft.com/zh-cn/c6c65214-8411-4e16-b254-163ed4099c26)