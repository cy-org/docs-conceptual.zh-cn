---
title: "Windows 窗体中额外的安全注意事项 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "API 调用, Windows 窗体安全设置"
  - "API, 调用"
  - "剪贴板, 保证访问安全"
  - "安全性 [Windows 窗体]"
  - "安全性 [Windows 窗体], 调用 API"
  - "Windows API, 调用"
  - "Windows API, 安全调用"
  - "Windows API, Windows 窗体安全设置"
  - "Windows 窗体, 对 Windows API 的安全调用"
ms.assetid: 15abda8b-0527-47c7-aedb-77ab595f2bf1
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# Windows 窗体中额外的安全注意事项
[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 安全设置可能导致应用程序在部分信任环境中运行与在本地计算机上运行有所不同。  [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 限制对关键本地资源的访问，如文件系统、网络和非托管 API 等。  安全性设置会影响对安全系统无法验证的 Microsoft Win32 API 或其他 API 进行调用的能力。  安全性还会影响应用程序的其他方面，包括文件和数据访问以及打印。  有关在部分信任环境中访问文件和数据的更多信息，请参见 [Windows 窗体中更加安全的文件和数据访问](../../../docs/framework/winforms/more-secure-file-and-data-access-in-windows-forms.md)。  有关在部分信任环境中进行打印的更多信息，请参见 [Windows 窗体中的更加安全的打印](../../../docs/framework/winforms/more-secure-printing-in-windows-forms.md)。  
  
 以下各节讨论从在部分信任环境下运行的应用程序中，如何使用剪贴板，如何执行窗口操作以及如何调用 Win32 API。  
  
## 剪贴板访问  
 <xref:System.Security.Permissions.UIPermission> 类控制对剪贴板的访问，而相关联的 <xref:System.Security.Permissions.UIPermissionClipboard> 枚举值指示访问级别。  下表显示可能的权限级别。  
  
|UIPermissionClipboard 值|说明|  
|-----------------------------|--------|  
|<xref:System.Security.Permissions.UIPermissionClipboard>|可以随意使用剪贴板而无任何限制。|  
|<xref:System.Security.Permissions.UIPermissionClipboard>|使用剪贴板时有某些限制。  将数据放置到剪贴板中的能力（“复制”或“剪切”命令操作）是不受限制的。  接受粘贴的内部控件（例如文本框）可接受剪贴板数据，但用户控件无法以编程方式从剪贴板读取数据。|  
|<xref:System.Security.Permissions.UIPermissionClipboard>|不能使用剪贴板。|  
  
 默认情况下，“本地 Intranet”区域接收 <xref:System.Security.Permissions.UIPermissionClipboard> 访问，而“Internet”区域接收 <xref:System.Security.Permissions.UIPermissionClipboard> 访问。  这意味着，应用程序可以将数据复制到剪贴板，但无法通过编程方式进行粘贴或从剪贴板进行读取。  这些限制可以防止不完全受信任的程序读取另一应用程序复制到剪贴板中的内容。  如果应用程序需要完全的剪贴板访问权限，但您又不具有这些权限，则必须提升应用程序的权限。  有关提升权限的更多信息，请参见[常规安全策略管理](http://msdn.microsoft.com/zh-cn/5121fe35-f0e3-402c-94ab-4f35b0a87b4b)。  
  
## 窗口操作  
 <xref:System.Security.Permissions.UIPermission> 类还控制执行窗口操作和其他 UI 相关操作的权限，其关联的 <xref:System.Security.Permissions.UIPermissionWindow> 枚举值用于指示访问级别。  下表显示可能的权限级别。  
  
 默认情况下，“本地 Intranet”区域接收 <xref:System.Security.Permissions.UIPermissionWindow> 访问，而“Internet”区域接收 <xref:System.Security.Permissions.UIPermissionWindow> 访问。  这意味着，在“Internet”区域中，应用程序可以执行大多数窗口操作和 UI 操作，但窗口的外观将被修改。  修改后的窗口在第一次运行时将显示一则旁述通知，包含修改的标题栏文本，并需要标题栏上有一个关闭按钮。  气球状通知和标题栏将向应用程序的用户标识：应用程序正在部分信任环境下运行。  
  
|UIPermissionWindow 值|说明|  
|--------------------------|--------|  
|<xref:System.Security.Permissions.UIPermissionWindow>|用户可以不受限制地使用所有窗口和用户输入事件。|  
|<xref:System.Security.Permissions.UIPermissionWindow>|用户只能使用较安全的顶级窗口和子窗口进行绘制，并且只能在这些顶级窗口和子窗口中使用用户界面的用户输入事件。  这些较安全窗口具有明显的标签，并具有最小化和最大化限制。  这些限制可以防止潜在的有害欺骗攻击（例如模拟系统登录屏幕或系统桌面），还可以限制对父窗口及与焦点相关的 API 的编程访问以及 <xref:System.Windows.Forms.ToolTip> 控件的使用。|  
|<xref:System.Security.Permissions.UIPermissionWindow>|用户只能使用较安全子窗口进行绘制，并且只能在该子窗口中使用用户界面的用户输入事件。  浏览器中显示的控件就是一个较安全子窗口的示例。|  
|<xref:System.Security.Permissions.UIPermissionWindow>|用户不能使用任何窗口或用户界面事件。  不能使用任何用户界面。|  
  
 <xref:System.Security.Permissions.UIPermissionWindow> 枚举标识的每个权限级别都只能执行比上一级别更少的操作。  以下各表指示由 <xref:System.Security.Permissions.UIPermissionWindow> 和 <xref:System.Security.Permissions.UIPermissionWindow> 值限制的操作。  有关每个成员所需的确切权限，请参见 .NET Framework 类库文档中有关该成员的参考。  
  
 <xref:System.Security.Permissions.UIPermissionWindow> 权限限制下表中列出的操作。  
  
|组件|受限制的操作|  
|--------|------------|  
|<xref:System.Windows.Forms.Application>|-   设置 <xref:System.Windows.Forms.Application.SafeTopLevelCaptionFormat%2A> 属性。|  
|<xref:System.Windows.Forms.Control>|-   获取 <xref:System.Windows.Forms.Control.Parent%2A> 属性。<br />-   设置 `Region` 属性。<br />-   调用 <xref:System.Windows.Forms.Control.FindForm%2A>、<xref:System.Windows.Forms.Control.Focus%2A>、<xref:System.Windows.Forms.Control.FromChildHandle%2A> 和 <xref:System.Windows.Forms.Control.FromHandle%2A>、<xref:System.Windows.Forms.Control.PreProcessMessage%2A>、<xref:System.Windows.Forms.Control.ReflectMessage%2A> 或 <xref:System.Windows.Forms.Control.SetTopLevel%2A> 方法。<br />-   如果返回的控件不是正在调用控件的子控件，则调用 <xref:System.Windows.Forms.Control.GetChildAtPoint%2A> 方法。<br />-   修改容器控件内部的控件焦点。|  
|<xref:System.Windows.Forms.Cursor>|-   设置 <xref:System.Windows.Forms.Cursor.Clip%2A> 属性。<br />-   调用 <xref:System.Windows.Forms.Control.Hide%2A> 方法。|  
|<xref:System.Windows.Forms.DataGrid>|-   调用 <xref:System.Windows.Forms.ContainerControl.ProcessTabKey%2A> 方法。|  
|<xref:System.Windows.Forms.Form>|-   获取 <xref:System.Windows.Forms.Form.ActiveForm%2A> 或 <xref:System.Windows.Forms.Form.MdiParent%2A> 属性。<br />-   设置 <xref:System.Windows.Forms.Form.ControlBox%2A>、<xref:System.Windows.Forms.Form.ShowInTaskbar%2A> 或 <xref:System.Windows.Forms.Form.TopMost%2A> 属性。<br />-   将 <xref:System.Windows.Forms.Form.Opacity%2A> 属性设置为低于 50%。<br />-   以编程方式将 <xref:System.Windows.Forms.Form.WindowState%2A> 属性设置为 <xref:System.Windows.Forms.FormWindowState>。<br />-   调用 <xref:System.Windows.Forms.Form.Activate%2A> 方法。<br />-   使用 <xref:System.Windows.Forms.FormBorderStyle>、<xref:System.Windows.Forms.FormBorderStyle> 和 <xref:System.Windows.Forms.FormBorderStyle> <xref:System.Windows.Forms.FormBorderStyle> 枚举值。|  
|<xref:System.Windows.Forms.NotifyIcon>|-   对 <xref:System.Windows.Forms.NotifyIcon> 组件的使用是完全受限制的。|  
  
 除 <xref:System.Security.Permissions.UIPermissionWindow> 值所设置的限制外，<xref:System.Security.Permissions.UIPermissionWindow> 值还限制下表中列出的操作。  
  
|组件|受限制的操作|  
|--------|------------|  
|<xref:System.Windows.Forms.CommonDialog>|-   显示从 <xref:System.Windows.Forms.CommonDialog> 类派生的对话框。|  
|<xref:System.Windows.Forms.Control>|-   调用 <xref:System.Windows.Forms.Control.CreateGraphics%2A> 方法。<br />-   设置 <xref:System.Windows.Forms.Control.Cursor%2A> 属性。|  
|<xref:System.Windows.Forms.Control.Cursor%2A>|-   设置 <xref:System.Windows.Forms.Cursor.Current%2A> 属性。|  
|<xref:System.Windows.Forms.MessageBox>|-   调用 <xref:System.Windows.Forms.Form.Show%2A> 方法。|  
  
### 承载第三方控件  
 如果您的窗体承载第三方控件，可能会发生另一种窗口操作。  第三方控件是指并非由您自己开发和编译的任何自定义 <xref:System.Windows.Forms.UserControl>。  尽管承载方案难以侵入，但第三方控件理论上仍有可能扩展其呈现图面以覆盖整个窗体区域。  此控件随后即可模仿关键对话框，并从您的用户那里请求诸如用户名\/密码组合或银行帐号等信息。  
  
 要限制这种潜在风险，应仅使用来自您可信任的供应商的第三方控件。  如果您使用的第三方控件是从无法验证的源下载的，则建议您检查源代码是否有潜在侵入风险。  确认源无恶意后，应自己编译程序集以确保源与程序集匹配。  
  
## Win32 API 调用  
 如果应用程序设计要求从 Win32 API 调用函数，则表示您正在访问非托管的代码。  在这种情况下，当使用 Win32 API 调用或值时，将无法确定代码将对窗口或操作系统执行的操作。  <xref:System.Security.Permissions.SecurityPermission> 类和 <xref:System.Security.Permissions.SecurityPermissionFlag> 枚举的 <xref:System.Security.Permissions.SecurityPermissionFlag> 值控制对非托管代码的访问。  只有向应用程序授予 <xref:System.Security.Permissions.SecurityPermissionFlag> 权限后，它才能访问非托管代码。  默认情况下，只有本地运行的应用程序才能调用非托管代码。  
  
 某些 Windows 窗体成员提供需要 <xref:System.Security.Permissions.SecurityPermissionFlag> 权限的非托管访问。  下表列出了需要该权限的 <xref:System.Windows.Forms> 命名空间中的成员。  有关各个成员所需权限的更多信息，请参见 .NET Framework 类库文档。  
  
|组件|成员|  
|--------|--------|  
|<xref:System.Windows.Forms.Application>|-   <xref:System.Windows.Forms.Application.AddMessageFilter%2A> 方法<br />-   <xref:System.Windows.Forms.Application.CurrentInputLanguage%2A> 属性<br />-   `Exit` 方法<br />-   <xref:System.Windows.Forms.Application.ExitThread%2A> 方法<br />-   <xref:System.Windows.Forms.Application.ThreadException> 事件|  
|<xref:System.Windows.Forms.CommonDialog>|-   <xref:System.Windows.Forms.CommonDialog.HookProc%2A> 方法<br />-   <xref:System.Windows.Forms.CommonDialog.OwnerWndProc%2A>\\ 方法<br />-   <xref:System.Windows.Forms.CommonDialog.Reset%2A> 方法<br />-   <xref:System.Windows.Forms.CommonDialog.RunDialog%2A> 方法|  
|<xref:System.Windows.Forms.Control>|-   <xref:System.Windows.Forms.Control.CreateParams%2A> 方法<br />-   <xref:System.Windows.Forms.Control.DefWndProc%2A> 方法<br />-   <xref:System.Windows.Forms.Control.DestroyHandle%2A> 方法<br />-   <xref:System.Windows.Forms.Control.WndProc%2A> 方法|  
|<xref:System.Windows.Forms.Help>|-   <xref:System.Windows.Forms.Help.ShowHelp%2A> 方法<br />-   <xref:System.Windows.Forms.Help.ShowHelpIndex%2A> 方法|  
|<xref:System.Windows.Forms.NativeWindow>|-   <xref:System.Windows.Forms.NativeWindow> 类|  
|<xref:System.Windows.Forms.Screen>|-   <xref:System.Windows.Forms.Screen.FromHandle%2A> 方法|  
|<xref:System.Windows.Forms.SendKeys>|-   <xref:System.Windows.Forms.SendKeys.Send%2A> 方法<br />-   <xref:System.Windows.Forms.SendKeys.SendWait%2A> 方法|  
  
 如果应用程序不具有调用非托管代码的权限，则应用程序必须请求 <xref:System.Security.Permissions.SecurityPermissionFlag> 权限，或者您应该考虑实现这些功能的其他方法；在许多情况下，Windows 窗体提供了对 Win32 API 函数的备选托管函数。  如果不存在任何备选方法并且应用程序必须访问非托管代码，则必须提升应用程序的权限。  
  
 调用非托管代码的权限使应用程序几乎可以执行任何操作。  因此，应该只向来自于受信任源的应用程序授予调用非托管代码的权限。  另外，根据应用程序的不同，调用非托管代码的应用程序功能块可以是可选的，或者只在完全受信任的环境中启用。  有关危险权限的更多信息，请参见[危险权限和策略管理](../../../docs/framework/misc/dangerous-permissions-and-policy-administration.md)。  有关提升权限的更多信息，请参见[NIB: General Security Policy Administration](http://msdn.microsoft.com/zh-cn/5121fe35-f0e3-402c-94ab-4f35b0a87b4b)。  
  
## 请参阅  
 [Windows 窗体中更加安全的文件和数据访问](../../../docs/framework/winforms/more-secure-file-and-data-access-in-windows-forms.md)   
 [Windows 窗体中的更加安全的打印](../../../docs/framework/winforms/more-secure-printing-in-windows-forms.md)   
 [Windows 窗体中的安全性概述](../../../docs/framework/winforms/security-in-windows-forms-overview.md)   
 [Windows 窗体安全](../../../docs/framework/winforms/windows-forms-security.md)   
 [保护 ClickOnce 应用程序](../Topic/Securing%20ClickOnce%20Applications.md)