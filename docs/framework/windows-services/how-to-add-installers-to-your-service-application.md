---
title: "如何：将安装程序添加到服务应用程序 | Microsoft Docs"
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
  - "安装组件, 添加到服务"
  - "安装程序, 添加到服务"
  - "ServiceInstaller 类, 向服务添加安装程序"
  - "ServiceProcessInstaller 类, 向服务添加安装程序"
  - "服务, 添加安装程序"
  - "Windows 服务应用程序, 添加安装程序"
  - "Windows 服务应用程序, 部署"
ms.assetid: 8b698e9a-b88e-4f44-ae45-e0c5ea0ae5a8
caps.latest.revision: 14
author: "ghogen"
ms.author: "ghogen"
manager: "douge"
caps.handback.revision: 14
---
# 如何：将安装程序添加到服务应用程序
Visual Studio 随附有安装组件，这些组件可以安装与服务应用程序相关的资源。  安装组件在正在安装到的系统上注册一项单个的服务，并使服务控制管理器知道该服务的存在。  当使用服务应用程序时，可以在“属性”窗口选择一个链接，以自动将适当的安装程序添加到项目中。  
  
> [!NOTE]
>  服务的属性值将从服务类复制到安装程序类。  如果更新服务类上的属性值，这些属性值在安装程序中将不会自动更新。  
  
 当向项目添加安装程序时，项目中会创建一个新类（默认情况下名为 `ProjectInstaller`），并在其中创建适当的安装组件的实例。  该类作为项目所需的所有安装组件的中心点。  例如，如果向应用程序添加第二项服务并单击“添加安装程序”链接，这时并不创建第二个安装程序类，而是将第二项服务所需的其他安装组件添加到现有类。  
  
 要正确安装服务，并不需要在安装程序中进行任何特殊编码。  但是，如果需要向安装进程添加特殊功能，则可能偶尔需要修改安装程序的内容。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 将安装程序添加到服务应用程序  
  
1.  在**“解决方案资源管理器”**中，访问要为其添加安装组件的服务的**“设计”**视图。  
  
2.  单击设计器的背景以选择服务本身，而不是它的任何内容。  
  
3.  设计器具有焦点时，右击然后单击**“添加安装程序”**。  
  
     这时项目中就添加了一个新类 `ProjectInstaller` 和两个安装组件 <xref:System.ServiceProcess.ServiceProcessInstaller> 和 <xref:System.ServiceProcess.ServiceInstaller>，并且服务的属性值被复制到组件。  
  
4.  单击 <xref:System.ServiceProcess.ServiceInstaller> 组件，验证 <xref:System.ServiceProcess.ServiceInstaller.ServiceName%2A> 属性的值已为与服务本身的 <xref:System.ServiceProcess.ServiceInstaller.ServiceName%2A> 属性的值相同。  
  
5.  若要确定如何启动服务，请单击 <xref:System.ServiceProcess.ServiceInstaller> 组件并将 <xref:System.ServiceProcess.ServiceInstaller.StartType%2A> 属性设置为适当的值。  
  
    |值|结果|  
    |-------|--------|  
    |<xref:System.ServiceProcess.ServiceStartMode>|服务安装后，必须手动启动。  有关更多信息，请参见[如何：启动服务](../../../docs/framework/windows-services/how-to-start-services.md)。|  
    |<xref:System.ServiceProcess.ServiceStartMode>|每次计算机重新启动时，服务都会自动启动。|  
    |<xref:System.ServiceProcess.ServiceStartMode>|服务无法启动。|  
  
6.  若要确定将要运行服务的安全上下文，请单击 <xref:System.ServiceProcess.ServiceProcessInstaller> 组件并设置适当的属性值。  有关更多信息，请参见[如何：为服务指定安全上下文](../../../docs/framework/windows-services/how-to-specify-the-security-context-for-services.md)。  
  
7.  重写需要为其执行自定义处理的所有方法。  
  
8.  对项目中的每项附加服务执行步骤 1 到步骤 7。  
  
    > [!NOTE]
    >  对于项目中的每项附加服务，必须将附加的 <xref:System.ServiceProcess.ServiceInstaller> 组件添加到项目的 `ProjectInstaller` 类中。  步骤三中添加的 <xref:System.ServiceProcess.ServiceProcessInstaller> 组件适用于项目中的所有单个服务安装程序。  
  
## 请参阅  
 [Windows 服务应用程序介绍](../../../docs/framework/windows-services/introduction-to-windows-service-applications.md)   
 [如何：安装和卸载服务](../../../docs/framework/windows-services/how-to-install-and-uninstall-services.md)   
 [如何：启动服务](../../../docs/framework/windows-services/how-to-start-services.md)   
 [如何：为服务指定安全上下文](../../../docs/framework/windows-services/how-to-specify-the-security-context-for-services.md)