---
title: "如何：将快捷菜单与 Windows 窗体 NotifyIcon 组件关联 | Microsoft Docs"
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
  - "上下文菜单, 用于后台进程"
  - "NotifyIcon 组件, 关联快捷菜单"
  - "快捷菜单, 用于后台进程"
ms.assetid: d68f3926-08d3-4f7d-949f-1981b29cf188
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# 如何：将快捷菜单与 Windows 窗体 NotifyIcon 组件关联
> [!NOTE]
>  尽管 <xref:System.Windows.Forms.MenuStrip> 和 <xref:System.Windows.Forms.ContextMenuStrip> 取代了早期版本的 <xref:System.Windows.Forms.MainMenu> 和 <xref:System.Windows.Forms.ContextMenu> 控件并添加了功能，但是，可以选择保留 <xref:System.Windows.Forms.MainMenu> 和 <xref:System.Windows.Forms.ContextMenu> 以实现向后兼容并供将来使用。  
  
 <xref:System.Windows.Forms.NotifyIcon> 组件在任务栏的状态通知区域中显示一个图标。  通常，应用程序允许您右击此图标将命令发送到它表示的应用程序。  将 <xref:System.Windows.Forms.ContextMenu> 组件与 <xref:System.Windows.Forms.NotifyIcon> 组件关联，便可以将此功能添加到应用程序中。  
  
> [!NOTE]
>  如果要让应用程序在启动时最小化，同时在任务栏中显示 <xref:System.Windows.Forms.NotifyIcon> 组件的一个实例，可将主窗体的 <xref:System.Windows.Forms.Form.WindowState%2A> 属性设置为 <xref:System.Windows.Forms.FormWindowState>，并确保将 <xref:System.Windows.Forms.NotifyIcon> 组件的 <xref:System.Windows.Forms.NotifyIcon.Visible%2A> 属性设置为 `true`。  
  
### 在设计时将快捷菜单与 NotifyIcon 组件关联  
  
1.  向窗体添加 <xref:System.Windows.Forms.NotifyIcon> 组件，并设置重要属性，如 <xref:System.Windows.Forms.NotifyIcon.Icon%2A> 和 <xref:System.Windows.Forms.NotifyIcon.Visible%2A> 属性。  
  
     有关更多信息，请参见 [如何：使用 Windows 窗体 NotifyIcon 组件向任务栏添加应用程序图标](../../../../docs/framework/winforms/controls/app-icons-to-the-taskbar-with-wf-notifyicon.md)。  
  
2.  向 Windows 窗体添加 <xref:System.Windows.Forms.ContextMenu> 组件。  
  
     向表示您希望在运行时使其可用的命令的快捷菜单添加菜单项。  这也是向这些菜单项添加菜单增强功能的好时机，如访问键。  
  
3.  将 <xref:System.Windows.Forms.NotifyIcon> 组件的 <xref:System.Windows.Forms.NotifyIcon.ContextMenu%2A> 属性设置为您添加的快捷菜单。  
  
     设置此属性后，单击任务栏上的图标时将显示快捷菜单。  
  
### 以编程方式将快捷菜单与 NotifyIcon 组件关联  
  
1.  使用应用程序所需的任何属性设置（<xref:System.Windows.Forms.NotifyIcon> 组件的 <xref:System.Windows.Forms.NotifyIcon.Icon%2A> 和 <xref:System.Windows.Forms.NotifyIcon.Visible%2A> 属性，<xref:System.Windows.Forms.ContextMenu> 组件的菜单项），创建 <xref:System.Windows.Forms.NotifyIcon> 类的一个实例和一个 <xref:System.Windows.Forms.ContextMenu> 类。  
  
