---
title: "演练：创建一个利用 Visual Studio 设计时功能的 Windows 窗体控件 | Microsoft Docs"
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
  - "设计时功能, Windows 窗体"
  - "DocumentDesigner 类 [Windows 窗体]"
  - "演练 [Windows 窗体], 控件"
  - "Windows 窗体控件, 创建"
ms.assetid: 6f487c59-cb38-4afa-ad2e-95edacb1d626
caps.latest.revision: 46
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 46
---
# 演练：创建一个利用 Visual Studio 设计时功能的 Windows 窗体控件
通过创作关联的自定义设计器可以改善自定义控件的设计时体验。  
  
 本演练演示如何为自定义控件创建自定义设计器。  您将实现一个 `MarqueeControl` 类型以及一个名为 `MarqueeControlRootDesigner` 的关联设计器类。  
  
 `MarqueeControl` 类型实现类似舞台字幕的显示效果，带有变幻灯光和闪烁文本。  
  
 此控件的设计器与设计环境交互以提供自定义设计时体验。  通过自定义设计器，可以在自定义 `MarqueeControl` 实现中按照各种搭配方式组合变幻灯光和闪烁文本。  在窗体上可以像使用其他任何 Windows 窗体控件一样使用组合的控件。  
  
 本演练涉及以下任务：  
  
-   创建项目  
  
-   创建控件库项目  
  
-   引用自定义控件项目  
  
-   定义自定义控件及其自定义设计器  
  
-   创建自定义控件的实例  
  
-   设置项目以便进行设计时调试  
  
-   实现自定义控件  
  
-   创建自定义控件的子控件  
  
-   创建 MarqueeBorder 子控件  
  
-   创建自定义设计器以隐藏和筛选属性  
  
-   处理组件更改  
  
-   将设计器谓词添加到自定义设计器  
  
-   创建自定义 UITypeEditor  
  
-   在设计器中测试自定义控件  
  
 完成这些操作后，自定义控件看起来会类似于下面这样：  
  
 ![可能的 MarqueeControl 排列](../../../../docs/framework/winforms/controls/media/demomarqueecontrol.gif "DemoMarqueeControl")  
  
 有关完整的代码清单，请参见[How to: Create a Windows Forms Control That Takes Advantage of Design\-Time Features](../Topic/How%20to:%20Create%20a%20Windows%20Forms%20Control%20That%20Takes%20Advantage%20of%20Design-Time%20Features.md)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
## 系统必备  
 若要完成本演练，您需要：  
  
-   足够的权限，以便能够在安装 Visual Studio 的计算机上创建和运行 Windows 窗体应用程序项目。  
  
## 创建项目  
 第一步是创建应用程序项目。  将使用此项目生成承载自定义控件的应用程序。  
  
#### 创建项目  
  
-   创建一个名为“MarqueeControlTest”的 Windows 窗体应用程序项目。有关更多信息，请参见[How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)。  
  
## 创建控件库项目  
 下一步是创建控件库项目。  将创建一个新的自定义控件及其相应的自定义设计器。  
  
#### 创建控件库项目  
  
1.  将 Windows 窗体控件库项目添加到解决方案。  将项目命名为“MarqueeControlLibrary”。  
  
