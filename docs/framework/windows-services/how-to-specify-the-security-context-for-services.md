---
title: "如何：为服务指定安全上下文 | Microsoft Docs"
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
  - "上下文, Visual Studio 安全"
  - "安全性 [Visual Studio], 上下文"
  - "安全性 [Visual Studio], 服务应用程序"
  - "ServiceInstaller 类, 安全性上下文"
  - "ServiceProcessInstaller 类, 安全性上下文"
  - "服务, 安全性"
  - "Windows 服务应用程序, 安全性"
ms.assetid: 02187c7b-dbf2-45f2-96c2-e11010225a22
caps.latest.revision: 10
author: "ghogen"
ms.author: "ghogen"
manager: "douge"
caps.handback.revision: 10
---
# 如何：为服务指定安全上下文
默认情况下，服务与已登录的用户在不同的安全上下文中运行。  服务在称为 `LocalSystem` 的默认系统帐户的上下文中运行，该帐户给服务提供的系统资源访问特权不同于给用户提供的。  可以更改此行为，指定一个不同的用户帐户来运行服务。  
  
 可以通过操作运行服务的进程的 <xref:System.ServiceProcess.ServiceProcessInstaller.Account%2A> 属性来设置安全上下文。  这一属性允许您将服务设置为以下 4 种 Account 类型之一：  
  
-   `User`，当服务已安装并且在由网络上的单一用户指定的帐户的上下文中运行时，该类型将使系统要求提供有效的用户名和密码；  
  
-   `LocalService`，该类型在用作本地计算机上的非特权用户并向任意远程服务器显示匿名凭据的帐户的上下文中运行；  
  
-   `LocalSystem`，帐户的上下文中运行提供多种本地特权，并显示计算机凭据的向任意远程服务器上；  
  
-   `NetworkService`，该类型在用作本地计算机上的非特权用户并向任意远程服务器显示计算机凭据的帐户的上下文中运行。  
  
 有关更多信息，请参见 <xref:System.ServiceProcess.ServiceAccount>。  
  
### 为服务指定安全上下文  
  
1.  创建服务后，为其添加必要的安装程序。  有关更多信息，请参见[如何：将安装程序添加到服务应用程序](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md)。  
  
2.  在设计器中，访问 `ProjectInstaller` 类并单击正在处理的服务的服务进程安装程序。  
  
    > [!NOTE]
    >  对于每个服务应用程序，在 `ProjectInstaller` 类中至少有两个安装组件：一个为项目中的所有服务安装进程，另一个是应用程序所包含的每项服务的安装程序。  在此实例中，需要选择 <xref:System.ServiceProcess.ServiceProcessInstaller>。  
  
3.  在**“属性”**窗口中，将 <xref:System.ServiceProcess.ServiceProcessInstaller.Account%2A> 设置为适当的值。  
  
## 请参阅  
 [Windows 服务应用程序介绍](../../../docs/framework/windows-services/introduction-to-windows-service-applications.md)   
 [如何：将安装程序添加到服务应用程序](../../../docs/framework/windows-services/how-to-add-installers-to-your-service-application.md)   
 [如何：创建 Windows 服务](../../../docs/framework/windows-services/how-to-create-windows-services.md)