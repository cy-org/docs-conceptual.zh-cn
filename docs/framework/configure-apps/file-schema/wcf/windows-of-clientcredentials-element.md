---
title: "&lt;clientCredentials&gt; 的 &lt;windows&gt; 元素 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 793e41c2-31ea-4159-abbc-2123bf097233
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# &lt;clientCredentials&gt; 的 &lt;windows&gt; 元素
指定用于表示客户端的 Windows 凭据的设置。  
  
## 语法  
  
```  
  
<windows   
    allowedImpersonationLevel="Identification/Impersonation/Delegation/Anonymous/None"  
        allowNtlm="Boolean"  
/>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|`allowedImpersonationLevel`|设置客户端用于与服务器进行通信的模拟首选项。  服务器上不强制使用客户端所选择的模拟模式。  包括以下有效值：<br /><br /> -   Identification：服务器可以获取客户端的标识和特权，但无法模拟客户端。<br />-   Impersonation：服务器可以在本地系统上模拟客户端的安全上下文。<br />-   Delegation：服务器可以在远程系统上模拟客户端的安全上下文。<br />-   Anonymous：服务器无法模拟或标识客户端。<br />-   None：未指定模拟级别。<br /><br /> 默认值为 Identification。  此属性的类型为 <xref:System.Security.Principal.TokenImpersonationLevel>。|  
|`allowNtlm`|如果 Kerberos 不可用，则将此属性设置为 `true` 可令身份验证降级到 NTLM。<br /><br /> 如果使用 NTLM，则将此属性设置为 `false` 将导致 [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 尽最大努力引发异常。  请注意，将此属性设置为 `false` 可能不阻止通过网络发送 NTLM 凭据。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<clientCredentials\>](../../../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md)|指定用于向服务证明客户端身份的凭据。|  
  
## 请参阅  
 <xref:System.ServiceModel.Configuration.WindowsClientElement>   
 <xref:System.ServiceModel.Configuration.ClientCredentialsElement>   
 <xref:System.ServiceModel.Description.ClientCredentials>   
 <xref:System.ServiceModel.Configuration.ClientCredentialsElement.Windows%2A>   
 <xref:System.ServiceModel.Description.ClientCredentials>   
 <xref:System.ServiceModel.Description.ClientCredentials.Windows%2A>   
 <xref:System.ServiceModel.Security.WindowsClientCredential>   
 [保证客户端的安全](../../../../../docs/framework/wcf/securing-clients.md)   
 [使用证书](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md)   
 [保护服务和客户端的安全](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)