---
title: "&lt;smtp&gt; 元素（网络设置） | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/mailSettings/smtp"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#smtp"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<smtp> 元素"
  - "smtp 元素"
ms.assetid: 220b0329-e384-4e0c-86b4-0945ad17efd9
caps.latest.revision: 13
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 13
---
# &lt;smtp&gt; 元素（网络设置）
配置电子邮件的传递方法，传送格式和发件人地址以便发送邮件。  
  
## 语法  
  
```  
  
      <smtp  
  deliveryFormat="format"   
  deliveryMethod="method"   
  from="from address"   
  <specifiedPickupDirectory> … </ specifiedPickupDirectory >  
  <network> … </network>  
/smtp>  
```  
  
## 特性和元素  
 以下几节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|`deliveryFormat`|为传出的电子邮件指定传送格式。  可接受的值为 SevenBit 和International。|  
|`deliveryMethod`|指定电子邮件的传递方法。  可接受的值有 network、pickupDirectoryFromIis 和 specifiedPickupDirectory。|  
|`from`|指定发出的电子邮件的发件人地址。|  
  
### 子元素  
  
|特性|描述|  
|--------|--------|  
|`specifiedPickupDirectory`|配置简单邮件传输协议 \(SMTP\) 服务器的本地目录。|  
|`network`|配置外部 SMTP 服务器的网络选项。|  
  
### 父元素  
  
|**元素**|**描述**|  
|------------|------------|  
|[\<mailSettings\> 元素（网络设置）](../../../../../docs/framework/configure-apps/file-schema/network/mailsettings-element-network-settings.md)|配置邮件发送选项。|  
  
## 示例  
 下面的代码示例指定使用默认网络凭据发送电子邮件时所需的适当 SMTP 参数。  
  
```  
<configuration>  
  <system.net>  
    <mailSettings>  
      <smtp deliveryMethod="network" deliveryFormat="SevenBit"  from="ben@contoso.com">  
        <network  
          host="localhost"  
          port="25"  
          defaultCredentials="true"  
        />  
      </smtp>  
    </mailSettings>  
  </system.net>  
</configuration>  
```  
  
## 请参阅  
 <xref:System.Net.Configuration.SmtpSection?displayProperty=fullName>   
 <xref:System.Net.Mail.SmtpClient?displayProperty=fullName>   
 <xref:System.Net.Mail.SmtpDeliveryFormat>   
 <xref:System.Net.Mail.SmtpDeliveryMethod>   
 [网络设置架构](../../../../../docs/framework/configure-apps/file-schema/network/index.md)