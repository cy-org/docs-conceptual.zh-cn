---
title: "&lt;soapProcessing&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e8707027-e6b8-4539-893d-3cd7c13fbc18
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# &lt;soapProcessing&gt;
定义用于封送不同绑定类型和消息版本之间消息的客户端终结点行为。  
  
## 语法  
  
```  
  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|元素|描述|  
|--------|--------|  
|processMessages|一个布尔值，指定是否应封送 SOAP 消息版本之间的消息。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<行为\>](../../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)|指定终结点行为。|  
  
## 备注  
 SOAP 处理是指在各消息版本之间转换消息的过程。  
  
 [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 路由服务可以将消息从一个协议转换为另一个协议。  如果传入消息和传出消息的版本不相同，则会创建一条具有正确版本的新消息。  将消息从一个 <xref:System.ServiceModel.Channel.MessageVersion> 处理为另一个版本是通过构造一个新的 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 消息来实现的，该消息包含传入 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 消息的正文部分和相关标头。  在构造新的 WCF 消息的过程中，不会使用特定于寻址的标头或在路由器级别理解的标头，这是因为这些标头要么具有不同的版本（如果为寻址标头），要么已作为客户端和路由器之间的通信的一部分处理。  
  
 是否将一个标头置于出站消息内由此标头在通过传入通道层时是否已标记为已理解来决定。  不会移除不理解的标头（如自定义标头），并且会将此标头复制到出站消息中，以通过路由服务。  系统会将消息正文复制到出站消息中，  然后将此消息外发到出站通道，此时将创建和添加特定于该通信协议\/传输的所有标头和其他信封数据。  
  
 当指定了 SOAP 处理行为时，将执行此类处理步骤。  此 [\<soapProcessingExtension\>](../../../../../docs/framework/configure-apps/file-schema/wcf/soapprocessing.md) 行为是在启动路由服务时应用于所有客户端（传出）终结点的终结点行为。  默认情况下，[\<路由\>](../../../../../docs/framework/configure-apps/file-schema/wcf/routing-of-servicebehavior.md) 行为将为每个客户端终结点创建并附加一个新的 [\<soapProcessingExtension\>](../../../../../docs/framework/configure-apps/file-schema/wcf/soapprocessing.md) 行为（其 `processMessages` 设置为 `true`）。  如果您具有路由服务无法理解的协议，或者希望重写默认处理行为，则可以针对整个路由服务或仅针对特定终结点禁用 SOAP 处理。若要针对整个路由服务在所有终结点上禁用 SOAP 处理，请将 [\<路由\>](../../../../../docs/framework/configure-apps/file-schema/wcf/routing-of-servicebehavior.md) 行为的 `soapProcessing` 特性设置为 `false`。  若要针对特定终结点禁用 SOAP 处理，请使用此行为，并将其 `processMessages` 特性设置为 `false`，然后将此行为附加到不希望运行默认处理代码的终结点。当 [\<路由\>](../../../../../docs/framework/configure-apps/file-schema/wcf/routing-of-servicebehavior.md) 行为设置路由服务时，它将跳过重新应用终结点行为，由于已存在一个终结点行为。  
  
## 请参阅  
 <xref:System.ServiceModel.Routing.Configuration.> SoapProcessingExtensionElement?qualifyHint=False&autoUpgrade=True   
 <xref:System.ServiceModel.Routing.SoapProcessingBehavior>