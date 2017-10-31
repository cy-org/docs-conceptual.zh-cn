---
title: "设计时开发 Windows 窗体控件 | Microsoft Docs"
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
  - "Windows 窗体控件"
  - "Windows 窗体控件创建"
  - "控件 [Windows 窗体]"
  - "创建控件 [Windows 窗体]"
  - "用户控件 [Windows 窗体]"
  - "自定义控件 [Windows 窗体]"
ms.assetid: e5a8e088-7ec8-4fd9-bcb3-9078fd134829
caps.latest.revision: 22
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 22
---
# 设计时开发 Windows 窗体控件
为控件创建者，.NET Framework 提供了丰富的控件创作技术。 作者将不再局限于设计复合控件，后者将作为预先存在的控件的集合。 通过继承，可以从现有复合控件或预先存在的 Windows 窗体控件来创建您自己的控件。 您还可以设计您自己实现自定义绘制的控件。 这些选项使带来大量的灵活性，可以设计和可视界面的功能。 若要利用这些功能，您应熟悉基于对象的编程概念。  
  
> [!NOTE]
>  不需要透彻理解的继承，但您会发现有用来指代[不在生成中︰ 在 Visual Basic 中的继承](http://msdn.microsoft.com/zh-cn/e5e6e240-ed31-4657-820c-079b7c79313c)。  
  
 如果您想要创建自定义控件，以在 Web 窗体上使用，请参阅[开发自定义 ASP.NET 服务器控件](../Topic/Developing%20Custom%20ASP.NET%20Server%20Controls.md)。  
  
## <a name="in-this-section"></a>本节内容  
 [演练︰ 创作复合控件使用 Visual Basic](../../../../docs/framework/winforms/controls/walkthrough-authoring-a-composite-control-with-visual-basic.md)  
 演示如何在 Visual Basic 中创建简单复合控件。  
  
 [演练︰ 创作复合控件使用 Visual C#](../../../../docs/framework/winforms/controls/walkthrough-authoring-a-composite-control-with-visual-csharp.md)  
 演示如何在 C# 中创建简单复合控件。  
  
 [演练︰ 从使用 Visual Basic 的 Windows 窗体控件继承](../../../../docs/framework/winforms/controls/walkthrough-inheriting-from-a-windows-forms-control-with-visual-basic.md)  
 演示如何创建简单的 Windows 窗体控件使用 Visual Basic 中继承。  
  
 [演练︰ 从使用 Visual C# 的 Windows 窗体控件继承](../../../../docs/framework/winforms/controls/walkthrough-inheriting-from-a-windows-forms-control-with-visual-csharp.md)  
 演示如何创建在 C# 中使用继承的简单 Windows 窗体控件。  
  
 [演练︰ 在 Windows 上使用智能标记的常见任务窗体控件执行](../../../../docs/framework/winforms/controls/performing-common-tasks-using-smart-tags-on-wf-controls.md)  
 演示如何使用 Windows 窗体控件上的智能标记功能。  
  
 [演练︰ 序列化与 DesignerSerializationVisibilityAttribute 标准类型](../../../../docs/framework/winforms/controls/serializing-collections-designerserializationvisibilityattribute.md)  
 演示如何使用<xref:System.ComponentModel.DesignerSerializationVisibilityAttribute.Content?displayProperty=fullName>属性序列化集合。  
  
 [在设计时，演练︰ 调试自定义 Windows 窗体控件](../../../../docs/framework/winforms/controls/walkthrough-debugging-custom-windows-forms-controls-at-design-time.md)  
 演示如何调试 Windows 窗体控件的设计时行为。  
  
 [演练︰ 创建利用 Visual Studio 设计时功能的 Windows 窗体控件](../../../../docs/framework/winforms/controls/creating-a-wf-control-design-time-features.md)  
 演示如何将复合控件紧密集成到设计环境。  
  
 [如何︰ 创作 Windows 窗体控件](../../../../docs/framework/winforms/controls/how-to-author-controls-for-windows-forms.md)  
 概述用于实现 Windows 窗体控件的注意事项。  
  
 [如何︰ 创作复合控件](../../../../docs/framework/winforms/controls/how-to-author-composite-controls.md)  
 演示如何通过继承复合控件创建控件。  
  
 [如何︰ 从 UserControl 类继承](../../../../docs/framework/winforms/controls/how-to-inherit-from-the-usercontrol-class.md)  
 提供用于创建复合控件的过程的概述。  
  
 [如何︰ 从现有 Windows 窗体控件继承](../../../../docs/framework/winforms/controls/how-to-inherit-from-existing-windows-forms-controls.md)  
 演示如何创建通过继承扩展的控件<xref:System.Windows.Forms.Button>控件类。  
  
 [如何︰ 从 Control 类继承](../../../../docs/framework/winforms/controls/how-to-inherit-from-the-control-class.md)  
 提供创建扩展的控件的概述。  
  
 [如何︰ 在设计时将控件与窗体边缘对齐](../../../../docs/framework/winforms/controls/how-to-align-a-control-to-the-edges-of-forms-at-design-time.md)  
 演示如何使用<xref:System.Windows.Forms.Control.Dock%2A>属性以将控件与它所占据窗体的边缘对齐。  
  
 [如何︰ 显示控件在选择工具箱项对话框](../../../../docs/framework/winforms/controls/how-to-display-a-control-in-the-choose-toolbox-items-dialog-box.md)  
 显示安装控件，以便它出现在过程**自定义工具箱**对话框。  
  
 [如何︰ 为控件提供工具箱位图](../../../../docs/framework/winforms/controls/how-to-provide-a-toolbox-bitmap-for-a-control.md)  
 演示如何使用<xref:System.Drawing.ToolboxBitmapAttribute>若要在自定义控件旁边显示一个图标**工具箱**。  
  
 [如何︰ 测试 UserControl 的运行时行为](../../../../docs/framework/winforms/controls/how-to-test-the-run-time-behavior-of-a-usercontrol.md)  
 演示如何使用**UserControl 测试容器**来测试复合控件的行为。  
  
 [Windows 窗体设计器中的设计时错误](../../../../docs/framework/winforms/controls/design-time-errors-in-the-windows-forms-designer.md)  
 说明的含义和使用 Windows 窗体设计器无法加载时将显示在 Microsoft Visual Studio 设计时错误列表。  
  
 [控件和组件创作疑难解答](../../../../docs/framework/winforms/controls/troubleshooting-control-and-component-authoring.md)  
 演示如何诊断和解决在自定义组件或控件创作时可能发生的常见问题。  
  
## <a name="reference"></a>参考  
 <xref:System.Windows.Forms.Control?displayProperty=fullName>  
 对此类进行描述，并提供指向其所有成员的链接。  
  
 <xref:System.Windows.Forms.UserControl?displayProperty=fullName>  
 对此类进行描述，并提供指向其所有成员的链接。  
  
## <a name="related-sections"></a>相关章节  
 [开发自定义 Windows 窗体使用.NET Framework 的控件](../../../../docs/framework/winforms/controls/developing-custom-windows-forms-controls.md)  
 讨论如何使用.NET Framework 创建您自己的自定义控件。  
  
 [语言独立性和与语言无关的组件](../../../../docs/standard/language-independence-and-language-independent-components.md)  
 引入了公共语言运行时，它旨在简化创建和使用的组件。 这种简化的一个重要方面是使用不同的编程语言编写的组件之间的增强互操作性。 公共语言规范 (CLS) 使可以创建工具和使用多种编程语言的组件。  
  
 [演练︰ 自动填充了自定义组件的工具箱](../../../../docs/framework/winforms/controls/walkthrough-automatically-populating-the-toolbox-with-custom-components.md)  
 描述如何启用您的组件或控件中显示**自定义工具箱**对话框。