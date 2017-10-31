---
title: "Windows 窗体的 ClickOnce 部署 | Microsoft Docs"
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
  - "ClickOnce 部署 [Windows 窗体]"
  - "演练 [Windows 窗体], ClickOnce 部署"
  - "Windows 窗体, ClickOnce 部署"
ms.assetid: 1451fce9-1965-4a03-b4d3-831b5fe4ad66
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# Windows 窗体的 ClickOnce 部署
下面的主题描述了 [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)]，这是一种用于将 Windows 窗体应用程序轻松部署到客户端计算机的技术。  
  
## 相关章节  
 [选择 ClickOnce 部署策略](../Topic/Choosing%20a%20ClickOnce%20Deployment%20Strategy.md)  
 演示用于部署 [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] 应用程序的若干选项。  
  
 [选择 ClickOnce 更新策略](../Topic/Choosing%20a%20ClickOnce%20Update%20Strategy.md)  
 演示用于更新 [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] 应用程序的若干选项。  
  
 [保护 ClickOnce 应用程序](../Topic/Securing%20ClickOnce%20Applications.md)  
 解释 [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] 部署的安全问题。  
  
 [ClickOnce 部署疑难解答](../Topic/Troubleshooting%20ClickOnce%20Deployments.md)  
 描述在部署 [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] 应用程序时可能发生的各种问题，并记录 [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] 可能生成的顶级错误消息。  
  
 [ClickOnce 和应用程序设置](../Topic/ClickOnce%20and%20Application%20Settings.md)  
 描述 [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] 部署如何使用应用程序设置，从而存储应用程序和用户设置以便未来检索。  
  
 [受信任的应用程序部署概述](../Topic/Trusted%20Application%20Deployment%20Overview.md)  
 描述一项 [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] 功能，该功能允许受信任的应用程序在客户端计算机上以更高级别的权限运行。  
  
 [ClickOnce 和 Authenticode](../Topic/ClickOnce%20and%20Authenticode.md)  
 描述如何在受信任的应用程序部署中使用验证码技术。  
  
 [演练：手动部署 ClickOnce 应用程序](../Topic/Walkthrough:%20Manually%20Deploying%20a%20ClickOnce%20Application.md)  
 演示如何使用命令行和 SDK 工具（而不使用 Visual Studio）来部署 [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] 应用程序。  
  
 [如何：为 ClickOnce 应用程序向客户端计算机添加一个受信任的发行者](../Topic/How%20to:%20Add%20a%20Trusted%20Publisher%20to%20a%20Client%20Computer%20for%20ClickOnce%20Applications.md)  
 演示如何一次性配置受信任的应用程序部署所需要的客户端计算机。  
  
 [如何：指定部署更新的其他位置](../Topic/How%20to:%20Specify%20an%20Alternate%20Location%20for%20Deployment%20Updates.md)  
 演示如何使用 SDK 工具来配置 [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] 应用程序，以检查另一个用于新版本应用程序的位置。  
  
 [演练：使用 ClickOnce 部署 API 按需下载程序集](../Topic/Walkthrough:%20Downloading%20Assemblies%20on%20Demand%20with%20the%20ClickOnce%20Deployment%20API.md)  
 演示如何在应用程序第一次尝试加载程序集时使用 API 调用来检索程序集。  
  
 [如何：在联机 ClickOnce 应用程序中检索查询字符串信息](../Topic/How%20to:%20Retrieve%20Query%20String%20Information%20in%20an%20Online%20ClickOnce%20Application.md)  
 演示如何从 URL 检索用于运行 [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] 应用程序的参数。  
  
 [ClickOnce 缓存概述](../Topic/ClickOnce%20Cache%20Overview.md)  
 描述用于在本地计算机上存储 [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] 应用程序的缓存。  
  
 [在 ClickOnce 应用程序中访问本地数据和远程数据](../Topic/Accessing%20Local%20and%20Remote%20Data%20in%20ClickOnce%20Applications.md)  
 介绍如何从 [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] 应用程序访问本地数据文件和远程数据源。  
  
 [如何：将数据文件包括到 ClickOnce 应用程序中](../Topic/How%20to:%20Include%20a%20Data%20File%20in%20a%20ClickOnce%20Application.md)  
 演示如何标记文件以使它在 [!INCLUDE[ndptecclick](../../../includes/ndptecclick-md.md)] 数据目录中可用。  
  
## 请参阅  
 [应用程序设置概述](../../../docs/framework/winforms/advanced/application-settings-overview.md)   
 [发布 ClickOnce 应用程序](../Topic/Publishing%20ClickOnce%20Applications.md)   
 [从命令行生成 ClickOnce 应用程序](../Topic/Building%20ClickOnce%20Applications%20from%20the%20Command%20Line.md)   
 [调试使用 System.Deployment.Application 的 ClickOnce 应用程序](../Topic/Debugging%20ClickOnce%20Applications%20That%20Use%20System.Deployment.Application.md)   
 [使用 ClickOnce 部署 COM 组件](../Topic/Deploying%20COM%20Components%20with%20ClickOnce.md)   
 [如何：使用发布向导发布 ClickOnce 应用程序](../Topic/How%20to:%20Publish%20a%20ClickOnce%20Application%20using%20the%20Publish%20Wizard.md)