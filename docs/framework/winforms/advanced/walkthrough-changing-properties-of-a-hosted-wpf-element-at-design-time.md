---
title: "演练：设计时更改承载的 WPF 元素的属性 | Microsoft Docs"
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
  - "互操作性 [WPF]"
  - "Windows 窗体, 在设计时更改 WPF 的属性"
  - "WPF 内容 [Windows 窗体], 在设计时更改属性"
  - "WPF 内容, 在 Windows 窗体中承载"
ms.assetid: a1f7a90c-0bbb-4781-8c3c-8cc8bef2488d
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 演练：设计时更改承载的 WPF 元素的属性
本演练展示了如何更改 Windows 窗体上承载的 Windows Presentation Foundation \(WPF\) 控件的属性值。  
  
 在本演练中，你将要执行以下任务：  
  
-   创建项目。  
  
-   创建 WPF 控件。  
  
-   在 Windows 窗体上承载 WPF 控件。  
  
-   使用 Visual Studio 的 WPF 设计器来更改属性值。  
  
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
  
-   在 Visual Basic 或 Visual C\# 中创建名为 `WpfHost` 的新 Windows 窗体应用程序项目。  
  
## 创建 WPF 控件  
 将 WPF 控件添加到项目后，就可以在窗体上对其进行排列。  
  
#### 创建 WPF 控件  
  
1.  将新的 WPF <xref:System.Windows.Controls.UserControl> 添加到项目。  使用控件类型的默认名称，`UserControl1.xaml`。  有关详细信息，请参阅[演练：设计时在 Windows 窗体上创建新的 WPF 内容](../../../../docs/framework/winforms/advanced/walkthrough-creating-new-wpf-content-on-windows-forms-at-design-time.md)。  
  
2.  在“属性”窗口中，将 <xref:System.Windows.Controls.Control.Background%2A> 属性的值设置为`蓝色`。  
  
3.  生成项目。  
  
## 在 WPF 控件上更改属性值  
 通过使用 WPF 设计器，<xref:System.Windows.Forms.Integration.ElementHost> 智能标记使更改承载的 WPF 内容的属性变得轻松。  
  
#### 承载 WPF 控件  
  
1.  在 Windows 窗体设计器中打开 `Form1`。  
  
2.  在“工具箱”中的“WPF 用户控件”选项卡上，双击 `UserControl1` 在窗体上创建 `UserControl1` 的实例。  
  
     `UserControl1` 的实例承载在名为 `elementHost1` 的新 <xref:System.Windows.Forms.Integration.ElementHost> 控件中。  
  
3.  在“ElementHost 任务”智能标记面板中，选择“编辑所承载的内容”。  
  
     UserControl1.xaml 在 WPF 设计器中随即打开。  
  
4.  在“属性”窗口中，将 <xref:System.Windows.Controls.Control.Background%2A> 属性的值设置为`红色`。  
  
5.  重新生成项目。  
  
6.  在 Windows 窗体设计器中打开 `Form1`。  
  
     `UserControl1` 的实例具有红色背景。  
  
## 请参阅  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [如何：在 TableLayoutPanel 控件中锚定和停靠子控件](../../../../docs/framework/winforms/controls/how-to-anchor-and-dock-child-controls-in-a-tablelayoutpanel-control.md)   
 [如何：设计时将控件与窗体边缘对齐](../../../../docs/framework/winforms/controls/how-to-align-a-control-to-the-edges-of-forms-at-design-time.md)   
 [演练：使用对齐线在 Windows 窗体上排列控件](../../../../docs/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-snaplines.md)   
 [迁移和互操作性](../../../../docs/framework/wpf/advanced/migration-and-interoperability.md)   
 [使用 WPF 控件](../../../../docs/framework/winforms/advanced/using-wpf-controls.md)   
 [WPF 设计器](http://msdn.microsoft.com/zh-cn/c6c65214-8411-4e16-b254-163ed4099c26)