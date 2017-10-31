---
title: "服务应用程序编程体系结构 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "ServiceBase 类, 服务状态"
  - "ServiceController 类"
  - "ServiceController 组件, 编程体系结构"
  - "ServiceProcessInstaller 类, 服务应用程序代码模型"
  - "服务, 编程体系结构"
  - "服务, states"
  - "Windows 服务应用程序, 代码模型"
  - "Windows 服务应用程序, states"
ms.assetid: 83230026-d068-4174-97ff-e264c896eb2f
caps.latest.revision: 15
author: "ghogen"
ms.author: "ghogen"
manager: "douge"
caps.handback.revision: 15
---
# 服务应用程序编程体系结构
Windows 服务应用程序基于从 <xref:System.ServiceProcess.ServiceBase?displayProperty=fullName> 类继承的类。  从该类重写方法并为它们定义功能以确定服务的行为。  
  
 创建服务所涉及的类主要有：  
  
-   <xref:System.ServiceProcess.ServiceBase?displayProperty=fullName> \-\- 在创建服务时从 <xref:System.ServiceProcess.ServiceBase> 类重写方法并定义代码，以确定服务在此继承类中的运行方式。  
  
-   <xref:System.ServiceProcess.ServiceProcessInstaller?displayProperty=fullName> 和 <xref:System.ServiceProcess.ServiceInstaller?displayProperty=fullName> \-\- 使用这些类安装和卸载服务。  
  
 另外，可以使用名为 <xref:System.ServiceProcess.ServiceController> 的类来操作服务本身。  该类不参与服务的创建，但是可以用于启动和停止服务、将命令传递给服务和返回一系列枚举。  
  
## 定义服务的行为  
 在服务类中，重写基类函数，确定当服务状态在服务控制管理器更改后会带来何种结果。  <xref:System.ServiceProcess.ServiceBase> 类公开下列方法，可以重写这些方法以添加自定义行为。  
  
|方法|重写以便|  
|--------|----------|  
|<xref:System.ServiceProcess.ServiceBase.OnStart%2A>|指示当服务开始运行时应采取何种操作。  必须在此过程中为服务编写代码以执行有用的工作。|  
|<xref:System.ServiceProcess.ServiceBase.OnPause%2A>|指示服务暂停时发生什么。|  
|<xref:System.ServiceProcess.ServiceBase.OnStop%2A>|指示服务停止运行时发生什么。|  
|<xref:System.ServiceProcess.ServiceBase.OnContinue%2A>|指示服务在暂停后继续正常工作时发生什么。|  
|<xref:System.ServiceProcess.ServiceBase.OnShutdown%2A>|指示在系统关闭前且服务正在运行时发生什么。|  
|<xref:System.ServiceProcess.ServiceBase.OnCustomCommand%2A>|指示在服务接收到自定义命令时发生什么。  有关自定义命令的更多信息，请参见 MSDN Online。|  
|<xref:System.ServiceProcess.ServiceBase.OnPowerEvent%2A>|指示接收到电源管理事件（如电池不足或操作挂起）时，服务如何响应。|  
  
> [!NOTE]
>  这些方法表示服务在其整个生存期中的状态；服务从一种状态转换为下一种状态。  例如，在调用 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 之前，绝不可能使服务响应 <xref:System.ServiceProcess.ServiceBase.OnContinue%2A> 命令。  
  
 还有其他几种感兴趣的属性和方法，  这些元素包括：  
  
-   <xref:System.ServiceProcess.ServiceBase> 类上的 <xref:System.ServiceProcess.ServiceBase.Run%2A> 方法。  这是服务的主入口点。  使用 Windows 服务模板创建服务时，代码会插入到应用程序的 `Main` 方法中以运行服务。  此代码如下所示：  
  
     [!code-csharp[VbRadconService#6](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#6)]
     [!code-vb[VbRadconService#6](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#6)]  
  
    > [!NOTE]
    >  这两个示例使用了 <xref:System.ServiceProcess.ServiceBase> 类型的数组，应用程序包含的每个服务都可以添加到该数组中，然后所有这些服务可以一起运行。  但是，如果仅创建一个服务，则可以选择不使用该数组，而只是声明从 <xref:System.ServiceProcess.ServiceBase> 继承的一个新对象并运行该对象。  有关示例，请参见[如何：以编程方式编写服务](../../../docs/framework/windows-services/how-to-write-services-programmatically.md)。  
  
-   <xref:System.ServiceProcess.ServiceBase> 类上的一系列属性。  它们确定可以调用服务上的哪些方法。  例如，当 <xref:System.ServiceProcess.ServiceBase.CanStop%2A> 属性设置为 `true` 时，可以调用服务上的 <xref:System.ServiceProcess.ServiceBase.OnStop%2A> 方法。  当 <xref:System.ServiceProcess.ServiceBase.CanPauseAndContinue%2A> 属性设置为 `true` 时，可以调用 <xref:System.ServiceProcess.ServiceBase.OnPause%2A> 和 <xref:System.ServiceProcess.ServiceBase.OnContinue%2A> 方法。  当将这些属性中的一种设置为 `true` 时，应接着重写关联方法并定义其处理。  
  
    > [!NOTE]
    >  服务必须至少重写 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 和 <xref:System.ServiceProcess.ServiceBase.OnStop%2A> 才能有用。  
  
 还可以使用一个名为 <xref:System.ServiceProcess.ServiceController> 的组件，以与现有服务通信并控制其行为。  
  
## 请参阅  
 [Windows 服务应用程序介绍](../../../docs/framework/windows-services/introduction-to-windows-service-applications.md)   
 [如何：创建 Windows 服务](../../../docs/framework/windows-services/how-to-create-windows-services.md)