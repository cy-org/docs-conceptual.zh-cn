---
title: "如何：创作 Windows 窗体的控件 | Microsoft Docs"
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
  - "控件 [Windows 窗体], 创建"
  - "自定义控件 [Windows 窗体], 创建"
  - "UserControl 类, Windows 窗体"
ms.assetid: 7570e982-545b-4c3a-a7c7-55581d313400
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：创作 Windows 窗体的控件
控件表示用户和程序之间的图形化链接。  控件可以提供或处理数据、接受用户输入、对事件作出响应或执行任意次连接用户和应用程序的其他功能。  因为控件本质上是具有图形界面的组件，因此它能提供组件所提供的所有功能并提供用户交互。  控件是针对特定目的而创建的，而创作控件则是另一种编程任务，请记住这一点。  下列步骤概述了控件的创作过程。  链接提供个别步骤的附加信息。  
  
> [!NOTE]
>  如果希望创作在 Web 窗体上使用的自定义控件，请参见 [Developing Custom ASP.NET Server Controls](../Topic/Developing%20Custom%20ASP.NET%20Server%20Controls.md)。  
>   
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 创作控件  
  
1.  确定希望控件完成的操作或它在应用程序中所起的作用。  要考虑的因素有：  
  
    -   需要哪种图形界面？  
  
    -   该控件将处理何种特定的用户交互？  
  
    -   现有控件中有没有满足所需功能的？  
  
    -   能否通过将多个 Windows 窗体控件组合在一起来获得所需功能？  
  
2.  如果控件需要一个对象模型，则确定功能如何在对象模型中分配，并在控件和任何子对象中划分功能。  如果打算创作一个复杂的控件，或者想要并入一些功能，则对象模型可能会有用。  
  
3.  确定您需要的控件类型（例如用户控件、自定义控件、继承的 Windows 窗体控件）。  有关详细信息，请参见 [控件类型建议](../../../../docs/framework/winforms/controls/control-type-recommendations.md) 和 [各种自定义控件](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md)。  
  
4.  将功能表示为控件及其子对象或子一级结构的属性、方法和事件，并指派相应的访问级别（如 public、protected 等）。  
  
5.  如果控件需要自定义绘制，则为其添加代码。  有关详细信息，请参见 [自定义控件的绘制和呈现](../../../../docs/framework/winforms/controls/custom-control-painting-and-rendering.md)。  
  
6.  如果控件是从 <xref:System.Windows.Forms.UserControl> 继承的，可以生成控件项目并在**“用户控件测试容器”**中运行该控件，从而测试该控件的运行时行为。  有关更多信息，请参见 [如何：测试 UserControl 的运行时行为](../../../../docs/framework/winforms/controls/how-to-test-the-run-time-behavior-of-a-usercontrol.md)。  
  
7.  也可以新建一个项目（如 Windows 应用程序）并将控件置于一个容器中，以便对该控件进行测试和调试。  此过程的演示包括在 [演练：使用 Visual Basic 创作复合控件](../../../../docs/framework/winforms/controls/walkthrough-authoring-a-composite-control-with-visual-basic.md) 中。  
  
8.  在添加每个功能时，将功能添加到测试项目以试验新功能。  
  
9. 重复操作，改进设计。  
  
10. 打包和展开控件。  有关详细信息，请参见 [部署应用程序、服务器和组件](../Topic/Deploying%20Applications,%20Services,%20and%20Components.md)。  
  
## 请参阅  
 [演练：使用 Visual Basic 创作复合控件](../../../../docs/framework/winforms/controls/walkthrough-authoring-a-composite-control-with-visual-basic.md)   
 [演练：使用 Visual Basic 从 Windows 窗体控件继承](../../../../docs/framework/winforms/controls/walkthrough-inheriting-from-a-windows-forms-control-with-visual-basic.md)   
 [如何：从 UserControl 类继承](../../../../docs/framework/winforms/controls/how-to-inherit-from-the-usercontrol-class.md)   
 [如何：从 Control 类继承](../../../../docs/framework/winforms/controls/how-to-inherit-from-the-control-class.md)   
 [如何：从现有 Windows 窗体控件继承](../../../../docs/framework/winforms/controls/how-to-inherit-from-existing-windows-forms-controls.md)   
 [如何：测试 UserControl 的运行时行为](../../../../docs/framework/winforms/controls/how-to-test-the-run-time-behavior-of-a-usercontrol.md)   
 [各种自定义控件](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md)