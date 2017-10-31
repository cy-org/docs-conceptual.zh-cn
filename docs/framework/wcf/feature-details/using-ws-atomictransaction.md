---
title: "使用 WS-AtomicTransaction | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WS-AT 协议 [WCF]"
ms.assetid: 04a4c200-0af0-4c5d-a3d9-87cb7339e054
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# 使用 WS-AtomicTransaction
WS\-AtomicTransaction \(WS\-AT\) 是一种可互操作的事务协议。它使您能够使用 Web 服务消息对分布式事务进行流处理并以可互操作的方式在异类事务基础结构之间进行协调。WS\-AT 使用两阶段提交协议在分布式应用程序、事务管理器和资源管理器之间驱动原子结果的生成。  
  
 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 提供的 WS\-AT 实现包括 Microsoft 分布式事务处理协调器 \(MSDTC\) 事务管理器中内置的协议服务。使用 WS\-AT，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序可以使事务流动到其他应用程序，包括使用第三方技术生成的可互操作的 Web 服务。  
  
 在客户端应用程序和服务器应用程序之间流动事务时，使用的事务协议由服务器在终结点上公开的绑定确定，而该终结点由客户端选择。一些 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 系统提供的绑定在默认情况下指定 `OleTransactions` 协议作为事务传播格式，而其他绑定在默认情况下指定 WS\-AT。您也可以以编程方式修改给定绑定内所选的事务协议。  
  
 协议的选择可影响以下内容：  
  
-   使事务从客户端流动到服务器所使用的消息头的格式。  
  
-   用于在客户端的事务管理器和服务器的事务之间运行两阶段提交协议以便解析事务结果的网络协议。  
  
 如果服务器和客户端使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 进行写入，则不需要使用 WS\-AT。可以改为使用 `NetTcpBinding` 的默认设置并启用 `TransactionFlow` 属性，此设置将使用 `OleTransactions` 协议。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][\<netTcpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/nettcpbinding.md).否则，如果您要使事务流动到使用第三方技术生成的 Web 服务，则必须使用 WS\-AT。  
  
## 请参阅  
 [配置 WS\-Atomic 事务支持](../../../../docs/framework/wcf/feature-details/configuring-ws-atomic-transaction-support.md)