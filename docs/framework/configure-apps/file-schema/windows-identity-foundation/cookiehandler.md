---
title: "&lt;cookieHandler&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: bfdc127f-8d94-4566-8bef-f583c6ae7398
caps.latest.revision: 5
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 5
---
# &lt;cookieHandler&gt;
配置<xref:System.IdentityModel.Services.CookieHandler>的<xref:System.IdentityModel.Services.SessionAuthenticationModule> \(SAM\) 使用读取和写入的 cookie。  
  
## 语法  
  
```  
<system.identityModel.services>  
  <federationConfiguration>  
    <cookieHandler name=xs:string  
        path=Path  
        mode="Chunked||Custom||Default"  
        persistentSessionLifetime=xs:string  
        hideFromScript=xs:boolean  
        requireSSL=xs:boolean  
        domain=xs:string  
      <chunkedCookieHandler size=xs:int />  
      <customCookieHandler type="MyNamespace.MyCustomCookieHandler, MyAssembly" />  
    </cookieHandler>  
  </federationConfiguration>  
</system.identityModel.services>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|name|指定写入任何 cookie 的基名称。  默认为"FedAuth"。|  
|path|指定写入任何 cookie 路径值。  默认为"HttpRuntime.AppDomainAppVirtualPath"。|  
|mode|其中一个<xref:System.IdentityModel.Services.CookieHandlerMode>值，该值指定使用的 SAM 的 cookie 处理程序的类型。  可以使用以下值：<br /><br /> -   "默认"—"Chunked"相同。<br />-   "分块"— — 使用实例的<xref:System.IdentityModel.Services.ChunkedCookieHandler>类。  此 cookie 处理程序可确保各个 cookie 不能超过设置的最大大小。  实现此目的的可能"分块"逻辑的一个 cookie，为多个 cookie 上的线。<br />-   "自定义"，使用从派生的自定义类的实例<xref:System.IdentityModel.Services.CookieHandler>。  派生的类引用的`<customCookieHandler>`子元素。<br /><br /> 默认值为"默认值"。|  
|persistentSessionLifetime|指定的持续会话的生存期。  如果为零，始终使用瞬态会话。  默认值为外其余"全都，它指定一个暂时的会话。  最大值为"365:0:0"，指定一个会话的 365 天。  应以下列限制根据指定的值： `<xs:pattern value="([0-9.]+:){0,1}([0-9]+:){0,1}[0-9.]+" />`、 其中的最左边的值指定的天数、 中间值 （如果存在） 指定小时，而最右边的值 （如果存在） 指定的分钟数。|  
|requireSsl|指定写入任何 cookie 是否发出的"安全"标志。  如果此值设置的登录会话 cookie 将只能通过 HTTPS。  默认为"true"。|  
|hideFromScript|控制写入任何 cookie 是否发出了"HttpOnly"标志。  某些 web 浏览器接受此标志，通过禁止客户端脚本访问 cookie 值。  默认为"true"。|  
|域|写入所有 cookie 域值。  默认值是""。|  
  
### 子元素  
  
|元素|说明|  
|--------|--------|  
|[\<chunkedCookieHandler\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/chunkedcookiehandler.md)|配置<xref:System.IdentityModel.Services.ChunkedCookieHandler>。  此元素可能只会显示如果`mode`属性的`<cookieHandler>`元素是"默认"分块"。|  
|[\<customCookieHandler\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/customcookiehandler.md)|设置自定义 cookie 处理程序类型。  必须存在此元素如果`mode`属性的`<cookieHandler>`元素是"自定义"。  它不能有任何其他值的`mode`属性。  自定义的类型必须从派生<xref:System.IdentityModel.Services.CookieHandler>类。|  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[\<federationConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/federationconfiguration.md)|包含配置的设置<xref:System.IdentityModel.Services.WSFederationAuthenticationModule> \(WSFAM\) 和<xref:System.IdentityModel.Services.SessionAuthenticationModule> \(SAM\)。|  
  
## 备注  
 <xref:System.IdentityModel.Services.CookieHandler>负责读取和写入原始 cookie 在 HTTP 协议的级别。  您可以配置任何一个<xref:System.IdentityModel.Services.ChunkedCookieHandler>或自定义 cookie 处理源自<xref:System.IdentityModel.Services.CookieHandler>类。  
  
 若要配置分块的 cookie 处理程序，模式属性设置为"Chunked"或"默认"。  默认区块大小为 2000 个字节，但可以通过包括 （可选） 指定不同的区块大小`<chunkedCookieHandler>`子元素。  
  
 若要配置自定义 cookie 处理程序，模式属性设置为"自定义"。  您还必须指定`<customCookieHandler>`引用的自定义处理程序类型的子元素。  
  
 `<cookieHandler>`元素都由<xref:System.IdentityModel.Services.CookieHandlerElement>类。  在配置中指定的 cookie 处理程序，可从<xref:System.IdentityModel.Services.Configuration.FederationConfiguration.CookieHandler%2A>的<xref:System.IdentityModel.Services.Configuration.FederationConfiguration>对象上设置<xref:System.IdentityModel.Services.FederatedAuthentication.FederationConfiguration%2A?displayProperty=fullName>属性。  
  
## 示例  
 所示的 XML `<cookieHandler>`元素。  在此示例中，因为`mode`属性未指定，SAM 将使用默认的 cookie 的处理程序。  这是一个实例的<xref:System.IdentityModel.Services.ChunkedCookieHandler>类。  因为`<chunkedCookieHandler>`子元素未指定，则将使用默认区块大小。  因为不是必需 HTTPS `requireSsl`属性设置`false`。  
  
> [!WARNING]
>  在此示例中，不需要 HTTPS 写入会话 cookie。  这是因为`requireSsl`属性上`<cookieHandler>`元素设置为`false`。  此设置不建议对于大多数生产环境，其可能存在安全风险。  
  
```  
<cookieHandler requireSsl="false" />  
```  
  
## 请参阅  
 <xref:System.IdentityModel.Services.CookieHandler>   
 <xref:System.IdentityModel.Services.ChunkedCookieHandler>   
 <xref:System.IdentityModel.Services.SessionAuthenticationModule>