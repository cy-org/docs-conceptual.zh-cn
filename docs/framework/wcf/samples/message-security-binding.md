---
title: "消息安全绑定 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a4570ce7-864e-461b-85d8-0f7bcc53c2c8
caps.latest.revision: 4
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 4
---
# 消息安全绑定
本节包含演示 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的 Windows 服务中消息安全绑定的示例。  
  
## 本节内容  
 [匿名消息安全](../../../../docs/framework/wcf/samples/message-security-anonymous.md)  
 此示例演示如何实现 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 应用程序，该应用程序使用不带客户端身份验证的消息级安全性，但需要使用服务器的 X.509 证书进行服务器身份验证。  
  
 [消息安全证书](../../../../docs/framework/wcf/samples/message-security-certificate.md)  
 此示例演示如何实现一个应用程序，该应用程序对客户端使用 WS 安全性和 X.509 v3 证书身份验证，并要求使用服务器的 X.509 v3 证书进行服务器身份验证。  
  
 [用户名消息安全](../../../../docs/framework/wcf/samples/message-security-user-name.md)  
 本示例演示如何实现一个应用程序，该应用程序对客户端使用具有用户名身份验证的 WS\-Security，并要求使用服务器的 X.509v3 证书对服务器进行身份验证。  
  
 [Windows 消息安全](../../../../docs/framework/wcf/samples/message-security-windows.md)  
 本示例演示如何将 <xref:System.ServiceModel.WSHttpBinding> 绑定配置为使用具有 Windows 身份验证的消息级安全性。