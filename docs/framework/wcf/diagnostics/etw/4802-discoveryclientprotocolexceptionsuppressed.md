---
title: "4802 - DiscoveryClientProtocolExceptionSuppressed | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 568212f7-1060-4f5c-a7a0-1352c7cc743b
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 4802 - DiscoveryClientProtocolExceptionSuppressed
## 属性  
  
|||  
|-|-|  
|ID|4802|  
|关键字|发现|  
|级别|信息|  
|通道|Microsoft\-Windows\-应用程序服务器\-应用程序\/调试|  
  
## 描述  
 当关闭 DiscoveryClient 时，ProtocolException 被禁止，此时发出此事件。  
  
## 消息  
 关闭 DiscoveryClient 时，ProtocolException 被禁止。  这可能是由于 DiscoveryService 仍在尝试向 DiscoveryClient 发送响应。  
  
## 详细信息