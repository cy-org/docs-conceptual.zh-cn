---
title: "演练：在 Windows 窗体中承载 3-D WPF 复合控件 | Microsoft Docs"
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
  - "复合控件, 承载 WPF"
  - "在 Windows 窗体中承载 WPF 内容"
ms.assetid: 486369a9-606a-4a3b-b086-a06f2119c7b0
caps.latest.revision: 23
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 23
---
# 演练：在 Windows 窗体中承载 3-D WPF 复合控件
本演练演示如何创建 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 复合控件，并通过使用 <xref:System.Windows.Forms.Integration.ElementHost> 控件在 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]控件和窗体中承载它。  
  
 在本演练中，将实现一个包含两个子控件的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.UserControl>。  <xref:System.Windows.Controls.UserControl> 显示一个三维 \(3\-D\) 圆锥。  使用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 呈现三维对象比使用 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]更简单。  因此，对于在 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]中创建三维图形，承载 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.UserControl> 类非常有意义。  
  
 本演练涉及以下任务：  
  
-   创建 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.UserControl>。  
  
-   创建 Windows 窗体宿主项目。  
  
-   承载 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.UserControl>。  
  
 有关本演练中演示的任务的完整代码列表，请参见 [Hosting a 3\-D WPF Composite Control in Windows Forms Sample](http://go.microsoft.com/fwlink/?LinkID=160001)（在 Windows 窗体中承载三维 WPF 复合控件示例）。  
  
## 系统必备  
 您需要以下组件来完成本演练：  
  
-   [!INCLUDE[vs_orcas_long](../../../../includes/vs-orcas-long-md.md)].  
  
<a name="To_Create_the_UserControl"></a>   
## 创建 UserControl  
  
#### 创建 UserControl  
  
1.  创建一个名为 `HostingWpfUserControlInWf` 的 WPF 用户控件库项目。  
  
2.  在 [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)]中打开 UserControl1.xaml。  
  
3.  用下面的代码替换生成的代码。  
  
     该代码定义一个包含两个子控件的 <xref:System.Windows.Controls.UserControl?displayProperty=fullName>。  第一个子控件是 <xref:System.Windows.Controls.Label?displayProperty=fullName> 控件；第二个控件是显示三维圆锥的 <xref:System.Windows.Controls.Viewport3D> 控件。  
  
     [!code-xml[HostingWpfUserControlInWf#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HostingWpfUserControlInWf/CSharp/HostingWpfUserControlInWf/ConeControl.xaml#1)]  
  
<a name="To_Create_the_Windows_Forms_Host_Project"></a>   
## 创建 Windows 窗体宿主项目  
  
#### 创建宿主项目  
  
1.  将名为 `WpfUserControlHost` 的 Windows 应用程序项目添加到解决方案中。  有关更多信息，请参见[如何：创建新的 WPF 应用程序项目](http://msdn.microsoft.com/zh-cn/1f6aea7a-33e1-4d3f-8555-1daa42e95d82)。  
  
2.  在“解决方案资源管理器”中，添加一个对名为 WindowsFormsIntegration.dll 的 WindowsFormsIntegration 程序集的引用。  
  
3.  添加对以下 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 程序集的引用：  
  
    -   PresentationCore  
  
    -   PresentationFramework  
  
    -   WindowsBase  
  
4.  添加对 `HostingWpfUserControlInWf` 项目的引用。  
  
5.  在解决方案资源管理器中，将 `WpfUserControlHost` 项目设置为启动项目。  
  
<a name="To_Host_the_Windows_Presentation_Foundation"></a>   
## 承载 Windows Presentation Foundation UserControl  
  
#### 承载 UserControl  
  
1.  在 Windows 窗体设计器中打开 Form1。  
  
2.  在“属性”窗口中，单击**“事件”**，然后双击 <xref:System.Windows.Forms.Form.Load> 事件以创建事件处理程序。  
  
     代码编辑器打开并定位到新生成的 `Form1_Load` 事件处理程序。  
  
3.  将 Form1.cs 中的代码替换为以下代码。  
  
     `Form1_Load` 事件处理程序将创建一个 `UserControl1` 实例，并将其添加到 `` <xref:System.Windows.Forms.Integration.ElementHost> 控件的子控件集合中。  <xref:System.Windows.Forms.Integration.ElementHost> 控件将被添加到窗体的子控件集合中。  
  
     [!code-csharp[HostingWpfUserControlInWf#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HostingWpfUserControlInWf/CSharp/WpfUserControlHost/Form1.cs#10)]
     [!code-vb[HostingWpfUserControlInWf#10](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HostingWpfUserControlInWf/VisualBasic/WpfUserControlHost/Form1.vb#10)]  
  
4.  按 F5 生成并运行该应用程序。  
  
## 请参阅  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [WPF 设计器](http://msdn.microsoft.com/zh-cn/c6c65214-8411-4e16-b254-163ed4099c26)   
 [演练：在 Windows 窗体中承载 WPF 复合控件](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)   
 [演练：在 WPF 中承载 Windows 窗体复合控件](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)   
 [Hosting a WPF Composite Control in Windows Forms Sample](http://go.microsoft.com/fwlink/?LinkID=160001)