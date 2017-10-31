---
title: "Windows 服务应用程序介绍 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "ServiceController"
helpviewer_keywords: 
  - "框架服务, 创建服务"
  - "OnContinue 方法"
  - "OnPause 方法"
  - "OnStop 方法"
  - "Service 类, Windows 服务应用程序"
  - "服务状态"
  - "ServiceController 组件, 关于 Windows 服务"
  - "服务, 关于服务"
  - "服务, 生存期"
  - "服务, states"
  - "WaitForStatus 方法"
  - "Win32OwnProcess 服务类型"
  - "Win32ShareProcess 服务类型"
  - "Windows 服务应用程序, 关于 Windows 服务应用程序"
  - "Windows 服务应用程序, 部署"
  - "Windows 服务应用程序, 生存期"
ms.assetid: 1b1b5e67-3ff3-40c0-8154-322cfd6ef0ae
caps.latest.revision: 17
author: "ghogen"
ms.author: "ghogen"
manager: "douge"
caps.handback.revision: 17
---
# Windows 服务应用程序介绍
Microsoft Windows 服务（即，以前的 NT 服务）使您能够创建在它们自己的 Windows 会话中可长时间运行的可执行应用程序。  这些服务可以在计算机启动时自动启动，可以暂停和重新启动而且不显示任何用户界面。  这些功能使服务非常适合在服务器上使用，每当需要使用不会影响在同一台计算机上工作的其他用户的功能时也适用。  还可以在不同于登录用户的特定用户帐户或默认计算机帐户的安全上下文中运行服务。  有关服务和 Windows 会话的详细信息，请参见 MSDN Library 中的 Windows SDK 文档。  
  
 通过创建作为服务安装的应用程序，可以轻松地创建服务。  例如，假设要监视性能计数器数据并对阈值做出反应。  可以编写一个侦听性能计数器数据的 Windows 服务应用程序、部署该应用程序并开始收集和分析数据。  
  
 将服务创建为 Microsoft Visual Studio 项目，并在其中定义代码，以控制哪些命令可以发送到服务以及接收到这些命令时采取的操作。  可以发送到服务的命令包括启动、暂停、继续和停止该服务；还可以执行自定义命令。  
  
 创建并生成了应用程序后，可以通过运行命令行实用工具 InstallUtil.exe 并将路径传递给服务的可执行文件，来安装该应用程序。  然后可以使用**“服务控制管理器”**启动、停止、暂停、继续和配置服务。  这些任务中的许多种也可以在**“服务器资源管理器”**的**“服务”**节点中或通过使用 <xref:System.ServiceProcess.ServiceController> 类来完成。  
  
## 服务应用程序和其他 Visual Studio 应用程序  
 服务应用程序与其他许多项目类型的功能在几个方面有所不同：  
  
-   必须将服务应用程序项目创建的已编译可执行文件安装在服务器上，此项目才能以有意义的方式运行。  不能通过按 F5 或 F11 来调试或运行服务应用程序；不能立即运行服务或进入其代码。  相反，必须安装和启动服务，然后将一个调试器附加到服务的进程中。  有关详细信息，请参阅 [如何：调试 Windows 服务应用程序](../../../docs/framework/windows-services/how-to-debug-windows-service-applications.md)。  
  
-   与一些类型的项目不同，对于服务应用程序，必须为其创建安装组件。  安装组件在服务器上安装和注册服务，并用 Windows**“服务控制管理器”**为服务创建一个项。  有关详细信息，请参阅 [如何：将安装程序添加到服务应用程序](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md)。  
  
-   服务应用程序的 `Main` 方法必须为项目包含的服务发出 Run 命令。  `Run` 方法将服务加载到适当服务器上的**“服务控制管理器”**中。  如果使用**“Windows 服务”**项目模板，系统将自动为您写入此方法。  注意，加载服务与启动服务不同。  有关更多信息，请参见下面的“服务生存期”。  
  
-   Windows 服务应用程序在不同于登录用户的交互区域的窗口区域中运行。  窗口区域是包含剪贴板、一组全局原子和一组桌面对象的安全对象。  由于 Windows 服务的区域不是交互区域，因此 Windows 服务应用程序中引发的对话框将是不可见的，并且可能导致程序停止响应。  同样，错误信息应记录在 Windows 事件日志中，而不是在用户界面中引发。  
  
     .NET Framework 支持的 Windows 服务类不支持与交互区域（即登录用户）进行交互。  同时，.NET Framework 不包含表示区域和桌面的类。  如果 Windows 服务必须与其他区域进行交互，则需要访问非托管的 Windows API。  有关详细信息，请参见 Windows SDK 文档。  
  
     设计 Windows 服务与用户或其他区域的交互时必须非常小心，应考虑某些情况，例如没有登录的用户或用户具有一组意外的桌面对象的情况。  在某些情况下，编写一个在用户控制下运行的 Windows 应用程序可能更为妥当。  
  
