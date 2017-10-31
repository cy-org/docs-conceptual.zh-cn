---
title: "核心通信：连接框架 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 61ee00e1-896d-47c8-942f-1db28ac89cdc
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# 核心通信：连接框架
本主题列出了由 [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 连接框架生成的所有异常。  
  
## 异常列表  
  
|资源代码|资源字符串|  
|----------|-----------|  
|CloseTimedOut|Close 方法在指定的时间后超时。增加传给 Close 调用的超时值，或者增加绑定上的 CloseTimeout 值。分配给此操作的时间可能是更长超时的一部分。|  
|ContentTypeMismatch|指定的内容类型已发送到期望收到该指定内容类型的服务。客户端和服务绑定可能不匹配。|  
|DuplexChannelAbortedDuringOpen|在 Open 过程中，与指定对象的双工通道终止。|  
|FramingValueNotAvailable|值无法访问，因为该值未完全解码。|  
|OperationAbortedDuringConnectionEstablishment|在建立与指定对象的连接时操作终止。|  
|ReceiveTimedOut2|接收操作已经在指定的时间后超时。分配给此操作的时间可能是更长超时的一部分。|  
|SendCannotBeCalledAfterCloseOutputSession|在调用 CloseOutputSession 之后不能在通道上发送消息。|