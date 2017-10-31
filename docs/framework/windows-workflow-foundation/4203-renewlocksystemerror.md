---
title: "4203 - RenewLockSystemError | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6ec9ec6f-4ae2-45cf-b99b-02cdb9dc9ec9
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 4203 - RenewLockSystemError
## 属性  
  
|||  
|-|-|  
|ID|4203|  
|关键字|WFInstanceStore|  
|级别|错误|  
|通道|Microsoft\-Windows\-应用程序服务器\-应用程序\/调试|  
  
## 描述  
 指示 SQL 提供程序由于锁定到期日已过或者已删除锁定所有者，未能延长锁定到期日。  SqlWorkflowInstanceStore 将被中止。  
  
## 消息  
 未能延长锁定到期日，锁定到期日已过，或者已删除锁定所有者。  正在中止 SqlWorkflowInstanceStore。  
  
## 详细信息  
  
|数据项名称|数据项类型|描述|  
|-----------|-----------|--------|  
|AppDomain|xs:string|由 AppDomain.CurrentDomain.FriendlyName 返回的字符串。|