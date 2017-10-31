---
title: "控件类型建议 | Microsoft Docs"
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
  - "自定义控件 [Windows 窗体], 类型"
  - "继承, Windows 窗体自定义控件"
  - "用户控件 [Windows 窗体], 何时使用"
ms.assetid: 5235fe9d-c36a-4c08-ae76-6cb90b50085e
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 控件类型建议
.NET Framework 使你能够开发和实现新控件。  除了已熟悉的用户控件，现在你会发现你能够编写自定义控件用于执行其自己的绘制，甚至能够通过继承扩展现有控件的功能。  决定创建哪种类型的控件可能令人困惑。  本节重点介绍可以从其继承的各类控件之间的区别，并提供要为你的项目选择的类型的相关注意事项。  
  
> [!NOTE]
>  如果您想要编写在 Web 窗体上使用的控件，请参阅[Developing Custom ASP.NET Server Controls](../Topic/Developing%20Custom%20ASP.NET%20Server%20Controls.md)。  
  
## 从 Windows 窗体控件继承  
 你可以从任何现有的 Windows 窗体控件派生继承的控件。  此方法使你可以保留 Windows 窗体控件的所有固有功能，然后通过添加自定义属性、方法或其他功能来扩展该功能。  例如，可以创建一个派生自 <xref:System.Windows.Forms.TextBox> 的控件，它只能接受数字并自动将输入转换为一个值。  此类控件可能包含验证代码，该代码每当文本框中的文本更改时即被调用，而且可能具有附加属性，即“值”。  在有些控件中，你还可以通过重写基类的 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法，向控件的图形界面添加自定义外观。  
  
 如果为以下情况，则从 Windows 窗体控件继承：  
  
-   大部分所需功能与现有的 Windows 窗体控件相同。  
  
-   不需要自定义图形界面，或者你想要为现有控件设计一个新图形前端。  
  
## 从 UserControl 类继承  
 用户控件是封装到一个公共容器中的 Windows 窗体控件的集合。  容器保有与每个 Windows 窗体控件关联的所有固有功能，并允许你选择性地公开和绑定它们的属性。  用户控件的一个示例可能是这样一个控件，其生成的目的是显示来自数据库的客户地址数据。  该控件将包括多个用以显示每个字段的文本框以及用以在记录中导航的按钮控件。  可以选择性地公开数据绑定属性，并可以打包整个控件，并将其重复应用于不同的应用程序。  
  
 如果为以下情况，则从 <xref:System.Windows.Forms.UserControl> 类继承：  
  
-   你想要将多个 Windows 窗体控件的功能组合到单个可重用单元。  
  
## 从 Control 类继承  
 创建控件的另一种方法是通过从 <xref:System.Windows.Forms.Control> 继承，从头开始充分创建一个控件。  <xref:System.Windows.Forms.Control> 类提供控件（例如，事件）所需的所有基本功能，但没有特定于控件的功能或图形界面。  相比从用户控件或现有 Windows 窗体控件继承来说，通过从 <xref:System.Windows.Forms.Control> 类继承来创建控件需要更多的心思和精力。  作者必须为控件的 <xref:System.Windows.Forms.Control.OnPaint%2A> 事件以及任何所需的功能特定的代码编写代码。  但是允许更大的灵活性，并且可以自定义定制控件以满足你的具体需求。  自定义控件的一个示例是一个时钟控件，它复制了模拟时钟的外观和操作。  将调用自定义绘制来使指针移动，以响应来自内部计时器组件的 <xref:System.Windows.Forms.Timer.Tick> 事件。  
  
 如果为以下情况，则从 <xref:System.Windows.Forms.Control> 类继承：  
  
-   你想要提供控件的自定义图形表示形式。  
  
-   你需要实现不能通过标准控件实现的自定义功能。  
  
-   [如何：在“选择工具箱项”对话框中显示控件](http://msdn.microsoft.com/library/9yxtkx75\(v=vs.110\))  
  
-   [演练：使用 DesignerSerializationVisibilityAttribute 序列化标准类型的集合](http://msdn.microsoft.com/library/ms171731\(v=vs.110\))  
  
-   [演练：使用 Visual C\# 从 Windows 窗体控件继承](http://msdn.microsoft.com/en-us/library/5h0k2e6x\(v=vs.110\))  
  
-   [如何：为控件提供工具箱位图](http://msdn.microsoft.com/library/4wk1wc0a\(v=vs.110\))  
  
-   [如何：从现有 Windows 窗体控件继承](http://msdn.microsoft.com/library/7h62478z\(v=vs.110\))  
  
-   [演练：设计时调试自定义 Windows 窗体控件](http://msdn.microsoft.com/library/5ytx0z24\(v=vs.110\))  
  
-   [如何：从 Control 类继承](http://msdn.microsoft.com/library/skcysbt2\(v=vs.110\))  
  
-   [如何：测试 UserControl 的运行时行为](http://msdn.microsoft.com/library/ms171738\(v=vs.110\))  
  
-   [如何：设计时将控件与窗体边缘对齐](http://msdn.microsoft.com/library/1fxyb15b\(v=vs.110\))  
  
-   [如何：从 UserControl 类继承](http://msdn.microsoft.com/library/00ctb4z0\(v=vs.110\))  
  
-   [如何：创作 Windows 窗体的控件](http://msdn.microsoft.com/library/bs3yhkh7\(v=vs.110\))  
  
-   [如何：创作复合控件](http://msdn.microsoft.com/library/3sf86w5h\(v=vs.110\))  
  
-   [演练：使用 Visual Basic 创作复合控件](http://msdn.microsoft.com/library/c316f119\(v=vs.110\))  
  
-   [演练：使用 Visual C\# 创作复合控件](http://msdn.microsoft.com/en-us/library/a6h7e207\(v=vs.110\))  
  
-   [演练：使用 Visual Basic 从 Windows 窗体控件继承](http://msdn.microsoft.com/library/w2a8y03d\(v=vs.110\))  
  
-   [如何：创建利用设计时功能的 Windows 窗体控件](http://msdn.microsoft.com/library/307hck25\(v=vs.110\))  
  
-   [如何：创建利用设计时功能的 Windows 窗体控件](http://msdn.microsoft.com/library/307hck25\(v=vs.120\))  
  
## 请参阅  
 [如何：开发简单的 Windows 窗体控件](../../../../docs/framework/winforms/controls/how-to-develop-a-simple-windows-forms-control.md)   
 [各种自定义控件](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md)