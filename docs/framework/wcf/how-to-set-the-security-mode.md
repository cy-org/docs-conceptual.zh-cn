---
title: "如何：设置安全模式 | Microsoft Docs"
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
  - "模式属性"
  - "WCF, 安全"
  - "WCF, 安全模式"
ms.assetid: 6e01dd9f-b5dd-4474-b24c-06e124de4ff7
caps.latest.revision: 22
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 22
---
# 如何：设置安全模式
[!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 安全有三个常用安全模式：传输、消息和“使用消息凭据的传输”，这三种模式存在于大多数预定义绑定中。另外，还有两种特定于两个绑定的模式：<xref:System.ServiceModel.BasicHttpBinding> 上的“transport\-credential only”模式和 <xref:System.ServiceModel.NetMsmqBinding> 上的“Both”模式。不过，本主题主要讨论三种常见安全模式：<xref:System.ServiceModel.SecurityMode>、<xref:System.ServiceModel.SecurityMode> 和 <xref:System.ServiceModel.SecurityMode>。  
  
 请注意，并非所有预定义绑定都支持所有这些模式。本主题使用 <xref:System.ServiceModel.WSHttpBinding> 和 <xref:System.ServiceModel.NetTcpBinding> 类来设置模式，并演示如何以编程方式来设置安全模式，如何通过配置来设置安全模式。  
  
 [!INCLUDE[crabout](../../../includes/crabout-md.md)] [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 安全的更多信息，请参见[安全性概述](../../../docs/framework/wcf/feature-details/security-overview.md)、[保证服务的安全](../../../docs/framework/wcf/securing-services.md)和[保护服务和客户端的安全](../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)。[!INCLUDE[crabout](../../../includes/crabout-md.md)]传输模式和消息模式的更多信息，请参见[传输安全](../../../docs/framework/wcf/feature-details/transport-security.md)和 [消息安全](../../../docs/framework/wcf/feature-details/message-security-in-wcf.md)。  
  
### 在代码中设置安全模式  
  
1.  创建要使用的绑定类的一个实例。有关预定义绑定的列表，请参见[系统提供的绑定](../../../docs/framework/wcf/system-provided-bindings.md)。此示例创建 <xref:System.ServiceModel.WSHttpBinding> 类的一个实例。  
  
2.  设置 `Security` 属性所返回的对象的 `Mode` 属性。  
  
     [!code-csharp[c_SettingSecurityMode#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#1)]
     [!code-vb[c_SettingSecurityMode#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#1)]  
  
     或者，设置为消息模式，如下面的代码所示。  
  
     [!code-csharp[c_SettingSecurityMode#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#2)]
     [!code-vb[c_SettingSecurityMode#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#2)]  
  
     或者，设置为使用消息凭据的传输模式，如下面的代码所示。  
  
     [!code-csharp[c_SettingSecurityMode#3](../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#3)]
     [!code-vb[c_SettingSecurityMode#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#3)]  
  
3.  此外，还可以在绑定的构造函数中设置模式，如下面的代码所示。  
  
     [!code-csharp[c_SettingSecurityMode#4](../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#4)]
     [!code-vb[c_SettingSecurityMode#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#4)]  
  
## 设置 ClientCredentialType 属性  
 将模式设置为三个值之一，就确定了 `ClientCredentialType` 属性的设置方式。例如，使用 <xref:System.ServiceModel.WSHttpBinding> 类将模式设置为 `Transport`，意味着必须将 <xref:System.ServiceModel.HttpTransportSecurity> 类的 <xref:System.ServiceModel.HttpTransportSecurity.ClientCredentialType%2A> 属性设置为相应的值。  
  
#### 针对传输模式设置 ClientCredentialType 属性  
  
1.  创建绑定的一个实例。  
  
2.  将 `Mode` 属性设置为 `Transport`。  
  
3.  将 `ClientCredential` 属性设置为适当的值。下面的代码将该属性设置为 `Windows`。  
  
     [!code-csharp[c_SettingSecurityMode#5](../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#5)]
     [!code-vb[c_SettingSecurityMode#5](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#5)]  
  
#### 针对消息模式设置 ClientCredentialType 属性  
  
1.  创建绑定的一个实例。  
  
2.  将 `Mode` 属性设置为 `Message`。  
  
3.  将 `ClientCredential` 属性设置为适当的值。下面的代码将该属性设置为 `Certificate`。  
  
     [!code-csharp[c_SettingSecurityMode#6](../../../samples/snippets/csharp/VS_Snippets_CFX/c_settingsecuritymode/cs/source.cs#6)]
     [!code-vb[c_SettingSecurityMode#6](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_settingsecuritymode/vb/source.vb#6)]  
  
#### 在配置中设置 Mode 和 ClientCredentialType 属性  
  
1.  向配置文件的 [\<绑定\>](../../../docs/framework/configure-apps/file-schema/wcf/bindings.md) 元素添加一个适当的绑定元素。下面的示例添加了一个 [\<wsHttpBinding\>](../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md) 元素。  
  
2.  添加一个 `<binding>` 元素，并将其 `name` 属性设置为适当的值。  
  
3.  添加一个 `<security>` 元素，并将 `mode` 属性设置为 `Message`、`Transport` 或 `TransportWithMessageCredential`。  
  
4.  如果模式设置为 `Transport`，则添加一个 `<transport>` 元素，并将 `clientCredential` 属性设置为适当的值。  
  
     下面的示例将模式设置为 "`Transport"`，并将 `<transport>` 元素的 `clientCredentialType` 属性设置为 "`Windows"`。  
  
    ```  
    <wsHttpBinding>  
    <binding name="TransportSecurity">  
        <security mode="Transport" />  
           <transport clientCredentialType = "Windows" />  
        </security>  
    </binding>  
    </wsHttpBinding >  
    ```  
  
     或者，将 `security mode` 设置为 "`Message"`，后接一个 `<"message">` 元素。本示例将 `clientCredentialType` 设置为 "`Certificate"`。  
  
    ```  
    <wsHttpBinding>  
    <binding name="MessageSecurity">  
        <security mode="Message" />  
           <message clientCredentialType = "Certificate" />  
        </security>  
    </binding>  
    </wsHttpBinding >  
    ```  
  
     使用 <xref:System.ServiceModel.BasicHttpSecurityMode> 值是一种特殊情况，下面将进行说明。  
  
### 使用 TransportWithMessageCredential  
 在将安全模式设置为 `TransportWithMessageCredential` 时，传输会确定实际提供传输级安全的机制。例如，HTTP 协议使用基于 HTTP 的安全套接字层 \(SSL\)（SSL over HTPP，或 HTTPS）。因此，对任何传输安全对象（例如 <xref:System.ServiceModel.HttpTransportSecurity>）的 `ClientCredentialType` 属性进行的设置都将被忽略。换言之，只能设置消息安全对象（对于 `WSHttpBinding` 绑定，则是 <xref:System.ServiceModel.NonDualMessageSecurityOverHttp> 对象）的 `ClientCredentialType`。  
  
 [!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [如何：使用传输安全和消息凭据](../../../docs/framework/wcf/feature-details/how-to-use-transport-security-and-message-credentials.md).  
  
## 请参阅  
 [如何：使用 SSL 证书配置端口](../../../docs/framework/wcf/feature-details/how-to-configure-a-port-with-an-ssl-certificate.md)   
 [如何：使用传输安全和消息凭据](../../../docs/framework/wcf/feature-details/how-to-use-transport-security-and-message-credentials.md)   
 [传输安全](../../../docs/framework/wcf/feature-details/transport-security.md)   
 [消息安全](../../../docs/framework/wcf/feature-details/message-security-in-wcf.md)   
 [安全性概述](../../../docs/framework/wcf/feature-details/security-overview.md)   
 [系统提供的绑定](../../../docs/framework/wcf/system-provided-bindings.md)   
 [\<安全性\>](../../../docs/framework/configure-apps/file-schema/wcf/security-of-wshttpbinding.md)   
 [\<安全性\>](../../../docs/framework/configure-apps/file-schema/wcf/security-of-basichttpbinding.md)   
 [\<安全性\>](../../../docs/framework/configure-apps/file-schema/wcf/security-of-nettcpbinding.md)