-   Windows 服务应用程序在各自的安全上下文中运行，并且在用户登录到安装有该程序的 Windows 计算机之前启动。  应仔细计划在哪些用户帐户内运行服务；在系统帐户下运行的服务比在用户帐户下运行的服务具有更多的权限和特权。  
  
## 服务生存期  
 服务在其生存期内要经历几个内部状态。  首先，将服务安装在将要运行它的系统上。  此过程执行服务项目的安装程序，并将服务加载到该计算机的“服务控制管理器”中。  **“服务控制管理器”**是由 Windows 提供的管理服务的核心实用工具。  
  
 服务加载后，必须启动。  启动服务使服务开始运行。  可以从**“服务控制管理器”**、从**“服务器资源管理器”**或通过调用 <xref:System.ServiceProcess.ServiceController.Start%2A> 方法从代码启动服务。  <xref:System.ServiceProcess.ServiceController.Start%2A> 方法将处理传递给应用程序的 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 方法并处理您在该处定义的任何代码。  
  
 运行的服务可以以这种状态无限期地存在下去，直到它被停止或暂停或者计算机关闭。  服务可以以三种基本状态之一存在：<xref:System.ServiceProcess.ServiceControllerStatus>、<xref:System.ServiceProcess.ServiceControllerStatus> 或 <xref:System.ServiceProcess.ServiceControllerStatus>。  服务还可以报告挂起命令的状态：<xref:System.ServiceProcess.ServiceControllerStatus>、<xref:System.ServiceProcess.ServiceControllerStatus>、<xref:System.ServiceProcess.ServiceControllerStatus> 或 <xref:System.ServiceProcess.ServiceControllerStatus>。  这些状态指示命令已经发出（如暂停正在运行的服务的命令），但尚未执行。  您可以查询 <xref:System.ServiceProcess.ServiceController.Status%2A> 以确定服务的状态，也可以使用 <xref:System.ServiceProcess.ServiceController.WaitForStatus%2A> 在以上任一状态出现时执行操作。  
  
 可以从**“服务控制管理器”**、从**“服务器资源管理器”**或通过从代码调用方法来暂停、停止或继续服务。  每种操作都可以调用服务中的一个相关过程（<xref:System.ServiceProcess.ServiceBase.OnStop%2A>、<xref:System.ServiceProcess.ServiceBase.OnPause%2A> 或 <xref:System.ServiceProcess.ServiceBase.OnContinue%2A>），在其中可以定义当服务状态更改时所执行的其他处理。  
  
## 服务类型  
 在 Visual Studio 中使用 .NET Framework 可以创建两种类型的服务。  进程中的唯一服务被指定为 <xref:System.ServiceProcess.ServiceType> 类型。  与其他服务共享进程的服务被指定为 <xref:System.ServiceProcess.ServiceType> 类型。  可通过查询 <xref:System.ServiceProcess.ServiceController.ServiceType%2A> 属性检索服务类型。  
  
 如果查询不是在 Visual Studio 中创建的现有服务，则偶尔还可能看到其他服务类型。  有关这些内容的更多信息，请参见 <xref:System.ServiceProcess.ServiceType>。  
  
## 服务和 ServiceController 组件  
 <xref:System.ServiceProcess.ServiceController> 组件用于连接到已安装的服务并操作其状态；使用 <xref:System.ServiceProcess.ServiceController> 组件可以启动和停止服务、暂停和继续其运行以及将自定义命令发送到服务。  但是，在创建服务应用程序时不需使用 <xref:System.ServiceProcess.ServiceController> 组件。  实际上，多数情况下，<xref:System.ServiceProcess.ServiceController> 组件存在于与定义服务的 Windows 服务应用程序不同的应用程序中。  
  
 有关详细信息，请参阅 <xref:System.ServiceProcess.ServiceController>。  
  
## 要求  
  
-   服务必须创建在**“Windows 服务”**应用程序项目或其他支持 .NET Framework 的项目中，而该项目在从 <xref:System.ServiceProcess.ServiceBase> 类生成和继承时创建 .exe 文件。  
  
-   包含 Windows 服务的项目必须有该项目及其服务的安装组件。  这可以从**“属性”**窗口轻松实现。  有关详细信息，请参阅 [如何：将安装程序添加到服务应用程序](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md)。  
  
## 请参阅  
 [Windows Service Applications](../../../docs/framework/windows-services/index.md)   
 [服务应用程序编程体系结构](../../../docs/framework/windows-services/service-application-programming-architecture.md)   
 [如何：创建 Windows 服务](../../../docs/framework/windows-services/how-to-create-windows-services.md)   
 [如何：安装和卸载服务](../../../docs/framework/windows-services/how-to-install-and-uninstall-services.md)   
 [如何：启动服务](../../../docs/framework/windows-services/how-to-start-services.md)   
 [如何：调试 Windows 服务应用程序](../../../docs/framework/windows-services/how-to-debug-windows-service-applications.md)   
 [演练：在组件设计器中创建 Windows 服务应用程序](../../../docs/framework/windows-services/walkthrough-creating-a-windows-service-application-in-the-component-designer.md)   
 [如何：将安装程序添加到服务应用程序](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md)