---
title: "创建 WS-I 基本配置文件 1.1 可互操作服务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "配置 [WCF], 可互操作的服务"
ms.assetid: 91b70a21-8f5c-4679-808c-2ed5fa6b2013
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 创建 WS-I 基本配置文件 1.1 可互操作服务
将 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务终结点配置为可与 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] Web 服务客户端互操作：  
  
-   使用<xref:System.ServiceModel.BasicHttpBinding?displayProperty=fullName>作为服务终结点的绑定类型的类型。  
  
-   不要使用服务终结点上的回调和会话协定功能或事务行为  
  
 你可以根据需要在该绑定上启用对 HTTPS 和传输级客户端身份验证的支持。  
  
 以下功能<xref:System.ServiceModel.BasicHttpBinding>类需要 WS 之外的功能的基本配置文件 1.1:  
  
-   由消息传输优化机制 (MTOM) 消息编码控制<xref:System.ServiceModel.BasicHttpBinding.MessageEncoding%2A?displayProperty=fullName>属性。 将此属性保留为其默认值，即<xref:System.ServiceModel.WSMessageEncoding?displayProperty=fullName>以便不使用 MTOM。  
  
-   通过控制的消息安全<xref:System.ServiceModel.BasicHttpBinding.Security%2A?displayProperty=fullName>值提供的 WS-安全性支持符合 WS-我 Basic Security Profile 1.0。 将此属性保留为其默认值，即<xref:System.ServiceModel.SecurityMode?displayProperty=fullName>为不使用 Ws-security。  
  
 若要使元数据[!INCLUDE[indigo2](../../../includes/indigo2-md.md)]适用于服务[!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)]，使用 Web 服务客户端生成工具︰ [Web 服务描述语言工具 (Wsdl.exe)](http://msdn.microsoft.com/zh-cn/b9210348-8bc2-4367-8c91-d1a04b403e88)， [Web 服务发现工具 (Disco.exe)](http://msdn.microsoft.com/zh-cn/acd88078-c581-42bc-94ca-6633e2851979)，和`Add Web Reference`功能[!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]; 您必须启用元数据发布。 [!INCLUDE[crdefault](../../../includes/crdefault-md.md)][发布元数据终结点](../../../docs/framework/wcf/publishing-metadata-endpoints.md)。  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>描述  
 下面的代码示例演示如何添加与代码（或配置文件）中的 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] Web 服务客户端兼容的 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 终结点。  
  
### <a name="code"></a>代码  
 [!code-csharp[C_HowTo-WCFServiceAndASMXClient#0](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto-wcfserviceandasmxclient/cs/program.cs#0)]
 [!code-vb[C_HowTo-WCFServiceAndASMXClient#0](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto-wcfserviceandasmxclient/vb/program.vb#0)]  
  
 <!-- TODO: review snippet reference [!code[C_HowTo-WCFServiceAndASMXClient#1](../../../samples/snippets/common/VS_Snippets_CFX/c_howto-wcfserviceandasmxclient/common/app.config#1)]  -->  
  
## <a name="see-also"></a>另请参阅  
 [与 ASP.NET Web 服务互操作性](../../../docs/framework/wcf/feature-details/interop-with-aspnet-web-services.md)