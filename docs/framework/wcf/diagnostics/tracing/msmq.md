---
title: "MSMQ | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d9fca29f-fa44-4ec4-bb48-b10800694500
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# MSMQ
在 MSMQ 应用程序中，不会在 MSMQ 与队列通道之间传输任何额外活动。  
  
 另外，在执行 Send（发送）操作和 Receive（接收）操作时，还将 MSMQ 消息 ID 和 SOAP 消息 ID（连同活动 ID，如果存在）  
  
 作为队列通道跟踪的一部分来跟踪。  
  
 Receive（接收）操作所要求的传输的执行方式类似于其他任何传输（接收字节\-\>处理消息\-\>操作）。