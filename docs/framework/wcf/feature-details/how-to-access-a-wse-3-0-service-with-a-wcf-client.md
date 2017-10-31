---
title: "如何：使用 WCF 客户端访问 WSE 3.0 服务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1f9bcd9b-8f8f-47fa-8f1e-0d47236eb800
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# 如何：使用 WCF 客户端访问 WSE 3.0 服务
当 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 客户端配置为使用 2004 年 8 月版的 WS-Addressing 规范时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端在网络级别与 Web Services Enhancements (WSE) 3.0 for Microsoft .NET 服务兼容。 但是，WSE 3.0 服务不支持元数据交换 (MEX) 协议，因此当您使用[ServiceModel 元数据实用工具 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)创建[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]客户端类，在安全设置不能应用于生成[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]客户端。 因此，在生成 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端后，必须指定 WSE 3.0 服务要求的安全设置。  
  
 您可以在考虑 WSE 3.0 服务的要求以及 WSE 3.0 服务和 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端之间的互操作要求的情况下，使用自定义绑定来应用这些安全设置。 这些互操作性要求包括前面提到的使用 2004 年 8 月的 Ws-addressing 规范和 WSE 3.0 默认消息保护<xref:System.ServiceModel.Security.MessageProtectionOrder>。 默认消息保护为[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]是<xref:System.ServiceModel.Security.MessageProtectionOrder>。 本主题详细介绍如何创建与 WSE 3.0 服务互操作的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 绑定。 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 还提供了融入此绑定的示例。 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]此示例中，请参阅[与 ASMX Web 服务互操作性](../../../../docs/framework/wcf/samples/interoperating-with-asmx-web-services.md)。  
  
### <a name="to-access-a-wse-30-web-service-with-a-wcf-client"></a>使用 WCF 客户端访问 WSE 3.0 Web 服务  
  
1.  运行[ServiceModel 元数据实用工具 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)创建[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]WSE 3.0 Web 服务客户端。  
  
     对于 WSE 3.0 Web 服务，会创建一个 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端。 因为 WSE 3.0 不支持 MEX 协议，因此不能使用该工具检索 Web 服务的安全要求。 应用程序开发人员必须为客户端添加安全设置。  
  
     [!INCLUDE[crabout](../../../../includes/crabout-md.md)]创建[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]客户端，请参阅[如何︰ 创建客户端](../../../../docs/framework/wcf/how-to-create-a-wcf-client.md)。  
  
2.  创建一个类，表示可与 WSE 3.0 Web 服务进行通信的绑定。  
  
     下面的类是属于[与 WSE 互操作](http://msdn.microsoft.com/zh-cn/f6816861-96a0-45f9-8736-8e4e82cd3a41)示例︰  
  
    1.  创建一个类，派生自<xref:System.ServiceModel.Channels.Binding>类。  
  
         下面的代码示例创建一个名为类`WseHttpBinding`派生的<xref:System.ServiceModel.Channels.Binding>类。  
  
         [!code-csharp[c_WCFClientToWSEService#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/wsehttpbinding.cs#1)]
         [!code-vb[c_WCFClientToWSEService#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/wsehttpbinding.vb#1)]  
  
    2.  向该类中添加属性，用以指定 WSE 服务使用的 WSE 完整断言、是否需要派生密钥、是否使用安全会话、是否需要签名确认以及消息保护设置。 在 WSE 3.0 中，完整断言指定客户端或 Web 服务的安全要求，它类似于 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中绑定的身份验证模式。  
  
         下面的代码示例定义了 `SecurityAssertion`、`RequireDerivedKeys`、`EstablishSecurityContext` 和 `MessageProtectionOrder` 属性，这些属性分别指定 WSE 完整断言、是否需要派生密钥、是否使用安全会话、是否需要签名确认以及消息保护设置。  
  
         [!code-csharp[c_WCFClientToWSEService#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/wsehttpbinding.cs#3)]
         [!code-vb[c_WCFClientToWSEService#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/wsehttpbinding.vb#3)]  
  
    3.  重写<xref:System.ServiceModel.Channels.Binding.CreateBindingElements%2A>方法以设置绑定属性。  
  
         下面的代码示例通过获取 `SecurityAssertion` 和 `MessageProtectionOrder` 属性的值来指定传输协议、消息编码和消息保护设置。  
  
         [!code-csharp[c_WCFClientToWSEService#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/wsehttpbinding.cs#2)]
         [!code-vb[c_WCFClientToWSEService#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/wsehttpbinding.vb#2)]  
  
3.  在客户端应用程序代码中，添加设置绑定属性的代码。  
  
     下面的代码示例指定 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端必须使用 WSE 3.0 `AnonymousForCertificate` 完整安全断言定义的消息保护和身份验证。 此外，还需要安全会话和派生密钥。  
  
     [!code-csharp[c_WCFClientToWSEService#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/client.cs#4)]
     [!code-vb[c_WCFClientToWSEService#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/client.vb#4)]  
  
## <a name="example"></a>示例  
 下面的代码示例定义了一个自定义绑定，该绑定公开对应于 WSE 3.0 完整安全断言的各个属性的属性。 之后，使用该自定义绑定（名为 `WseHttpBinding`）来指定与 WSSecurityAnonymous WSE 3.0 QuickStart 示例通信的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端的绑定属性。  
  
  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.ServiceModel.Channels.Binding>   
 [与 WSE 互操作](http://msdn.microsoft.com/zh-cn/f6816861-96a0-45f9-8736-8e4e82cd3a41)