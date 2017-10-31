---
title: "如何：使用设计器用 Windows 窗体面板控件对控件进行分组 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "控件 [Windows 窗体], 分组"
  - "Panel 控件 [Windows 窗体], 将控件分组"
  - "Windows 窗体控件, 分组"
ms.assetid: 7e1cd708-fdb1-49d8-9ca2-5640b276bf2e
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：使用设计器用 Windows 窗体面板控件对控件进行分组
Windows 窗体 <xref:System.Windows.Forms.Panel> 控件用于对其他控件进行分组。  对控件分组的原因有三个。  第一是为获得清楚的用户界面而将相关窗体元素进行可视分组；第二是编程分组，例如对单选按钮进行分组；最后一个原因是为了在设计时将多个控件作为一个单元来移动。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 创建一组控件  
  
1.  将 <xref:System.Windows.Forms.Panel> 控件从“工具箱”的**“Windows 窗体”**选项卡中拖到窗体上。  
  
2.  向面板添加其他控件，在面板内绘制每个控件。  
  
     如果要将现有控件放到面板中，可以选择所有这些控件，将它们剪切到剪贴板，再选择 <xref:System.Windows.Forms.Panel> 控件，然后将现有控件粘贴到面板中。  也可以将它们拖到面板中。  
  
3.  （可选）如果要向面板添加边框，请设置其 <xref:System.Windows.Forms.BorderStyle> 属性。  有下面三个选择方案：<xref:System.Windows.Forms.BorderStyle>、<xref:System.Windows.Forms.BorderStyle> 和 <xref:System.Windows.Forms.BorderStyle>。  
  
## 请参阅  
 [Panel 控件](../../../../docs/framework/winforms/controls/panel-control-windows-forms.md)   
 [Panel 控件概述](../../../../docs/framework/winforms/controls/panel-control-overview-windows-forms.md)   
 [如何：设置面板的背景](../../../../docs/framework/winforms/controls/how-to-set-the-background-of-a-windows-forms-panel.md)