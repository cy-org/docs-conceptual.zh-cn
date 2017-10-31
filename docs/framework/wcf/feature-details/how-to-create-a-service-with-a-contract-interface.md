---
title: "如何：使用协定接口创建服务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7b6803f6-d6f9-4cc2-9f1b-6f4c920475d5
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# 如何：使用协定接口创建服务
创建 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 协定的首选方式是使用接口。此协定指定访问服务提供的操作所必需的消息的集合和结构。此接口通过将 <xref:System.ServiceModel.ServiceContractAttribute> 类应用到该接口并将 <xref:System.ServiceModel.OperationContractAttribute> 类应用到要公开的方法来定义输入和输出类型。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]服务协定的更多信息，请参见[设计服务协定](../../../../docs/framework/wcf/designing-service-contracts.md)。  
  
### 使用接口创建 WCF 协定  
  
1.  使用 [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)]、C\# 或任何其他公共语言运行库语言创建一个新接口。  
  
2.  将 <xref:System.ServiceModel.ServiceContractAttribute> 类应用到该接口。  
  
3.  定义该接口中的方法。  
  
4.  对必须作为公共 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 协定的一部分公开的每个方法应用 <xref:System.ServiceModel.OperationContractAttribute> 类。  
  
## 示例  
 下面的代码示例演示一个定义服务协定的接口。  
  
 [!code-csharp[c_HowTo_CreateContractWithInterface#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_createcontractwithinterface/cs/source.cs#1)]
 [!code-vb[c_HowTo_CreateContractWithInterface#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_createcontractwithinterface/vb/source.vb#1)]  
  
 默认情况下，应用了 <xref:System.ServiceModel.OperationContractAttribute> 类的方法使用请求\-答复消息模式。[!INCLUDE[crabout](../../../../includes/crabout-md.md)] 该模式的更多消息，请参见 [如何：创建请求\-答复协定](../../../../docs/framework/wcf/feature-details/how-to-create-a-request-reply-contract.md)。您还可以通过设置属性 \(Attribute\) 的属性 \(Property\) 来创建和使用其他消息模式。有关更多示例，请参见[如何：创建单向协定](../../../../docs/framework/wcf/feature-details/how-to-create-a-one-way-contract.md)和[如何：创建双工协定](../../../../docs/framework/wcf/feature-details/how-to-create-a-duplex-contract.md)。  
  
## 请参阅  
 <xref:System.ServiceModel.ServiceContractAttribute>   
 <xref:System.ServiceModel.OperationContractAttribute>