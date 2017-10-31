---
title: "&lt;chunkedCookieHandler&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7220de45-1d14-4aec-a29e-4a2ea8ac861f
caps.latest.revision: 5
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 5
---
# &lt;chunkedCookieHandler&gt;
配置<xref:System.IdentityModel.Services.ChunkedCookieHandler>。  此元素可能只会显示如果`mode`属性的`<cookieHandler>`元素是"默认"分块"。  
  
## 语法  
  
```  
<system.identityModel.services>  
  <federationConfiguration>  
    <cookieHandler mode="Chunked||Default" >  
      <chunkedCookieHandler size=xs:int >  
      </chunkedCookieHandler>  
    </cookieHandler>  
  </federationConfiguration>  
</system.identityModel.services>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|chunkSize|最大大小以字符为单位，任何一个 HTTP cookie 的 HTTP cookie 数据。  您必须调整大小文本块时要小心。  Web 浏览器大小的 cookie，并允许每个域的数目有不同的限制。  例如，原始 Netscape 规范规定这些限制： 300 cookie 求和，4096 个字节，每个 cookie 标头 （包括元数据，而不只是 cookie 值） 和每个域的 20 cookie。  默认值为 2000。  必选。|  
  
### 子元素  
 无  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[\<cookieHandler\>](../../../../../docs/framework/configure-apps/file-schema/windows-identity-foundation/cookiehandler.md)|配置<xref:System.IdentityModel.Services.CookieHandler>的<xref:System.IdentityModel.Services.SessionAuthenticationModule> \(SAM\) 使用读取和写入的 cookie。|  
  
## 备注  
 当您指定<xref:System.IdentityModel.Services.ChunkedCookieHandler>通过设置`mode`属性的`<cookieHandler>` "默认"或"Chunked"的元素，您可以指定块区大小的 cookie 处理程序用于读取和写入 cookie，通过包括`<chunkedCookieHandler>`子元素，并设置其`chunkSize`属性。  如果`<chunkedCookieHandler>`元素不存在，则使用默认区块大小的 2000 字节。  不能为此元素时指定`mode`属性设置为"自定义"。  
  
 `<chunkedCookieHandler>`元素都由<xref:System.IdentityModel.Services.ChunkedCookieHandlerElement>类。  
  
## 示例  
 下面的示例配置将 cookie 写入 3000 个字节的块中的 cookie 分块处理程序。  
  
```  
<cookieHandler mode="Chunked">  
    <chunkedCookieHandler chunkSize=3000/>  
</cookieHandler>  
```  
  
## 请参阅  
 <xref:System.IdentityModel.Services.ChunkedCookieHandler>