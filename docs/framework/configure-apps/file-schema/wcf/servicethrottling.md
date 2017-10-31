---
title: "&lt;serviceThrottling&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: a337d064-1e64-4209-b4a9-db7fdb7e3eaf
caps.latest.revision: 22
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 22
---
# &lt;serviceThrottling&gt;
指定 Windows Communication Foundation \(WCF\) 服务的限制机制。  
  
## 语法  
  
```  
  
<serviceThrottling maxConcurrentCalls="Integer"  
    maxConcurrentInstances="Integer"  
    maxConcurrentSessions="Integer" />  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|maxConcurrentCalls|一个正整数，用于限制当前在整个 <xref:System.ServiceModel.ServiceHost> 中处理的消息数目。  超出限制的调用会进行排队。  将此值设置为 0 与将其设置为 Int32.MaxValue 等效。  默认值是 16 \* 处理器计数。|  
|maxConcurrentInstances|一个正整数，用于限制在整个 <xref:System.ServiceModel.ServiceHost> 中一次执行的 <xref:System.ServiceModel.InstanceContext> 对象数。  用于创建其他实例的请求将会排队，并在出现低于该限值的槽时完成。  默认值是 maxConcurrentSessions 和 MaxConcurrentCalls 的和|  
|maxConcurrentSessions|一个正整数，用于限制 <xref:System.ServiceModel.ServiceHost> 对象可以接受的会话数。<br /><br /> 此服务将接受超出限制的连接，但是，只有处于限制范围之内的通道处于活动状态（会从此通道中读取消息）。  将此值设置为 0 与将其设置为 Int32.MaxValue 等效。  默认值是 100 \* 处理器计数。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<行为\>](../../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)|指定行为元素。|  
  
## 备注  
 限制控件会对并发调用、实例或会话的数目施加限制以防止过度使用资源。  
  
 每次达到属性值时，就会记录一个跟踪。  第一个跟踪将记录为警告。  
  
## 示例  
 下面的配置示例指定服务将最大并发调用数限制为 2，并将最大并发实例数限制为 10。  有关运行此示例的详细示例，请参见[遏制](../../../../../docs/framework/wcf/samples/throttling.md)。  
  
```  
<behaviors>   
  <serviceBehaviors>   
    <behavior name="CalculatorServiceBehavior">   
      <serviceDebug includeExceptionDetailInFaults="False" />   
      <serviceMetadata httpGetEnabled="True"/>   
      <!-- Specify throttling behavior -->  
      <serviceThrottling maxConcurrentCalls="2"   
           maxConcurrentInstances="10"/>   
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
## 请参阅  
 <xref:System.ServiceModel.Description.ServiceThrottlingBehavior>   
 <xref:System.ServiceModel.Configuration.ServiceThrottlingElement>   
 [使用 ServiceThrottlingBehavior 控制 WCF 服务性能](../../../../../docs/framework/wcf/feature-details/using-servicethrottlingbehavior-to-control-wcf-service-performance.md)