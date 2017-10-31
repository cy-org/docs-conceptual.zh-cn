---
title: "在 WPF 中承载 Win32 内容 | Microsoft Docs"
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
ms.assetid: 3cc8644a-34f3-4082-9ddc-77623e4df2d8
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 在 WPF 中承载 Win32 内容
## 系统必备  
 请参见 [WPF 和 Win32 互操作](../../../../docs/framework/wpf/advanced/wpf-and-win32-interoperation.md)。  
  
## 在 Windows Presentation Framework 中承载 Win32 的演练 \(HwndHost\)  
 若要在 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序中重复使用 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 内容，请使用 <xref:System.Windows.Interop.HwndHost>，该控件使 HWND 看起来像是 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容。  与 <xref:System.Windows.Interop.HwndSource> 一样，<xref:System.Windows.Interop.HwndHost> 简单易用：从 <xref:System.Windows.Interop.HwndHost> 派生，并实现 `BuildWindowCore` 和 `DestroyWindowCore` 方法，然后实例化 <xref:System.Windows.Interop.HwndHost> 派生类，最后将其放入 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序。  
  
 如果 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 逻辑已经打包为一个控件，则调用 `CreateWindow` 并执行少量的操作便可以完成 `BuildWindowCore` 实现。  例如，若要在 [!INCLUDE[TLA#tla_cpp](../../../../includes/tlasharptla-cpp-md.md)] 中创建 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] LISTBOX 控件：  
  
```  
virtual HandleRef BuildWindowCore(HandleRef hwndParent) override {  
    HWND handle = CreateWindowEx(0, L"LISTBOX",   
    L"this is a Win32 listbox",  
    WS_CHILD | WS_VISIBLE | LBS_NOTIFY  
    | WS_VSCROLL | WS_BORDER,  
    0, 0, // x, y  
    30, 70, // height, width  
    (HWND) hwndParent.Handle.ToPointer(), // parent hwnd  
    0, // hmenu  
    0, // hinstance  
    0); // lparam  
  
    return HandleRef(this, IntPtr(handle));  
}  
  
virtual void DestroyWindowCore(HandleRef hwnd) override {  
    // HwndHost will dispose the hwnd for us  
}  
```  
  
 但是，如果 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 代码并非如此独立，那么该怎么办？  如果是这样，则可以创建一个 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 对话框，然后将其内容嵌入到一个更大的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序中。  该示例中使用 [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)] 和 [!INCLUDE[TLA#tla_cpp](../../../../includes/tlasharptla-cpp-md.md)] 演示此操作，不过您也可以使用其他语言或者在命令行上完成此操作。  
  
 首先，创建一个编译为 [!INCLUDE[TLA#tla_cpp](../../../../includes/tlasharptla-cpp-md.md)] [!INCLUDE[TLA2#tla_dll](../../../../includes/tla2sharptla-dll-md.md)] 项目的简单对话框。  
  
 接下来，将该对话框引入到更大的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序中：  
  
-   将 [!INCLUDE[TLA2#tla_dll](../../../../includes/tla2sharptla-dll-md.md)] 编译为托管 \(`/clr`\)  
  
-   将对话框转换为控件  
  
-   使用 `BuildWindowCore` 和 `DestroyWindowCore` 方法定义 <xref:System.Windows.Interop.HwndHost> 的派生类  
  
-   重写 `TranslateAccelerator` 方法以处理对话框键  
  
-   重写 `TabInto` 方法以支持 Tab 键控  
  
-   重写 `OnMnemonic` 方法以支持助记键  
  
-   实例化 <xref:System.Windows.Interop.HwndHost> 子类，并将其放置在正确的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 元素下  
  
### 将对话框转换为控件  
 您可以使用 WS\_CHILD 和 DS\_CONTROL 样式将对话框转换为子 HWND。  转到定义对话框的资源文件 \(.rc\)，找到对话框定义的开始位置：  
  
```  
IDD_DIALOG1 DIALOGEX 0, 0, 303, 121  
STYLE DS_SETFONT | DS_MODALFRAME | DS_FIXEDSYS | WS_POPUP | WS_CAPTION | WS_SYSMENU  
```  
  
 将第二行代码更改为：  
  
```  
STYLE DS_SETFONT | WS_CHILD | WS_BORDER | DS_CONTROL  
```  
  
 此操作不会将其完全打包为独立控件；尽管您仍需要调用 `IsDialogMessage()` 以便 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 可以处理某些消息，但是控件更改确实提供了一种可将这些控件放入另一个 HWND 的简便方法。  
  
## 子类 HwndHost  
 导入下列命名空间：  
  
```  
namespace ManagedCpp  
{  
    using namespace System;  
    using namespace System::Windows;  
    using namespace System::Windows::Interop;  
    using namespace System::Windows::Input;  
    using namespace System::Windows::Media;  
    using namespace System::Runtime::InteropServices;  
```  
  
 然后创建 <xref:System.Windows.Interop.HwndHost> 的派生类，并重写 `BuildWindowCore` 和 `DestroyWindowCore` 方法：  
  
```  
public ref class MyHwndHost : public HwndHost, IKeyboardInputSink {  
    private:  
        HWND dialog;  
  
    protected:   
        virtual HandleRef BuildWindowCore(HandleRef hwndParent) override {  
            InitializeGlobals();   
            dialog = CreateDialog(hInstance,   
                MAKEINTRESOURCE(IDD_DIALOG1),   
                (HWND) hwndParent.Handle.ToPointer(),  
                (DLGPROC) About);   
            return HandleRef(this, IntPtr(dialog));  
        }  
  
        virtual void DestroyWindowCore(HandleRef hwnd) override {  
            // hwnd will be disposed for us  
        }  
```  
  
 现在，请使用 `CreateDialog` 创建对话框，该对话框实际上是一个控件。  因为这是在 [!INCLUDE[TLA2#tla_dll](../../../../includes/tla2sharptla-dll-md.md)] 中调用的前几个方法之一，所以还应当通过调用您稍后定义的函数 `InitializeGlobals()` 来进行一些标准的 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 初始化。  
  
```  
bool initialized = false;  
    void InitializeGlobals() {  
        if (initialized) return;  
        initialized = true;  
  
        // TODO: Place code here.  
        MSG msg;  
        HACCEL hAccelTable;  
  
        // Initialize global strings  
        LoadString(hInstance, IDS_APP_TITLE, szTitle, MAX_LOADSTRING);  
        LoadString(hInstance, IDC_TYPICALWIN32DIALOG, szWindowClass, MAX_LOADSTRING);  
        MyRegisterClass(hInstance);  
  
```  
  
### 重写 TranslateAccelerator 方法以处理对话框键  
 如果您现在运行此示例，则可以看到一个显示的对话框控件，但是该示例会忽略所有能够使某个对话框变成有用对话框的键盘处理。  您现在应当重写 `TranslateAccelerator` 实现（来自 <xref:System.Windows.Interop.HwndHost> 实现的接口 `IKeyboardInputSink`）。  当应用程序收到 WM\_KEYDOWN 和 WM\_SYSKEYDOWN 时会调用该方法。  
  
```  
  
#undef TranslateAccelerator  
        virtual bool TranslateAccelerator(System::Windows::Interop::MSG% msg,   
            ModifierKeys modifiers) override   
        {  
            ::MSG m = ConvertMessage(msg);  
  
            // Win32's IsDialogMessage() will handle most of our tabbing, but doesn't know   
            // what to do when it reaches the last tab stop  
            if (m.message == WM_KEYDOWN && m.wParam == VK_TAB) {  
                HWND firstTabStop = GetDlgItem(dialog, IDC_EDIT1);  
                HWND lastTabStop = GetDlgItem(dialog, IDCANCEL);  
                TraversalRequest^ request = nullptr;  
  
                if (GetKeyState(VK_SHIFT) && GetFocus() == firstTabStop) {  
                    // this code should work, but there’s a bug with interop shift-tab in current builds                      
                    request = gcnew TraversalRequest(FocusNavigationDirection::Last);  
                }  
                else if (!GetKeyState(VK_SHIFT) && GetFocus() == lastTabStop) {  
                    request = gcnew TraversalRequest(FocusNavigationDirection::Next);  
                }  
  
                if (request != nullptr)  
                    return ((IKeyboardInputSink^) this)->KeyboardInputSite->OnNoMoreTabStops(request);  
  
            }  
  
            // Only call IsDialogMessage for keys it will do something with.  
            if (msg.message == WM_SYSKEYDOWN || msg.message == WM_KEYDOWN) {  
                switch (m.wParam) {  
                    case VK_TAB:  
                    case VK_LEFT:  
                    case VK_UP:  
                    case VK_RIGHT:  
                    case VK_DOWN:  
                    case VK_EXECUTE:  
                    case VK_RETURN:  
                    case VK_ESCAPE:  
                    case VK_CANCEL:  
                        IsDialogMessage(dialog, &m);  
                        // IsDialogMessage should be called ProcessDialogMessage --  
                        // it processes messages without ever really telling you  
                        // if it handled a specific message or not  
                        return true;  
                }  
            }  
  
            return false; // not a key we handled  
        }  
```  
  
 这段包含很多代码，需要进行详细解释。  首先，该代码使用 [!INCLUDE[TLA#tla_cpp](../../../../includes/tlasharptla-cpp-md.md)] 和 [!INCLUDE[TLA#tla_cpp](../../../../includes/tlasharptla-cpp-md.md)] 宏；您需要知道已经存在一个名为 `TranslateAccelerator` 的宏，它是在 winuser.h 中定义的：  
  
```  
#define TranslateAccelerator  TranslateAcceleratorW  
```  
  
 因此，请确保定义的是 `TranslateAccelerator` 方法而不是 `TranslateAcceleratorW` 方法。  
  
 同样，同时存在非托管 winuser.h MSG 和托管 `Microsoft::Win32::MSG` 结构。  您可以使用 [!INCLUDE[TLA#tla_cpp](../../../../includes/tlasharptla-cpp-md.md)] `::` 运算符来消除两者之间的歧义。  
  
```  
  
virtual bool TranslateAccelerator(System::Windows::Interop::MSG% msg,   
    ModifierKeys modifiers) override   
{  
    ::MSG m = ConvertMessage(msg);  
```  
  
 两个 MSG 有相同的数据，但是有时使用非托管定义更容易，因此在本示例中，您可以定义明显转换例程：  
  
```  
::MSG ConvertMessage(System::Windows::Interop::MSG% msg) {  
    ::MSG m;  
    m.hwnd = (HWND) msg.hwnd.ToPointer();  
    m.lParam = (LPARAM) msg.lParam.ToPointer();  
    m.message = msg.message;  
    m.wParam = (WPARAM) msg.wParam.ToPointer();  
  
    m.time = msg.time;  
  
    POINT pt;  
    pt.x = msg.pt_x;  
    pt.y = msg.pt_y;  
    m.pt = pt;  
  
    return m;  
}  
```  
  
 返回到 `TranslateAccelerator`。  基本原则是调用 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 函数 `IsDialogMessage` 以尽量执行更多的操作，但是 `IsDialogMessage` 无权访问对话框外部的任何内容。当用户在对话框中按 Tab 键，并且 Tab 键遍历了对话框中的最后一个控件时，您需要通过调用 `IKeyboardInputSite::OnNoMoreStops` 来将焦点设置到 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 部分。  
  
```  
// Win32's IsDialogMessage() will handle most of the tabbing, but doesn't know   
// what to do when it reaches the last tab stop  
if (m.message == WM_KEYDOWN && m.wParam == VK_TAB) {  
    HWND firstTabStop = GetDlgItem(dialog, IDC_EDIT1);  
    HWND lastTabStop = GetDlgItem(dialog, IDCANCEL);  
    TraversalRequest^ request = nullptr;  
  
    if (GetKeyState(VK_SHIFT) && GetFocus() == firstTabStop) {  
        request = gcnew TraversalRequest(FocusNavigationDirection::Last);  
    }  
    else if (!GetKeyState(VK_SHIFT) && GetFocus() ==  lastTabStop) { {  
        request = gcnew TraversalRequest(FocusNavigationDirection::Next);  
    }  
  
    if (request != nullptr)  
        return ((IKeyboardInputSink^) this)->KeyboardInputSite->OnNoMoreTabStops(request);  
}  
```  
  
 最后，调用 `IsDialogMessage`。  但是 `TranslateAccelerator` 方法的责任之一是通知 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 您是否处理了键击。  如果您尚未处理，则输入事件可以向下或向上传递到应用程序的其他部分。  此时，您需要公开键盘消息处理的杂项和 [!INCLUDE[TLA2#tla_win32](../../../../includes/tla2sharptla-win32-md.md)] 中输入体系结构的性质。  不过，`IsDialogMessage` 无论如何不会返回它是否处理了特定键击。  更糟糕的是，它会对不应处理的键击调用 `DispatchMessage()`！  因此，您不得不对 `IsDialogMessage` 进行反向工程处理，并仅针对已知它将处理的键来调用它：  
  
```  
// Only call IsDialogMessage for keys it will do something with.  
if (msg.message == WM_SYSKEYDOWN || msg.message == WM_KEYDOWN) {  
    switch (m.wParam) {  
        case VK_TAB:  
        case VK_LEFT:  
        case VK_UP:  
        case VK_RIGHT:  
        case VK_DOWN:  
        case VK_EXECUTE:  
        case VK_RETURN:  
        case VK_ESCAPE:  
        case VK_CANCEL:  
            IsDialogMessage(dialog, &m);  
            // IsDialogMessage should be called ProcessDialogMessage --  
            // it processes messages without ever really telling you  
            // if it handled a specific message or not  
            return true;  
    }  
```  
  
### 重写 TabInto 方法以支持 Tab 键控  
 既然实现了 `TranslateAccelerator`，用户现在可以在对话框中按 Tab 键离开对话框，转移到更大的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序。  但是，用户不能按 Tab 键返回该对话框。  要解决这个问题，您需要重写 `TabInto`：  
  
```  
  
public:   
    virtual bool TabInto(TraversalRequest^ request) override {  
        if (request->FocusNavigationDirection == FocusNavigationDirection::Last) {  
            HWND lastTabStop = GetDlgItem(dialog, IDCANCEL);  
            SetFocus(lastTabStop);  
        }  
        else {  
            HWND firstTabStop = GetDlgItem(dialog, IDC_EDIT1);  
            SetFocus(firstTabStop);  
        }  
        return true;  
    }  
  
```  
  
 `TraversalRequest` 参数通知您 Tab 操作是普通的 Tab 还是 Shift Tab。  
  
### 重写 OnMnemonic 方法以支持助记键  
 键盘处理已基本完成，但是还有一件事情需要处理 \- 助记键还不能工作。  如果用户按 Alt\-F，焦点不会跳到“First name:”（名字:）编辑框。  因此，请重写 `OnMnemonic` 方法：  
  
```  
virtual bool OnMnemonic(System::Windows::Interop::MSG% msg, ModifierKeys modifiers) override {  
    ::MSG m = ConvertMessage(msg);  
  
    // If it's one of our mnemonics, set focus to the appropriate hwnd  
    if (msg.message == WM_SYSCHAR && GetKeyState(VK_MENU /*alt*/)) {  
        int dialogitem = 9999;  
        switch (m.wParam) {  
            case 's': dialogitem = IDOK; break;  
            case 'c': dialogitem = IDCANCEL; break;  
            case 'f': dialogitem = IDC_EDIT1; break;  
            case 'l': dialogitem = IDC_EDIT2; break;  
            case 'p': dialogitem = IDC_EDIT3; break;  
            case 'a': dialogitem = IDC_EDIT4; break;  
            case 'i': dialogitem = IDC_EDIT5; break;  
            case 't': dialogitem = IDC_EDIT6; break;  
            case 'z': dialogitem = IDC_EDIT7; break;  
        }  
        if (dialogitem != 9999) {  
            HWND hwnd = GetDlgItem(dialog, dialogitem);  
            SetFocus(hwnd);  
            return true;  
        }  
    }  
    return false; // key unhandled  
};  
```  
  
 为什么不在此调用 `IsDialogMessage`？  与前面的问题相同：您需要能够通知 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 代码您的代码是否已处理键击，但 `IsDialogMessage` 不能实现这一点。  同时，还存在另一个原因：如果获得焦点的 HWND 不在对话框内，`IsDialogMessage` 会拒绝处理助记键。  
  
### 实例化 HwndHost 派生类  
 最后，既然所有键和 Tab 键控支持都已准备就绪，您可以将您的 <xref:System.Windows.Interop.HwndHost> 放入更大的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序中。  如果主应用程序是使用 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 编写的，将其放入正确位置的最简便方式是在您想放入 <xref:System.Windows.Interop.HwndHost> 的位置保留一个空的 <xref:System.Windows.Controls.Border> 元素。  您可以在这里创建一个名为 `insertHwndHostHere` 的 <xref:System.Windows.Controls.Border>：  
  
```  
<Window x:Class="WPFApplication1.Window1"  
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
    Title="Windows Presentation Framework Application"  
    Loaded="Window1_Loaded"  
    >  
    <StackPanel>  
        <Button Content="WPF button"/>  
        <Border Name="insertHwndHostHere" Height="200" Width="500"/>  
        <Button Content="WPF button"/>  
    </StackPanel>  
</Window>  
```  
  
 至此，剩下的操作就是在代码序列中找到一个适当的位置来实例化 <xref:System.Windows.Interop.HwndHost>，并将其连接到 <xref:System.Windows.Controls.Border>。  在以下示例中，您可以将其放置到 <xref:System.Windows.Window> 派生类的构造函数中：  
  
```  
public partial class Window1 : Window {  
    public Window1() {  
    }  
  
    void Window1_Loaded(object sender, RoutedEventArgs e) {  
        HwndHost host = new ManagedCpp.MyHwndHost();  
        insertHwndHostHere.Child = host;  
    }  
}  
```  
  
 您会得到以下结果：  
  
 ![WPF 应用程序屏幕快照](../../../../docs/framework/wpf/advanced/media/interoparch09.png "InteropArch09")  
  
## 请参阅  
 [WPF 和 Win32 互操作](../../../../docs/framework/wpf/advanced/wpf-and-win32-interoperation.md)