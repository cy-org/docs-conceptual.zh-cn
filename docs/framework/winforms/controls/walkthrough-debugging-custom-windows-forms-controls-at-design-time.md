---
title: "演练：设计时调试自定义 Windows 窗体控件 | Microsoft Docs"
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
  - "控件 [Windows 窗体], 调试"
  - "自定义控件 [Windows 窗体], 调试"
  - "自定义控件 [Windows 窗体], 演练"
  - "调试 [Visual Studio], 演练"
  - "调试 [Visual Studio], Windows 窗体"
  - "设计器"
  - "设计时调试"
  - "可视编辑器"
  - "演练 [Windows 窗体], 调试"
ms.assetid: 1fd83ccd-3798-42fc-85a3-6cba99467387
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# 演练：设计时调试自定义 Windows 窗体控件
创建自定义控件时，经常会发现有必要调试其设计时行为。  在为自定义控件创作自定义设计器时尤其如此。  有关详细信息，请参见 [演练：创建一个利用 Visual Studio 设计时功能的 Windows 窗体控件](../../../../docs/framework/winforms/controls/creating-a-wf-control-design-time-features.md)。  
  
 同调试任何其他 .NET Framework 一样，可以使用 Visual Studio 调试自定义控件。  不同之处仅在于现在要调试的是运行自定义控件代码的一个单独的 Visual Studio 实例。  
  
 本演练涉及以下任务：  
  
-   创建一个 Windows 窗体项目以承载自定义控件  
  
-   创建控件库项目  
  
-   向自定义控件中添加属性  
  
-   向宿主窗体中添加自定义控件  
  
-   设置项目以便进行设计时调试  
  
-   在设计时调试自定义控件  
  
 完成以上步骤以后，您将会了解调试自定义控件的设计时行为所必需完成的一些任务。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
## 创建项目  
 第一步是创建应用程序项目。  将使用此项目生成承载自定义控件的应用程序。  
  
#### 创建项目  
  
-   创建一个名为“DebuggingExample”的 Windows 应用程序项目。  有关详细信息，请参见[How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)。  
  
## 创建控件库项目  
 下一步是创建控件库项目并设置自定义控件。  
  
#### 创建控件库项目  
  
1.  将**“Windows 控件库”**项目添加到解决方案中。  
  
