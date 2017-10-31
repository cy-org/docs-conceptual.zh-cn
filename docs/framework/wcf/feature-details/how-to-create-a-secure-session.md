---
title: "如何：创建安全会话 | Microsoft Docs"
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
  - "安全性 [WCF], 创建会话"
ms.assetid: b6f42b5a-bbf7-45cf-b917-7ec9fa7ae110
caps.latest.revision: 10
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 10
---
# 如何：创建安全会话
除 [\<basicHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md)绑定外，已启用消息安全时，[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 中系统提供的绑定将自动使用安全会话。  
  
 默认情况下，安全会话不会在已回收的 Web 服务器中存在。  建立安全会话时，客户端和服务将缓存与安全会话关联的密钥。  交换消息时，只交换已缓存密钥的标识符。  如果回收了 Web 服务器，则也会回收缓存，因此 Web 服务器将无法检索该标识符的已缓存密钥。  如果发生这种情况，将会引发异常并返回至客户端。  使用有状态安全上下文令牌 \(SCT\) 的安全会话可以在回收 Web 服务器后存在。  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]在安全会话中使用有状态 SCT，请参见[如何：为安全会话创建安全上下文令牌](../../../../docs/framework/wcf/feature-details/how-to-create-a-security-context-token-for-a-secure-session.md)。  
  
### 通过使用系统提供的一个绑定指定服务使用安全会话  
  
-   配置服务以使用支持消息安全的系统提供的绑定。  
  
     除 [\<basicHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md)绑定外，在系统提供的绑定配置为使用消息安全时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 将自动使用安全会话。  下表列出了支持消息安全的系统提供的绑定以及消息安全是否是默认的安全机制。  
  
    |系统提供的绑定|配置元素|默认情况下是否启用消息安全|  
    |-------------|----------|-------------------|  
    |<xref:System.ServiceModel.BasicHttpBinding>|[\<basicHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md)|No|  
    |<xref:System.ServiceModel.WSHttpBinding>|[\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md)|是|  
    |<xref:System.ServiceModel.WSDualHttpBinding>|[\<wsDualHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wsdualhttpbinding.md)|是|  
    |<xref:System.ServiceModel.WSFederationHttpBinding>|[\<wsFederationHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wsfederationhttpbinding.md)|是|  
    |<xref:System.ServiceModel.NetTcpBinding>|[\<netTcpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/nettcpbinding.md)|No|  
    |<xref:System.ServiceModel.NetMsmqBinding>|[\<netMsmqBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/netmsmqbinding.md)|No|  
  
     下面的代码示例使用配置指定名为 `wsHttpBinding_Calculator` 的绑定，该绑定使用了 [\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md)、消息安全和安全会话。  
  
    ```  
    <bindings>  
      <WSHttpBinding>  
       <binding name = "wsHttpBinding_Calculator">  
         <security mode="Message">  
           <message clientCredentialType="Windows"/>  
         </security>  
        </binding>  
      </WSHttpBinding>  
    </bindings>  
    ```  
  
     下面的代码示例指定了用于保护 `secureCalculator` 服务的 [\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md)、消息安全和安全会话。  
  
     [!code-csharp[c_CreateSecureSession#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_createsecuresession/cs/secureservice.cs#1)]
     [!code-vb[c_CreateSecureSession#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_createsecuresession/vb/secureservice.vb#1)]  
  
    > [!NOTE]
    >  通过将 `establishSecurityContext` 属性设置为 `false`，可以为 [\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md)关闭安全会话。  对于其他系统提供的绑定，只能通过创建自定义绑定来关闭安全会话。  
  
### 通过使用自定义绑定来指定服务使用安全会话  
  
-   创建一个自定义绑定，该绑定指定由安全会话保护 SOAP 消息。  
  
     [!INCLUDE[crabout](../../../../includes/crabout-md.md)]创建自定义绑定的更多信息，请参见[如何：自定义系统提供的绑定](../../../../docs/framework/wcf/extending/how-to-customize-a-system-provided-binding.md)。  
  
     下面的代码示例使用配置来指定使用安全会话的消息的自定义绑定。  
  
    ```  
    <bindings>  
      <!-- configure a custom binding -->  
      <customBinding>  
        <binding name="customBinding_Calculator">  
          <security authenticationMode="SecureConversation" />  
          <secureConversationBootstrap authenticationMode="SspiNegotiated" />  
          <textMessageEncoding messageVersion="Soap12WSAddressing10" writeEncoding="utf-8"/>  
          <httpTransport/>  
        </binding>  
      </customBinding>  
    </bindings>  
    ```  
  
     下面的代码示例创建一个自定义绑定，该绑定使用 <xref:System.ServiceModel.Configuration.AuthenticationMode> 身份验证模式启动安全会话。  
  
     [!code-csharp[c_CreateSecureSession#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_createsecuresession/cs/secureservice.cs#2)]
     [!code-vb[c_CreateSecureSession#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_createsecuresession/vb/secureservice.vb#2)]  
  
## 请参阅  
 [WCF 绑定概述](../../../../docs/framework/wcf/bindings-overview.md)