---
title: "&lt;synchronousReceive&gt; 元素 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cc070387-3d11-4b02-a952-bc08ad2df05a
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# &lt;synchronousReceive&gt; 元素
此配置元素用于指定服务或客户端应用程序中用来接收消息的运行时行为。  它不具有任何属性或子元素。  
  
## 语法  
  
```  
  
<synchronousReceive />  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
 无。  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<行为\>](../../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)|指定终结点行为。|  
  
## 备注  
 使用此行为可指示通道侦听器使用同步接收，而非默认的异步接受。  [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 发出一个新线程，以为每个接受的通道进行抽取。  如果有许多通道，则可能出现线程溢出的情况。  
  
## 请参阅  
 <xref:System.ServiceModel.Configuration.SynchronousReceiveElement>   
 <xref:System.ServiceModel.Description.SynchronousReceiveBehavior>