2.  将新的**“UserControl”**项添加到 DebugControlLibrary 项目中。  有关详细信息，请参见 [NIB:How to: Add New Project Items](http://msdn.microsoft.com/zh-cn/63d3e16b-de6e-4bb5-a0e3-ecec762201ce)。  将新的源文件的基本名称命名为“DebugControl”。  
  
3.  使用**“解决方案资源管理器”**通过删除基本名称为“`UserControl1`”的代码文件来删除项目的默认控件。  有关详细信息，请参见 [NIB:How to: Remove, Delete, and Exclude Items](http://msdn.microsoft.com/zh-cn/6dffdc86-29c8-4eff-bcd8-e3a0dd9e9a73)。  
  
4.  生成解决方案。  
  
## 检查点  
 此时，您将能够在**“工具箱”**中看到自定义控件。  
  
#### 检查进度  
  
-   找到名为**“DebugControlLibrary 组件”**的新选项卡，并单击选择该卡。  打开选项卡后，将会看到您的控件作为**“DebugControl”**列出，旁边还带有一个默认图标。  
  
## 向自定义控件中添加属性  
 为了演示自定义控件的代码正在设计时运行，将添加一个属性，并在实现该属性的代码中设置一个断点。  
  
#### 向自定义控件中添加属性  
  
1.  在**“代码编辑器”**中打开**“DebugControl”**。  将以下代码添加到类定义中：  
  
    ```vb  
    Private demoStringValue As String = Nothing  
    <BrowsableAttribute(true)>  
    Public Property DemoString() As String  
  
        Get  
            Return Me.demoStringValue  
        End Get  
  
        Set(ByVal value As String)  
            Me.demoStringValue = value  
        End Set  
  
    End Property  
    ```  
  
    ```csharp  
    private string demoStringValue = null;  
    [Browsable(true)]  
    public string DemoString  
    {  
        get  
        {  
            return this.demoStringValue;  
        }  
        set  
        {  
            demoStringValue = value;  
        }  
    }  
    ```  
  
2.  生成解决方案。  
  
## 向宿主窗体中添加自定义控件  
 为了调试自定义控件的设计时行为，将在宿主窗体上放置自定义控件类的一个实例。  
  
#### 向宿主窗体中添加自定义控件  
  
1.  在“DebuggingExample”项目中，在**“Windows 窗体设计器”**中打开 Form1。  
  
2.  在**“工具箱”**中打开**“DebugControlLibrary 组件”**选项卡，并将一个**“DebugControl”**实例拖到该窗体上。  
  
3.  在**“属性”**窗口中找到 `DemoString` 自定义属性。  注意，同任何其他属性一样，您可以更改此属性的值。  还需要注意的是，选择 `DemoString` 属性时，该属性的描述字符串会显示在**“属性”**窗口的底部。  
  
## 设置项目以便进行设计时调试  
 为了调试自定义控件的设计时行为，将调试一个单独的运行自定义控件代码的 Visual Studio 实例。  
  
#### 设置项目以便进行设计时调试  
  
1.  在**“解决方案资源管理器”**中右击**“DebugControlLibrary”**项目，然后选择**“属性”**。  
  
2.  在**“DebugControlLibrary”**属性表中选择**“调试”**选项卡。  
  
     在**“启动操作”**部分选择**“启动外部程序”**。  您将要调试一个单独的 Visual Studio 实例，因此请单击省略号 \(![VisualStudioEllipsesButton 屏幕快照](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) 按钮浏览找到 Visual Studio IDE。  该可执行文件的名称为 **devenv.exe**，如果将其安装在默认位置，则路径为 %programfiles%\\Microsoft Visual Studio 9.0\\Common7\\IDE\\devenv.exe。  
  
3.  单击**“确定”**关闭对话框。  
  
4.  右击**“DebugControlLibrary”**项目，然后选择**“设为启动项目”**以启用此调试配置。  
  
## 在设计时调试自定义控件  
 现在，自定义控件以设计模式运行，可以进行调试了。  启动调试会话时，将创建一个新的 Visual Studio 实例，您将使用它来加载“DebuggingExample”解决方案。  在**“窗体设计器”**中打开 Form1 时，将创建您的自定义控件的一个实例，并开始运行该实例。  
  
#### 在设计时调试自定义控件  
  
1.  在**“代码编辑器”**中打开**“DebugControl”**源文件，并在 `DemoString` 属性的 `Set` 访问器上设置一个断点。  
  
2.  按 F5 启动调试会话。  注意，将创建一个 Visual Studio 新实例。  可以通过以下两种方式来区分这些实例：  
  
    -   调试实例在其标题栏有**“正在运行”**字样  
  
    -   调试实例的**“调试”**工具栏上的**“启动”**按钮被禁用  
  
     断点是在调试实例中设置的。  
  
3.  在 Visual Studio 新实例中打开“DebuggingExample”解决方案。  通过从**“文件”**菜单选择**“最近的项目”**可以很容易地找到该解决方案。  在最近使用过的文件列表中将列出“DebuggingExample.sln”解决方案文件。  
  
4.  在**“窗体设计器”**中打开 Form1，然后选择**“DebugControl”**控件。  
  
5.  更改 `DemoString` 属性的值。  注意，提交更改时，Visual Studio 调试实例将获得焦点，并且执行将停止在断点处。  可以单步执行属性访问器代码，就像单步执行任何其他代码一样。  
  
6.  调试会话完成以后，可以释放寄宿的 Visual Studio 实例，或单击调试实例中的**“停止调试”**按钮，退出调试。  
  
## 后续步骤  
 注意，可以在设计时调试自定义控件，这样会有很多机会扩展控件与 Visual Studio IDE 的交互。  
  
-   可以使用 <xref:System.ComponentModel.Component> 类的 <xref:System.ComponentModel.Component.DesignMode%2A> 属性来编写仅在设计时执行的代码。  有关详细信息，请参见 <xref:System.ComponentModel.Component.DesignMode%2A>。  
  
-   有几个特性可以应用于控件的属性，以便控制自定义控件与设计器的交互。  这些特性可以在 <xref:System.ComponentModel?displayProperty=fullName> 命名空间中找到。  
  
-   可以为自定义控件编写自定义设计器。  这使得您能够通过使用 Visual Studio 公开的可扩展设计器基础结构来完全控制设计过程。  有关详细信息，请参见 [演练：创建一个利用 Visual Studio 设计时功能的 Windows 窗体控件](../../../../docs/framework/winforms/controls/creating-a-wf-control-design-time-features.md)。  
  
## 请参阅  
 [演练：创建一个利用 Visual Studio 设计时功能的 Windows 窗体控件](../../../../docs/framework/winforms/controls/creating-a-wf-control-design-time-features.md)   
 [How to: Access Design\-Time Services](../Topic/How%20to:%20Access%20Design-Time%20Services.md)   
 [How to: Access Design\-Time Support in Windows Forms](../Topic/How%20to:%20Access%20Design-Time%20Support%20in%20Windows%20Forms.md)