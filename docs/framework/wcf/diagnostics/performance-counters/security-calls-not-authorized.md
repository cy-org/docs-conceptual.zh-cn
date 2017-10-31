---
title: "Security Calls Not Authorized（未授权的安全调用次数） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cb6acdcd-7336-42e1-9ae8-ac891336cd58
caps.latest.revision: 6
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 6
---
# Security Calls Not Authorized（未授权的安全调用次数）
计数器名称：Security Calls Not Authorized（未授权的安全调用次数）。  
  
## 描述  
 当 <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccess%2A> 方法返回 `false` 时，此计数器将递增。  它指示传入的消息来自有效的用户并得到了良好保护，但该用户没有获得执行特定任务的授权。