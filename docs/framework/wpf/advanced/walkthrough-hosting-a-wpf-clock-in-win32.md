---
title: "演练：在 Win32 中承载 WPF 时钟 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "互操作性 [WPF], 教程"
  - "互操作性 [WPF], Win32"
  - "Win32 代码, WPF 互操作"
ms.assetid: 555e55a7-0851-4ec8-b1c6-0acba7e9b648
caps.latest.revision: 15
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 演练：在 Win32 中承载 WPF 时钟
若要在 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 应用程序中放置 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]，请使用 <xref:System.Windows.Interop.HwndSource>，它提供包含您的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容的 HWND。  首先，创建 <xref:System.Windows.Interop.HwndSource>，为它指定类似于 CreateWindow 的参数。  然后，通知 <xref:System.Windows.Interop.HwndSource> 有关您要在其中包含的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容。  最后，从 <xref:System.Windows.Interop.HwndSource> 获取 HWND。  此演练演示如何在 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 应用程序中创建一个重新实现操作系统**“日期和时间属性”**对话框的混合 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]。  
  
## 系统必备  
 请参见 [WPF 和 Win32 互操作](../../../../docs/framework/wpf/advanced/wpf-and-win32-interoperation.md)。  
  
## 如何使用本教程  
 本教程重点介绍生成互操作应用程序的重要步骤。  本教程与示例 [Win32 Clock Interoperation Sample](http://go.microsoft.com/fwlink/?LinkID=160051)（Win32 时钟互操作示例）相关，但该示例只是反映了最终结果。  本教程介绍的步骤假定您正在开始操作自己的现有 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 项目（也许是一个已经存在的项目），并向应用程序添加一个承载的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]。  可以将最终结果与 [Win32 Clock Interoperation Sample](http://go.microsoft.com/fwlink/?LinkID=160051)（Win32 时钟互操作示例）进行比较。  
  
## 在 Win32 中承载 Windows Presentation Framework 的演练 \(HwndSource\)  
 下图显示了本教程预期的最终生成结果：  
  
 ![“日期和时间属性”对话框](../../../../docs/framework/wpf/advanced/media/interoparch06.png "InteropArch06")  
  
 您可以通过在 [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)] 中创建 C\+\+ [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 项目并使用对话框编辑器创建下列内容来重新创建此对话框：  
  
 ![“日期和时间属性”对话框](../../../../docs/framework/wpf/advanced/media/interoparch07.png "InteropArch07")  
  
 （您不需要通过 [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)] 来使用<xref:System.Windows.Interop.HwndSource>，也不需要使用 C\+\+ 来编写 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 程序，但是通常都这么做，这样更易于分步说明教程）。  
  
 您需要完成五个特定的子步骤才能将 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 时钟放入对话框：  
  
1.  通过更改 [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)] 中的项目设置，使您的 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 项目可以调用托管代码 \(**\/clr**\)。  
  
2.  在一个单独的 DLL 中创建 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.Page>。  
  
3.  将该 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.Page> 放入 <xref:System.Windows.Interop.HwndSource> 中。  
  
4.  使用 <xref:System.Windows.Interop.HwndSource.Handle%2A> 属性获取该 <xref:System.Windows.Controls.Page> 的 HWND。  
  
5.  使用 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 来确定大型 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 应用程序中用于放置此 HWND 的位置。  
  
## \/clr  
 第一步是将此非托管 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 项目转换为能够调用托管代码的项目。  使用 \/clr 编译器选项（该选项将链接到您要使用的所需 DLL），然后调整要用于 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的 Main 方法。  
  
 若要在 C\+\+ 项目中使用托管代码，请右击 win32clock 项目，然后选择**“属性”**。  在**“常规”**属性页（默认值）上，将公共语言运行时支持更改为 `/clr`。  
  
 接下来，添加对 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 所需的下列 DLL 的引用：PresentationCore.dll、PresentationFramework.dll、System.dll、WindowsBase.dll、UIAutomationProvider.dll 和 UIAutomationTypes.dll。  （下面的说明假定操作系统安装在 C: 驱动器上。）  
  
1.  右击 win32clock 项目，选择**“引用…”**，然后在此对话框中执行以下操作：  
  
