---
title: "&lt;wsFederation&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c537f770-68bd-4f82-96ad-6424ad91369f
caps.latest.revision: 8
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 8
---
# &lt;wsFederation&gt;
提供了有关配置<xref:System.IdentityModel.Services.WSFederationAuthenticationModule> （WSFAM）。  
  
## 语法  
  
```  
<system.identityModel.services>  
  <federationConfiguration>  
    <wsFederation authenticationType=xs:string (URI)  
        freshness=xs:decimal  
        homerealm=xs:string (URI)  
        issuer=xs:string (URI)  
        persistentCookiesOnPassiveRedirects=xs:boolean  
        passiveRedirectEnabled=xs:boolean  
        policy=xs:string (URI)  
        realm=xs:string (URI)  
        reply=xs:string (URI)  
        request=xs:string (URI)  
        requestPtr=xs:string (URI)  
        requireHttps=xs:boolean  
        resource=xs:string (URI)  
        signInQueryString=xs:string  
        signOutQueryString=xs:string  
        signOutReply=xs:string (URL)  
    </wsFederation>  
  </federationConfiguration>  
</system.identityModel.services>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|authenticationType|指定的身份验证类型的 URI。  设置的 WS 联合身份验证登录请求 wauth 参数。  可选。  默认值为一个空字符串，指定在请求中未包含的 wauth 参数。|  
|刷新|所需的最长时间的身份验证请求，以分钟为单位。  设置的 WS 联合身份验证登录请求 wfresh 参数。  可选。  默认值为零。  可选。 **Warning:**  在下一版。NET 框架 4.5， `freshness`属性的类型将为`xs:string` ，其默认值将`null`。|  
|homeRealm|要用于身份验证的身份提供程序 \(IP\) 家庭的领域。  设置的 WS 联合身份验证登录请求瓦时参数。  可选。  默认值为一个空字符串，指定在请求中不包含 whr 参数。|  
|issuer|预期的令牌颁发者的 URI。  设置基本请求 URL 的 WS\-联合身份验证登录和注销请求所需。|  
|persistentCookiesOnPassiveRedirects|指定是否颁发永久性 cookie 身份验证。  可选。  默认值为"false"，不颁发的 cookie。|  
|passiveRedirectEnabled|指定是否自动进行未经授权的请求重定向到 STS 启用 WSFAM。  可选。  默认值为"true"，未经授权的请求会自动重定向。|  
|policy|指定要使用的登录请求的相关策略的位置的 URL。  默认值为空字符串。  设置的 WS 联合身份验证登录请求白皮书参数。  可选。  默认值为一个空字符串，指定在请求中不包含该白皮书参数。|  
|realm|请求的领域的 URI。  （安全令牌服务 \(STS\) 来标识依赖方 \(RP\) 的 URI。）设置请求 wtrealm WS 联合身份验证登录请求参数。  必选。|  
|答复|用于标识的依赖方 \(RP\) 应用程序希望接收答复安全令牌服务 \(STS\) 从地址的 URL。  设置的 WS 联合身份验证登录请求 wreply 参数。  可选。  默认值为一个空字符串，指定在请求中未包含的 wreply 参数。|  
|请求|该令牌颁发请求。  设置的 WS 联合身份验证登录请求 wreq 参数。  可选。  默认值为一个空字符串，指定在请求中未包含的 wreq 参数。  不包括在请求中的 wreq 或 wreqptr 参数意味着 STS 知道哪种类型的颁发令牌。|  
|requestPtr|指定颁发令牌请求的位置的 URL。  设置请求 wreqptr 参数。  可选。  默认值为一个空字符串，指定在请求中未包含的 wreqptr 参数。  不包括在请求中的 wreq 或 wreqptr 参数意味着 STS 知道哪种类型的颁发令牌。|  
|requireHttps|指定与安全令牌服务 \(STS\) 的通信是否必须使用 HTTPS 协议。  可选。  默认值为"true"，则必须使用 HTTPS。|  
|Resource — 资源|URI 标识的资源访问，依赖方 \(RP\)，为安全令牌服务 \(STS\)。  可选。  设置的 WS 联合身份验证登录请求 wres 参数。  可选。  默认值为一个空字符串，指定在请求中未包含的 wres 参数。 **Note:**  wres 是一个传统的参数。  指定`realm`改为使用 wtrealm 参数的属性。|  
|signInQueryString|提供了一个可扩展性点，以指定应用程序定义查询参数的 WS 联合身份验证登录请求的 URL 中。  可选。  默认值为空字符串，它指定任何其他参数应包含在请求中。  参数指定为查询字符串片段使用以下格式： `“param1=value1&param2=value2&param3=value3”` ，依此类推。 **Note:**  在配置文件中 &"的查询字符串中的字符，必须使用其实体引用，指定`&`。|  
|signOutQueryString|提供了一个可扩展性点，以指定应用程序定义查询参数的 WS 联合身份验证登录请求的 URL 中。  可选。  默认值为空字符串，它指定任何其他参数应包含在请求中。  参数指定为查询字符串片段使用以下格式： `“param1=value1&param2=value2&param3=value3”` ，依此类推。 **Note:**  在配置文件中 &"的查询字符串中的字符，必须使用其实体引用，指定`&`。|  
|signOutReply|在被动的 WS 联合身份验证协议通过注销过程中指定的 URL 的客户端应被重定向到安全令牌服务 \(STS\)。  将 wreply 参数设置的 WS 联合身份验证的注销请求。  可选。  默认值为空字符串，它指定任何其他参数应包含在请求中。|  
  
### 子元素  
 无  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[\<federationConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/federationconfiguration.md)|包含配置的设置<xref:System.IdentityModel.Services.WSFederationAuthenticationModule> \(WSFAM\) 和<xref:System.IdentityModel.Services.SessionAuthenticationModule> \(SAM\)。|  
  
## 备注  
 您可以使用`<wsFederation>` WSFAM 配置 WS 联合身份验证参数的默认设置和默认行为的元素。  WS 联合身份验证参数设置下定义`<wsFederation>`元素集公开的等效属性<xref:System.IdentityModel.Services.WSFederationAuthenticationModule>类。  这些属性保持不变发出 WSFAM 的每个请求。  可通过添加 WSFAM ； 提供的事件的事件处理程序处理请求过程中动态变化的 WS 联合身份验证参数 例如， <xref:System.IdentityModel.Services.WSFederationAuthenticationModule.RedirectingToIdentityProvider>事件。  有关更多信息，请参见 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule> 类的文档。  
  
 `<wsFederation>`元素都由<xref:System.IdentityModel.Services.Configuration.WSFederationElement>类。  配置对象本身由<xref:System.IdentityModel.Services.Configuration.WSFederationConfiguration>类。  一个<xref:System.IdentityModel.Services.Configuration.WSFederationConfiguration>实例上设置<xref:System.IdentityModel.Services.Configuration.FederationConfiguration>对象，它通过访问<xref:System.IdentityModel.Services.FederatedAuthentication.FederationConfiguration%2A?displayProperty=fullName>属性，并提供 WSFAM 的配置。  
  
## 示例  
 所示的 XML `<wsFederation>`指定的 WSFAM 设置的元素。  
  
> [!WARNING]
>  在此示例中，WSFAM 不是需要使用 HTTPS。  这是因为`requireHttps`属性上`<wsFederation>`元素设置`false`。  此设置不建议对于大多数生产环境，其可能存在安全风险。  
  
```  
<wsFederation passiveRedirectEnabled="true"   
  issuer="http://localhost:15839/wsFederationSTS/Issue"   
  realm="http://localhost:50969/"   
  reply="http://localhost:50969/"   
  requireHttps="false"   
  signOutReply="http://localhost:50969/SignedOutPage.html"   
  signOutQueryString="Param1=value2&Param2=value2"   
  persistentCookiesOnPassiveRedirects="true" />  
  
```  
  
## 请参阅  
 <xref:System.IdentityModel.Services.WSFederationAuthenticationModule>   
 <xref:System.IdentityModel.Services.FederatedAuthentication.FederationConfiguration%2A?displayProperty=fullName>