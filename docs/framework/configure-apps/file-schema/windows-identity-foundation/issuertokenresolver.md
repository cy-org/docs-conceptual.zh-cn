---
title: "&lt;issuerTokenResolver&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f74392f6-3f5b-4880-bd8a-3a9130d31e65
caps.latest.revision: 9
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 8
---
# &lt;issuerTokenResolver&gt;
注册颁发令牌解析所使用的标记处理程序集合中的处理程序。  颁发者令牌解析用于解析上传入令牌和邮件的签名标记。  
  
## 语法  
  
```  
<system.identityModel>  
  <identityConfiguration>  
    <securityTokenHandlers>  
      <securityTokenHandlerConfiguration>  
        <issuerTokenResolver type=xs:string>  
        </issuerTokenResolver>  
      </securityTokenHandlerConfiguration>  
    </securityTokenHandlers>  
  </identityConfiguration>  
</system.identityModel>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|type|指定颁发者令牌解析的类型。  必须是<xref:System.IdentityModel.Tokens.IssuerTokenResolver>类或类型派生自的<xref:System.IdentityModel.Tokens.IssuerTokenResolver>类。  有关如何指定`type`属性，请参阅[Custom Type References](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/index.md#BKMK_CustomTypeReferences)。  必选。|  
  
### 子元素  
 无  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[\<securityTokenHandlerConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/securitytokenhandlerconfiguration.md)|提供配置集合的安全令牌的处理程序。|  
  
## 备注  
 颁发者令牌解析用于解析上传入令牌和邮件的签名标记。  它用于检索用于检查签名的加密材料。  您必须指定`type`属性。  指定的类型可以是<xref:System.IdentityModel.Tokens.IssuerTokenResolver>或自定义类型派生自的<xref:System.IdentityModel.Tokens.IssuerTokenResolver>类。  
  
 某些标记处理程序允许您在配置中指定颁发者令牌解析程序设置。  在单个标记处理程序的设置会覆盖指定的安全令牌的处理程序集合。  
  
> [!NOTE]
>  指定`<issuerTokenResolver>`元素的子元素作为[\<identityConfiguration\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/identityconfiguration.md)元素已被否决，但仍然支持向后兼容性。  在设置`<securityTokenHandlerConfiguration>`元素会覆盖那些在`<identityConfiguration>`元素。  
  
## 示例  
 下面的 XML 显示了配置颁发的令牌解析基于自定义派生自的类的<xref:System.IdentityModel.Tokens.IssuerTokenResolver>。  令牌解析维护从自定义配置元素初始化的观众密钥对的字典 \(`<AddAudienceKeyPair>`） 为类定义。  类重写<xref:System.IdentityModel.Selectors.SecurityTokenResolver.LoadCustomConfiguration%2A>处理此元素的方法。  重写中将显示在下面的示例。 但是，它调用的方法不会显示为简洁起见。  有关完整的示例，请参阅`CustomToken`的示例。  
  
```  
<issuerTokenResolver type="SimpleWebToken.CustomIssuerTokenResolver, SimpleWebToken">  
  <AddAudienceKeyPair  symmetricKey="wAVkldQiFypTQ+kdNdGWCYCHRcee8XmXxOvgmak8vSY=" audience="http://localhost:19851/" />  
</issuerTokenResolver>  
```  
  
## 示例  
  
```  
public override void LoadCustomConfiguration(System.Xml.XmlNodeList nodelist)  
{  
    foreach (XmlNode node in nodelist)  
    {  
        XmlDictionaryReader rdr = XmlDictionaryReader.CreateDictionaryReader(new XmlTextReader(new StringReader(node.OuterXml)));  
        rdr.MoveToContent();  
  
        string symmetricKey = rdr.GetAttribute("symmetricKey");  
        string audience = rdr.GetAttribute("audience");  
  
        this.AddAudienceKeyPair(audience, symmetricKey);  
    }  
}  
```  
  
## 请参阅  
 <xref:System.IdentityModel.Tokens.IssuerTokenResolver>