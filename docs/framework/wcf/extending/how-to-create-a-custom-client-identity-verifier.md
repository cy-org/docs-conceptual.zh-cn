---
title: "如何：创建自定义客户端标识验证工具 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f2d34e43-fa8b-46d2-91cf-d2960e13e16b
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# 如何：创建自定义客户端标识验证工具
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 的标识功能使客户端能够预先指定服务所需的标识。  无论服务器何时向客户端验证其自身身份，都将检查该标识是否为所需的标识。  （有关标识的解释及其工作原理，请参见[服务标识和身份验证](../../../../docs/framework/wcf/feature-details/service-identity-and-authentication.md)。）  
  
 如果需要，可使用自定义标识验证工具自定义该验证。  例如，您可以执行其他服务标识验证检查。  在本示例中，自定义标识验证工具将检查从服务器返回的 X.509 证书中的其他声明。  有关示例应用程序，请参见[服务标识示例](../../../../docs/framework/wcf/samples/service-identity-sample.md)。  
  
### 扩展 EndpointIdentity 类  
  
1.  定义一个从 <xref:System.ServiceModel.EndpointIdentity> 类派生的新类。  本示例将此扩展命名为 `OrgEndpointIdentity`。  
  
2.  添加私有成员和属性，扩展的 <xref:System.ServiceModel.Security.IdentityVerifier> 类将使用这些属性根据从服务返回的安全令牌中的声明执行标识检查。  本示例定义一个属性：`OrganizationClaim` 属性。  
  
     [!code-csharp[c_HowToSetCustomClientIdentity#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#6)]
     [!code-vb[c_HowToSetCustomClientIdentity#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#6)]  
  
### 扩展 IdentityVerifier 类  
  
1.  定义一个从 <xref:System.ServiceModel.Security.IdentityVerifier> 派生的新类。  本示例将此扩展命名为 `CustomIdentityVerifier`。  
  
     [!code-csharp[c_HowToSetCustomClientIdentity#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#7)]
     [!code-vb[c_HowToSetCustomClientIdentity#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#7)]  
  
2.  重写 <xref:System.ServiceModel.Security.IdentityVerifier.CheckAccess%2A> 方法。  该方法确定标识检查是成功还是失败。  
  
3.  `CheckAccess` 方法有两个参数。  第一个参数是 <xref:System.ServiceModel.EndpointIdentity> 类的一个实例。  第二个参数是 <xref:System.IdentityModel.Policy.AuthorizationContext> 类的一个实例。  
  
     在方法的实现过程中，检查 <xref:System.IdentityModel.Policy.AuthorizationContext> 类的 <xref:System.IdentityModel.Policy.AuthorizationContext.ClaimSets%2A> 属性返回的声明集合，并根据需要执行身份验证检查。  本示例首先查找类型为“可分辨名称”的任何声明，然后将此名称与 <xref:System.ServiceModel.EndpointIdentity> 扩展的名称 \(`OrgEndpointIdentity`\) 进行比较。  
  
     [!code-csharp[c_HowToSetCustomClientIdentity#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#1)]
     [!code-vb[c_HowToSetCustomClientIdentity#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#1)]  
  
### 实现 TryGetIdentity 方法  
  
1.  实现 <xref:System.ServiceModel.Security.IdentityVerifier.TryGetIdentity%2A> 方法，该方法确定客户端是否可返回 <xref:System.ServiceModel.EndpointIdentity> 类的实例。  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 基础结构首先调用 `TryGetIdentity` 方法的实现来检索消息中的服务标识。  然后，该基础结构使用返回的 `EndpointIdentity` 和 <xref:System.IdentityModel.Policy.AuthorizationContext> 调用 `CheckAccess` 实现。  
  
2.  在 `TryGetIdentity` 方法中，添加以下代码：  
  
     [!code-csharp[c_HowToSetCustomClientIdentity#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#2)]
     [!code-vb[c_HowToSetCustomClientIdentity#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#2)]  
  
### 实现自定义绑定并设置自定义标识验证工具  
  
1.  创建一个返回 <xref:System.ServiceModel.Channels.Binding> 对象的方法。  本示例首先创建 <xref:System.ServiceModel.WSHttpBinding> 类的一个实例，然后将其安全模式设置为 <xref:System.ServiceModel.SecurityMode>，并且将其 <xref:System.ServiceModel.MessageSecurityOverHttp.ClientCredentialType%2A> 设置为 <xref:System.ServiceModel.MessageCredentialType>。  
  
2.  使用 <xref:System.ServiceModel.WSHttpBinding.CreateBindingElements%2A> 方法创建一个 <xref:System.ServiceModel.Channels.BindingElementCollection>。  
  
3.  从集合返回 <xref:System.ServiceModel.Channels.SecurityBindingElement>，并将其强制转换为一个 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> 变量。  
  
4.  将 <xref:System.ServiceModel.Channels.LocalClientSecuritySettings> 类的 <xref:System.ServiceModel.Channels.LocalClientSecuritySettings.IdentityVerifier%2A> 属性设置为先前创建的 `CustomIdentityVerifier` 类的一个新实例。  
  
     [!code-csharp[c_HowToSetCustomClientIdentity#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#3)]
     [!code-vb[c_HowToSetCustomClientIdentity#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#3)]  
  
5.  使用返回的自定义绑定创建客户端和类的一个实例。  然后，客户端可执行服务的自定义标识验证检查，如以下代码中所示。  
  
     [!code-csharp[c_HowToSetCustomClientIdentity#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#4)]
     [!code-vb[c_HowToSetCustomClientIdentity#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#4)]  
  
## 示例  
 下面的示例演示 <xref:System.ServiceModel.Security.IdentityVerifier> 类的完整实现。  
  
 [!code-csharp[c_HowToSetCustomClientIdentity#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#5)]
 [!code-vb[c_HowToSetCustomClientIdentity#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#5)]  
  
## 示例  
 下面的示例演示 <xref:System.ServiceModel.EndpointIdentity> 类的完整实现。  
  
 [!code-csharp[c_HowToSetCustomClientIdentity#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howtosetcustomclientidentity/cs/source.cs#6)]
 [!code-vb[c_HowToSetCustomClientIdentity#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howtosetcustomclientidentity/vb/source.vb#6)]  
  
## 请参阅  
 <xref:System.ServiceModel.ServiceAuthorizationManager>   
 <xref:System.ServiceModel.EndpointIdentity>   
 <xref:System.ServiceModel.Security.IdentityVerifier>   
 [服务标识示例](../../../../docs/framework/wcf/samples/service-identity-sample.md)   
 [授权策略](../../../../docs/framework/wcf/samples/authorization-policy.md)   
 [授权策略](../../../../docs/framework/wcf/samples/authorization-policy.md)