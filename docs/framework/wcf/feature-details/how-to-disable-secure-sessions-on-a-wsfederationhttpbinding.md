---
title: "如何：在 WSFederationHttpBinding 上禁用安全会话 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "联合"
  - "WCF, 联合"
ms.assetid: 675fa143-6a4e-4be3-8afc-673334ab55ec
caps.latest.revision: 16
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 16
---
# 如何：在 WSFederationHttpBinding 上禁用安全会话
某些服务可能需要联合凭据，但不支持安全会话。在这种情况下，必须禁用安全会话功能。与 <xref:System.ServiceModel.WsHttpBinding> 不同，<xref:System.ServiceModel.WSFederationHttpBinding> 类不支持在与服务通信时禁用安全会话。相反，您必须创建一个自定义绑定，以便用引导来替换安全会话设置。  
  
 本主题演示如何修改 <xref:System.ServiceModel.WSFederationHttpBinding> 中包含的绑定元素以创建自定义绑定。结果与 <xref:System.ServiceModel.WSFederationHttpBinding> 基本相同，只是它不使用安全会话。  
  
### 创建不使用安全会话的自定义联合绑定  
  
1.  创建 <xref:System.ServiceModel.WSFederationHttpBinding> 类的一个实例，方法可以是在代码中以强制方式创建，也可以是从配置文件中加载。  
  
2.  将 <xref:System.ServiceModel.WSFederationHttpBinding> 克隆到一个 <xref:System.ServiceModel.Channels.CustomBinding> 中。  
  
3.  在 <xref:System.ServiceModel.Channels.CustomBinding> 中查找 <xref:System.ServiceModel.Channels.SecurityBindingElement>。  
  
4.  在 <xref:System.ServiceModel.Channels.SecurityBindingElement> 中查找 <xref:System.ServiceModel.Security.Tokens.SecureConversationSecurityTokenParameters>。  
  
5.  用 <xref:System.ServiceModel.Security.Tokens.SecureConversationSecurityTokenParameters> 中的引导安全绑定元素替换原始 <xref:System.ServiceModel.Channels.SecurityBindingElement>。  
  
## 示例  
 下面的示例创建一个不使用安全会话的自定义联合绑定。  
  
 [!code-csharp[c_CustomFederationBinding#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customfederationbinding/cs/c_customfederationbinding.cs#0)]
 [!code-vb[c_CustomFederationBinding#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customfederationbinding/vb/c_customfederationbinding.vb#0)]  
  
## 编译代码  
  
-   若要编译代码示例，请创建一个引用 System.ServiceModel.dll 程序集的项目。  
  
## 请参阅  
 [绑定与安全](../../../../docs/framework/wcf/feature-details/bindings-and-security.md)