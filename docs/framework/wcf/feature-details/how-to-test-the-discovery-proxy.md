---
title: "如何：测试发现代理 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d96e3fa2-3c42-4e5d-8244-2694081bdc32
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# 如何：测试发现代理
本主题是演示如何实现发现代理的四个主题中的第四个。  在上一个主题[如何：实现使用发现代理查找服务的客户端应用程序](../../../../docs/framework/wcf/feature-details/client-app-discovery-proxy-to-find-a-service.md)中，您实现了使用发现代理查找服务然后调用该服务的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端应用程序。  本主题说明如何验证发现代理、服务以及客户端应用程序是否按预期方式工作。  
  
### 运行发现代理  
  
1.  作为管理员打开命令提示。  
  
2.  您可能会看到显示如下内容的对话框：Windows 防火墙已经阻止此程序的部分功能。  如果看到此消息，请单击**“取消阻止”**按钮。  
  
3.  在命令提示中，运行发现代理 DiscoveryProxy.exe。  
  
4.  应用程序应显示以下文本：`Proxy started. Hit Enter to exit`。  
  
### 运行可检测服务  
  
1.  作为管理员打开命令提示。  
  
2.  在命令提示中，运行 Service.exe 可检测服务。  
  
3.  DiscoveryProxy.exe 应显示以下文本：`******* Adding the following service: ** [Service Contract Name] ** [Service Endpoint Addr] 3.******* Done *******` .  
  
### 运行客户端应用程序  
  
1.  打开命令提示。  
  
2.  在命令提示中，运行 client.exe 应用程序。  
  
3.  几秒钟后，客户端应用程序显示以下文本：Connecting to \[Service\-Endpoint\]。  
  
4.  然后，service.exe 应显示以下文本：Greeting request received, I will respond.  
  
5.  然后，client.exe 应显示以下文本：Hello Client\!  
  
### 关闭应用程序  
  
1.  关闭客户端应用程序。  
  
2.  关闭服务。  此时，发现代理显示以下文本：`******* Removing the following service: ** [Service Contract Name] ** [Service Endpoint Addr] 2.3.******* Done *******`。  
  
3.  关闭发现代理。  
  
## 请参阅  
 [WCF Discovery 概述](../../../../docs/framework/wcf/feature-details/wcf-discovery-overview.md)   
 [如何：实现发现代理](../../../../docs/framework/wcf/feature-details/how-to-implement-a-discovery-proxy.md)   
 [如何：实现向发现代理注册的可检测到的服务](../../../../docs/framework/wcf/feature-details/discoverable-service-that-registers-with-the-discovery-proxy.md)   
 [如何：实现使用发现代理查找服务的客户端应用程序](../../../../docs/framework/wcf/feature-details/client-app-discovery-proxy-to-find-a-service.md)