---
title: "如何：部署 COM+ 集成应用程序 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2e5a0510-db3c-4988-a09c-696285836650
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# 如何：部署 COM+ 集成应用程序
编写了 COM\+ 集成应用程序后，您可能要将它部署在另一台计算机上。本主题说明如何将 COM\+ 集成应用程序从一台计算机移动到另一台计算机。  
  
### 移动 COM\+ 承载的集成应用程序  
  
1.  确保两台计算机上都安装了 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]。  
  
2.  从计算机 A 中导出应用程序。  
  
3.  在计算机 B 上导入应用程序。  
  
4.  设置应用程序根目录。按照约定，此目录为 %PROGRAMFILES%\/ComPlus Applications\/{AppGUID}。  
  
5.  将计算机 A 上应用程序根目录中的 Application.config 和 Application.manifest 文件复制到计算机 B 上的应用程序根目录。  
  
6.  在计算机 B 的 Application.config 文件中编辑服务终结点地址以标识相应计算机。例如，将 http:\/\/machineA\/MyService 更改为 http:\/\/machineB\/MyService。  
  
### 移动 Web 承载的集成应用程序  
  
1.  确保两台计算机上都安装了 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]。  
  
2.  从计算机 A 中导出应用程序。  
  
3.  在计算机 B 上导入应用程序。  
  
4.  在计算机 B 上创建 IIS 虚拟根目录。  
  
5.  将计算机 A 上虚拟根目录中的 .svc 文件 \(componentName.svc\) 和 Web.config 文件复制到计算机 B 上新创建的虚拟根目录。  
  
## 请参阅  
 [与 COM\+ 应用程序集成的概述](../../../../docs/framework/wcf/feature-details/integrating-with-com-plus-applications-overview.md)   
 [如何：配置 COM\+ 服务设置](../../../../docs/framework/wcf/feature-details/how-to-configure-com-service-settings.md)   
 [如何：使用 COM\+ 服务模型配置工具](../../../../docs/framework/wcf/feature-details/how-to-use-the-com-service-model-configuration-tool.md)