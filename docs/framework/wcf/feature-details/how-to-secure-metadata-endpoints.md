---
title: "如何：保护元数据终结点 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9f71b6ae-737c-4382-8d89-0a7b1c7e182b
caps.latest.revision: 13
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 13
---
# 如何：保护元数据终结点
服务的元数据中可能包含恶意用户可以利用的关于您的应用程序的敏感信息。服务使用者可能还要求一种用于获取关于服务的元数据的安全机制。因此，有时需要使用安全终结点来发布元数据。  
  
 通常使用在用于保护应用程序终结点的 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 中定义的标准安全机制来保护元数据终结点。\([!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][安全性概述](../../../../docs/framework/wcf/feature-details/security-overview.md).\)  
  
 本主题演示创建由安全套接字层 \(SSL\) 证书保护的终结点（换言之，HTTPS 终结点）的步骤。  
  
### 在代码中创建安全的 HTTPS GET 元数据终结点  
  
1.  使用适当的 X.509 证书配置端口。该证书必须来自受信任的颁发机构，而且还必须有既定的“服务授权”用途。必须使用 HttpCfg.exe 工具将该证书附加到该端口。请参见[如何：使用 SSL 证书配置端口](../../../../docs/framework/wcf/feature-details/how-to-configure-a-port-with-an-ssl-certificate.md)。  
  
    > [!IMPORTANT]
    >  该证书或其域名系统 \(DNS\) 的主题必须与计算机的名称匹配。这一点非常重要，原因是 HTTPS 机制所执行的前几个步骤之一是检查是否将证书颁发给了在其上调用了该证书的地址的统一资源标识符 \(URI\)。  
  
2.  创建 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 类的新实例。  
  
3.  将 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 类的 <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetEnabled%2A> 属性设置为 `true`。  
  
4.  将 <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetUrl%2A> 属性设置为适当的 URL。请注意，如果指定绝对地址，则 URL 必须以方案“https:\/\/”开始。如果指定相对地址，则必须为服务主机提供一个 HTTPS 基址。如果不设置此属性，则默认地址为 ""，或者直接为服务的 HTTPS 基址。  
  
5.  将该实例添加到 <xref:System.ServiceModel.Description.ServiceDescription> 类的 <xref:System.ServiceModel.Description.ServiceDescription.Behaviors%2A> 属性返回的行为集合中，如下面的代码所示：  
  
     [!code-csharp[c_HowToSecureEndpoint#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosecureendpoint/cs/source.cs#1)]
     [!code-vb[c_HowToSecureEndpoint#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosecureendpoint/vb/source.vb#1)]  
  
### 在配置中创建安全的 HTTPS GET 元数据终结点  
  
1.  将 [\<行为\>](../../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md) 元素添加到服务配置文件的 [\<system.serviceModel\>](../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md) 元素中。  
  
2.  向 [\<行为\>](../../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md) 元素中添加一个 [\<serviceBehaviors\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicebehaviors.md) 元素。  
  
3.  向 `<serviceBehaviors>` 元素中添加一个 [\<行为\>](../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-servicebehaviors.md) 元素。  
  
4.  将 `<behavior>` 元素的 `name` 属性设置为适当的值。需要 `name` 属性。下面的示例使用 `mySvcBehavior` 值。  
  
5.  向 `<behavior>` 元素中添加一个 [\<serviceMetadata\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicemetadata.md)。  
  
6.  将 `<serviceMetadata>` 元素的 `httpsGetEnabled` 属性设置为 `true`。  
  
7.  将 `<serviceMetadata>` 元素的 `httpsGetUrl` 属性设置为适当的值。请注意，如果指定绝对地址，则 URL 必须以方案“https:\/\/”开始。如果指定相对地址，则必须为服务主机提供一个 HTTPS 基址。如果不设置此属性，则默认地址为 ""，或者直接为服务的 HTTPS 基址。  
  
8.  若要将该行为用于服务，需要将 [\<service\>](../../../../docs/framework/configure-apps/file-schema/wcf/service.md) 元素的 `behaviorConfiguration` 属性设置为该行为元素的名称属性的值下面的配置代码演示了一个完整的示例。  
  
    ```  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
     <system.serviceModel>  
      <behaviors>  
       <serviceBehaviors>  
        <behavior name="mySvcBehavior">  
         <serviceMetadata httpsGetEnabled="true"   
              httpsGetUrl="https://localhost:8036/calcMetadata" />  
        </behavior>  
       </serviceBehaviors>  
      </behaviors>  
     <services>  
      <service behaviorConfiguration="mySvcBehavior"   
            name="Microsoft.Security.Samples.Calculator">  
       <endpoint address="http://localhost:8037/ServiceModelSamples/calculator"  
       binding="wsHttpBinding" bindingConfiguration=""     
       contract="Microsoft.Security.Samples.ICalculator" />  
      </service>  
     </services>  
    </system.serviceModel>  
    </configuration>  
    ```  
  
## 示例  
 下面的示例创建 <xref:System.ServiceModel.ServiceHost> 类的一个实例并添加一个终结点。然后，该代码创建 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> 类的一个实例并设置属性以创建一个安全的元数据交换点。  
  
 [!code-csharp[c_HowToSecureEndpoint#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosecureendpoint/cs/source.cs#0)]
 [!code-vb[c_HowToSecureEndpoint#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosecureendpoint/vb/source.vb#0)]  
  
## 编译代码  
 该代码示例使用下列命名空间：  
  
-   <xref:System.ServiceModel?displayProperty=fullName>  
  
-   <xref:System.ServiceModel.Description?displayProperty=fullName>  
  
## 请参阅  
 <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetEnabled%2A>   
 <xref:System.ServiceModel.Description.ServiceMetadataBehavior>   
 <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetUrl%2A>   
 [如何：使用 SSL 证书配置端口](../../../../docs/framework/wcf/feature-details/how-to-configure-a-port-with-an-ssl-certificate.md)   
 [使用证书](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)   
 [元数据的安全注意事项](../../../../docs/framework/wcf/feature-details/security-considerations-with-metadata.md)   
 [保护服务和客户端的安全](../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)