---
title: "如何：设置签名确认 | Microsoft Docs"
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
  - "签名确认"
  - "WCF, 安全"
ms.assetid: 2424c137-c7c2-4aa9-8d5d-a066e12fefda
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# 如何：设置签名确认
签名确认是消息发起方使用的一种机制，用于确保接收到的答复是为响应发送方的原始消息而生成的。WS\-Security 1.1 规范中对签名确认进行了定义。如果终结点支持 WS\-Security 1.0，则不能使用签名确认。  
  
 下面的过程指定如何使用 <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement> 来启用签名确认。可以对 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> 使用相同的过程。该过程是以[如何：使用 SecurityBindingElement 创建自定义绑定](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)中的基本步骤为基础而建立的。  
  
### 在代码中启用签名确认  
  
1.  创建 <xref:System.ServiceModel.Channels.BindingElementCollection> 类的实例。  
  
2.  创建 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> 类的实例。  
  
3.  将 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement.RequireSignatureConfirmation%2A> 设置为 `true`。  
  
4.  将安全元素添加到绑定集合中。  
  
5.  按照[如何：使用 SecurityBindingElement 创建自定义绑定](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)中的说明创建自定义绑定。  
  
### 在配置中启用签名确认  
  
1.  将 `<customBinding>` 元素添加到配置文件的 `<bindings>` 节。  
  
2.  添加一个 `<binding>` 元素，并将 name 属性设置为适当的值。  
  
3.  添加一个适当的编码元素。下面的示例添加了一个 `<TextMessageEncoding>` 元素。  
  
4.  添加一个 `<security>` 子元素并将 `requireSignatureConfirmation` 属性设置为 `true`。  
  
5.  可选。若要在启动过程中启用签名确认，请添加一个 [\<secureConversationBootstrap\>](../../../../docs/framework/configure-apps/file-schema/wcf/secureconversationbootstrap.md) 子元素并将 `equireSignatureConfirmation` 属性设置为 `true`。  
  
6.  添加一个适当的传输元素。下面的示例添加一个 [\<httpTransport\>](../../../../docs/framework/configure-apps/file-schema/wcf/httptransport.md)：  
  
    ```  
    <bindings>  
      <customBinding>  
        <binding name="SignatureConfirmationBinding">  
          <security requireSignatureConfirmation="true">  
            <secureConversationBootstrap requireSignatureConfirmation="true" />  
              </security>  
           <textMessageEncoding />  
             <httpTransport />  
        </binding>  
      </customBinding>  
    </bindings>  
    ```  
  
## 示例  
 下面的代码创建 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> 的实例并将 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement.RequireSignatureConfirmation%2A> 属性设置为 `true`。请注意，此示例不使用上一示例中所示的 `<secureConversationBootstrap>` 元素。此示例演示了使用 Windows（Kerberos 协议）令牌时的签名确认。在本例中，在来自服务的所有响应中均返回客户端的签名，并且该签名由客户端进行确认。  
  
 [!code-csharp[c_SignatureConfirmation#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_signatureconfirmation/cs/source.cs#1)]
 [!code-vb[c_SignatureConfirmation#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_signatureconfirmation/vb/source.vb#1)]  
  
## 请参阅  
 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>   
 <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement>   
 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateMutualCertificateBindingElement%2A>   
 [如何：使用 SecurityBindingElement 创建自定义绑定](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)   
 [如何：为指定的身份验证模式创建 SecurityBindingElement](../../../../docs/framework/wcf/feature-details/how-to-create-a-securitybindingelement-for-a-specified-authentication-mode.md)