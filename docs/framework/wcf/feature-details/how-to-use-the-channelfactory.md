---
title: "如何：使用 ChannelFactory | Microsoft Docs"
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
ms.assetid: d48f01b5-582b-4c8b-b547-8adddae7e371
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# 如何：使用 ChannelFactory
<xref:System.ServiceModel.ChannelFactory%601> 泛型类用于某些高级方案中，这些方案要求创建可用于创建多个通道的通道工厂。  
  
### 创建和使用 ChannelFactory 类  
  
1.  生成并运行一个 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务。  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [设计和实现服务](../../../../docs/framework/wcf/designing-and-implementing-services.md)、[正在配置服务](../../../../docs/framework/wcf/configuring-services.md) 和 [承载服务](../../../../docs/framework/wcf/hosting-services.md)。  
  
2.  使用 [ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 生成客户端协定（接口）。  
  
3.  在客户端代码中，使用 <xref:System.ServiceModel.ChannelFactory%601> 类创建多个终结点侦听器。  
  
## 示例  
 [!code-csharp[c_HowToUseChannelFactory#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtousechannelfactory/cs/source.cs#1)]
 [!code-vb[c_HowToUseChannelFactory#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtousechannelfactory/vb/source.vb#1)]