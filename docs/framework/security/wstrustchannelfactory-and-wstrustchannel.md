---
title: "WSTrustChannelFactory 和 WSTrustChannel"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 96cec467-e963-4132-b18b-7d0b3a2e979f
caps.latest.revision: 9
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: e400d68924f1ed57ea1e71892e52f5aae2f5eebc
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="wstrustchannelfactory-and-wstrustchannel"></a>WSTrustChannelFactory 和 WSTrustChannel
如果已熟悉 Windows Communication Foundation (WCF)，便知道 WCF 客户端已可感知联合。 通过使用 <xref:System.ServiceModel.WSFederationHttpBinding> 或相似的自定义绑定配置 WCF 客户端，便可对服务启用联合身份验证。  
  
 WCF 获取由后台安全令牌服务 (STS) 颁发的令牌，并使用此令牌对服务进行身份验证。 此方法的主要限制在于无法查看客户端与服务器之间的通信。 WCF 基于在绑定上颁发的令牌参数，自动生成 STS 的请求安全令牌 (RST)。 这意味着客户端不能改变每个请求的 RST 参数、无法通过检查请求安全令牌响应 (RSTR) 获取显示声明等信息，也不能缓存令牌供将来使用。  
  
 目前，WCF 客户端适用于基本联合方案。 然而，Windows Identity Foundation (WIF) 支持的其中一个主要方案需要对 RST 拥有 WCF 不轻易允许的级别的控制。 因此，WIF 添加了针对与 STS 的通信提供更强控制的功能。  
  
 WIF 支持以下联合方案：  
  
-   在没有任何 WIF 依赖项的情况下使用 WCF 客户端对联合服务进行身份验证  
  
-   在 WCF 客户端上启用 WIF，将 ActAs 或 OnBehalfOf 元素插入 STS 的 RST 中  
  