2.  右击 win32clock 项目，然后选择**“引用…”**。  
  
3.  单击**“添加新引用”**，单击“浏览”选项卡，输入 C:\\Program Files\\Reference Assemblies\\Microsoft\\Framework\\v3.0\\PresentationCore.dll，然后单击“确定”。  
  
4.  对 PresentationFramework.dll 重复上述操作，但输入的是：C:\\Program Files\\Reference Assemblies\\Microsoft\\Framework\\v3.0\\PresentationFramework.dll。  
  
5.  对 WindowsBase.dll 重复上述操作，但输入的是：C:\\Program Files\\Reference Assemblies\\Microsoft\\Framework\\v3.0\\WindowsBase.dll。  
  
6.  对 UIAutomationTypes.dll 重复上述操作，但输入的是：C:\\Program Files\\Reference Assemblies\\Microsoft\\Framework\\v3.0\\UIAutomationTypes.dll。  
  
7.  对 UIAutomationProvider.dll 重复上述操作，但输入的是：C:\\Program Files\\Reference Assemblies\\Microsoft\\Framework\\v3.0\\UIAutomationProvider.dll。  
  
8.  单击**“添加新引用”**，选择 System.dll，然后单击**“确定”**。  
  
9. 单击**“确定”**退出用于添加引用的 win32clock 属性页。  
  
 最后，将 `STAThreadAttribute` 添加到用于 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 的 `_tWinMain` 方法：  
  
```  
[System::STAThreadAttribute]  
int APIENTRY _tWinMain(HINSTANCE hInstance,  
                     HINSTANCE hPrevInstance,  
                     LPTSTR    lpCmdLine,  
                     int       nCmdShow)  
```  
  
 该特性通知 [!INCLUDE[TLA#tla_clr](../../../../includes/tlasharptla-clr-md.md)] 当它初始化[!INCLUDE[TLA#tla_com](../../../../includes/tlasharptla-com-md.md)] 时，应当使用单线程的单元模型 \(STA\)，该模型对于 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 和 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]是必需的。  
  
## 创建 Windows Presentation Framework 页  
 接下来，创建定义 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.Page> 的 DLL。  通常最简便的方法是以独立应用程序的方式创建 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.Page>，然后按照相应的方式编写并调试 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 部分。  完成后，可以将该项目转换为 DLL，方法是右击该项目，单击**“属性”**，转到“应用程序”，然后将“输出类型”更改为“Windows 类库”。  
  
 然后 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] DLL 项目可以与 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 项目合并（包含两个项目的一个解决方案）\- 右击该解决方案，选择**“添加\\现有项目”**。  
  
 若要从 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 项目中使用该 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] DLL，需要添加引用：  
  
1.  右击 win32clock 项目，然后选择**“引用…”**。  
  
2.  单击**“添加新引用”**。  
  
3.  单击**“项目”**选项卡。  选择“WPFClock”，然后单击“确定”。  
  
4.  单击**“确定”**退出用于添加引用的 win32clock 属性页。  
  
## HwndSource  
 接下来，使用 <xref:System.Windows.Interop.HwndSource> 使 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.Page> 看起来与 HWND 一样。  请将以下代码块添加到 C\+\+ 文件：  
  
```  
namespace ManagedCode  
{  
    using namespace System;  
    using namespace System::Windows;  
    using namespace System::Windows::Interop;  
    using namespace System::Windows::Media;  
  
    HWND GetHwnd(HWND parent, int x, int y, int width, int height) {  
        HwndSource^ source = gcnew HwndSource(  
            0, // class style  
            WS_VISIBLE | WS_CHILD, // style  
            0, // exstyle  
            x, y, width, height,  
            "hi", // NAME  
            IntPtr(parent)        // parent window   
            );  
  
        UIElement^ page = gcnew WPFClock::Clock();  
        source->RootVisual = page;  
        return (HWND) source->Handle.ToPointer();  
    }  
}  
}  
```  
  
 这段代码内容较长，需要进一步解释。  第一部分包括各种子句，使您不需要完全限定所有调用：  
  
```  
namespace ManagedCode  
{  
    using namespace System;  
    using namespace System::Windows;  
    using namespace System::Windows::Interop;  
    using namespace System::Windows::Media;  
```  
  
 然后定义一个函数，该函数用于创建 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容、围绕其放置一个 <xref:System.Windows.Interop.HwndSource> 并返回 HWND：  
  
