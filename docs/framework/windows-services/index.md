---
title: "Developing Windows Service Applications | Microsoft Docs"
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
  - "ServiceInstaller class, Windows Service applications"
  - "Service class, Windows Service applications"
  - "Windows Service applications"
  - "Windows NT services"
  - "ServiceProcessInstaller class, Windows Service applications"
  - "services"
  - ".NET applications, Windows applications"
ms.assetid: ba72d648-9553-4849-b829-069ad5ea014b
caps.latest.revision: 18
author: "ghogen"
ms.author: "ghogen"
manager: "douge"
caps.handback.revision: 18
---
# Developing Windows Service Applications
使用 Microsoft [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 或 Microsoft [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK，可以通过创建以服务方式安装的应用程序来轻松创建服务。  这种类型的应用程序称为 Windows 服务。  使用框架功能，可以创建服务，安装服务和启动、停止服务以及用其他方式控制服务的行为。  
  
> [!WARNING]
>  C\+\+的Windows服务模板在Visual Studio 2010不包含。  若要创建Windows服务，可以在visual C\#托管代码可以创建服务或Visual Basic中，使用 [ATL 项目向导](../Topic/ATL%20Project%20Wizard.md)，可以与现有C\+\+代码如果必须兼容，也可以在本机C\+\+可以创建Windows服务。  
  
## 本节内容  
 [Windows 服务应用程序介绍](../../../docs/framework/windows-services/introduction-to-windows-service-applications.md)  
 提供Windows服务应用程序的概述，服务的生存期和服务应用程序与其他通用项目类型键入。  
  
 [演练：在组件设计器中创建 Windows 服务应用程序](../../../docs/framework/windows-services/walkthrough-creating-a-windows-service-application-in-the-component-designer.md)  
 提供在 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 和 Visual C\# 中创建服务的示例。  
  
 [服务应用程序编程体系结构](../../../docs/framework/windows-services/service-application-programming-architecture.md)  
 解释用于服务编程的语言元素。  
  
 [如何：创建 Windows 服务](../../../docs/framework/windows-services/how-to-create-windows-services.md)  
 使用Windows服务项目模板，描述创建和配置的Windows服务进程。  
  
## 相关章节  
 <xref:System.ServiceProcess.ServiceBase>  
 描述 <xref:System.ServiceProcess.ServiceBase> 类的主要功能，该类用于创建服务。  
  
 <xref:System.ServiceProcess.ServiceProcessInstaller>  
 描述 <xref:System.ServiceProcess.ServiceProcessInstaller> 类的功能，该类与 <xref:System.ServiceProcess.ServiceInstaller> 类一起用来安装和卸载您的服务。  
  
 <xref:System.ServiceProcess.ServiceInstaller>  
 描述 <xref:System.ServiceProcess.ServiceInstaller> 类的功能，该类与 <xref:System.ServiceProcess.ServiceProcessInstaller> 类一起用来安装和卸载您的服务。  
  
 [从模板创建项目](http://msdn.microsoft.com/zh-cn/7c36d86a-6b79-4480-8228-0f925f1204b2)  
 描述本章中使用的项目类型以及如何对它们进行选择。