---
title: "3550 - BufferOutOfOrderMessageNoInstance | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1299d294-99b8-430e-98b1-55f5f17002f3
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 3550 - BufferOutOfOrderMessageNoInstance
## 属性  
  
|||  
|-|-|  
|ID|3550|  
|关键字|WFServices|  
|级别|信息|  
|通道|Microsoft\-Windows\-应用程序服务器\-应用程序\/分析|  
  
## 描述  
 指示缓冲接收已失败。  服务实例准备好处理此特定操作时，将再次尝试该操作。  
  
## 消息  
 此时不能执行操作“%1”。  服务实例准备好处理此特定操作时，将进行另一个尝试。  
  
## 详细信息  
  
|数据项名称|数据项类型|描述|  
|-----------|-----------|--------|  
|OperationName|xs:string|操作的名称。|  
|AppDomain|xs:string|由 AppDomain.CurrentDomain.FriendlyName 返回的字符串。|