---
title: "如何：安装和卸载服务 | Microsoft Docs"
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
  - "安装, Windows 服务"
  - "安装 Windows 服务"
  - "installutil.exe 工具"
  - "服务, 安装"
  - "服务, 卸载"
  - "卸载应用程序, Windows 服务"
  - "卸载 Windows 服务"
  - "Windows 服务应用程序, 部署"
ms.assetid: c89c5169-f567-4305-9d62-db31a1de5481
caps.latest.revision: 19
author: "ghogen"
ms.author: "ghogen"
manager: "douge"
caps.handback.revision: 17
---
# 如何：安装和卸载服务
如果你正使用 .NET Framework 开发 Windows 服务，你可以使用名为 InstallUtil.exe 的命令行实用工具快速安装服务应用程序。  如果你是一个想要发布用户可以安装和卸载的 Windows 服务的开发人员，应使用 InstallShield。  请参阅 [Windows Installer 部署](http://msdn.microsoft.com/zh-cn/121be21b-b916-43e2-8f10-8b080516d2a0)。  
  
> [!WARNING]
>  如果你想要从你的计算机卸载服务，不要遵循本文中的步骤。  相反，你应找出哪些程序或软件包安装了该服务，然后在控制面板中选择**“添加\/删除程序”**卸载该程序。  请注意，许多服务是 Windows 不可或缺的部分；如果你删除它们，可能导致系统不稳定。  
  
 要使用本文中的步骤，你首先需要将服务安装程序添加到你的 Windows 服务。  请参阅[演练：在组件设计器中创建 Windows 服务应用程序](../../../docs/framework/windows-services/walkthrough-creating-a-windows-service-application-in-the-component-designer.md)。  
  
 无法通过按 F5 从 Visual Studio 开发环境直接运行 Windows 服务项目。  这是因为必须先安装项目中的服务，然后才能运行项目。  
  
> [!TIP]
>  你可以启动**“服务器资源管理器”**，验证是否已经安装或卸载你的服务。  有关详细信息，请参阅[如何：访问和初始化服务器资源管理器\/数据库资源管理器](../Topic/How%20to:%20Access%20and%20Initialize%20Server%20Explorer-Database%20Explorer.md)。  
  
### 若要手动安装你的服务  
  
1.  在 Windows**“启动”**菜单或**“启动”**屏幕上，依次选择 **Visual Studio**、**Visual Studio 工具**、**开发人员命令提示**。  
  
     出现 Visual Studio 命令提示。  
  
2.  访问你的项目的已编译可执行文件所在的目录。  
  
3.  以你的项目的可执行文件作为参数，通过命令提示运行 InstallUtil.exe：  
  
    ```  
    installutil <yourproject>.exe  
    ```  
  
     如果使用 Visual Studio 命令提示，InstallUtil.exe 应该在系统路径上。  如果不在，你可以将其添加到该路径，或使用完全限定的路径来调用它。  此工具随 .NET Framework 安装，其路径为 `%WINDIR%\Microsoft.NET\Framework[64]\<framework_version>`。  例如，对于 32 位版本的 .NET Framework 4 或 4.5.\*，如果你的 Windows 安装目录为 C:\\Windows，则该路径为 `C:\Windows\Microsoft.NET\Framework\v4.0.30319\InstallUtil.exe`。  对于 64 位版本的 .NET Framework 4 或 4.5.\*，默认路径为 `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\InstallUtil.exe`。  
  
### 若要手动卸载你的服务  
  
1.  在 Windows**“启动”**菜单或**“启动”**屏幕上，依次选择 **Visual Studio**、**Visual Studio 工具**、**开发人员命令提示**。  
  
     出现 Visual Studio 命令提示。  
  
2.  以你的项目的输出作为参数，通过命令提示运行 InstallUtil.exe：  
  
    ```  
    installutil /u <yourproject>.exe  
    ```  
  
3.  有时，服务的可执行文件被删除后，该服务可能仍然会出现在注册表中。  这种情况下，请使用命令 [sc delete](http://technet.microsoft.com/library/cc742045.aspx) 从注册表中删除服务的条目。  
  
## 请参阅  
 [Windows 服务应用程序介绍](../../../docs/framework/windows-services/introduction-to-windows-service-applications.md)   
 [如何：创建 Windows 服务](../../../docs/framework/windows-services/how-to-create-windows-services.md)   
 [如何：将安装程序添加到服务应用程序](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md)   
 [Installutil.exe（安装程序工具）](../../../docs/framework/tools/installutil-exe-installer-tool.md)