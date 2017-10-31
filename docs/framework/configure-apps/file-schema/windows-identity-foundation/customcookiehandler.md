---
title: "&lt;customCookieHandler&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a03b153d-5ec6-4915-9031-6f0c3fd348be
caps.latest.revision: 7
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 6
---
# &lt;customCookieHandler&gt;
设置自定义 cookie 处理程序类型。  此元素可能只会显示如果`mode`属性的`<cookieHandler>`元素是"自定义"。  自定义的类型必须从派生<xref:System.IdentityModel.Services.CookieHandler>类。  
  
## 语法  
  
```  
<system.identityModel.services>  
  <federationConfiguration>  
    <cookieHandler mode=”Custom”>  
      <customCookieHandler type="MyNamespace.MyCustomCookieHandler, MyAssembly" >  
      </customCookieHandler>  
    </cookieHandler>  
  </federationConfiguration>  
</system.identityModel.services>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|type|指定自定义类型派生自的<xref:System.IdentityModel.Services.CookieHandler>类。  有关如何指定`type`属性，请参阅[Custom Type References](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/index.md#BKMK_CustomTypeReferences)。|  
  
### 子元素  
 无  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[\<cookieHandler\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/cookiehandler.md)|配置<xref:System.IdentityModel.Services.CookieHandler>的<xref:System.IdentityModel.Services.SessionAuthenticationModule>使用读取和写入的 cookie。|  
  
## 备注  
 当您指定一个自定义 cookie 处理程序通过设置`mode`属性的`<cookieHandler>`元素"自定义"，则必须指定自定义 cookie 处理程序的类型包括`<customCookieHandler>`引用的 cookie 处理程序类型的子元素。  不能为此元素时指定`mode`属性设置为"Chunked"或"默认"。  自定义 cookie 处理程序必须从派生<xref:System.IdentityModel.Services.CookieHandler>类。  
  
 `<customCookieHandler>`元素都由<xref:System.IdentityModel.Configuration.CustomTypeElement>类。  
  
## 示例  
 下面的示例配置以使用自定义 cookie 处理程序类型的 SAM `MyNamespace.MyCustomCookieHandler`。  
  
```  
<cookieHandler mode="Custom">  
    <customCookieHandler type="MyNamespace.MyCustomCookieHandler, MyAssembly" />  
</cookieHandler>  
```  
  
## 请参阅  
 <xref:System.IdentityModel.Services.CookieHandler>