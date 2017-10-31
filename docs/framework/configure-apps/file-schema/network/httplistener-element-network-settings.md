---
title: "&lt;httpListener&gt; 元素（网络设置） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: 62f121fd-3f2e-4033-bb39-48ae996bfbd9
caps.latest.revision: 7
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 7
---
# &lt;httpListener&gt; 元素（网络设置）
自定义 <xref:System.Net.HttpListener> 类使用的参数。  
  
## 语法  
  
```  
  
      <httpListener  
  unescapeRequestUrl ="true|false"  
/>  
```  
  
## 类型  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|unescapeRequestUrl|一个布尔值，该值指示 <xref:System.Net.HttpListener> 实例是否使用未经转义的原始 URI，而非经过转换的 URI。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|**元素**|**说明**|  
|------------|------------|  
|[设置](../../../../../docs/framework/configure-apps/file-schema/network/settings-element-network-settings.md)|配置 <xref:System.Net> 命名空间的基本网络选项。|  
  
## 备注  
 **unescapeRequestUrl** 特性指示是否 <xref:System.Net.HttpListener> 使用原始未转义 URI 而不是转换后的 URI，其中任何百分比编码的值都被转换，需要执行其他规范化步骤。  
  
 当 <xref:System.Net.HttpListener> 实例通过 `http.sys` 服务接收请求时，它会创建 `http.sys` 所提供的 URI 字符串的实例，并将其公开为 <xref:System.Net.HttpListenerRequest.Url%2A?displayProperty=fullName> 属性。  
  
 `http.sys` 服务公开两个请求 URI 字符串：  
  
-   原始 URI  
  
-   已转换的 URI  
  
 原始 URI 是 HTTP 请求的请求行中提供的 <xref:System.Uri?displayProperty=fullName>：  
  
 `GET /path/`  
  
 `Host: www.contoso.com`  
  
 `http.sys` 为上述请求提供的原始 URI 是 "\/path\/"。  这表示通过网络发送 HTTP 谓词时后面所跟的字符串。  
  
 `http.sys` 服务从请求中提供的信息创建转换的 URI，方法是使用 HTTP 请求行和主机标题中提供的 URI 以确定请求应提交至的原服务器。  这是通过将来自请求的信息与一组已注册的 URI 前缀进行比较来实现的。  HTTP 服务器 SDK 文档涉及该转换的 URI，形式为 HTTP\_COOKED\_URL 结构。  
  
 为了能够将该请求与已注册 URI 前缀进行比较，需要对该请求进行一些正常化。  对于以上示例，转换的 URI 将如下所示：  
  
 `http://www.contoso.com/path/`  
  
 `http.sys` 服务结合了 <xref:System.Uri.Host%2A?displayProperty=fullName> 属性值以及请求行中的字符串以创建转换的 URI。  此外，`http.sys` 和 <xref:System.Uri?displayProperty=fullName> 类也会执行以下操作：  
  
-   取消转义所有百分比编码的值。  
  
-   将百分比编码的非 ASCII 字符转换为 UTF\-16 字符表示形式。  请注意，UTF\-8字符、ANSI\/DBCS 字符和 Unicode 字符（使用 %uXXXX 格式的 Unicode 编码）都受支持。  
  
-   执行其他规范化步骤，如路径压缩。  
  
 由于请求不包含任何有关用于百分比编码值的编码信息，因此可能无法只是通过分析百分比编码值确定正确的编码。  
  
 因此，`http.sys` 可提供用于修改进程的两个注册表项：  
  
|注册表项|默认值|说明|  
|----------|---------|--------|  
|EnableNonUTF8|1|如果为零，则 `http.sys` 仅接受 UTF\-8 编码的 URL。<br /><br /> 如果非零，则 `http.sys` 也接受请求中的 ANSI 编码或 DBCS 编码的 URL。|  
|FavorUTF8|1|如果非零，则 `http.sys` 始终首先尝试将 URL 解码为 UTF\-8；如果该转换将失败，并且 EnableNonUTF8 为非零，Http.sys 则尝试将其解码为 ANSI 或 DBCS。<br /><br /> 如果为零（且 EnableNonUTF8 为非零值），则 `http.sys` 尝试将其解码为 ANSI 或 DBCS；如果不成功，它将尝试 UTF\-8 转换。|  
  
 当 <xref:System.Net.HttpListener> 接收到请求时，它将使用从 `http.sys` 转换而来的 URI 作为 <xref:System.Net.HttpListenerRequest.Url%2A> 属性的输入。  
  
 除了 URI 中的字符和数字以外，还需要支持其他字符和数字。  例如，下面的 URI 用于检索客户的客户信息数字 "1\/3812"：  
  
 `http://www.contoso.com/Customer('1%2F3812')/`  
  
 请注意 Uri \(%2F\) 中以百分比编码的斜杠。  这是必要的，因为在这种情况下斜杠字符表示数据而不是路径分隔符。  
  
 将字符串传递给 Uri 构造函数，就会带来以下 URI：  
  
 `http://www.contoso.com/Customer('1/3812')/`  
  
 将路径拆分成段将会生成以下元素：  
  
 `Customer('1`  
  
 `3812')`  
  
 这不是请求的发件人的意图。  
  
 如果 **unescapeRequestUrl** 特性设置为 **false**，则当 <xref:System.Net.HttpListener> 接收了请求时，它会使用原始 URI，而不是由 `http.sys` 转换而来，作为 <xref:System.Net.HttpListenerRequest.Url%2A> 属性的输入的 URI。  
  
 **unescapeRequestUrl** 特性的默认值为 **true**。  
  
 <xref:System.Net.Configuration.HttpListenerElement.UnescapeRequestUrl%2A> 属性可用于从适用的配置文件获取 **unescapeRequestUrl** 特性的当前值。  
  
## 示例  
 下面的代码示例示出如何配置 <xref:System.Net.HttpListener> 类，前提是在其接收使用原始 URI 请求，而不是从作为输入的 `http.sys` 转换为 <xref:System.Net.HttpListenerRequest.Url%2A> 属性的请求时。  
  
```  
<configuration>  
  <system.net>  
    <settings>  
      <httpListener  
        unescapeRequestUrl="false"  
      />  
    </settings>  
  </system.net>  
</configuration>  
```  
  
## 元素信息  
  
|||  
|-|-|  
|命名空间|System.Net|  
|架构名称||  
|验证文件||  
|可以为空||  
  
## 请参阅  
 <xref:System.Net.Configuration.HttpListenerElement>   
 <xref:System.Net.HttpListener>   
 <xref:System.Net.HttpListenerRequest.Url%2A>   
 [网络设置架构](../../../../../docs/framework/configure-apps/file-schema/network/index.md)