---
title: "疑难解答：服务应用程序无法安装 | Microsoft Docs"
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
  - "服务, 调试"
  - "服务, 疑难解答"
  - "NT 服务疑难解答"
  - "服务应用程序疑难解答"
  - "Windows NT 服务, 疑难解答"
  - "Windows 服务应用程序, 疑难解答"
ms.assetid: 45c48e2e-b97d-44bc-8896-14f328e0ce33
caps.latest.revision: 8
author: "ghogen"
ms.author: "ghogen"
manager: "douge"
caps.handback.revision: 8
---
# 疑难解答：服务应用程序无法安装
如果服务应用程序无法正确安装，检查以确保服务类的 <xref:System.ServiceProcess.ServiceBase.ServiceName%2A> 属性值设置为与该服务的安装程序所显示的值相同。  该值在两种情况中必须相同，服务才能正确安装。  
  
> [!NOTE]
>  还可以查看安装日志，获得安装进程的反馈。  
  
 还应检查以确定是否已安装了另一个具有相同名称的服务。  服务名必须唯一，安装才能成功。  
  
## 请参阅  
 [Windows 服务应用程序介绍](../../../docs/framework/windows-services/introduction-to-windows-service-applications.md)