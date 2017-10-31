---
title: "配置应用程序 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a2f995b0-669d-4721-b00f-4561ec7eb6a4
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# 配置应用程序
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 使用 .NET 配置系统并允许您在计算机和应用程序范围配置服务。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 定义的配置设置位于 `<system.serviceModel>` 节组中。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]如何配置 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务的更多信息，请参见以下主题：  
  
-   [正在配置服务](../../../../docs/framework/wcf/configuring-services.md)  
  
-   [\<system.serviceModel\>](../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md)  
  
 应用程序是在 `<appSettings>` 节组中定义配置设置的。[!INCLUDE[crabout](../../../../includes/crabout-md.md)] .NET 配置文件中应用程序设置的更多信息，请参见 [\<appSettings\>](http://go.microsoft.com/fwlink/?LinkId=95159)。  
  
## 使用配置编辑器  
 使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)][配置编辑器工具 \(SvcConfigEditor.exe\)](../../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md)，管理员和开发人员可以使用图形用户界面来创建和修改 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务的配置设置。利用此工具，您无需直接编辑 XML 配置文件就可管理 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 绑定、行为、服务和诊断的设置。  
  
## 在 Visual Studio 中编辑配置文件  
 若要在 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 中编辑 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务项目的配置文件，请在**“解决方案资源管理器”**中右击该配置文件，然后选择**“编辑 WCF 配置”**上下文菜单项。这将启动[配置编辑器工具 \(SvcConfigEditor.exe\)](../../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md)。  
  
> [!NOTE]
>  如果通过在 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 的**“解决方案资源管理器”**中右击 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] Web 服务项目的配置文件来编辑该配置文件，应注意到缺少了**“编辑 WCF 配置”**上下文菜单项。若要解决此问题，请单击**“工具”**菜单，然后选择**“WCF 服务配置编辑器”**。此后，可以右击配置文件，并使用**“编辑 WCF 配置”**上下文菜单项。  
  
## 请参阅  
 [配置编辑器工具 \(SvcConfigEditor.exe\)](../../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md)   
 [正在配置服务](../../../../docs/framework/wcf/configuring-services.md)   
 [\<system.serviceModel\>](../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md)