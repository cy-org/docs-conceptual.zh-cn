---
title: "如何：从 UserControl 类继承 | Microsoft Docs"
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
  - "复合控件, 创建"
  - "继承, Windows 窗体自定义控件"
  - "用户控件 [Windows 窗体], 创建"
  - "UserControl 类, 继承来源"
ms.assetid: 67713625-e2e4-4f6a-bce7-0855ee5043d9
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 如何：从 UserControl 类继承
若要通过自定义代码将一个或多个 Windows 窗体控件的功能进行组合，可以创建“用户控件”。  用户控件将快速控件开发与标准 Windows 窗体控件功能以及自定义属性和方法的多功能综合在了一起。  开始创建用户控件时，系统会提供一个可视设计器，您可以将标准 Windows 窗体控件置于该可视设计器中。  这些控件保留其所有的继承功能以及标准控件的外观和行为。  但是，这些控件一旦被置入用户控件，就不能再通过代码来使用。  用户控件执行其自身的绘图工作，同时也处理与控件相关联的所有基本功能。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 创建用户控件  
  
1.  新建一个**“Windows 控件库”**项目。  
  
     创建的新项目中包含一个空白的用户控件。  
  
2.  将一个控件从**“工具箱”**的**“Windows 窗体”**选项卡中拖到设计器上。  
  
3.  应将这些控件定位到和设计成您希望它们在最终用户控件中出现的样子。  如果要使开发人员得以访问构成控件，则必须将它们声明为公共的，或有选择地公开其属性。  有关详细信息，请参见 [如何：公开构成控件的属性](../../../../docs/framework/winforms/controls/how-to-expose-properties-of-constituent-controls.md)。  
  
4.  实现将合并到控件中的任合自定义方法或属性。  
  
5.  按 F5 生成该项目，然后在**“用户控件测试容器”**中运行控件。  有关更多信息，请参见 [如何：测试 UserControl 的运行时行为](../../../../docs/framework/winforms/controls/how-to-test-the-run-time-behavior-of-a-usercontrol.md)。  
  
## 请参阅  
 [各种自定义控件](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md)   
 [如何：从 Control 类继承](../../../../docs/framework/winforms/controls/how-to-inherit-from-the-control-class.md)   
 [如何：从现有 Windows 窗体控件继承](../../../../docs/framework/winforms/controls/how-to-inherit-from-existing-windows-forms-controls.md)   
 [如何：创作 Windows 窗体的控件](../../../../docs/framework/winforms/controls/how-to-author-controls-for-windows-forms.md)   
 [有关 Visual Basic 中继承的事件处理程序的疑难解答](../Topic/Troubleshooting%20Inherited%20Event%20Handlers%20in%20Visual%20Basic.md)   
 [如何：测试 UserControl 的运行时行为](../../../../docs/framework/winforms/controls/how-to-test-the-run-time-behavior-of-a-usercontrol.md)