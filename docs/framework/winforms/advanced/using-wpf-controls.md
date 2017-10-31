---
title: "使用 WPF 控件 | Microsoft Docs"
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
  - "Windows 窗体设计器, 与 WPF 的互操作性"
ms.assetid: 03c85dce-26ad-44cd-bc1d-8e0cb56de096
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 使用 WPF 控件
可以在基于 Windows 窗体的应用程序中使用 Windows Presentation Foundation \(WPF\) 控件。  虽然是两种不同的视图技术，但它们可以顺利地进行交互操作。  
  
 Windows 窗体设计器为承载 Windows Presentation Foundation 控件提供可视化设计环境。  WPF 控件由名为 <xref:System.Windows.Forms.Integration.ElementHost> 的特殊 Windows 窗体控件承载。  此控件使 WPF 控件能够参与窗体的布局并接收键盘和鼠标消息。  在设计时，可以像排列任何 Windows 窗体控件那样来排列 <xref:System.Windows.Forms.Integration.ElementHost> 控件。  
  
 也可以在基于 WPF 的应用程序中使用 Windows 窗体控件。  有关更多信息，请参见 [WPF 设计器](http://msdn.microsoft.com/zh-cn/c6c65214-8411-4e16-b254-163ed4099c26)。  
  
## 本节内容  
 [如何：在设计时复制并粘贴 ElementHost 控件](../../../../docs/framework/winforms/advanced/how-to-copy-and-paste-an-elementhost-control-at-design-time.md)  
 演示如何在 Windows 窗体上复制 Windows Presentation Foundation 控件。  
  
 [演练：设计时在 Windows 窗体上排列 WPF 内容](../../../../docs/framework/winforms/advanced/walkthrough-arranging-wpf-content-on-windows-forms-at-design-time.md)  
 演示如何使用 Windows 窗体布局功能（例如锚定和对齐线）来排列 Windows Presentation Foundation 控件。  
  
 [演练：设计时更改承载的 WPF 元素的属性](../../../../docs/framework/winforms/advanced/walkthrough-changing-properties-of-a-hosted-wpf-element-at-design-time.md)  
 演示 Windows 窗体设计器和 [!INCLUDE[wpfdesigner_current_long](../../../../includes/wpfdesigner-current-long-md.md)]之间用于更改 WPF 控件属性的工作流。  
  
 [演练：设计时在 Windows 窗体上创建新的 WPF 内容](../../../../docs/framework/winforms/advanced/walkthrough-creating-new-wpf-content-on-windows-forms-at-design-time.md)  
 演示如何创建 Windows Presentation Foundation 控件，以便在基于 Windows 窗体的应用程序中使用。  
  
 [演练：将 ElementHost 控件复制并粘贴到单独的 Windows 窗体中](../../../../docs/framework/winforms/advanced/copy--paste-an-elementhost-control-into-forms.md)  
 演示如何将 Windows Presentation Foundation 控件从一个 Windows 窗体复制到另一个窗体。  
  
 [演练：设计时在 Windows 窗体上分配 WPF 内容](../../../../docs/framework/winforms/advanced/walkthrough-assigning-wpf-content-on-windows-forms-at-design-time.md)  
 演示如何选择要在窗体上显示的 Windows Presentation Foundation 控件类型。  
  
 [演练：设置 WPF 内容的样式](../../../../docs/framework/winforms/advanced/walkthrough-styling-wpf-content.md)  
 演示 Windows 窗体设计器和 [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)]之间的将样式应用到 Windows Presentation Foundation 控件的工作流。  
  
## 参考  
 <xref:System.Windows.Forms.Integration.ElementHost>  
 描述一个可用于在基于 Windows 窗体的应用程序中承载 Windows Presentation Foundation 控件的类。  
  
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>  
 描述一个可用于在基于 Windows Presentation Foundation 的应用程序中承载 Windows 窗体控件的类。  
  
## 相关章节  
 [迁移和互操作性](../../../../docs/framework/wpf/advanced/migration-and-interoperability.md)  
 描述 Windows Presentation Foundation 和 Windows 窗体技术之间的交互操作。  
  
 [WPF 设计器](http://msdn.microsoft.com/zh-cn/c6c65214-8411-4e16-b254-163ed4099c26)  
 描述如何在 [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] 中设计 Windows Presentation Foundation 控件。