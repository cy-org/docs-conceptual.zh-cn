---
title: "System.ServiceModel.Channels.TcpConnectError | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 22d93797-072e-405d-a3e0-5c519ddf290b
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# System.ServiceModel.Channels.TcpConnectError
TCP 连接操作失败。  
  
## 说明  
 此警告级别的跟踪指示未能连接到 TCP 终结点。如果远程终结点在给定 IP 地址和端口没有响应，则可能出现此情况。如果随后进行的连接到其他有效 IP 地址（如 IPv4 或 IPv6 地址，或表示给定主机名的其他 IP 地址）的尝试成功，则可以忽略此跟踪。此跟踪内的异常可披露与错误有关的其他信息。  
  
## 请参阅  
 [跟踪](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [使用跟踪来排除应用程序故障](../../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)   
 [管理和诊断](../../../../../docs/framework/wcf/diagnostics/index.md)