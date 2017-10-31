---
title: "如何：启动服务 | Microsoft Docs"
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
  - "服务, 启动"
  - "Windows 服务应用程序, 启动"
ms.assetid: 9ea77955-2d96-4c3d-913c-14db7604cdad
caps.latest.revision: 16
author: "ghogen"
ms.author: "ghogen"
manager: "douge"
caps.handback.revision: 14
---
# 如何：启动服务
服务安装后，必须启动。  启动会调用服务类上 <xref:System.ServiceProcess.ServiceBase.OnStart%2A> 方法。  通常，<xref:System.ServiceProcess.ServiceBase.OnStart%2A> 方法定义服务将执行的有用工作。  服务启动后一直保持活动，直到被手动暂停或停止。  
  
 可以将服务设置为自动启动或手动启动。  自动启动的服务将在安装了该服务的计算机重新启动或首次打开时启动。  而手动启动的服务需要用户来启动。  
  
> [!NOTE]
>  默认情况下，使用 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 创建的服务会设置为手动启动。  
  
 存在多种手动启动服务的方法：从**“服务器资源管理器”**启动，从**“服务控制管理器”**启动，或使用名为 <xref:System.ServiceProcess.ServiceController> 的组件从代码启动。  
  
 在 <xref:System.ServiceProcess.ServiceInstaller> 类中设置 <xref:System.ServiceProcess.ServiceInstaller.StartType%2A> 属性，以确定是手动启动还是自动启动服务。  
  
### 指定服务的启动方式  
  
1.  创建服务后，为其添加必要的安装程序。  有关详细信息，请参阅 [如何：将安装程序添加到服务应用程序](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md)。  
  
2.  在设计器中，单击正在处理的服务的服务安装程序。  
  
3.  在**“属性”**窗口中，将 <xref:System.ServiceProcess.ServiceInstaller.StartType%2A> 属性设置为以下值之一：  
  
    |安装服务|设置该值|  
    |----------|----------|  
    |当计算机重新启动时|**自动**|  
    |当一个显式用户操作启动服务时|**手动**|  
  
    > [!TIP]
    >  若要完全防止启动服务，可以将 <xref:System.ServiceProcess.ServiceInstaller.StartType%2A> 属性设置为**“Disabled”**。  如果将多次重启服务器，并且希望通常会启动的服务禁止启动以便节省时间，可以这样做。  
  
    > [!NOTE]
    >  安装服务之后，可以更改这些属性和其他属性。  
  
     存在多种方法可以启动 <xref:System.ServiceProcess.ServiceInstaller.StartType%2A> 进程设置为**“Manual”**的服务：从**“服务器资源管理器”**启动，从**“Windows 服务控制管理器”**启动或从代码启动。  值得注意的是，并不是所有这些方法都在**“服务控制管理器”**的上下文中实际启动服务；**“服务器资源管理器”**和启动服务的编程方法实际操作控制器。  
  
### 从服务器资源管理器手动启动服务  
  
1.  在**“服务器资源管理器”**中，如果需要的服务器没有列出，则添加该服务器。  有关详细信息，请参阅 [如何：访问和初始化服务器资源管理器\/数据库资源管理器](../Topic/How%20to:%20Access%20and%20Initialize%20Server%20Explorer-Database%20Explorer.md)。  
  
2.  展开**“服务”**节点，然后找到要启动的服务。  
  
3.  右击服务的名称，然后单击**“启动”**。  
  
### 从服务控制管理器手动启动服务  
  
1.  通过执行下列操作之一打开**“服务控制管理器”**：  
  
    -   在 Windows XP 和 2000 专业版中，在桌面上右击**“我的电脑”**，然后单击**“管理”**。  在出现的对话框中，展开**“服务和应用程序”**节点。  
  
         \- 或 \-  
  
    -   在 Windows Server 2003 和 Windows 2000 Server 中，单击**“开始”**，指向**“程序”**，单击**“管理工具”**，然后单击**“服务”**。  
  
        > [!NOTE]
        >  在 Windows NT 4.0 版中，可以从**“控制面板”**中打开此对话框。  
  
     现在应该看到您的服务列在窗口的**“服务”**区域中。  
  
2.  从列表中选择您的服务，右击该服务，然后单击**“启动”**。  
  
### 用代码手动启动服务  
  
1.  创建一个 <xref:System.ServiceProcess.ServiceController> 类的实例，并将它配置为与要管理的服务进行交互。  
  
2.  调用 <xref:System.ServiceProcess.ServiceController.Start%2A> 方法启动该服务。  
  
## 请参阅  
 [Windows 服务应用程序介绍](../../../docs/framework/windows-services/introduction-to-windows-service-applications.md)   
 [如何：创建 Windows 服务](../../../docs/framework/windows-services/how-to-create-windows-services.md)   
 [如何：将安装程序添加到服务应用程序](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md)   
 [如何：访问和初始化服务器资源管理器\/数据库资源管理器](../Topic/How%20to:%20Access%20and%20Initialize%20Server%20Explorer-Database%20Explorer.md)