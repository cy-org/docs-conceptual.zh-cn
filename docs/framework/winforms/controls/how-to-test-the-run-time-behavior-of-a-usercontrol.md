---
title: "如何：测试 UserControl 的运行时行为 | Microsoft Docs"
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
  - "复合控件, 测试"
  - "用户控件 [Windows 窗体], 测试"
  - "UserControl 类, 运行时行为"
  - "UserControl 类, 测试"
  - "UserControl 测试容器"
ms.assetid: 4e4d5c49-1346-40ac-9d96-40211b573583
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：测试 UserControl 的运行时行为
在开发 <xref:System.Windows.Forms.UserControl> 时，需要测试它的运行时行为。  可以创建一个单独的基于 Windows 的应用程序项目，并将控件放置在测试窗体上，但这种过程很不方便。  一种更快速、更简单的方法是使用 Visual Studio 提供的**“UserControl 测试容器”**。  此测试容器直接从 Windows 控件库项目启动。  
  
> [!IMPORTANT]
>  为了使测试容器加载 <xref:System.Windows.Forms.UserControl>，控件必须至少有一个公共构造函数。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
> [!NOTE]
>  Visual C\+\+ 控件不能使用**“UserControl 测试容器”**进行测试。  
  
### 测试 UserControl 的运行时行为  
  
1.  创建一个名为 TestContainerExample 的 Windows 控件库项目。  有关详细信息，请参见 [Windows Control Library Template](http://msdn.microsoft.com/zh-cn/722f4e2d-1310-4ed5-8f33-593337ab66b4)。  
  
2.  在**“Windows 窗体设计器”**中，从**“工具箱”**中将一个 <xref:System.Windows.Forms.Label> 控件拖到控件的设计图面。  
  
3.  按 F5 以生成项目并运行**“UserControl 测试容器”**。  测试容器将出现，并且在**“预览”**窗格中显示 <xref:System.Windows.Forms.UserControl>。  
  
4.  选择位于**“预览”**窗格右边的 <xref:System.Windows.Forms.PropertyGrid> 控件中显示的 <xref:System.Windows.Forms.Control.BackColor%2A> 属性。  将其值更改为 `ControlDark`。  可以看到控件的颜色变得更暗。  尝试更改其他的属性值并观察控件的效果。  
  
5.  单击位于**“预览”**窗格下面的**“停靠填充用户控件”**复选框。  可以看到控件尺寸被重调以填充窗格。  重新调整测试容器的大小，并可以看到控件和窗格的大小一同调整。  
  
6.  关闭测试容器。  
  
7.  向 TestContainerExample 项目添加另一个用户控件。  有关详细信息，请参见 [NIB:How to: Add Existing Items to a Project](http://msdn.microsoft.com/zh-cn/15f4cfb7-78ab-457f-9f14-099a25a6a2d3)。  
  
8.  在**“Windows 窗体设计器”**中，从**“工具箱”**中将一个 <xref:System.Windows.Forms.Button> 控件拖到控件的设计图面上。  
  
9. 按 F5 以生成项目并运行测试容器。  
  
10. 单击**“选择用户控件”**<xref:System.Windows.Forms.ComboBox> 在两个用户控件之间切换。  
  
## 测试另一个项目的用户控件  
 可以在当前项目的测试容器中测试其他项目的用户控件。  
  
#### 测试另一个项目的用户控件  
  
1.  创建一个名称为 TestContainerExample2 的 Windows 控件库项目。  有关详细信息，请参见 [Windows Control Library Template](http://msdn.microsoft.com/zh-cn/722f4e2d-1310-4ed5-8f33-593337ab66b4)。  
  
2.  在**“Windows 窗体设计器”**中，从**“工具箱”**将一个 <xref:System.Windows.Forms.RadioButton> 控件拖到该控件的设计图面上。  
  
3.  按 F5 以生成项目并运行测试容器。  测试容器将出现，并且在**“预览”**窗格中显示 <xref:System.Windows.Forms.UserControl>。  
  
4.  单击**“加载”**按钮。  
  
5.  在**“打开”**对话框中，导航到在前一个过程中生成的 TestContainerExample.dll。  选择 TestContainerExample.dll 并单击**“打开”**按钮以加载用户控件。  
  
6.  使用**“选择用户控件”**<xref:System.Windows.Forms.ComboBox> 以在 TestContainerExample 项目中的两个用户控件之间切换。  
  
## 请参阅  
 <xref:System.Windows.Forms.UserControl>   
 [如何：创作复合控件](../../../../docs/framework/winforms/controls/how-to-author-composite-controls.md)   
 [演练：使用 Visual Basic 创作复合控件](../../../../docs/framework/winforms/controls/walkthrough-authoring-a-composite-control-with-visual-basic.md)   
 [演练：使用 Visual C\# 创作复合控件](../../../../docs/framework/winforms/controls/walkthrough-authoring-a-composite-control-with-visual-csharp.md)   
 [User Control Designer](http://msdn.microsoft.com/zh-cn/2abb9eec-ba32-45cb-b73d-8b52a8bd6bf1)