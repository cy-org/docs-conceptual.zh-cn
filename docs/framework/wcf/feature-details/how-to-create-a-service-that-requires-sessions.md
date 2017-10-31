---
title: "如何：创建要求会话的服务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8a7613ef-0df9-47c3-b8dc-47f42cb1fd8b
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# 如何：创建要求会话的服务
会话在两个或更多终结点之间创建一个共享状态，从而启用一些有用的功能，例如回调、多跳安全性以及客户端和服务实例之间的关联。 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]中的会话[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]应用程序，请参阅[使用会话](../../../../docs/framework/wcf/using-sessions.md)。  
  
### <a name="to-specify-that-a-contract-require-its-binding-to-support-sessions"></a>指定协定需要其绑定来支持会话  
  
1.  创建至少包含一个操作的服务协定。 有关如何创建服务协定的示例，请参阅[如何︰ 定义服务协定](../../../../docs/framework/wcf/how-to-define-a-wcf-service-contract.md)。  
  
2.  修改<xref:System.ServiceModel.ServiceContractAttribute?displayProperty=fullName> ，通过设置声明的约定<xref:System.ServiceModel.ServiceContractAttribute.SessionMode%2A?displayProperty=fullName>至任一属性︰  
  
    -   <xref:System.ServiceModel.SessionMode?displayProperty=fullName>如果必须在会话中运行此协定。  
  
    -   <xref:System.ServiceModel.SessionMode?displayProperty=fullName>如果可以在会话中运行此协定。  
  
    -   <xref:System.ServiceModel.SessionMode?displayProperty=fullName>如果不得在会话中运行此协定。  
  
3.  配置服务终结点以使用支持会话的绑定。 下面的配置示例演示如何使用<xref:System.ServiceModel.WSDualHttpBinding?displayProperty=fullName>，支持 WS`-`ReliableMessaging 会话。  
  
     <!-- TODO: review snippet reference [!code[SCA.Session#2](../../../../samples/snippets/common/VS_Snippets_CFX/sca.session/common/hostapplication.exe.config#2)]  -->
     <!-- TODO: review snippet reference [!code-csharp[SCA.Session#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/sca.session/cs/hostapplication.exe.config#2)]  -->
     <!-- TODO: review snippet reference [!code-vb[SCA.Session#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/sca.session/vb/hostapplication.exe.config#2)]  -->  
  
## <a name="example"></a>示例  
 下面的代码示例演示如何指定协定级别会话要求并使用配置文件以支持与该要求<xref:System.ServiceModel.WSDualHttpBinding?displayProperty=fullName>绑定。  
  
 [!code-csharp[SCA.Session#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/sca.session/cs/services.cs#1)]
 [!code-vb[SCA.Session#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/sca.session/vb/services.vb#1)]  
  
 <!-- TODO: review snippet reference [!code[SCA.Session#2](../../../../samples/snippets/common/VS_Snippets_CFX/sca.session/common/hostapplication.exe.config#2)]  -->
 <!-- TODO: review snippet reference [!code-csharp[SCA.Session#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/sca.session/cs/hostapplication.exe.config#2)]  -->
 <!-- TODO: review snippet reference [!code-vb[SCA.Session#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/sca.session/vb/hostapplication.exe.config#2)]  -->  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.ServiceModel.ServiceContractAttribute?displayProperty=fullName>   
 <xref:System.ServiceModel.ServiceContractAttribute.SessionMode%2A?displayProperty=fullName>   
 <xref:System.ServiceModel.SessionMode?displayProperty=fullName>