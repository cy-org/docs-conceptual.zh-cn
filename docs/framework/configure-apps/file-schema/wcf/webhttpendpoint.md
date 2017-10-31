---
title: "&lt;webHttpEndpoint&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ecaaeb6f-ebd0-411d-8b53-92477cd45347
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# &lt;webHttpEndpoint&gt;
此配置元素定义带有自动添加 [\<webHttp\>](../../../../../docs/framework/configure-apps/file-schema/wcf/webhttp.md) 行为的固定 [\<webHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/webhttpbinding.md) 绑定的标准终结点。  在编写 REST 服务时，请使用此终结点。  
  
## 语法  
  
```  
  
<system.serviceModel>  
    <standardEndpoints>  
       <webHttpEndpoint>   
          <standardEndpoint  
             automaticFormatSelectionEnabled="String"   
             defaultOutgoingResponseFormat=”Xml/Json”  
             helpEnabled=”Boolean”  
             webEndpointType=”String”/>        
       </webHttpEndpoint>   
    </standardEndpoints>  
</system.serviceModel>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|automaticFormatSelectionEnabled|一个布尔值，指示是否启用自动格式选择。<br /><br /> 如果启用了自动格式选择，基础结构将分析请求消息的 `Accept` 标头，并确定最适合的响应格式。  如果 `Accept` 标头未指定适合的响应格式，则基础结构将使用请求消息的 `Content-Type`，或使用操作的默认响应格式。|  
|defaultOutgoingResponseFormat|一个指定默认传出响应格式的特性。  此特性的类型为 <xref:System.Servicemodel.Web.Webmessageformat>|  
|helpEnabled|一个布尔值，指示是否为终结点启用了 HTTP 帮助页。|  
|webEndpointType|一个字符串，指定终结点的类型。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<standardEndpoints\>](../../../../../docs/framework/configure-apps/file-schema/wcf/standardendpoints.md)|具有一个或多个固定属性（地址、绑定和协定）的预定义终结点的标准终结点集合。|  
  
## 请参阅  
 <xref:System.ServiceModel.Description.WebHttpEndpoint>   
 <xref:System.ServiceModel.Configuration.WebHttpEndpointElement>