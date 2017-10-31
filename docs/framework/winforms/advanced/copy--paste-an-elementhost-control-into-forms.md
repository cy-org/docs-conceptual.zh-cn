---
title: "演练：将 ElementHost 控件复制并粘贴到单独的 Windows 窗体中 | Microsoft Docs"
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
  - "ElementHost 控件, 在设计时复制和粘贴"
  - "互操作性 [WPF]"
  - "Windows 窗体, 内容复制和粘贴"
  - "WPF 用户控件, 在 Windows 窗体中承载"
ms.assetid: 6e81bb13-577c-46c3-a1cf-8d15969fb83e
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# 演练：将 ElementHost 控件复制并粘贴到单独的 Windows 窗体中
本演练显示了如何将 Windows Presentation Foundation \(WPF\) 控件从一个 Windows 窗体复制到其他 Windows 窗体。  
  
 在本演练中，你将要执行以下任务：  
  
-   创建项目。  
  
-   复制 WPF 控件。  
  
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
  
-   在 Visual Basic 或 Visual C\# 中创建名为 `CopyElementHost` 的新 Windows 窗体应用程序项目。  
  
## 复制 WPF 控件  
 将 WPF 控件添加到项目后，可将它复制到项目中的其他窗体。  
  
#### 复制 WPF 控件  
  
1.  将新的 WPF <xref:System.Windows.Controls.UserControl> 项目添加到解决方案。  使用控件类型的默认名称，`UserControl1.xaml`。  有关详细信息，请参阅[演练：设计时在 Windows 窗体上创建新的 WPF 内容](../../../../docs/framework/winforms/advanced/walkthrough-creating-new-wpf-content-on-windows-forms-at-design-time.md)。  
  
2.  生成项目。  
  
3.  在 Windows 窗体设计器中打开 `Form1`。  
  
4.  从“工具箱”中，将 `UserControl1` 的一个实例拖到窗体上。  
  
     `UserControl1` 的实例托管在名为 `elementHost1` 的新 <xref:System.Windows.Forms.Integration.ElementHost> 控件中。  
  
5.  选择`elementHost1` 后，按 CTRL \+ C 将它复制到剪贴板。  
  
6.  向项目添加新的 Windows 窗体。  使用窗体类型的默认名称：`Form2`。  
  
7.  在 Windows 窗体设计器中打开 `Form2` 的情况下，按 CTRL\+V 将 `elementHost1` 的副本粘贴到窗体。  
  
     复制的控件名称也命名为 `elementHost1`，因为它是 `Form2` 类的私有字段。  `Form1` 类中不存在与 `elementHost1` 的名称冲突。  
  
## 请参阅  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [迁移和互操作性](../../../../docs/framework/wpf/advanced/migration-and-interoperability.md)   
 [使用 WPF 控件](../../../../docs/framework/winforms/advanced/using-wpf-controls.md)   
 [WPF 设计器](http://msdn.microsoft.com/zh-cn/c6c65214-8411-4e16-b254-163ed4099c26)