```  
HWND GetHwnd(HWND parent, int x, int y, int width, int height) {  
```  
  
 首先，创建一个 <xref:System.Windows.Interop.HwndSource>，其参数类似于 CreateWindow：  
  
```  
HwndSource^ source = gcnew HwndSource(  
    0, // class style  
    WS_VISIBLE | WS_CHILD, // style  
    0, // exstyle  
    x, y, width, height,  
    "hi", // NAME  
    IntPtr(parent) // parent window   
    );  
```  
  
 然后通过调用 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容类的构造函数创建该类：  
  
```  
UIElement^ page = gcnew WPFClock::Clock();  
```  
  
 然后将页连接到 <xref:System.Windows.Interop.HwndSource>：  
  
```  
source->RootVisual = page;  
```  
  
 在最后一行中，返回 <xref:System.Windows.Interop.HwndSource> 的 HWND：  
  
```  
return (HWND) source->Handle.ToPointer();  
```  
  
## 定位 HWND  
 生成了包含 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 时钟的 HWND 后，需要将此 HWND 放入 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 对话框。  如果您知道 HWND 的确切放置位置，您只需要将此大小和位置传递到以前定义的 `GetHwnd` 函数。  但是，由于您以前使用资源文件定义了对话框，因此您无法确定所有 HWND 的确切位置。  您可以使用 [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)] 对话框编辑器在要放置时钟的位置（“在此插入时钟”）添加一个 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] STATIC 控件，然后使用该控件定位 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 时钟。  
  
 如果要处理 WM\_INITDIALOG，则使用 `GetDlgItem` 来检索 STATIC 占位符的 HWND：  
  
```  
HWND placeholder = GetDlgItem(hDlg, IDC_CLOCK);  
```  
  
 然后计算该 STATIC 占位符的大小和位置，从而可以将 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 时钟放入该位置：  
  
 RECT rectangle;  
  
```  
GetWindowRect(placeholder, &rectangle);  
int width = rectangle.right - rectangle.left;  
int height = rectangle.bottom - rectangle.top;  
POINT point;  
point.x = rectangle.left;  
point.y = rectangle.top;  
result = MapWindowPoints(NULL, hDlg, &point, 1);  
```  
  
 然后隐藏 STATIC 占位符：  
  
```  
ShowWindow(placeholder, SW_HIDE);  
```  
  
 接着在此位置创建 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 时钟 HWND：  
  
```  
HWND clock = ManagedCode::GetHwnd(hDlg, point.x, point.y, width, height);  
```  
  
 为了使教程生动有趣，并生成一个真实的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 时钟，此时您需要创建一个 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 时钟控件。  一般可以在标记中完成此操作，在代码隐藏中使用几个事件处理程序即可。  由于本教程与互操作有关，而与控件设计无关，因此这里以代码块的形式提供 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 时钟的完整代码，而不另外说明如何生成这些代码以及每个部分的含义。  可以随意修改此代码来更改控件的外观或功能。  
  
 标记如下：  
  
 [!code-xml[Win32Clock#AllClockXAML](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Win32Clock/CS/Clock.xaml#allclockxaml)]  
  
 附带的代码隐藏如下：  
  
 [!code-csharp[Win32Clock#AllClockCS](../../../../samples/snippets/csharp/VS_Snippets_Wpf/Win32Clock/CS/Clock.xaml.cs#allclockcs)]  
  
 最终结果类似于：  
  
 ![“日期和时间属性”对话框](../../../../docs/framework/wpf/advanced/media/interoparch08.png "InteropArch08")  
  
 若要将您的最终结果与生成此屏幕快照的代码进行比较，请参见 [Win32 Clock Interoperation Sample](http://go.microsoft.com/fwlink/?LinkID=160051)（Win32 时钟互操作示例）。  
  
## 请参阅  
 <xref:System.Windows.Interop.HwndSource>   
 [WPF 和 Win32 互操作](../../../../docs/framework/wpf/advanced/wpf-and-win32-interoperation.md)   
 [Win32 Clock Interoperation Sample](http://go.microsoft.com/fwlink/?LinkID=160051)