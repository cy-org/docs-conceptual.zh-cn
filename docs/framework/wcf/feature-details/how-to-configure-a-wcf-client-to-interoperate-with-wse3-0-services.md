---
title: "如何：配置 WCF 客户端以与 WSE&amp;3;.0 服务进行互操作 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3dadd7f1-d207-4ea5-a73b-3e8aa44407f8
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 如何：配置 WCF 客户端以与 WSE&amp;3;.0 服务进行互操作
当 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 客户端配置为使用 2004 年 8 月版的 WS-Addressing 规范时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端在网络级与 Web Services Enhancements 3.0 for Microsoft .NET (WSE) 服务兼容。  
  
### <a name="to-configure-a-wcf-client-to-interoperate-with-a-wse-30-web-service"></a>配置 WCF 客户端以与 WSE 3.0 Web 服务进行互操作  
  
1.  运行[ServiceModel 元数据实用工具 (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)创建[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]WSE 3.0 Web 服务客户端。  
  
     对于 WSE Web 服务，将创建一个 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端类。  
  
     有关创建详细信息[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]客户端，请参阅[如何︰ 创建客户端](../../../../docs/framework/wcf/how-to-create-a-wcf-client.md)。  
  
2.  创建一个类，表示可与 WSE 3.0 Web 服务进行通信的绑定。  
  
     下面的类是属于[与 WSE 互操作](http://msdn.microsoft.com/zh-cn/f6816861-96a0-45f9-8736-8e4e82cd3a41)示例。  
  
    1.  创建一个类，派生自<xref:System.ServiceModel.Channels.Binding>类。  
  
         下面的代码示例创建一个名为类`WseHttpBinding`派生的<xref:System.ServiceModel.Channels.Binding>类。  
  
         [!code-csharp[c_WCFClientToWSEService#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/wsehttpbinding.cs#1)]
         [!code-vb[c_WCFClientToWSEService#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/wsehttpbinding.vb#1)]  
  
    2.  向该类添加指定 WSE 完整声明、是否需要派生密钥、是否使用安全会话、是否需要签名确认以及消息保护设置的属性。  
  
         下面的代码示例定义`SecurityAssertion,``RequireDerivedKeys, EstablishSecurityContext, MessageProtectionOrder`分别指定 WSE 完整断言、 是否需要派生的密钥、 是否使用安全会话、 是否需要签名确认以及消息保护设置的属性。  
  
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
 下面的代码示例定义了一个自定义绑定，该绑定公开对应于 WSE 3.0 完整安全断言的各个属性的属性。 该自定义绑定（名为 `WseHttpBinding`）然后用于指定 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端的绑定属性。  
  
  
[!code-csharp[c_WCFClientToWSEService#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_wcfclienttowseservice/cs/client.cs#0)]
[!code-vb[c_WCFClientToWSEService#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_wcfclienttowseservice/vb/client.vb#0)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.ServiceModel.Channels.Binding>   
 [与 WSE 互操作](http://msdn.microsoft.com/zh-cn/f6816861-96a0-45f9-8736-8e4e82cd3a41)