-   仅使用 WIF 从 STS 获取令牌，然后启用 WCF 客户端，以便使用此令牌进行身份验证。 有关详细信息，请参阅 [ClaimsAwareWebService](http://go.microsoft.com/fwlink/?LinkID=248406) 示例。  
  
 第一个方案很容易理解：现有的 WCF 客户端将继续适用于 WIF 信赖方和 STS。 本主题讨论剩余的两个方案。  
  
## <a name="enhancing-an-existing-wcf-client-with-actas--onbehalfof"></a>通过 ActAs/OnBehalfOf 增强现有的 WCF 客户端  
 在典型的标识委派方案中，客户端调用中间层服务，该服务随后调用后端服务。 中间层服务充当客户端或代表客户端执行操作。  
  
> [!TIP]
>  ActAs 和 OnBehalfOf 有何区别？  
>   
>  从 WS-Trust 协议的角度来看：  
>   
>  1.  ActAs RST 元素指示请求者想要的令牌包含有关两个不同实体的声明，这两个实体分别是请求者和由 ActAs 元素中的令牌表示的外部实体。  
> 2.  OnBehalfOf RST 元素指示请求者想要的令牌包含仅与一个实体有关的声明，这个实体是由 OnBehalfOf 元素中的令牌表示的外部实体。  
>   
>  ActAs 功能通常用于需要复合委派的方案，其中所颁发令牌的最终接收方可以检查整个委派链，可以查看客户端和所有中介。 这样，它可以基于整个标识委派链执行访问控制、审核和其他相关活动。 ActAs 功能通常用于在多层系统中进行身份验证以及在层之间传递有关标识的信息（无需在应用程序/业务逻辑层传递此信息）。  
>   
>  OnBehalfOf 功能用于仅原始客户端的标识重要并且与 Windows 中可用的标识模拟功能同样高效的情况。 使用 OnBehalfOf 时，所颁发令牌的最终接收方只能查看有关原始客户端的声明，未保留有关中介的信息。 使用 OnBehalfOf 功能的常见模式是代理模式，在此模式中，客户端无法直接访问 STS，但可以通过代理网关通信。 代理网关对调用方进行身份验证并将有关调用方的信息放入 RST 消息的 OnBehalfOf 元素中，然后将该消息发送到真正的 STS 中以供处理。 生成的令牌仅包含与代理的客户端有关的声明，因此此代理对所颁发令牌的接收方来说完全透明。请注意，WIF 不支持 \<wsse:SecurityTokenReference> 或 \<wsa:EndpointReferences> 作为 \<wst:OnBehalfOf> 的子级。 WS-Trust 规范允许三种标识原始请求者（代理代表其执行操作）的方法。 这些是：  
>   
>  -   安全令牌引用。 对令牌的引用（消息中的引用，或者可能是带外检索的引用）。  
> -   终结点引用。 作为查找数据的密钥使用（仍为带外）。  
> -   安全令牌。 直接标识原始请求方。  
>   
>  WIF 仅支持安全令牌（加密或未加密）作为 \<wst:OnBehalfOf> 的直接子元素。  
  
 使用 RST 中的 ActAs 和 OnBehalfOf 令牌元素将此信息传达给 WS-Trust 颁发者。  
  
 WCF 在允许将任意 XML 元素添加到 RST 的绑定上公开扩展点。 然而，因为扩展点与该绑定关联，所以每次调用都需要改变 RST 内容的方案必须在每次调用时重新创建客户端，这将降低性能。 WIF 使用 `ChannelFactory` 类上的扩展方法，因此开发人员可以将带外获取的任何令牌附加到 RST。 下方的代码示例演示如何获取表示客户端（例如 X.509、用户名或安全断言标记语言 (SAML) 令牌）的令牌并将它附加到发送给颁发者的 RST。  
  
```  
IHelloService serviceChannel = channelFactory.CreateChannelActingAs<IHelloService>( clientSamlToken );  
serviceChannel.Hello("Hi!");  
```  
  
 WIF 提供如下优点：  
  
-   可以按通道修改 RST；因此，中间层服务不需要为每个客户端重新创建通道工厂，从而提高性能。  
  
-   这适用于现有的 WCF 客户端，可能为要启用标识委派语义的现有 WCF 中间层服务提供简单的升级路径。  
  
 然而，仍看不到客户端与 STS 之间的通信。 我们将在第三个方案中查看此问题。  
  
## <a name="communicating-directly-with-an-issuer-and-using-the-issued-token-to-authenticate"></a>与颁发者直接通信并使用颁发的令牌进行身份验证  
 对于某些高级方案，增强 WCF 客户端是不够的。 仅使用 WCF 的开发人员通常使用 Message In/Message Out 协定，手动处理颁发者响应的客户端分析。  
  
 WIF 引入了 <xref:System.ServiceModel.Security.WSTrustChannelFactory> 和 <xref:System.ServiceModel.Security.WSTrustChannel> 类，使客户端直接与 WS-Trust 颁发者通信。 通过 <xref:System.ServiceModel.Security.WSTrustChannelFactory> 和 <xref:System.ServiceModel.Security.WSTrustChannel> 类，强类型 RST 和 RSTR 对象可在客户端和颁发者之间流动，如以下代码示例所示。  
  
```  
WSTrustChannelFactory trustChannelFactory = new WSTrustChannelFactory( stsBinding, stsAddress );  
WSTrustChannel channel = (WSTrustChannel) trustChannelFactory.CreateChannel();  
RequestSecurityToken rst = new RequestSecurityToken(RequestTypes.Issue);  
rst.AppliesTo = new EndpointAddress(serviceAddress);  
RequestSecurityTokenResponse rstr = null;  
SecurityToken token = channel.Issue(rst, out rstr);  
```  
  
 请注意，<xref:System.ServiceModel.Security.WSTrustChannel.Issue%2A> 方法上的 `out` 参数允许访问 RSTR 进行客户端检查。  
  
 至此，我们仅了解到如何获取令牌。 从 <xref:System.ServiceModel.Security.WSTrustChannel> 对象返回的令牌是 `GenericXmlSecurityToken`，其中包含对信赖方进行身份验证所需的所有信息。 下方的代码示例演示如何使用此令牌。  
  
```  
IHelloService serviceChannel = channelFactory.CreateChannelWithIssuedToken<IHelloService>( token ); serviceChannel.Hello("Hi!");  
```  
  
 `ChannelFactory` 对象上的 <xref:System.ServiceModel.ChannelFactory%601.CreateChannelWithIssuedToken%2A> 扩展方法会让 WIF 知道你已在带外获取令牌，且它应该停止对颁发者的常规 WCF 调用，而改用你所获取的令牌对信赖方进行身份验证。 这具有如下优点：  
  
-   可以完全控制令牌颁发进程。  
  
-   通过直接在传出 RST 上设置这些属性来支持 ActAs/OnBehalfOf 方案。  
  
-   可以基于 RSTR 的内容做出动态客户端信任决策。  
  
-   可以缓存并重新使用从 <xref:System.ServiceModel.Security.WSTrustChannel.Issue%2A> 方法返回的令牌。  
  
-   可根据 WCF 最佳做法通过 <xref:System.ServiceModel.Security.WSTrustChannelFactory> 和 <xref:System.ServiceModel.Security.WSTrustChannel> 控制通道缓存、错误和恢复语义。  
  
## <a name="see-also"></a>另请参阅  
 [WIF 功能](../../../docs/framework/security/wif-features.md)

