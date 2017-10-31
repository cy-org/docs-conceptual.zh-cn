---
title: "在客户端上调试 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 56f9ad05-ea1b-4ef6-85f2-890f7ed71567
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# 在客户端上调试
为了让用户能够更容易地编写针对您的 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 服务的客户端应用程序，可以将 [\<serviceDebug\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicedebug.md) 服务行为添加到您的服务的配置文件中。此行为可用于发布帮助页，以及在返回到客户端的 SOAP 错误的详细信息中返回托管异常信息。