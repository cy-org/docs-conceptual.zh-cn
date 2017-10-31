---
title: "如何：控制服务实例化 | Microsoft Docs"
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
ms.assetid: e0b12b34-8004-443a-a46d-83a5c00f2601
caps.latest.revision: 19
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 19
---
# 如何：控制服务实例化
通过设置服务的实例模式，可以指定创建 <xref:System.ServiceModel.InstanceContext?displayProperty=fullName>（及其关联的用户定义服务对象）的时间。  有关可能模式，请参见 <xref:System.ServiceModel.InstanceContextMode> 枚举。  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]行为的详细信息，请参见[使用行为配置和扩展运行时](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md)。  有关工作示例，请参见[行为](../../../../docs/framework/wcf/samples/behaviors.md)。  
  
### 使用代码控制服务实例生存期  
  
1.  将 <xref:System.ServiceModel.ServiceBehaviorAttribute> 应用于服务类。  
  
2.  将 <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A> 属性设置为下列值之一：<xref:System.ServiceModel.InstanceContextMode>、<xref:System.ServiceModel.InstanceContextMode> 或 <xref:System.ServiceModel.InstanceContextMode>。  
  
     [!code-csharp[C_ControlServiceInstancing#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_controlserviceinstancing/cs/source.cs#1)]
     [!code-vb[C_ControlServiceInstancing#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_controlserviceinstancing/vb/source.vb#1)]  
  
## 示例  
 下面的代码示例将 <xref:System.ServiceModel.ServiceBehaviorAttribute> 属性（attribute）的 <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A> 属性（property）设置为 <xref:System.ServiceModel.InstanceContextMode>。  
  
 [!code-csharp[c_ControlServiceInstancing#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_controlserviceinstancing/cs/source.cs#2)]
 [!code-vb[c_ControlServiceInstancing#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_controlserviceinstancing/vb/source.vb#2)]  
  
## 请参阅  
 <xref:System.ServiceModel.ServiceBehaviorAttribute>   
 <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A>   
 <xref:System.ServiceModel.InstanceContextMode>   
 [Service: Behaviors Samples](http://msdn.microsoft.com/zh-cn/4e3c6513-a7ff-4b35-8dcf-b5506c6f39a7)