2.  将 <xref:System.Windows.Forms.NotifyIcon> 组件的 <xref:System.Windows.Forms.NotifyIcon.ContextMenu%2A> 属性设置为您添加的快捷菜单。  
  
     设置此属性后，单击任务栏上的图标时将显示快捷菜单。  
  
    > [!NOTE]
    >  下面的代码示例可创建基本菜单结构。  您需要将菜单选项自定义为适合正在开发的应用程序的菜单项。  另外，您需要编写处理这些菜单项的 <xref:System.Windows.Forms.MenuItem.Click> 事件的代码。  
  
    ```vb  
    Public ContextMenu1 As New ContextMenu  
    Public NotifyIcon1 As New NotifyIcon  
  
    Public Sub CreateIconMenuStructure()  
       ' Add menu items to shortcut menu.  
       ContextMenu1.MenuItems.Add("&Open Application")  
       ContextMenu1.MenuItems.Add("S&uspend Application")  
       ContextMenu1.MenuItems.Add("E&xit")  
  
       ' Set properties of NotifyIcon component.  
       NotifyIcon1.Icon = New System.Drawing.Icon _   
          (System.Environment.GetFolderPath _   
          (System.Environment.SpecialFolder.Personal)  _   
          & "\Icon.ico")  
       NotifyIcon1.Text = "Right-click me!"  
       NotifyIcon1.Visible = True  
       NotifyIcon1.ContextMenu = ContextMenu1  
    End Sub  
  
    ```  
  
```csharp  
public NotifyIcon notifyIcon1 = new NotifyIcon();  
public ContextMenu contextMenu1 = new ContextMenu();  
  
public void createIconMenuStructure()  
{  
   // Add menu items to shortcut menu.  
   contextMenu1.MenuItems.Add("&Open Application");  
   contextMenu1.MenuItems.Add("S&uspend Application");  
   contextMenu1.MenuItems.Add("E&xit");  
  
   // Set properties of NotifyIcon component.  
   notifyIcon1.Icon = new System.Drawing.Icon  
      (System.Environment.GetFolderPath  
      (System.Environment.SpecialFolder.Personal)  
      + @"\Icon.ico");  
   notifyIcon1.Visible = true;  
   notifyIcon1.Text = "Right-click me!";  
   notifyIcon1.Visible = true;  
   notifyIcon1.ContextMenu = contextMenu1;  
}  
  
```  
  
```cpp  
public:  
   System::Windows::Forms::NotifyIcon ^ notifyIcon1;  
   System::Windows::Forms::ContextMenu ^ contextMenu1;  
  
   void createIconMenuStructure()  
   {  
      // Add menu items to shortcut menu.  
      contextMenu1->MenuItems->Add("&Open Application");  
      contextMenu1->MenuItems->Add("S&uspend Application");  
      contextMenu1->MenuItems->Add("E&xit");  
  
      // Set properties of NotifyIcon component.  
      notifyIcon1->Icon = gcnew System::Drawing::Icon  
          (String::Concat(System::Environment::GetFolderPath  
          (System::Environment::SpecialFolder::Personal),  
          "\\Icon.ico"));  
      notifyIcon1->Text = "Right-click me!";  
      notifyIcon1->Visible = true;  
      notifyIcon1->ContextMenu = contextMenu1;  
   }  
```  
  
> [!NOTE]
>  必须初始化 `notifyIcon1` 和 `contextMenu1,`，可以通过在窗体的构造函数中包含以下语句来执行此操作：  
  
```cpp  
notifyIcon1 = gcnew System::Windows::Forms::NotifyIcon();  
contextMenu1 = gcnew System::Windows::Forms::ContextMenu();  
```  
  
## 请参阅  
 <xref:System.Windows.Forms.NotifyIcon>   
 <xref:System.Windows.Forms.NotifyIcon.Icon%2A>   
 [如何：使用 Windows 窗体 NotifyIcon 组件向任务栏添加应用程序图标](../../../../docs/framework/winforms/controls/app-icons-to-the-taskbar-with-wf-notifyicon.md)   
 [NotifyIcon 组件](../../../../docs/framework/winforms/controls/notifyicon-component-windows-forms.md)   
 [NotifyIcon 组件概述](../../../../docs/framework/winforms/controls/notifyicon-component-overview-windows-forms.md)