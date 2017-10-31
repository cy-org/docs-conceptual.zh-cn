---
title: "工作流的 &lt;behaviors&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 3c6017b6-0c4f-4192-bd67-9515f5d1ec82
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 工作流的 &lt;behaviors&gt;
此元素包含 **serviceBehaviors** 集合。  集合中的每个元素定义工作流服务所使用的行为元素。  每个行为元素由其唯一的 **name** 属性标识。  
  
 \<system.ServiceModel\>  
  
## 语法  
  
```  
  
<behaviors>  
   <serviceBehaviors>  
   </serviceBehaviors>  
</behaviors>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
 无  
  
### 子元素  
  
|元素|描述|  
|--------|--------|  
|[\<serviceBehaviors\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/servicebehaviors-of-workflow.md)|此配置节表示为特定工作流服务定义的所有行为。|  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<system.serviceModel\>](../../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md)|所有工作流配置元素的根元素。|  
  
## 请参阅  
 <xref:System.ServiceModel.Configuration.BehaviorsSection>   
 <xref:System.ServiceModel.Configuration.ServiceBehaviorElementCollection>   
 <xref:System.ServiceModel.Configuration.ServiceBehaviorElement>   
 [使用行为配置和扩展运行时](../../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md)