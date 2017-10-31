---
title: "如何：配置 WCF 服务以便与 ASP.NET Web 服务客户端进行互操作 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 48e1cd90-de80-4d6c-846e-631878955762
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# 如何：配置 WCF 服务以便与 ASP.NET Web 服务客户端进行互操作
若要配置[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]服务终结点进行互操作与[!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]Web 服务客户端，请使用<xref:System.ServiceModel.BasicHttpBinding?displayProperty=fullName>作为服务终结点的绑定类型的类型。  
  
 你可以根据需要在该绑定上启用对 HTTPS 和传输级客户端身份验证的支持。 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]Web 服务客户端不支持 MTOM 消息编码，因此<xref:System.ServiceModel.BasicHttpBinding.MessageEncoding%2A?displayProperty=fullName>属性应保留为其默认值，即<xref:System.ServiceModel.WSMessageEncoding?displayProperty=fullName>。 ASP.Net Web 服务客户端不支持 WS-安全性，因此<xref:System.ServiceModel.BasicHttpBinding.Security%2A?displayProperty=fullName>应设置为<xref:System.ServiceModel.BasicHttpSecurityMode>。  
  
 若要使元数据[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]适用于服务[!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]Web 服务代理生成工具 (即， [Web 服务描述语言工具 (Wsdl.exe)](http://go.microsoft.com/fwlink/?LinkId=73833)， [Web 服务发现工具 (Disco.exe)](http://go.microsoft.com/fwlink/?LinkId=73834)，和 Visual Studio 中的添加 Web 引用功能)，你应将公开一个 HTTP/GET 元数据终结点。  
  
### <a name="to-add-a-wcf-endpoint-that-is-compatible-with-aspnet-web-service-clients-in-code"></a>在代码中添加与 ASP.NET Web 服务客户端兼容的 WCF 终结点  
  
1.  创建一个新<xref:System.ServiceModel.BasicHttpBinding>实例  
  
2.  （可选） 启用此服务终结点绑定的传输安全的安全模式设置为绑定到<xref:System.ServiceModel.BasicHttpSecurityMode>。 有关详细信息，请参阅[传输安全性](../../../../docs/framework/wcf/feature-details/transport-security.md)。  
  
3.  使用刚创建的绑定实例，向服务主机添加一个新的应用程序终结点。 有关如何在代码中添加服务终结点的详细信息，请参阅[如何︰ 在代码中创建服务终结点](../../../../docs/framework/wcf/feature-details/how-to-create-a-service-endpoint-in-code.md)。  
  
4.  为服务启用一个 HTTP/GET 元数据终结点。 有关详细信息，请参阅[如何︰ 发布元数据服务使用代码](../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-code.md)。  
  
### <a name="to-add-a-wcf-endpoint-that-is-compatible-with-aspnet-web-service-clients-in-a-configuration-file"></a>在配置文件中添加与 ASP.NET Web 服务客户端兼容的 WCF 终结点  
  
1.  创建一个新<xref:System.ServiceModel.BasicHttpBinding>绑定配置。 有关详细信息，请参阅[如何︰ 在配置中指定服务绑定](../../../../docs/framework/wcf/how-to-specify-a-service-binding-in-configuration.md)。  
  
2.  （可选） 启用此服务终结点绑定配置的传输安全的安全模式设置为绑定到<xref:System.ServiceModel.BasicHttpSecurityMode>。 有关详细信息，请参阅[传输安全性](../../../../docs/framework/wcf/feature-details/transport-security.md)。  
  
3.  使用刚创建的绑定配置，为服务配置一个新的应用程序终结点。 有关如何在配置文件中添加服务终结点的详细信息，请参阅[如何︰ 在配置中创建服务终结点](../../../../docs/framework/wcf/feature-details/how-to-create-a-service-endpoint-in-configuration.md)。  
  
4.  为服务启用一个 HTTP/GET 元数据终结点。 有关详细信息，请参阅[如何︰ 使用配置文件服务的发布元数据](../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-a-configuration-file.md)。  
  
## <a name="example"></a>示例  
 下面的示例代码演示如何在代码（或配置文件）中添加一个与 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] Web 服务客户端兼容的 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 终结点。  
  
 [!code-csharp[C_HowTo-WCFServiceAndASMXClient#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto-wcfserviceandasmxclient/cs/program.cs#0)]
 [!code-vb[C_HowTo-WCFServiceAndASMXClient#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto-wcfserviceandasmxclient/vb/program.vb#0)]  
  
 <!-- TODO: review snippet reference [!code[C_HowTo-WCFServiceAndASMXClient#1](../../../../samples/snippets/common/VS_Snippets_CFX/c_howto-wcfserviceandasmxclient/common/app.config#1)]  -->  
  
## <a name="see-also"></a>另请参阅  
 [如何︰ 在代码中创建的服务终结点](../../../../docs/framework/wcf/feature-details/how-to-create-a-service-endpoint-in-code.md)   
 [如何︰ 使用代码为服务中发布元数据](../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-code.md)   
 [如何︰ 在配置中指定的服务绑定](../../../../docs/framework/wcf/how-to-specify-a-service-binding-in-configuration.md)   
 [如何︰ 在配置中创建的服务终结点](../../../../docs/framework/wcf/feature-details/how-to-create-a-service-endpoint-in-configuration.md)   
 [如何︰ 使用配置文件为服务中发布元数据](../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-a-configuration-file.md)   
 [传输安全](../../../../docs/framework/wcf/feature-details/transport-security.md)   
 [使用元数据](../../../../docs/framework/wcf/feature-details/using-metadata.md)