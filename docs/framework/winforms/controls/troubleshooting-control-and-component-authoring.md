---
title: "控件和组件创作疑难解答 | Microsoft Docs"
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
  - "组件 [Windows 窗体], 疑难解答"
  - "控件 [Windows 窗体], 疑难解答"
  - "组件疑难解答"
  - "控件疑难解答"
  - "Windows 窗体控件, 调试"
ms.assetid: e9c8c099-2271-4737-882f-50f336c7a55e
caps.latest.revision: 22
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 22
---
# 控件和组件创作疑难解答
本主题列出了开发组件和控件时遇到的下列常见问题。  有关更多信息，请参见 [使用组件编程](../Topic/Programming%20with%20Components.md)。  
  
-   无法将控件添加到工具箱  
  
-   无法调试 Windows 窗体用户控件或组件  
  
-   事件在继承的控件或组件中引发两次  
  
-   设计时错误：“创建组件‘*组件名称*’失败”  
  
-   STAThreadAttribute  
  
-   组件图标不出现在工具箱中  
  
## 无法将控件添加到工具箱  
 要将在另一项目中创建的自定义控件或第三方控件添加到**“工具箱”**中，必须手动操作。  如果当前项目中包含您的控件或组件，它应自动显示在**“工具箱”**中。  有关更多信息，请参见[演练：使用自定义组件自动填充工具箱](../../../../docs/framework/winforms/controls/walkthrough-automatically-populating-the-toolbox-with-custom-components.md)。  
  
#### 将控件添加到工具箱  
  
1.  右击**“工具箱”**，从快捷菜单中选择**“选择项”**。  
  
2.  在**“选择工具箱项”**对话框中，添加以下组件：  
  
    -   如果要添加 .NET Framework 组件或控件，请单击**“.NET Framework 组件”**选项卡。  
  
         – 或 –  
  
    -   如果要添加 COM 组件或 ActiveX 控件，请单击**“COM 组件”**选项卡。  
  
3.  如果对话框中列出了该控件，请务必将它选中，然后单击**“确定”**。  
  
     该控件即会添加到**“工具箱”**中。  
  
4.  如果对话框中未列出要添加的控件，请执行以下操作：  
  
    1.  单击**“浏览”**按钮。  
  
    2.  浏览到包含 .dll 文件（它包含您的控件）的文件夹。  
  
    3.  选择 .dll 文件并单击**“打开”**。  
  
         控件即会出现在对话框中。  
  
    4.  确认您的控件已被选中，然后单击**“确定”**。  
  
         控件即会添加到**“工具箱”**中。  
  
## 无法调试 Windows 窗体用户控件或组件  
 如果您的控件是从 <xref:System.Windows.Forms.UserControl> 类中派生出来的，在可以借助测试容器对它的运行时行为进行调试。  有关更多信息，请参见 [如何：测试 UserControl 的运行时行为](../../../../docs/framework/winforms/controls/how-to-test-the-run-time-behavior-of-a-usercontrol.md)。  
  
 其他自定义控件和组件不是独立的项目。  它们必须由像 Windows 窗体项目这样的应用程序来承载。  若要调试控件或组件，您必须将其添加到 Windows 窗体项目中。  
  
#### 调试控件或组件  
  
1.  在**“生成”**菜单中，单击**“生成解决方案”**以生成您的解决方案。  
  
2.  在**“文件”**菜单中，选择**“添加”**，然后选择**“新建项目”**，将测试项目添加到您的应用程序中。  
  
3.  在**“添加新项目”**对话框中选择**“Windows 应用程序”**作为项目类型。  
  
4.  在**“解决方案资源管理器”**中，右击新项目的**“引用”**节点。  在快捷菜单上单击**“添加引用”**，为包含控件或组件的项目添加一个引用。  
  
5.  在测试项目中创建控件或组件的实例。  如果组件在**“工具箱”**中，则可将其拖动到设计器图面，或者如下面的代码示例所示，以编程方式创建实例：  
  
    ```vb  
    Dim Component1 As New MyNeatComponent()  
    ```  
  
    ```csharp  
    MyNeatComponent Component1 = new MyNeatComponent();  
    ```  
  
     现在您就可以像平常一样调试控件或组件了。  
  
 有关调试的更多信息，请参见[使用 Visual Studio 进行调试](../Topic/Debugging%20in%20Visual%20Studio.md)和[演练：设计时调试自定义 Windows 窗体控件](../../../../docs/framework/winforms/controls/walkthrough-debugging-custom-windows-forms-controls-at-design-time.md)。  
  
## 事件在继承的控件或组件中引发两次  
 这可能是由于重复的 `Handles` 子句引起的。  有关更多信息，请参见[有关 Visual Basic 中继承的事件处理程序的疑难解答](../Topic/Troubleshooting%20Inherited%20Event%20Handlers%20in%20Visual%20Basic.md)。  
  
## 设计时错误：“创建组件‘Component Name’失败”  
 您的组件或控件必须提供一个不带参数的默认构造函数。  当设计环境创建一个组件或控件的实例时，它不会尝试为使用参数的构造函数重载提供任何参数。  
  
## STAThreadAttribute  
 <xref:System.STAThreadAttribute> 会向公共语言运行时 \(CLR\) 发出通知，指出 Windows 窗体使用了单线程的单元模型。  如果您没有对 Windows 窗体应用程序的 `Main` 方法应用此特性，则可能会出现意外的行为。  例如，<xref:System.Windows.Forms.ListView> 等控件的背景图像可能无法显示。  某些控件也可能需要此特性才能正确地实现自动完成和拖放行为。  
  
## 组件图标不出现在工具箱中  
 当您使用 <xref:System.Drawing.ToolboxBitmapAttribute> 将图标与自定义组件关联时，对于自动生成的组件，位图将不会出现在工具箱中。  若要查看位图，请使用**“选择工具箱项”**对话框重新加载控件。  有关更多信息，请参见[如何：为控件提供工具箱位图](../../../../docs/framework/winforms/controls/how-to-provide-a-toolbox-bitmap-for-a-control.md)。  
  
## 请参阅  
 [设计时开发 Windows 窗体控件](../../../../docs/framework/winforms/controls/developing-windows-forms-controls-at-design-time.md)   
 [演练：使用自定义组件自动填充工具箱](../../../../docs/framework/winforms/controls/walkthrough-automatically-populating-the-toolbox-with-custom-components.md)   
 [如何：测试 UserControl 的运行时行为](../../../../docs/framework/winforms/controls/how-to-test-the-run-time-behavior-of-a-usercontrol.md)   
 [演练：设计时调试自定义 Windows 窗体控件](../../../../docs/framework/winforms/controls/walkthrough-debugging-custom-windows-forms-controls-at-design-time.md)   
 [组件创作](../Topic/Component%20Authoring.md)   
 [Troubleshooting Design\-Time Development](../Topic/Troubleshooting%20Design-Time%20Development.md)   
 [使用组件编程](../Topic/Programming%20with%20Components.md)