---
title: "&lt;peerAuthentication&gt; 元素 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 09a8a9ff-e395-42f6-8ceb-9d44bdc1cbe1
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# &lt;peerAuthentication&gt; 元素
指定用于对等客户端的身份验证选项。  
  
 [!INCLUDE[crabout](../../../../../includes/crabout-md.md)]对等编程的更多信息，请参见[对等网络](../../../../../docs/framework/wcf/feature-details/peer-to-peer-networking.md)。  
  
## 语法  
  
```  
  
<peerAuthentication  
customCertificateValidatorType = "namespace.typeName, [,AssemblyName] [,Version=version number] [,Culture=culture] [,PublicKeyToken=token]"  
certificateValidationMode = "ChainTrust/None/PeerTrust/PeerOrChainTrust/Custom"  
revocationMode="NoCheck/Online/Offline"  
trustedStoreLocation="CurrentUser/LocalMachine"   
/>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|`customCertificateValidatorType`|可选的字符串。  一个用于验证自定义类型的类型和程序集。  当 `certificateValidationMode` 设置为 `Custom` 时，必须设置此属性。|  
|`certifcateValidationMode`|可选的枚举。  指定用来验证凭据的三种模式之一。  如果设置为 `Custom`，则还必须提供 `customCertificateValidator`。  默认值为 `ChainTrust`。|  
|`revocationMode`|可选的枚举。  用于检查吊销证书列表 \(CRL\) 的一种模式。  默认值为 `Online`。|  
|`trustedStoreLocation`|可选的枚举。  两个系统存储位置之一：`LocalMachine` 或 `CurrentUser`。  在向客户端协商服务证书时使用此值。  将根据指定存储位置中的**“受信任人”**存储执行验证。  默认值为 `CurrentUser`。|  
  
## customCertificateValidatorType 属性  
  
|值|描述|  
|-------|--------|  
|String|指定类型名称和程序集以及用于查找类型的其他数据。  至少需要命名空间和类型名称。  可选信息包括：程序集名称、版本号、区域性和公钥标记。|  
  
## certificateValidationMode 属性  
  
|值|描述|  
|-------|--------|  
|枚举|下列值之一：`None`、`PeerTrust`、`ChainTrust`、`PeerOrChainTrust` 和 `Custom`。  默认值为 `ChainTrust`。<br /><br /> 有关详细信息，请参阅[使用证书](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md)。|  
  
## revocationMode 属性  
  
|值|描述|  
|-------|--------|  
|枚举|下列值之一：`NoCheck`、`Online` 和 `Offline`。  默认值为 `Online`。<br /><br /> 有关详细信息，请参阅[使用证书](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md)。|  
  
## trustedStoreLocation 属性  
  
|值|描述|  
|-------|--------|  
|枚举|下列值之一：`LocalMachine` 或 `CurrentUser`。  默认值为 `CurrentUser`。  如果客户端应用程序在系统帐户下运行，则证书通常位于 `LocalMachine`。  如果客户端应用程序在用户帐户下运行，则证书通常位于 `CurrentUser`。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<peer\>](../../../../../docs/framework/configure-apps/file-schema/wcf/peer-of-clientcredentials-element.md)|指定一个用于向对等服务证明客户端身份的凭据。|  
  
## 备注  
 `<authentication>` 元素与 <xref:System.ServiceModel.Security.X509PeerCertificateAuthentication> 类相对应。  此元素指定一个验证程序，在网格中执行邻居对等身份验证的过程中将调用该验证程序。  当新对等方尝试建立邻居连接时，它会将自己的凭据传递到响应的对等方。  将调用响应方的验证程序来验证远程方的凭据。  每当在网格中建立对等连接时，对等方将会相互进行身份验证，这意味着会同时在两方调用验证程序。  
  
## 示例  
 下面的代码将证书验证模式设置为 `PeerOrChainTrust`。  
  
```  
<behaviors>  
 <endpointBehaviors>  
  <behavior name="MyEndpointBehavior">  
   <clientCredentials>  
    <peer>  
     <certificate findValue="www.contoso.com"   
                   storeLocation="LocalMachine"  
                   x509FindType="FindByIssuerName" />  
     <peerAuthentication   
          certificateValidationMode="PeerOrChainTrust" />  
     <messageSenderAuthentication certificateValidationMode="None" />  
    </peer>  
   </clientCredentials>  
  </behavior>  
</endpointBehaviors>  
```  
  
## 请参阅  
 <xref:System.ServiceModel.Configuration.PeerCredentialElement>   
 <xref:System.ServiceModel.Security.X509PeerCertificateAuthentication>   
 <xref:System.ServiceModel.Security.PeerCredential.PeerAuthentication%2A>   
 <xref:System.ServiceModel.Configuration.PeerCredentialElement.PeerAuthentication%2A>   
 <xref:System.ServiceModel.Configuration.X509PeerCertificateAuthenticationElement>   
 [使用证书](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md)   
 [对等网络](../../../../../docs/framework/wcf/feature-details/peer-to-peer-networking.md)   
 [Peer Channel Message Authentication](http://msdn.microsoft.com/zh-cn/80e73386-514e-4c30-9e4a-b9ca8c173a95)   
 [Peer Channel Custom Authentication](http://msdn.microsoft.com/zh-cn/4aa8a82e-41a8-48e2-8621-7e1cbabdca7c)   
 [保护对等通道应用程序](../../../../../docs/framework/wcf/feature-details/securing-peer-channel-applications.md)