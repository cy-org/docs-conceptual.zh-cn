---
title: "如何：使用 SecurityBindingElement 创建自定义绑定 | Microsoft Docs"
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
  - "创建自定义绑定的安全 [WCF]"
ms.assetid: 203a9f9e-3a73-427c-87aa-721c56265b29
caps.latest.revision: 19
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 19
---
# 如何：使用 SecurityBindingElement 创建自定义绑定
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 包括多个系统提供的绑定，虽然这些绑定可进行配置，但在配置 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 支持的所有安全选项时仍显得不够灵活。 本主题演示如何直接从各个绑定元素创建自定义绑定，并着重说明创建这样的绑定时可以指定的一些安全设置。 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]创建自定义绑定，请参阅[扩展绑定](../../../../docs/framework/wcf/extending/extending-bindings.md)。  
  
> [!WARNING]
>  <xref:System.ServiceModel.Channels.SecurityBindingElement>不支持<xref:System.ServiceModel.Channels.IDuplexSessionChannel>通道形状，它是 tcp 使用的默认通道形状传输时<xref:System.ServiceModel.TransferMode>设置为<xref:System.ServiceModel.TransferMode.Buffered>。 必须设置<xref:System.ServiceModel.TransferMode>到<xref:System.ServiceModel.TransferMode.Streamed>为了使用<xref:System.ServiceModel.Channels.SecurityBindingElement>在此方案中。  
  
## <a name="creating-a-custom-binding"></a>创建自定义绑定  
 在[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]所有绑定都组成*绑定元素*。 每个绑定元素派生自<xref:System.ServiceModel.Channels.BindingElement>类。 对于系统提供的标准绑定，已为你创建和配置绑定元素，但你仍可以自定义某些属性设置。  
  
 与此相反，若要创建自定义绑定，绑定元素创建和配置和<xref:System.ServiceModel.Channels.CustomBinding>从绑定元素创建的。  
  
 若要执行此操作，您将各个绑定元素添加到集合的实例所表示<xref:System.ServiceModel.Channels.BindingElementCollection>类，并将`Elements`属性`CustomBinding`等于该对象。 必须按以下顺序添加绑定元素：事务流、可靠会话、安全、复合双工、单向、流安全、消息编码和传输。 请注意，并不是每个绑定中都需要所列的所有绑定元素。  
  
## <a name="securitybindingelement"></a>SecurityBindingElement  
 三个绑定元素与消息级安全性，它们都派生自<xref:System.ServiceModel.Channels.SecurityBindingElement>类。 三种<xref:System.ServiceModel.Channels.TransportSecurityBindingElement>， <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>，和<xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement>。 <xref:System.ServiceModel.Channels.TransportSecurityBindingElement>用于提供混合的模式安全。 当消息层提供安全时，使用其他两个元素。  
  
 在提供传输级安全时，将使用其他类：  
  
-   <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>  
  
-   <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement>  
  
-   <xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement>  
  
## <a name="required-binding-elements"></a>必需的绑定元素  
 有大量的可能绑定元素可以组合为绑定。 并非所有这些组合都是有效的。 本节介绍安全绑定中必须存在的元素。  
  
 有效的安全绑定取决于多种因素，其中包括：  
  
-   安全模式。  
  
-   传输协议。  
  
-   协定中指定的消息交换模式 (MEP)。  
  
 下表显示上述因素各种组合的有效绑定元素组合配置。 请注意，这些是最低要求。 您可以向绑定添加更多绑定元素，如消息编码绑定元素、事务绑定元素和其他绑定元素。  
  
