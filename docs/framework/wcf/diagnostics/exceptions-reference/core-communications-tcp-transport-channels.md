---
title: "核心通信：TCP 传输通道 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d5cd057f-faec-4e21-ae0e-18bbc22bcfb1
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# 核心通信：TCP 传输通道
本主题列出由 TCP 传输通道生成的所有异常。  
  
## 异常列表  
  
|资源代码|资源字符串|  
|----------|-----------|  
|SocketCloseReadTimeout|指定套接字的远程终结点未在指定和分配的超时内响应关闭请求。  可能远程终结点在从 Receive 操作接收 EOF 信号 \(Null\) 后未调用 Close。  分配给此操作的时间可能是更长超时的一部分。|