---
title: "终结点：Calls Faulted（出错的调用次数） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 271e6284-9c4b-465f-b619-069e1555a5e4
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# 终结点：Calls Faulted（出错的调用次数）
计数器名称：Calls Faulted（出错的调用次数）。  
  
## 说明  
 对此终结点返回错误的调用次数。在 [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 应用程序中，服务方法使用 SOAP 错误消息来传递处理错误信息。SOAP 错误是包括在服务操作元数据中的消息类型，因此会创建一个错误协定，客户端可使用该协定来使执行更加可靠或更具交互性。由于 SOAP 错误在客户端以 XML 格式表示，因此具有高度的互操作性。  
  
## 请参阅  
 [在协定和服务中指定和处理错误](../../../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md)