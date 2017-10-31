---
title: "扩展通道层 | Microsoft Docs"
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
  - "扩展通道 [WCF]"
ms.assetid: 4238db74-2fb6-4dc8-a326-f58527230810
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# 扩展通道层
通道层负责在客户端和服务之间交换消息。通道扩展可以实现新的协议功能（例如安全性）或传输功能（例如实现新的网络传输来传送 SOAP 消息）。  
  
## 本节内容  
 [通道模型概述](../../../../docs/framework/wcf/extending/channel-model-overview.md)  
 在较高层面概述了什么是通道、通道提供的功能以及通道在服务和客户端应用程序中的工作方式。  
  
 [开发通道](../../../../docs/framework/wcf/extending/developing-channels.md)  
 深入描述各种通道基础结构类型所起的作用、状态引擎和状态生命周期的工作方式、如何处理异常和错误、如何实现元数据支持以及通道如何使用消息编码器。  
  
 [自定义编码器](../../../../docs/framework/wcf/extending/custom-encoders.md)  
 描述消息编码器在通道中所起的作用以及如何生成消息编码器。  
  
 [自定义流升级](../../../../docs/framework/wcf/extending/custom-stream-upgrades.md)  
 描述由面向流的传输所提供的流的升级过程。