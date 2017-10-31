---
title: "如何：从 Control 类继承 | Microsoft Docs"
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
  - "Control 类, 继承来源"
  - "自定义控件 [Windows 窗体], 创建"
  - "自定义控件 [Windows 窗体], 继承"
  - "继承, Windows 窗体自定义控件"
  - "OnPaint 方法 [Windows 窗体]"
ms.assetid: 46ba0df3-5cf7-443c-a3b4-a72660172476
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：从 Control 类继承
如果想要创建一个用于 Windows 窗体的完全自定义的控件，则应从 <xref:System.Windows.Forms.Control> 类继承。  而从 <xref:System.Windows.Forms.Control> 类继承要求进行更多的规划和实现，同时也为您提供了最大程度的选择自由。  当从 <xref:System.Windows.Forms.Control> 继承时，将继承使控件能够运行的最基本功能。  <xref:System.Windows.Forms.Control> 类的固有功能可处理用户通过键盘和鼠标的输入，定义控件的边界和大小，提供窗口句柄，以及提供信息处理和安全。  它没有并入任何绘图功能（在此指的是控件图形界面的实际呈现），也没有并入任何特定用户的交互功能。  必须通过自定义代码提供所有这些功能。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 创建自定义控件  
  
1.  创建新的**“Windows 应用程序”**或**“Windows 控件库”**项目。  
  
2.  从**“项目”**菜单中选择**“添加类”**。  
  
3.  在**“添加新项”**对话框中单击**“自定义控件”**。  
  
     一个新的自定义控件被添加到项目中。  
  
4.  按 F7 为自定义控件打开**“代码编辑器”**。  
  
5.  定位到 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法，该方法除了调用基类的 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法外，其他情况均为空。  
  
6.  修改代码以便并入控件所需的任何自定义绘图。  
  
     有关编写代码以呈现控件图形的更多信息，请参见 [自定义控件的绘制和呈现](../../../../docs/framework/winforms/controls/custom-control-painting-and-rendering.md)。  
  
7.  实现控件将并入的所有自定义方法、属性或事件。  
  
8.  保存并测试控件。  
  
## 请参阅  
 [各种自定义控件](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md)   
 [如何：从 UserControl 类继承](../../../../docs/framework/winforms/controls/how-to-inherit-from-the-usercontrol-class.md)   
 [如何：从现有 Windows 窗体控件继承](../../../../docs/framework/winforms/controls/how-to-inherit-from-existing-windows-forms-controls.md)   
 [如何：创作 Windows 窗体的控件](../../../../docs/framework/winforms/controls/how-to-author-controls-for-windows-forms.md)   
 [有关 Visual Basic 中继承的事件处理程序的疑难解答](../Topic/Troubleshooting%20Inherited%20Event%20Handlers%20in%20Visual%20Basic.md)   
 [设计时开发 Windows 窗体控件](../../../../docs/framework/winforms/controls/developing-windows-forms-controls-at-design-time.md)