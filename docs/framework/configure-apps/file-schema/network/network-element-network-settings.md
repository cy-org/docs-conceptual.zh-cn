---
title: "&lt;network&gt; 元素（网络设置） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#network"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/mailSettings/smtp/network"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<network> 元素"
  - "network 元素"
ms.assetid: 2c2c6ad4-ed11-48ab-b28e-2bc0ba9b42c7
caps.latest.revision: 13
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 13
---
# &lt;network&gt; 元素（网络设置）
针对外部的简单邮件传输协议 \(SMTP\) 服务器配置网络选项。  
  
## 语法  
  
```  
  
      <network  
  clientDomain="string"   
  defaultCredentials="true|false"  
  enableSsl="true|false"  
  host="string"   
  password="string"  
  port="integer"   
  targetName="string"  
  userName="string"  
/>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|`clientDomain`|指定初始 SMTP 协议请求中用来连接到 SMTP 邮件服务器的客户端域名。  默认值是发送请求的本地计算机的 localhost 名称。|  
|`defaultCredentials`|指定是否应将默认用户凭据用于访问 SMTP 事务的 SMTP 邮件服务器。  默认值为 `false`。|  
|`enableSsl`|指定是否使用 SSL 访问 SMTP 邮件服务器。  默认值为 `false`。|  
|`host`|指定 SMTP 邮件服务器的主机名以用于 SMTP 事务。  此特性无默认值。|  
|`password`|指定用于 SMTP 邮件服务器验证的密码。  此特性无默认值。|  
|`port`|指定用于连接到 SMTP 邮件服务器的端口号码。  默认值为 25。|  
|`targetName`|指定在使用 SMTP 事务扩展保护时用于身份验证的服务提供程序名称 \(SPN\)。  此特性无默认值。|  
|`userName`|指定用于 SMTP 邮件服务器验证的用户名。  此特性无默认值。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|[\<smtp\> 元素（网络设置）](../../../../../docs/framework/configure-apps/file-schema/network/smtp-element-network-settings.md)|配置简单邮件传输协议 \(SMTP\) 邮件发送选项。|  
  
## 备注  
 某些 SMTP 服务器要求您在使用服务器之前先通过该服务器的身份验证。  如果您希望使用主机上的默认网络凭据来通过身份验证，请将 `defaultCredentials` 特性设置为 `true`。  <xref:System.Net.Configuration.SmtpNetworkElement.DefaultCredentials%2A?displayProperty=fullName> 属性可用于从适用的配置文件获取 `defaultCredentials` 特性的当前值。  
  
 还可以使用基本身份验证（用户名和密码）来通过 SMTP 服务器的身份验证。  若要使用此选项，必须指定对指定的 SMTP 服务器有效的用户名和密码。  
  
> [!NOTE]
>  基本身份验证功能将 `userName` 和 `password` 值以未加密的形式发送到服务器。  监视网络流量的任何人都可以查看凭据并使用它们连接服务器。  您应当考虑使用更安全的身份验证机制，如 Kerberos 或 NT LAN Manager \(NTLM\)。如果 `defaultCredentials` 为 `true`，并且服务器支持 Kerberos 或 NTLM 协议，将使用这些协议。  
  
 基本身份验证和默认网络凭据选项是互斥的；如果将 `defaultCredentials` 设置为 `true`，并指定用户名和密码，将使用默认网络凭据，而忽略基本身份验证数据。  
  
 对于基本身份验证，如果指定 `userName`，则还应指定 `password`，以通过邮件服务器的身份验证。  
  
 <xref:System.Net.Configuration.SmtpNetworkElement.UserName%2A?displayProperty=fullName> 属性可用于从适用的配置文件获取 `userName` 特性的当前值。  <xref:System.Net.Configuration.SmtpNetworkElement.Password%2A?displayProperty=fullName> 属性可用于从适用的配置文件获取 `password` 特性的当前值。  出于安全原因，`password` 特性通常不输入到配置文件中。  
  
 `clientDomain` 特性更改初始 SMTP 协议请求中用来连接到 SMTP 邮件服务器的客户端域名。  可以将 `clientDomain` 特性设置为本地计算机的完全限定域名称，而不是默认情况下使用的本地主机名称。  这样会更加符合 SMTP 协议标准。  默认值是发送请求的本地计算机的 localhost 名称。  <xref:System.Net.Configuration.SmtpNetworkElement.ClientDomain%2A?displayProperty=fullName> 属性可用于从适用的配置文件获取 `clientDomain` 特性的当前值。  
  
 `targetName` 特性用于采用扩展保护时的身份验证。  表格"SMTPSVC\/\<host\>" where \<host\>的默认值是SMTP邮件服务器的主机名。  <xref:System.Net.Configuration.SmtpNetworkElement.TargetName%2A?displayProperty=fullName> 属性可用于从适用的配置文件获取 `targetName` 特性的当前值。  
  
 `enableSsl`  特性指定是否使用 SSL 访问 SMTP 邮件服务器。  <xref:System.Net.Mail.SmtpClient?displayProperty=fullName> 类只支持传输层安全上的安全 SMTP 的 SMTP 服务扩展，如 RFC 3207 中所定义。  在此模式中，SMTP 会话在一个未加密的通道上开始，然后 STARTTLS 命令由客户端向服务器发出，以切换到使用 SSL 安全通信。  有关更多信息，请参见 Internet 工程任务组 \(IETF\) 发布的 RFC 3207。  
  
 一个备用连接方法是在发送任何协议命令之前预先建立 SSL 会话。  这种连接方法有时被称为 SMTPS，并且默认情况下使用端口 465。  当前不支持这种使用 SSL 的备用连接方法。  
  
 <xref:System.Net.Configuration.SmtpNetworkElement.EnableSsl%2A?displayProperty=fullName> 属性可用于从适用的配置文件获取 `enableSsl` 特性的当前值。  
  
## 示例  
 下面的代码示例指定使用默认网络凭据发送电子邮件时所需的适当 SMTP 参数。  
  
```  
<configuration>  
  <system.net>  
    <mailSettings>  
      <smtp deliveryMethod="network">  
        <network  
          clientDomain="www.contoso.com"  
          defaultCredentials="true"  
          enableSsl="false"  
          host="mail.contoso.com"  
          port="25"  
        />  
      </smtp>  
    </mailSettings>  
  </system.net>  
</configuration>  
```  
  
## 请参阅  
 <xref:System.Net.Configuration.SmtpNetworkElement?displayProperty=fullName>   
 <xref:System.Net.Configuration.SmtpSection?displayProperty=fullName>   
 <xref:System.Net.Mail.SmtpClient?displayProperty=fullName>   
 [网络设置架构](../../../../../docs/framework/configure-apps/file-schema/network/index.md)