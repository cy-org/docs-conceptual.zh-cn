---
title: "如何：在设计时复制并粘贴 ElementHost 控件 | Microsoft Docs"
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
ms.assetid: e570375d-2a68-44ba-b4f7-c781af2d20e8
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：在设计时复制并粘贴 ElementHost 控件
本过程演示如何在 Windows 窗体上复制 Windows Presentation Foundation \(WPF\) 控件。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 设计时复制并粘贴 ElementHost 控件  
  
1.  将新的 WPF <xref:System.Windows.Controls.UserControl> 添加到 Windows 窗体项目中。  使用该控件类型的默认名称 `UserControl1.xaml`。  有关更多信息，请参见[演练：设计时在 Windows 窗体上创建新的 WPF 内容](../../../../docs/framework/winforms/advanced/walkthrough-creating-new-wpf-content-on-windows-forms-at-design-time.md)。  
  
2.  在**“属性”**窗口中，将 `UserControl1` 的 <xref:System.Windows.FrameworkElement.Width%2A> 和 <xref:System.Windows.FrameworkElement.Height%2A> 属性的值设置为 `200`。  
  
3.  将 <xref:System.Windows.Controls.Control.Background%2A> 属性的值设置为 `Blue`。  
  
4.  生成项目。  
  
5.  在 Windows 窗体设计器中打开 `Form1`。  
  
6.  将 `UserControl1` 的实例从**“工具箱”**中拖动到窗体上。  
  
     `UserControl1` 的实例承载在一个名为 `elementHost1` 的新 <xref:System.Windows.Forms.Integration.ElementHost> 控件中。  
  
7.  选中 `elementHost1` 时，按 Ctrl\+C 将该控件复制到剪贴板。  
  
8.  按 Ctrl\+V 将复制的控件粘贴到窗体中。  
  
     在该窗体中创建名为 `elementHost2` 的新 <xref:System.Windows.Forms.Integration.ElementHost> 控件。  
  
## 请参阅  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [演练：将 ElementHost 控件复制并粘贴到单独的 Windows 窗体中](../../../../docs/framework/winforms/advanced/copy--paste-an-elementhost-control-into-forms.md)   
 [迁移和互操作性](../../../../docs/framework/wpf/advanced/migration-and-interoperability.md)   
 [使用 WPF 控件](../../../../docs/framework/winforms/advanced/using-wpf-controls.md)   
 [WPF 设计器](http://msdn.microsoft.com/zh-cn/c6c65214-8411-4e16-b254-163ed4099c26)