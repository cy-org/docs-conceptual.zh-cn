---
title: "&lt;workflowControlEndpoint&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6c89e76c-643b-4b6a-9b25-628f753d7027
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# &lt;workflowControlEndpoint&gt;
此配置元素定义用于控制工作流实例的执行（创建、运行、挂起、终止等）的标准终结点。  
  
## 语法  
  
```  
  
<system.serviceModel>  
    <standardEndpoints>  
       <workflowControlEndpoint>   
          <standardEndpoint  
                  name="String" />   
       </workflowControlEndpoint>          
    </standardEndpoints>  
</system.serviceModel>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|name|一个字符串，指定标准终结点的配置的名称。  此名称在服务终结点的 `endpointConfiguration` 特性中用于将标准终结点链接到其配置。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<standardEndpoints\>](../../../../../docs/framework/configure-apps/file-schema/wcf/standardendpoints.md)|具有一个或多个固定属性（地址、绑定和协定）的预定义终结点的标准终结点集合。|  
  
## 请参阅  
 <xref:System.ServiceModel.Activites.WorkflowControlEndpoint>