|安全模式|传输|协定消息交换模式|协定消息交换模式|协定消息交换模式|  
|-------------------|---------------|---------------------------------------|---------------------------------------|---------------------------------------|  
|||`Datagram`|`Request Reply`|`Duplex`|  
|传输|Https||||  
|||OneWayBindingElement|||  
|||HttpsTransportBindingElement|HttpsTransportBindingElement||  
||TCP||||  
|||OneWayBindingElement|||  
|||SSL 或 Windows StreamSecurityBindingElement|SSL 或 Windows StreamSecurityBindingElement|SSL 或 Windows StreamSecurityBindingElement|  
|||TcpTransportBindingElement|TcpTransportBindingElement|TcpTransportBindingElement|  
|消息|Http|SymmetricSecurityBindingElement|SymmetricSecurityBindingElement|SymmetricSecurityBindingElement（身份验证模式 = SecureConversation）|  
|||||CompositeDuplexBindingElement|  
|||OneWayBindingElement||OneWayBindingElement|  
|||HttpTransportBindingElement|HttpTransportBindingElement|HttpTransportBindingElement|  
||Tcp|SecurityBindingElement|SecurityBindingElement|SymmetricSecurityBindingElement（身份验证模式 = SecureConversation）|  
|||TcpTransportBindingElement|TcpTransportBindingElement|TcpTransportBindingElement|  
|混合（带有消息凭据的传输）|Https|TransportSecurityBindingElement|TransportSecurityBindingElement||  
|||OneWayBindingElement|||  
|||HttpsTransportBindingElement|HttpsTransportBindingElement||  
||TCP|TransportSecurityBindingElement|SymmetricSecurityBindingElement（身份验证模式 = SecureConversation）|SymmetricSecurityBindingElement（身份验证模式 = SecureConversation）|  
|||OneWayBindingElement|||  
|||SSL 或 Windows StreamSecurityBindingElement|SSL 或 Windows StreamSecurityBindingElement|SSL 或 Windows StreamSecurityBindingElement|  
|||TcpTransportBindingElement|TcpTransportBindingElement|TcpTransportBindingElement|  
  
 请注意，SecurityBindingElements 有许多可配置的设置。 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][SecurityBindingElement 身份验证模式](../../../../docs/framework/wcf/feature-details/securitybindingelement-authentication-modes.md)。  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][安全对话和安全会话](../../../../docs/framework/wcf/feature-details/secure-conversations-and-secure-sessions.md)。  
  
## <a name="procedures"></a>过程  
  
#### <a name="to-create-a-custom-binding-that-uses-a-symmetricsecuritybindingelement"></a>创建使用 SymmetricSecurityBindingElement 的自定义绑定。  
  
1.  创建的实例<xref:System.ServiceModel.Channels.BindingElementCollection>类同名`outputBec`。  
  
2.  调用静态方法`M:System.ServiceModel.Channels.SecurityBindingElement.CreateSspiNegotiationBindingElement(true)`，它返回的实例<xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>类。  
  
3.  添加<xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>到集合 (`outputBec`) 通过调用`Add`方法<xref:System.Collections.ObjectModel.Collection%601>的<xref:System.ServiceModel.Channels.BindingElement>类。  
  
4.  创建的实例<xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>类并将其添加到集合 (`outputBec`)。 这将指定该绑定所使用的编码。  
  
5.  创建<xref:System.ServiceModel.Channels.HttpTransportBindingElement>并将其添加到集合 (`outputBec`)。 这将指定该绑定使用 HTTP 传输。  
  
6.  通过创建的实例创建新的自定义绑定<xref:System.ServiceModel.Channels.CustomBinding>类并将集合传递`outputBec`给构造函数。  
  
7.  生成的自定义绑定共享许多相同的特征与标准<xref:System.ServiceModel.WSHttpBinding>。 它指定消息级别的安全性和 Windows 凭据，但禁用安全会话，要求在带外指定服务凭据且不对签名进行加密。 上一次可以仅通过设置控制<xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement.MessageProtectionOrder%2A>属性，如步骤 4 中所示。 其他两条可以使用标准绑定上的设置进行控制。  
  
## <a name="example"></a>示例  
  
### <a name="description"></a>描述  
 下面的示例提供一个完整的函数来创建使用的自定义绑定<xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>。  
  
### <a name="code"></a>代码  
 [!code-csharp[c_CustomBinding#20](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_custombinding/cs/c_custombinding.cs#20)]
 [!code-vb[c_CustomBinding#20](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_custombinding/vb/source.vb#20)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.ServiceModel.Channels.SecurityBindingElement>   
 <xref:System.ServiceModel.Channels.TransportSecurityBindingElement>   
 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 [扩展绑定](../../../../docs/framework/wcf/extending/extending-bindings.md)   
 [系统提供的绑定](../../../../docs/framework/wcf/system-provided-bindings.md)