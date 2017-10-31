---
title: "如何：为安全会话创建安全上下文令牌 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 640676b6-c75a-4ff7-aea4-b1a1524d71b2
caps.latest.revision: 14
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 14
---
# 如何：为安全会话创建安全上下文令牌
通过在安全会话中使用有状态安全上下文令牌 \(SCT\)，可以使该会话避免因为重新使用服务而受到影响。例如，如果在安全会话中使用了无状态 SCT 并且 Internet 信息服务 \(IIS\) 被重置，则与该服务相关联的会话数据将丢失。这些会话数据包括一个 SCT 令牌缓存。因此，当客户端下一次向该服务发送无状态 SCT 时，将返回错误，这是因为无法检索到与该 SCT 相关联的密钥。但是，如果使用有状态 SCT，则与该 SCT 相关联的密钥将包含在该 SCT 中。由于密钥包含在 SCT 中并因而包含在消息中，因此安全会话不会因为重新使用服务而受到影响。默认情况下，[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 在安全会话中使用无状态 SCT。本主题详细介绍如何在安全会话中使用有状态 SCT。  
  
> [!NOTE]
>  如果安全会话涉及到派生自 <xref:System.ServiceModel.Channels.IDuplexChannel> 的协定，则无法在该安全会话中使用有状态 SCT。  
  
> [!NOTE]
>  对于在安全会话中使用有状态 SCT 的应用程序，服务的线程标识必须是具有关联用户配置文件的用户帐户。如果服务在不具有用户配置文件的帐户下运行（如 `Local Service`），则可能引发异常。  
  
> [!NOTE]
>  当需要在 Windows XP 上进行模拟时，请不要在安全会话中使用有状态 SCT。如果在模拟时使用有状态 SCT，则会引发 <xref:System.InvalidOperationException>。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][不支持的方案](../../../../docs/framework/wcf/feature-details/unsupported-scenarios.md).  
  
### 在安全会话中使用有状态 SCT  
  
-   创建一个自定义绑定，该绑定指定由使用有状态 SCT 的安全会话来保护 SOAP 消息。  
  
    1.  通过向服务的配置文件中添加一个 [\<customBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)，定义一个自定义绑定。  
  
        ```  
        <customBinding>  
        ```  
  
    2.  将一个 [\<绑定\>](../../../../docs/framework/misc/binding.md) 子元素添加到 [\<customBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)中。  
  
         通过在配置文件中将 `name` 属性设置为一个唯一的名称，指定一个绑定名称。  
  
        ```  
        <binding name="StatefulSCTSecureSession">  
        ```  
  
    3.  通过将一个 [\<安全性\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md) 子元素添加到 [\<customBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)，指定发送到此服务以及从此服务发送出去的消息的身份验证模式。  
  
         通过将 `authenticationMode` 属性设置为 `SecureConversation`，指定使用安全会话。通过将 `requireSecurityContextCancellation` 属性设置为 `false`，指定使用有状态 SCT。  
  
        ```  
        <security authenticationMode="SecureConversation"  
                  requireSecurityContextCancellation="false">  
        ```  
  
    4.  通过将一个 [\<secureConversationBootstrap\>](../../../../docs/framework/configure-apps/file-schema/wcf/secureconversationbootstrap.md)子元素添加到 [\<安全性\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)，指定在建立安全会话时如何对客户端进行身份验证。  
  
         通过设置 `authenticationMode` 属性，指定如何对客户端进行身份验证。  
  
        ```  
        <secureConversationBootstrap authenticationMode="UserNameForCertificate" />  
        ```  
  
    5.  指定消息编码，方法是添加一个编码元素，如 [\<textMessageEncoding\>](../../../../docs/framework/configure-apps/file-schema/wcf/textmessageencoding.md)。  
  
        ```  
        <textMessageEncoding />  
        ```  
  
    6.  指定传输，方法是添加一个传输元素，如 [\<httpTransport\>](../../../../docs/framework/configure-apps/file-schema/wcf/httptransport.md)。  
  
        ```  
        <httpTransport />  
        ```  
  
     下面的代码示例使用配置来指定一个自定义绑定，消息可以将该绑定与安全会话中的有状态 SCT 结合使用。  
  
    ```  
    <customBinding>  
      <binding name="StatefulSCTSecureSession">  
        <security authenticationMode="SecureConversation"  
                  requireSecurityContextCancellation="false">  
          <secureConversationBootstrap authenticationMode="UserNameForCertificate" />  
        </security>  
        <textMessageEncoding />  
        <httpTransport />  
      </binding>  
    </customBinding>  
    ```  
  
## 示例  
 下面的代码示例创建一个自定义绑定，该绑定使用 <xref:System.ServiceModel.Configuration.AuthenticationMode> 身份验证模式启动安全会话。  
  
 [!code-csharp[c_CreateStatefulSCT#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_createstatefulsct/cs/secureservice.cs#2)]
 [!code-vb[c_CreateStatefulSCT#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_createstatefulsct/vb/secureservice.vb#2)]  
  
 在将 Windows 身份验证与有状态 SCT 结合起来使用时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 不使用实际调用方的标识来填充 <xref:System.ServiceModel.ServiceSecurityContext.WindowsIdentity%2A> 属性，而是将该属性设置为匿名。由于 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 安全必须为来自传入 SCT 的每个请求重新创建服务安全上下文的内容，因此服务器不会跟踪内存中的安全会话。因为不可能将 <xref:System.Security.Principal.WindowsIdentity> 实例序列化为 SCT，所以 <xref:System.ServiceModel.ServiceSecurityContext.WindowsIdentity%2A> 属性返回一个匿名标识。  
  
 下面的配置演示这一行为。  
  
```  
<customBinding>  
  <binding name="Cancellation">  
       <textMessageEncoding />  
        <security   
            requireSecurityContextCancellation="false">  
              <secureConversationBootstrap />  
      </security>  
    <httpTransport />  
  </binding>  
</customBinding>  
  
```  
  
## 请参阅  
 [\<customBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)