2.  使用**“解决方案资源管理器”**通过删除名为“UserControl1.cs”或“UserControl1.vb”的源文件来删除项目的默认控件，具体删除哪个源文件取决于您选择的语言。  有关更多信息，请参见[NIB:How to: Remove, Delete, and Exclude Items](http://msdn.microsoft.com/zh-cn/6dffdc86-29c8-4eff-bcd8-e3a0dd9e9a73)。  
  
3.  将新的 <xref:System.Windows.Forms.UserControl> 项添加到 `MarqueeControlLibrary` 项目。  将新源文件的基名称命名为“MarqueeControl”。  
  
4.  使用**“解决方案资源管理器”**在 `MarqueeControlLibrary` 项目中新建一个文件夹。  有关更多信息，请参见[NIB:How to: Add New Project Items](http://msdn.microsoft.com/zh-cn/63d3e16b-de6e-4bb5-a0e3-ecec762201ce)。  将新文件夹命名为“Design”。  
  
5.  右击**“设计”**文件夹并添加一个新类。  将源文件的基名称命名为“MarqueeControlRootDesigner”。  
  
6.  您将需要使用 System.Design 程序集中的类型，因此请将此引用添加到 `MarqueeControlLibrary` 项目。  
  
    > [!NOTE]
    >  若要使用 System.Design 程序集，您的项目必须面向完整版 .NET Framework，而不是 .NET Framework Client Profile。  若要更改目标框架，请参见[如何：面向 .NET Framework 的某个版本](../Topic/How%20to:%20Target%20a%20Version%20of%20the%20.NET%20Framework.md)。  
  
## 引用自定义控件项目  
 将使用 `MarqueeControlTest` 项目测试自定义控件。  在添加对 `MarqueeControlLibrary` 程序集的项目引用时，该测试项目就会知悉该自定义控件。  
  
#### 引用自定义控件项目  
  
-   在 `MarqueeControlTest` 项目中添加对 `MarqueeControlLibrary` 程序集的项目引用。  请确保使用**“添加引用”**对话框中的**“项目”**选项卡，而不要直接引用 `MarqueeControlLibrary` 程序集。  
  
## 定义自定义控件及其自定义设计器  
 自定义控件将从 <xref:System.Windows.Forms.UserControl> 类派生。  这允许您的控件包含其他控件，并为您的控件提供大量默认功能。  
  
 自定义控件将有一个关联的自定义设计器。  这允许您创建专为自定义控件定制的独特设计体验。  
  
 将通过使用 <xref:System.ComponentModel.DesignerAttribute> 类将该控件与其设计器关联起来。  由于要开发自定义控件的整个设计时行为，自定义设计器将实现 <xref:System.ComponentModel.Design.IRootDesigner> 接口。  
  
#### 定义自定义控件及其自定义设计器  
  
1.  在**“代码编辑器”**中打开 `MarqueeControl` 源文件。  在文件顶部导入以下命名空间：  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#220](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrol.cs#220)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#220](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrol.vb#220)]  
  
2.  将 <xref:System.ComponentModel.DesignerAttribute> 添加到 `MarqueeControl` 类声明。  这将自定义控件与其设计器关联起来。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#240](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrol.cs#240)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#240](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrol.vb#240)]  
  
3.  在**“代码编辑器”**中打开 `MarqueeControlRootDesigner` 源文件。  在文件顶部导入以下命名空间：  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#520](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrolrootdesigner.cs#520)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#520](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrolrootdesigner.vb#520)]  
  
4.  更改 `MarqueeControlRootDesigner` 的声明，以便从 <xref:System.Windows.Forms.Design.DocumentDesigner> 类继承。  应用 <xref:System.ComponentModel.ToolboxItemFilterAttribute>，以指定该设计器与**“工具箱”**进行交互。  
  
     **注意** `MarqueeControlRootDesigner` 类的定义放在名为“MarqueeControlLibrary.Design”的命名空间中。此声明将设计器放在一个为设计相关类型保留的专用命名空间中。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#530](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrolrootdesigner.cs#530)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#530](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrolrootdesigner.vb#530)]  
  
5.  定义 `MarqueeControlRootDesigner` 类的构造函数。  将一条 <xref:System.Diagnostics.Trace.WriteLine%2A> 语句插入到构造函数体中。  这对调试很有用。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#540](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrolrootdesigner.cs#540)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#540](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrolrootdesigner.vb#540)]  
  
## 创建自定义控件的实例  
 若要观察控件的自定义设计时行为，需将控件实例置于 `MarqueeControlTest` 项目中的窗体上。  
  
#### 创建自定义控件的实例  
  
1.  将新的 <xref:System.Windows.Forms.UserControl> 项添加到 `MarqueeControlTest` 项目。  将新源文件的基名称命名为“DemoMarqueeControl”。  
  
2.  在**“代码编辑器”**中打开 `DemoMarqueeControl` 文件。  在文件顶部导入 `MarqueeControlLibrary` 命名空间：  
  
```vb  
Imports MarqueeControlLibrary  
```  
  
```csharp  
using MarqueeControlLibrary;  
```  
  
1.  更改 `DemoMarqueeControl` 的声明，以便从 `MarqueeControl` 类继承。  
  
2.  生成项目。  
  
3.  在 Windows 窗体设计器中打开 `Form1`。  
  
4.  在**“工具箱”**中找到**“MarqueeControlTest 组件”**选项卡并将其打开。  从**“工具箱”**中将一个 `DemoMarqueeControl` 拖到窗体上。  
  
5.  生成项目。  
  
## 设置项目以便进行设计时调试  
 开发自定义设计时体验时，将有必要调试您的控件和组件。  若要设置项目以允许在设计时调试，有一种简单的方法。  有关更多信息，请参见[演练：设计时调试自定义 Windows 窗体控件](../../../../docs/framework/winforms/controls/walkthrough-debugging-custom-windows-forms-controls-at-design-time.md)。  
  
#### 设置项目以便进行设计时调试  
  
1.  右击 `MarqueeControlLibrary` 项目并选择**“属性”**。  
  
2.  在“MarqueeControlLibrary 属性页”对话框中选择**“调试”**页。  
  
3.  在**“启动操作”**部分选择**“启动外部程序”**。  您将要调试一个单独的 Visual Studio 实例，因此请单击省略号 \(![VisualStudioEllipsesButton 屏幕快照](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\) 按钮浏览找到 Visual Studio IDE。  可执行文件的名称为 devenv.exe，如果将其安装在默认位置，则路径是 %programfiles%\\Microsoft Visual Studio 9.0\\Common7\\IDE\\devenv.exe。  
  
4.  单击“确定”关闭对话框。  
  
5.  右击 `MarqueeControlLibrary` 项目并选择“设置为启动项目”以启用此调试配置。  
  
## 检查点  
 现在就可以调试自定义控件的设计时行为了。  确定正确设置了调试环境之后，将测试自定义控件与自定义设计器之间的关联。  
  
#### 测试调试环境和设计器关联  
  
1.  在**“代码编辑器”**中打开 `MarqueeControlRootDesigner` 源文件，并在 <xref:System.Diagnostics.Trace.WriteLine%2A> 语句上放置一个断点。  
  
2.  按 F5 启动调试会话。  注意，将创建一个 Visual Studio 新实例。  
  
3.  在 Visual Studio 的新实例中打开“MarqueeControlTest”解决方案。  通过从**“文件”**菜单选择**“最近的项目”**可以很容易地找到该解决方案。  “MarqueeControlTest.sln”解决方案文件将会作为最新使用过的文件列出来。  
  
4.  在设计器中打开 `DemoMarqueeControl`。  注意，Visual Studio 调试实例将获得焦点，并且执行会在断点处停止。  按 F5 继续调试会话。  
  
 此时，开发和调试自定义控件及其关联的自定义设计器所需的一切准备工作均已就绪。  本演练的其余部分将关注于实现控件和设计器功能的细节。  
  
## 实现自定义控件  
 `MarqueeControl` 是一个略加定制的 <xref:System.Windows.Forms.UserControl>。  它公开两个方法：一个是启动字幕动画的 `Start`，一个是停止动画的 `Stop`。  由于 `MarqueeControl` 包含一些可实现 `IMarqueeWidget` 接口的子控件，因此，`Start` 和 `Stop` 将枚举每个子控件，并对实现 `IMarqueeWidget` 的每个子控件分别调用 `StartMarquee` 和 `StopMarquee` 方法。  
  
 `MarqueeBorder` 和 `MarqueeText` 控件的外观依赖于布局，因此 `MarqueeControl` 将重写 <xref:System.Windows.Forms.Control.OnLayout%2A> 方法并对此类型的子控件调用 <xref:System.Windows.Forms.Control.PerformLayout%2A>。  
  
 这就是 `MarqueeControl` 自定义的范围。  运行时功能由 `MarqueeBorder` 和 `MarqueeText` 控件实现，而设计时功能则由 `MarqueeBorderDesigner` 和 `MarqueeControlRootDesigner` 类实现。  
  
#### 实现自定义控件  
  
1.  在**“代码编辑器”**中打开 `MarqueeControl` 源文件。  实现 `Start` 和 `Stop` 方法。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#260](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrol.cs#260)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#260](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrol.vb#260)]  
  
2.  重写 <xref:System.Windows.Forms.Control.OnLayout%2A> 方法。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#270](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrol.cs#270)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#270](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrol.vb#270)]  
  
## 创建自定义控件的子控件  
 `MarqueeControl` 将承载两种子控件：`MarqueeBorder` 控件和 `MarqueeText` 控件。  
  
-   `MarqueeBorder`：此控件用紧密排列的“灯”围绕其边缘绘制边框。  这些灯会依次闪烁，所以灯光看起来似乎在边框上流转。  灯光闪烁的速度由一个名为 `UpdatePeriod` 的属性来控制。  其他几个自定义属性相应确定该控件外观的其他方面。  名称为别为 `StartMarquee` 和 `StopMarquee` 的两个方法控制动画开始和停止的时间。  
  
-   `MarqueeText`：此控件绘制一个闪烁的字符串。  与 `MarqueeBorder` 控件类似，文本闪烁的速度由 `UpdatePeriod` 属性控制。  `MarqueeText` 控件还与 `MarqueeBorder` 控件共有 `StartMarquee` 和 `StopMarquee` 方法。  
  
 在设计时，`MarqueeControlRootDesigner` 允许将这两个控件类型以任意组合方式添加到 `MarqueeControl` 中。  
  
 这两个控件的公共特性包含在一个名为 `IMarqueeWidget` 的接口中。  这允许 `MarqueeControl` 发现任何与 Marquee 相关的子控件并对其进行特殊处理。  
  
 为实现周期动画特性，需要使用 <xref:System.ComponentModel?displayProperty=fullName> 命名空间中的 <xref:System.ComponentModel.BackgroundWorker> 对象。  您可以使用 <xref:System.Windows.Forms.Timer> 对象，但存在较多 `IMarqueeWidget` 对象时，单个 UI 线程可能无法跟上动画的速度。  
  
#### 创建自定义控件的子控件  
  
1.  将新的类项添加到 `MarqueeControlLibrary` 项目。  将新源文件的基名称命名为“IMarqueeWidget”。  
  
2.  在**“代码编辑器”**中打开 `IMarqueeWidget` 源文件，并将声明从 `class` 更改为 `interface`：  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#2](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/imarqueewidget.cs#2)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#2](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/imarqueewidget.vb#2)]  
  
3.  将下面的代码添加到 `IMarqueeWidget` 接口以公开操作字幕动画的两个方法和一个属性：  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#3](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/imarqueewidget.cs#3)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#3](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/imarqueewidget.vb#3)]  
  
4.  将新的**“自定义控件”**项添加到 `MarqueeControlLibrary` 项目中。  将新源文件的基名称命名为“MarqueeText”。  
  
5.  从**“工具箱”**中将一个 <xref:System.ComponentModel.BackgroundWorker> 组件拖到 `MarqueeText` 控件上。  此组件将允许 `MarqueeText` 控件对其自身进行异步更新。  
  
6.  在“属性”窗口中，将 <xref:System.ComponentModel.BackgroundWorker> 组件的 `WorkerReportsProgess` 和 <xref:System.ComponentModel.BackgroundWorker.WorkerSupportsCancellation%2A> 属性设置为 `true`。  这些设置允许 <xref:System.ComponentModel.BackgroundWorker> 组件定期引发 <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> 事件和取消异步更新。  有关更多信息，请参见 [BackgroundWorker 组件](../../../../docs/framework/winforms/controls/backgroundworker-component.md)。  
  
7.  在**“代码编辑器”**中打开 `MarqueeText` 源文件。  在文件顶部导入以下命名空间：  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#120](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueetext.cs#120)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#120](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueetext.vb#120)]  
  
8.  更改 `MarqueeText` 的声明以便从 <xref:System.Windows.Forms.Label> 继承并实现 `IMarqueeWidget` 接口：  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#130](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueetext.cs#130)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#130](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueetext.vb#130)]  
  
9. 声明与公开的属性对应的实例变量，并在构造函数中对其初始化。  `isLit` 字段确定是否用由 `LightColor` 属性给定的颜色绘制文本。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#140](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueetext.cs#140)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#140](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueetext.vb#140)]  
  
10. 实现 `IMarqueeWidget` 接口。  
  
     `StartMarquee` 和 `StopMarquee` 方法调用 <xref:System.ComponentModel.BackgroundWorker> 组件的 <xref:System.ComponentModel.BackgroundWorker.RunWorkerAsync%2A> 和 <xref:System.ComponentModel.BackgroundWorker.CancelAsync%2A> 方法来启动和停止动画。  
  
     对 `UpdatePeriod` 属性应用 <xref:System.ComponentModel.CategoryAttribute.Category%2A> 和 <xref:System.ComponentModel.BrowsableAttribute.Browsable%2A> 特性，以便在“属性”窗口中名为“Marquee”的自定义部分显示该属性。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#150](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueetext.cs#150)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#150](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueetext.vb#150)]  
  
11. 实现属性访问器。  将向客户端公开两个属性：`LightColor` 和 `DarkColor`。  对这些属性应用 <xref:System.ComponentModel.CategoryAttribute.Category%2A> 和 <xref:System.ComponentModel.BrowsableAttribute.Browsable%2A> 特性，以便在“属性”窗口中名为“Marquee”的自定义部分显示这些属性。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#160](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueetext.cs#160)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#160](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueetext.vb#160)]  
  
12. 实现 <xref:System.ComponentModel.BackgroundWorker> 组件的 <xref:System.ComponentModel.BackgroundWorker.DoWork> 和 <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> 事件的处理程序。  
  
     <xref:System.ComponentModel.BackgroundWorker.DoWork> 事件处理程序休眠一段由 `UpdatePeriod` 指定的时间（以毫秒表示），然后引发 <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> 事件，直至代码通过调用 <xref:System.ComponentModel.BackgroundWorker.CancelAsync%2A> 停止动画。  
  
     <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> 事件处理程序在文本的亮和暗这两种状态之间切换，给人以闪烁的感觉。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#180](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueetext.cs#180)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#180](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueetext.vb#180)]  
  
13. 重写 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法以启用动画。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#170](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueetext.cs#170)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#170](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueetext.vb#170)]  
  
14. 按 F6 键生成解决方案。  
  
## 创建 MarqueeBorder 子控件  
 `MarqueeBorder` 控件比 `MarqueeText` 控件稍复杂。  它有更多属性，并且 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法中的动画也更为繁杂。  大体上，它与 `MarqueeText` 控件非常类似。  
  
 由于 `MarqueeBorder` 控件可有子控件，因此需要向其通知 <xref:System.Windows.Forms.Control.Layout> 事件。  
  
#### 创建 MarqueeBorder 控件  
  
1.  将新的**“自定义控件”**项添加到 `MarqueeControlLibrary` 项目中。  将新源文件的基名称命名为“MarqueeBorder”。  
  
2.  从**“工具箱”**中将一个 <xref:System.ComponentModel.BackgroundWorker> 组件拖到 `MarqueeBorder` 控件上。  此组件将允许 `MarqueeBorder` 控件对其自身进行异步更新。  
  
3.  在“属性”窗口中，将 <xref:System.ComponentModel.BackgroundWorker> 组件的 `WorkerReportsProgess` 和 <xref:System.ComponentModel.BackgroundWorker.WorkerSupportsCancellation%2A> 属性设置为 `true`。  这些设置允许 <xref:System.ComponentModel.BackgroundWorker> 组件定期引发 <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> 事件和取消异步更新。  有关更多信息，请参见 [BackgroundWorker 组件](../../../../docs/framework/winforms/controls/backgroundworker-component.md)。  
  
4.  在“属性”窗口中单击“事件”按钮。  为 <xref:System.ComponentModel.BackgroundWorker.DoWork> 和 <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> 事件附加处理程序。  
  
5.  在**“代码编辑器”**中打开 `MarqueeBorder` 源文件。  在文件顶部导入以下命名空间：  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#20](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#20)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#20](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#20)]  
  
6.  更改 `MarqueeBorder` 的声明以便从 <xref:System.Windows.Forms.Panel> 继承以及实现 `IMarqueeWidget` 接口。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#30](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#30)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#30](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#30)]  
  
7.  声明两个枚举以用于管理 `MarqueeBorder` 控件的状态：一个是 `MarqueeSpinDirection`，它确定灯光绕边框“旋转”的方向；另一个是 `MarqueeLightShape`，它确定灯光的形状（方形还是圆形）。  将这些声明放在 `MarqueeBorder` 类声明之前。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#97](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#97)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#97](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#97)]  
  
8.  声明与公开的属性对应的实例变量，并在构造函数中对其初始化。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#40](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#40)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#40](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#40)]  
  
9. 实现 `IMarqueeWidget` 接口。  
  
     `StartMarquee` 和 `StopMarquee` 方法调用 <xref:System.ComponentModel.BackgroundWorker> 组件的 <xref:System.ComponentModel.BackgroundWorker.RunWorkerAsync%2A> 和 <xref:System.ComponentModel.BackgroundWorker.CancelAsync%2A> 方法来启动和停止动画。  
  
     由于 `MarqueeBorder` 控件可以包含子控件，所以 `StartMarquee` 方法将枚举所有子控件，并对其中实现了 `IMarqueeWidget` 的子控件调用 `StartMarquee`。  `StopMarquee` 方法有类似实现。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#50](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#50)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#50](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#50)]  
  
10. 实现属性访问器。  `MarqueeBorder` 控件有几个用来控制其自身外观的属性。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#60](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#60)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#60](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#60)]  
  
11. 实现 <xref:System.ComponentModel.BackgroundWorker> 组件的 <xref:System.ComponentModel.BackgroundWorker.DoWork> 和 <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> 事件的处理程序。  
  
     <xref:System.ComponentModel.BackgroundWorker.DoWork> 事件处理程序休眠一段由 `UpdatePeriod` 指定的时间（以毫秒表示），然后引发 <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> 事件，直至代码通过调用 <xref:System.ComponentModel.BackgroundWorker.CancelAsync%2A> 停止动画。  
  
     <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> 事件处理程序递增“基”灯的位置，从基灯确定其他各灯的亮\/暗状态；并调用 <xref:System.Windows.Forms.Control.Refresh%2A> 方法促使控件重新绘制自身。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#90](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#90)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#90](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#90)]  
  
12. 实现这两个帮助器方法：`IsLit` 和 `DrawLight`。  
  
     `IsLit` 方法确定某一给定位置的灯光颜色。  “亮”的灯光绘制成 `LightColor` 属性指定的颜色，“暗”的灯光绘制成 `DarkColor` 属性指定的颜色。  
  
     `DrawLight` 方法使用适当的颜色、形状和位置绘制灯光。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#80](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#80)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#80](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#80)]  
  
13. 重写 <xref:System.Windows.Forms.Control.OnLayout%2A> 和 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法。  
  
     <xref:System.Windows.Forms.Control.OnPaint%2A> 方法沿 `MarqueeBorder` 控件的边缘绘制灯光。  
  
     由于 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法依赖于 `MarqueeBorder` 控件的尺寸，所以只要布局更改就需要调用它。  为此，请重写 <xref:System.Windows.Forms.Control.OnLayout%2A> 并调用 <xref:System.Windows.Forms.Control.Refresh%2A>。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#70](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#70)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#70](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#70)]  
  
## 创建自定义设计器以隐藏和筛选属性  
 `MarqueeControlRootDesigner` 类提供根设计器的实现。  除作用于 `MarqueeControl` 的此设计器以外，您还将需要一个专门与 `MarqueeBorder` 控件关联的自定义设计器。  此设计器提供适合于自定义根设计器上下文的自定义行为。  
  
 具体说来，`MarqueeBorderDesigner` 将“隐藏”和筛选 `MarqueeBorder` 控件上的某些属性，更改它们与设计环境的交互。  
  
 对组件的属性访问器的调用的截获操作称为“隐藏”。它允许设计器跟踪由用户设置的值，并且还可以将该值传递到要设计的组件。  
  
 对于此示例，<xref:System.Windows.Forms.Control.Visible%2A> 和 <xref:System.Windows.Forms.Control.Enabled%2A> 属性将被 `MarqueeBorderDesigner` 隐藏起来，这能够防止用户在设计时使 `MarqueeBorder` 控件不可见或被禁用。  
  
 设计器还可以添加和移除属性。  对于此示例，由于 `MarqueeBorder` 控件基于由 `LightSize` 属性指定的灯光尺寸以编程方式设置边距，所以将在设计时移除 <xref:System.Windows.Forms.Control.Padding%2A> 属性。  
  
 `MarqueeBorderDesigner` 的基类是 <xref:System.ComponentModel.Design.ComponentDesigner>，该类包含能够更改控件在设计时公开的特性、属性和事件的方法：  
  
-   <xref:System.ComponentModel.Design.ComponentDesigner.PreFilterProperties%2A>  
  
-   <xref:System.ComponentModel.Design.ComponentDesigner.PostFilterProperties%2A>  
  
-   <xref:System.ComponentModel.Design.ComponentDesigner.PreFilterAttributes%2A>  
  
-   <xref:System.ComponentModel.Design.ComponentDesigner.PostFilterAttributes%2A>  
  
-   <xref:System.ComponentModel.Design.ComponentDesigner.PreFilterEvents%2A>  
  
-   <xref:System.ComponentModel.Design.ComponentDesigner.PostFilterEvents%2A>  
  
 使用这些方法更改组件的公共接口时，必须遵循下列规则：  
  
-   仅在 `PreFilter` 方法中移除项  
  
-   仅在 `PostFilter` 方法中修改现有项  
  
-   在 `PreFilter` 方法中始终首先调用基实现  
  
-   在 `PostFilter` 方法中始终最后调用基实现  
  
 遵循这些规则可确保设计时环境中的所有这些设计器能够一致地显示所有要设计的组件。  
  
 <xref:System.ComponentModel.Design.ComponentDesigner> 类提供了一个字典，以便管理被隐藏的属性的值，从而免除了您创建特定实例变量的需要。  
  
#### 创建自定义设计器以隐藏和筛选属性  
  
1.  右击**“设计”**文件夹并添加一个新类。  将源文件的基名称命名为“MarqueeBorderDesigner”。  
  
2.  在**“代码编辑器”**中打开 `MarqueeBorderDesigner` 源文件。  在文件顶部导入以下命名空间：  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#420](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborderdesigner.cs#420)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#420](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborderdesigner.vb#420)]  
  
3.  更改 `MarqueeBorderDesigner` 的声明，以便从 <xref:System.Windows.Forms.Design.ParentControlDesigner> 继承。  
  
     由于 `MarqueeBorder` 控件可包含子控件，`MarqueeBorderDesigner` 将从处理父子交互的 <xref:System.Windows.Forms.Design.ParentControlDesigner> 继承。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#430](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborderdesigner.cs#430)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#430](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborderdesigner.vb#430)]  
  
4.  重写 <xref:System.ComponentModel.Design.ComponentDesigner.PreFilterProperties%2A> 的基实现。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#450](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborderdesigner.cs#450)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#450](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborderdesigner.vb#450)]  
  
5.  实现 <xref:System.Windows.Forms.Control.Enabled%2A> 和 <xref:System.Windows.Forms.Control.Visible%2A> 属性。  这些实现隐藏了该控件的属性。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#440](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborderdesigner.cs#440)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#440](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborderdesigner.vb#440)]  
  
## 处理组件更改  
 `MarqueeControlRootDesigner` 类为您的 `MarqueeControl` 实例提供自定义设计时体验。  大多数设计时功能是从 <xref:System.Windows.Forms.Design.DocumentDesigner> 类继承的；您的代码将实现两个特定的定制：处理组件更改和添加设计器谓词。  
  
 用户设计 `MarqueeControl` 实例时，根设计器将跟踪对 `MarqueeControl` 及其子控件的更改。  设计时环境提供了一项便利服务 <xref:System.ComponentModel.Design.IComponentChangeService> 以用于跟踪对组件状态的更改。  
  
 通过使用 <xref:System.ComponentModel.Design.ComponentDesigner.GetService%2A> 方法查询环境可获得对此服务的引用。  如果查询成功，设计器可为 <xref:System.ComponentModel.Design.IComponentChangeService.ComponentChanged> 事件附加处理程序，执行在设计时维护状态一致所需的任何任务。  
  
 对于 `MarqueeControlRootDesigner` 类，将对 `MarqueeControl` 所包含的每个 `IMarqueeWidget` 对象调用 <xref:System.Windows.Forms.Control.Refresh%2A> 方法。  这将导致 `IMarqueeWidget` 对象在诸如其父控件的 <xref:System.Windows.Forms.Control.Size%2A> 等属性更改时相应地重新绘制自身。  
  
#### 处理组件更改  
  
1.  在**“代码编辑器”**中打开 `MarqueeControlRootDesigner` 源文件，并重写 <xref:System.Windows.Forms.Design.DocumentDesigner.Initialize%2A> 方法。  调用 <xref:System.Windows.Forms.Design.DocumentDesigner.Initialize%2A> 的基实现并查询 <xref:System.ComponentModel.Design.IComponentChangeService> 是否存在。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#580](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrolrootdesigner.cs#580)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#580](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrolrootdesigner.vb#580)]  
  
2.  实现 <xref:System.ComponentModel.Design.IComponentChangeService.OnComponentChanged%2A> 事件处理程序。  测试发送组件的类型，如果类型为 `IMarqueeWidget`，则调用其 <xref:System.Windows.Forms.Control.Refresh%2A> 方法。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#560](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrolrootdesigner.cs#560)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#560](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrolrootdesigner.vb#560)]  
  
## 将设计器谓词添加到自定义设计器  
 设计器谓词是与事件处理程序链接的菜单命令。  设计器谓词在设计时被添加到组件的快捷菜单上。  有关更多信息，请参见 <xref:System.ComponentModel.Design.DesignerVerb>。  
  
 将向设计器添加两个设计器谓词：**“运行测试”**和**“停止测试”**。  这些谓词将允许您在设计时查看 `MarqueeControl` 的运行时行为。  这些谓词将被添加到 `MarqueeControlRootDesigner`。  
  
 调用**“运行测试”**时，谓词事件处理程序将对 `MarqueeControl` 调用 `StartMarquee` 方法。  调用**“停止测试”**时，谓词事件处理程序将对 `MarqueeControl` 调用 `StopMarquee` 方法。  `StartMarquee` 和 `StopMarquee` 方法的实现对实现 `IMarqueeWidget` 的被包含的控件调用这些方法，因此被包含的任何 `IMarqueeWidget` 控件也将参与测试。  
  
#### 将设计器谓词添加到自定义设计器  
  
1.  在 `MarqueeControlRootDesigner` 类中添加名为 `OnVerbRunTest` 和 `OnVerbStopTest` 的事件处理程序。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#570](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrolrootdesigner.cs#570)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#570](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrolrootdesigner.vb#570)]  
  
2.  将这些事件处理程序连接至其对应的设计器谓词。  `MarqueeControlRootDesigner` 从其基类继承 <xref:System.ComponentModel.Design.DesignerVerbCollection>。  将在 <xref:System.Windows.Forms.Design.DocumentDesigner.Initialize%2A> 方法中创建两个新的 <xref:System.ComponentModel.Design.DesignerVerb> 对象并将其添加至此集合。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#590](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueecontrolrootdesigner.cs#590)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#590](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueecontrolrootdesigner.vb#590)]  
  
## 创建自定义 UITypeEditor  
 为用户创建自定义设计时体验时，通常需要创建与“属性”窗口的自定义交互。  这可以通过创建 <xref:System.Drawing.Design.UITypeEditor> 来实现。  有关更多信息，请参见[How to: Create a UI Type Editor](../Topic/How%20to:%20Create%20a%20UI%20Type%20Editor.md)。  
  
 `MarqueeBorder` 控件将在“属性”窗口中公开几个属性。  其中的两个属性 `MarqueeSpinDirection` 和 `MarqueeLightShape` 由枚举表示。  为演示 UI 类型编辑器的用法，`MarqueeLightShape` 属性将有一个关联 <xref:System.Drawing.Design.UITypeEditor> 类。  
  
#### 创建自定义 UI 类型编辑器  
  
1.  在**“代码编辑器”**中打开 `MarqueeBorder` 源文件。  
  
2.  在 `MarqueeBorder` 类的定义中声明一个名为 `LightShapeEditor`、从 <xref:System.Drawing.Design.UITypeEditor> 派生的类。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#96](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#96)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#96](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#96)]  
  
3.  声明一个名为 `editorService` 的 <xref:System.Windows.Forms.Design.IWindowsFormsEditorService> 实例变量。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#92](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#92)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#92](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#92)]  
  
4.  重写 <xref:System.Drawing.Design.UITypeEditor.GetEditStyle%2A> 方法。  此实现返回 <xref:System.Drawing.Design.UITypeEditorEditStyle>，它指示设计环境如何显示 `LightShapeEditor`。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#93](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#93)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#93](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#93)]  
  
5.  重写 <xref:System.Drawing.Design.UITypeEditor.EditValue%2A> 方法。  此实现在设计环境中查询一个 <xref:System.Windows.Forms.Design.IWindowsFormsEditorService> 对象。  如果成功，它将创建一个 `LightShapeSelectionControl`。  将调用 <xref:System.Windows.Forms.Design.IWindowsFormsEditorService.DropDownControl%2A> 方法以启动 `LightShapeEditor`。  此调用的返回值将被返回到设计环境。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#94](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/marqueeborder.cs#94)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#94](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/marqueeborder.vb#94)]  
  
## 创建自定义 UITypeEditor 的视图控件  
  
1.  `MarqueeLightShape` 属性支持两种类型的灯光形状：`Square` 和 `Circle`。  将专为以图形方式在“属性”窗口中显示这些值创建一个自定义控件。  <xref:System.Drawing.Design.UITypeEditor> 将使用此自定义控件来与“属性”窗口交互。  
  
#### 创建自定义 UI 类型编辑器的视图控件  
  
1.  将新的 <xref:System.Windows.Forms.UserControl> 项添加到 `MarqueeControlLibrary` 项目。  将新源文件的基名称命名为“LightShapeSelectionControl”。  
  
2.  从**“工具箱”**中将两个 <xref:System.Windows.Forms.Panel> 控件拖到 `LightShapeSelectionControl` 上。  将它们命名为 `squarePanel` 和 `circlePanel`，  并使它们并排排列。  将这两个 <xref:System.Windows.Forms.Panel> 控件的 <xref:System.Windows.Forms.Control.Size%2A> 属性均设置为 \(60, 60\)。  将 `squarePanel` 控件的 <xref:System.Windows.Forms.Control.Location%2A> 属性设置为 \(8, 10\)。  将 `circlePanel` 控件的 <xref:System.Windows.Forms.Control.Location%2A> 属性设置为 \(80, 10\)。  最后，将 `LightShapeSelectionControl` 的 <xref:System.Windows.Forms.Control.Size%2A> 属性设置为 \(150, 80\)。  
  
3.  在**“代码编辑器”**中打开 `LightShapeSelectionControl` 源文件。  在文件顶部导入 <xref:System.Windows.Forms.Design?displayProperty=fullName> 命名空间：  
  
```vb  
Imports System.Windows.Forms.Design  
```  
  
```csharp  
using System.Windows.Forms.Design;  
```  
  
1.  实现 `squarePanel` 和 `circlePanel` 控件的 <xref:System.Windows.Forms.Control.Click> 事件处理程序。  这些方法将调用 <xref:System.Windows.Forms.Design.IWindowsFormsEditorService.CloseDropDown%2A> 以结束自定义 <xref:System.Drawing.Design.UITypeEditor> 编辑会话。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#390](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/lightshapeselectioncontrol.cs#390)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#390](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/lightshapeselectioncontrol.vb#390)]  
  
2.  声明一个名为 `editorService` 的 <xref:System.Windows.Forms.Design.IWindowsFormsEditorService> 实例变量。  
  
```vb  
Private editorService As IWindowsFormsEditorService  
```  
  
```csharp  
private IWindowsFormsEditorService editorService;  
```  
  
1.  声明一个名为 `lightShapeValue` 的 `MarqueeLightShape` 实例变量。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#330](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/lightshapeselectioncontrol.cs#330)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#330](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/lightshapeselectioncontrol.vb#330)]  
  
2.  在 `LightShapeSelectionControl` 构造函数中，将 <xref:System.Windows.Forms.Control.Click> 事件处理程序附加到 `squarePanel` 和 `circlePanel` 控件的 <xref:System.Windows.Forms.Control.Click> 事件。  另外，请定义一个构造函数重载，以便将设计环境中的 `MarqueeLightShape` 值赋予 `lightShapeValue` 字段。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#340](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/lightshapeselectioncontrol.cs#340)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#340](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/lightshapeselectioncontrol.vb#340)]  
  
3.  在 <xref:System.ComponentModel.Component.Dispose%2A> 方法中，分离 <xref:System.Windows.Forms.Control.Click> 事件处理程序。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#350](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/lightshapeselectioncontrol.cs#350)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#350](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/lightshapeselectioncontrol.vb#350)]  
  
4.  在**“解决方案资源管理器”**中，单击**“显示所有文件”**按钮。  打开 LightShapeSelectionControl.Designer.cs 或 LightShapeSelectionControl.Designer.vb 文件，然后移除 <xref:System.ComponentModel.Component.Dispose%2A> 方法的默认定义。  
  
5.  实现 `LightShape` 属性。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#360](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/lightshapeselectioncontrol.cs#360)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#360](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/lightshapeselectioncontrol.vb#360)]  
  
6.  重写 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法。  此实现将绘制一个实心正方形和一个实心圆形。  此外，它还会在其中一个形状周围绘制边框，以突出显示选定的值。  
  
     [!code-csharp[System.Windows.Forms.Design.DocumentDesigner#380](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/CS/lightshapeselectioncontrol.cs#380)]
     [!code-vb[System.Windows.Forms.Design.DocumentDesigner#380](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.Design.DocumentDesigner/VB/lightshapeselectioncontrol.vb#380)]  
  
## 在设计器中测试自定义控件  
 此时，您就可以生成 `MarqueeControlLibrary` 项目了。  通过创建一个从 `MarqueeControl` 类继承的控件，并在窗体中使用该控件，来测试您实现的自定义控件。  
  
#### 创建自定义 MarqueeControl 实现  
  
1.  在 Windows 窗体设计器中打开 `DemoMarqueeControl`。  这将创建一个 `DemoMarqueeControl` 类型的实例，并在 `MarqueeControlRootDesigner` 类型的一个实例中显示它。  
  
2.  在**“工具箱”**中打开**“MarqueeControlLibrary 组件”**选项卡。  将显示 `MarqueeBorder` 和 `MarqueeText` 控件以供选择。  
  
3.  将 `MarqueeBorder` 控件的一个实例拖到 `DemoMarqueeControl` 设计图面上。  将此 `MarqueeBorder` 控件停靠到父控件上。  
  
4.  将 `MarqueeText` 控件的一个实例拖到 `DemoMarqueeControl` 设计图面上。  
  
5.  生成解决方案。  
  
6.  右击 `DemoMarqueeControl`，然后从快捷菜单中选择**“运行测试”**选项启动动画。  单击**“停止测试”**以停止动画。  
  
7.  在“设计”视图中打开**“Form1”**。  
  
8.  将两个 <xref:System.Windows.Forms.Button> 控件放置至窗体上。  将其分别命名为 `startButton` 和 `stopButton`，并将 <xref:System.Windows.Forms.Control.Text%2A> 属性值分别更改为“启动”和“停止”。  
  
9. 分别为这两个 <xref:System.Windows.Forms.Button> 控件实现 <xref:System.Windows.Forms.Control.Click> 事件处理程序。  
  
10. 在**“工具箱”**中打开**“MarqueeControlTest 组件”**选项卡。  将显示 `DemoMarqueeControl` 以供选择。  
  
11. 将 `DemoMarqueeControl` 的一个实例拖到**“Form1”**设计图面上。  
  
12. 在 <xref:System.Windows.Forms.Control.Click> 事件处理程序中对 `DemoMarqueeControl` 调用 `Start` 和 `Stop` 方法。  
  
```vb  
Private Sub startButton_Click(sender As Object, e As System.EventArgs)  
    Me.demoMarqueeControl1.Start()  
End Sub 'startButton_Click  
  
Private Sub stopButton_Click(sender As Object, e As System.EventArgs)  
Me.demoMarqueeControl1.Stop()  
End Sub 'stopButton_Click  
```  
  
```csharp  
private void startButton_Click(object sender, System.EventArgs e)  
{  
    this.demoMarqueeControl1.Start();  
}  
  
private void stopButton_Click(object sender, System.EventArgs e)  
{  
    this.demoMarqueeControl1.Stop();  
}  
```  
  
1.  将 `MarqueeControlTest` 项目设置为启动项目，然后运行该项目。  您将看到显示 `DemoMarqueeControl` 的窗体。  单击**“启动”**按钮以启动动画。  您应当会看到文本在闪烁，且边框上有亮点在移动。  
  
## 后续步骤  
 `MarqueeControlLibrary` 演示了自定义控件及其关联设计器的一个简单实现。  您可以采用以下几种方式来使此示例更复杂些：  
  
-   在设计器中更改 `DemoMarqueeControl` 的属性值。  添加更多 `MarqueBorder` 控件，并将其停靠在它们的父实例中以产生嵌套效果。  尝试对 `UpdatePeriod` 和灯光相关属性进行不同的设置。  
  
-   创作自己的 `IMarqueeWidget` 的实现。  例如，可以创建一个闪烁的“霓虹标志”或带有多个图像的动画标志。  
  
-   进一步自定义设计时体验。  可以尝试在 <xref:System.Windows.Forms.Control.Enabled%2A> 和 <xref:System.Windows.Forms.Control.Visible%2A> 之外隐藏更多属性，而且可以添加新的属性。  添加新的设计器谓词以简化常规任务，例如停靠子控件。  
  
-   为 `MarqueeControl` 添加许可控制。  有关更多信息，请参见[如何：授予组件和控件许可权限](../Topic/How%20to:%20License%20Components%20and%20Controls.md)。  
  
-   控制如何序列化控件以及如何为控件生成代码。  有关更多信息，请参见[动态源代码生成和编译](../../../../docs/framework/reflection-and-codedom/dynamic-source-code-generation-and-compilation.md)。  
  
## 请参阅  
 <xref:System.Windows.Forms.UserControl>   
 <xref:System.Windows.Forms.Design.ParentControlDesigner>   
 <xref:System.Windows.Forms.Design.DocumentDesigner>   
 <xref:System.ComponentModel.Design.IRootDesigner>   
 <xref:System.ComponentModel.Design.DesignerVerb>   
 <xref:System.Drawing.Design.UITypeEditor>   
 <xref:System.ComponentModel.BackgroundWorker>   
 [How to: Create a Windows Forms Control That Takes Advantage of Design\-Time Features](../Topic/How%20to:%20Create%20a%20Windows%20Forms%20Control%20That%20Takes%20Advantage%20of%20Design-Time%20Features.md)   
 [Extending Design\-Time Support](../Topic/Extending%20Design-Time%20Support.md)   
 [Custom Designers](../Topic/Custom%20Designers.md)   
 [.NET Shape Library: A Sample Designer](http://windowsforms.net/articles/shapedesigner.aspx)