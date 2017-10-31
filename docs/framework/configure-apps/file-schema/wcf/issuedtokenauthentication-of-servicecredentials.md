---
title: "&lt;serviceCredentials&gt; 的 &lt;issuedTokenAuthentication&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5c2e288f-f603-4d13-839a-0fd6d1981bec
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# &lt;serviceCredentials&gt; 的 &lt;issuedTokenAuthentication&gt;
指定作为服务凭据颁发的自定义令牌。  
  
## 语法  
  
```  
  
<issuedTokenAuthentication   
   allowUntrustedRsaIssuers="Boolean"  
   audienceUriMode="Always/BearerKeyOnly/Never"  
      customCertificateValidatorType="namespace.typeName, [,AssemblyName] [,Version=version number] [,Culture=culture] [,PublicKeyToken=token]"  
certificateValidationMode="ChainTrust/None/PeerTrust/PeerOrChainTrust/Custom"  
   revocationMode="NoCheck/Online/Offline"  
   samlSerializer="String"  
    trustedStoreLocation="CurrentUser/LocalMachine">  
      <allowedAudienceUris>  
      <add allowedAudienceUri="String"/>  
      </allowedAudienceUris>  
      <knownCertificates>   
         <add findValue="String"  
                 storeLocation="CurrentUser/LocalMachine"  
                storeName=" CurrentUser/LocalMachine"  
                x509FindType="FindByThumbprint/FindBySubjectName/FindBySubjectDistinguishedName/FindByIssuerName/FindByIssuerDistinguishedName/FindBySerialNumber/FindByTimeValid/FindByTimeNotYetValid/FindBySerialNumber/FindByTimeExpired/FindByTemplateName/FindByApplicationPolicy/FindByCertificatePolicy/FindByExtension/FindByKeyUsage/FindBySubjectKeyIdentifier"/>  
      </knownCertificates>  
</issuedTokenAuthentication>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|`allowedAudienceUris`|获取 <xref:System.IdentityModel.Tokens.SamlSecurityToken> 安全令牌的目标 URI 集，只有在使用这些目标 URI 时，<xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator> 实例才会将该令牌视为有效令牌。  有关使用此属性的更多信息，请参见 <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator.AllowedAudienceUris%2A>。|  
|`allowUntrustedRsaIssuers`|一个布尔值，指定是否允许不可信的 RSA 证书颁发者。<br /><br /> 证书由证书颁发机构 \(CA\) 签名，以验证真实性。  不可信的颁发者是指未被指定为可信的证书签名者的 CA。|  
|`audienceUriMode`|获取一个值，该值指定是否应验证 <xref:System.IdentityModel.Tokens.SamlSecurityToken> 安全令牌的 <xref:System.IdentityModel.Tokens.SamlAudienceRestrictionCondition>。  此值的类型为 <xref:System.IdentityModel.Selectors.AudienceUriMode>。  有关使用此属性的更多信息，请参见 <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator.AudienceUriMode%2A>。|  
|`certificateValidationMode`|设置证书验证模式。  <xref:System.ServiceModel.Security.X509CertificateValidationMode> 的有效值之一。  如果设置为 `Custom`，则还必须提供 `customCertificateValidator`。  默认值为 `ChainTrust`。|  
|`customCertificateValidatorType`|可选的字符串。  一个用于验证自定义类型的类型和程序集。  当 `certificateValidationMode` 设置为 `Custom` 时，必须设置此属性。|  
|`revocationMode`|设置吊销模式以指定是否进行吊销检查，以及是联机执行还是脱机执行。  此属性的类型为 <xref:System.Security.Cryptography.X509Certificates.X509RevocationMode>。|  
|`samlSerializer`|一个可选字符串属性，指定用于服务凭据的 SamlSerializer 的类型。  默认值为一个空字符串。|  
|`trustedStoreLocation`|可选的枚举。  两个系统存储位置之一：`LocalMachine` 或 `CurrentUser`。|  
  
### 子元素  
  
|元素|描述|  
|--------|--------|  
|`knownCertificates`|指定一个 <xref:System.ServiceModel.Configuration.X509CertificateTrustedIssuerElement> 元素的集合，此集合指定服务凭据的可信颁发者。|  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<serviceCredentials\>](../../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md)|指定要用于对服务进行身份验证的凭据以及与客户端凭据验证相关的设置。|  
  
## 备注  
 颁发的令牌方案包含三个阶段。  在第一个阶段中，尝试访问服务的客户端被指引到安全令牌服务。  然后，安全令牌服务对该客户端进行身份验证，随后向该客户端颁发一个令牌（通常是一个安全断言标记语言 \(SAML\) 令牌）。  接下来，客户端携带此令牌返回服务。  服务检查该令牌，以获取使其可以对该令牌并进而对该客户端进行身份验证的数据。  若要对令牌进行身份验证，安全令牌服务所使用的证书必须为该服务所知。  
  
 此元素是所有此类安全令牌服务证书的储存库。  若要添加证书，请使用 [\<knownCertificates\>](../../../../../docs/framework/configure-apps/file-schema/wcf/knowncertificates.md)。  请为每个证书插入一个 [\<添加\>](../../../../../docs/framework/configure-apps/file-schema/wcf/add-of-knowncertificates.md)，如下面的示例所示。  
  
```  
<issuedTokenAuthorization>  
   <knownCertificates>  
      <add findValue="www.contoso.com"   
           storeLocation="LocalMachine" storeName="My"   
           X509FindType="FindBySubjectName" />  
    </knownCertificates>  
</issuedTokenAuthentication>  
```  
  
 默认情况下，必须从安全令牌服务那里获取证书。  这些“已知的”证书可以确保只有合法的客户端才能访问服务。  
  
 有关使用此配置元素的更多信息，请参见[如何：在联合身份验证服务上配置凭据](../../../../../docs/framework/wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md)。  
  
## 请参阅  
 <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator>   
 <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator.AllowedAudienceUris%2A>   
 <xref:System.IdentityModel.Selectors.SamlSecurityTokenAuthenticator.AudienceUriMode%2A>   
 <xref:System.ServiceModel.Configuration.ServiceCredentialsElement.IssuedTokenAuthentication%2A>   
 <xref:System.ServiceModel.Configuration.IssuedTokenServiceElement>   
 <xref:System.ServiceModel.Description.ServiceCredentials.IssuedTokenAuthentication%2A>   
 <xref:System.ServiceModel.Security.IssuedTokenServiceCredential>   
 [保护服务和客户端的安全](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [如何：在联合身份验证服务上配置凭据](../../../../../docs/framework/wcf/feature-details/how-to-configure-credentials-on-a-federation-service.md)