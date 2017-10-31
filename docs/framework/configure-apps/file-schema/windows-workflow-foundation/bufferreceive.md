---
title: "&lt;bufferReceive&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: b23c3a54-10d4-4f13-ab6d-98b26b76f22a
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# &lt;bufferReceive&gt;
一种服务行为，允许服务使用缓冲接收处理，以使工作流服务能够处理无序消息。  
  
## 语法  
  
```  
  
<behaviors>  
  <serviceBehaviors>  
    <behavior name=String">  
      <bufferReceive maxPendingMessagesPerChannel=”Integer” />  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|maxPendingMessagesPerChannel|一个整数，指定每个通道允许的最大挂起消息数。  默认值为 512。  此属性限制工作流服务可接收的无序消息数。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<serviceBehaviors\> 的 \<behavior\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/behavior-of-servicebehaviors-of-workflow.md)|指定行为元素。|  
  
## 请参阅  
 <xref:System.ServiceModel.Activities.Description.BufferReceiveServiceBehavior>   
 <xref:System.ServiceModel.Activities.Configuration.BufferedReceiveElement>