---
title: "如何：使用 Windows 窗体 NotifyIcon 组件向任务栏添加应用程序图标 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "TrayIcon"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "图标, 添加到任务栏"
  - "NotifyIcon 组件"
  - "状态区域图标"
  - "任务栏, 添加图标"
ms.assetid: d28c0fe6-aaf2-4df7-ad74-928d861a8510
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：使用 Windows 窗体 NotifyIcon 组件向任务栏添加应用程序图标
Windows 窗体 <xref:System.Windows.Forms.NotifyIcon> 组件在任务栏的状态通知区域中显示单个图标。  若要在状态区域中显示多个图标，则必须在窗体上要有多个 <xref:System.Windows.Forms.NotifyIcon> 组件。  若要为控件设置所显示的图标，请使用 <xref:System.Windows.Forms.NotifyIcon.Icon%2A> 属性。  也可以在 <xref:System.Windows.Forms.NotifyIcon.DoubleClick> 事件处理程序中编写代码，以便当用户双击图标时执行相应操作。  例如，可以为用户显示一个对话框，以便配置由图标表示的后台处理。  
  
> [!NOTE]
>  <xref:System.Windows.Forms.NotifyIcon> 组件仅用于通知目的，以提醒用户发生了某一操作或事件，或发生了某种状态更改。  您应该使用菜单、工具栏和其他用户界面元素与应用程序进行标准交互。  
  
### 设置图标  
  
1.  向 <xref:System.Windows.Forms.NotifyIcon.Icon%2A> 属性赋值。  该值的类型必须为  `System.Drawing.Icon` ，并可以从 .ico 文件加载。  您可以用代码指定图标文件，或者通过单击**“属性”**窗口中 <xref:System.Windows.Forms.NotifyIcon.Icon%2A> 属性旁边的省略号按钮 \(![VisualStudioEllipsesButton 屏幕快照](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\)，然后在显示的**“打开”**对话框中选择文件来指定图标文件。  
  
2.  将 <xref:System.Windows.Forms.NotifyIcon.Visible%2A> 属性设置为 `true`。  
  
3.  将 <xref:System.Windows.Forms.NotifyIcon.Text%2A> 属性设置为相应的工具提示字符串。  
  
     在下面的代码示例中，图标位置的路径设置是 **My Documents** 文件夹。  使用此位置是因为可假定大多数运行 Windows 操作系统的计算机都包含该文件夹。  选择此位置还能让具有最低系统访问级别的用户安全地运行应用程序。  下面的示例需要一个已添加 <xref:System.Windows.Forms.NotifyIcon> 控件的窗体。  它还需要一个名为 `Icon.ico` 的图标文件。  
  
     \[Visual Basic\]  
  
    ```  
    ' You should replace the bold icon in the sample below  
    ' with an icon of your own choosing.  
    NotifyIcon1.Icon = New _   
       System.Drawing.Icon(System.Environment.GetFolderPath _  
       (System.Environment.SpecialFolder.Personal) _  
       & "\Icon.ico")  
    NotifyIcon1.Visible = True  
    NotifyIcon1.Text = "Antivirus program"  
  
    ```  
  
     \[C\#\]  
  
    ```  
    // You should replace the bold icon in the sample below  
    // with an icon of your own choosing.  
    // Note the escape character used (@) when specifying the path.  
    notifyIcon1.Icon =   
       new System.Drawing.Icon (System.Environment.GetFolderPath  
       (System.Environment.SpecialFolder.Personal)  
       + @"\Icon.ico");  
    notifyIcon1.Visible = true;  
    notifyIcon1.Text = "Antivirus program";  
  
    ```  
  
     \[cpp\]  
  
    ```  
    // You should replace the bold icon in the sample below  
    // with an icon of your own choosing.  
    notifyIcon1->Icon = gcnew   
       System::Drawing::Icon(String::Concat  
       (System::Environment::GetFolderPath  
       (System::Environment::SpecialFolder::Personal),  
       "\\Icon.ico"));  
    notifyIcon1->Visible = true;  
    notifyIcon1->Text = "Antivirus program";  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.NotifyIcon>   
 <xref:System.Windows.Forms.NotifyIcon.Icon%2A>   
 [如何：将快捷菜单与 Windows 窗体 NotifyIcon 组件关联](../../../../docs/framework/winforms/controls/how-to-associate-a-shortcut-menu-with-a-windows-forms-notifyicon-component.md)   
 [NotifyIcon 组件](../../../../docs/framework/winforms/controls/notifyicon-component-windows-forms.md)   
 [NotifyIcon 组件概述](../../../../docs/framework/winforms/controls/notifyicon-component-overview-windows-forms.md)