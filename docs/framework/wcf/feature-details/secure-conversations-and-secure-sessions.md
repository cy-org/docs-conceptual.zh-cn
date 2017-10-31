---
title: "安全对话和安全会话 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 48cb104a-532d-40ae-aa57-769dae103fda
caps.latest.revision: 13
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 13
---
# 安全对话和安全会话
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 的一项功能是能够在如下两个终结点之间建立安全会话：这两个终结点互相进行身份验证，并就加密和数字签名过程达成一致。例如，服务终结点可能要求客户端终结点发送一个基于 X.509 证书的安全令牌，以便进行身份验证。在对客户端进行身份验证之后，服务终结点将向客户端返回一个安全上下文令牌 \(SCT\)，该令牌随后将用于保护该会话中的所有后续消息。通过建立这一安全会话，可使两个终结点之间交换的一组消息更有效率，因为 SCT 具有对称密钥。在生成数字签名或加密一组数据时，与对称密钥相比，作为 X.509 证书基础的非对称密钥明显需要更多的计算能力。  
  
 启动策略（在 [WS\-SecurityPolicy](http://go.microsoft.com/fwlink/?LinkId=99817)（可能为英文网页）标准的第 6.2.7 节中定义）包含消息安全断言，这些断言用于保护通道，并用于在进行 RST\/SCT 和 RSTR\/SCT 交换之前对客户端进行身份验证。某些 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 标准绑定具有一个 `Security.Message.EstablishSecurityContext` 属性，该属性用于控制是否使用安全对话。使用自定义绑定时，启动由嵌套安全绑定元素来指示，具体方法是使用配置文件中的 [\<secureConversationBootstrap\>](../../../../docs/framework/configure-apps/file-schema/wcf/secureconversationbootstrap.md)<xref:System.ServiceModel.Channels.SecurityBindingElement.CreateSecureConversationBindingElement%2A> 或在代码中调用。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]会话的更多信息，请参见[使用会话](../../../../docs/framework/wcf/using-sessions.md)。  
  
## 请参阅  
 [会话、实例化和并发](../../../../docs/framework/wcf/feature-details/sessions-instancing-and-concurrency.md)   
 [如何：创建要求会话的服务](../../../../docs/framework/wcf/feature-details/how-to-create-a-service-that-requires-sessions.md)