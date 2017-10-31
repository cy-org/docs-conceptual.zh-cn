---
title: "&lt;httpDigest&gt; 元素 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3da4f276-dfd9-4247-8c07-01d83618727c
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# &lt;httpDigest&gt; 元素
指定一个在向服务证明客户端身份时使用的摘要类型凭据。  
  
## 语法  
  
```  
  
<digest impersonationLevel="Identification/Impersonation/Delegation/Anonymous/None" />  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|`impersonationLevel`|设置客户端用于与服务器进行通信的模拟首选项。  服务器上不强制使用客户端所选择的模拟模式。  包括以下有效值：<br /><br /> -   Identification：服务器可以获取客户端的标识和特权，但无法模拟客户端。<br />-   Impersonation：服务器可以在本地系统上模拟客户端的安全上下文。<br />-   Delegation：服务器可以在远程系统上模拟客户端的安全上下文。<br />-   Anonymous：服务器无法模拟或标识客户端。<br />-   None：未指定模拟级别。<br /><br /> 默认值为 Identification。  此属性的类型为 <xref:System.Security.Principal.TokenImpersonationLevel>。|  
  
### 子元素  
 无  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<clientCredentials\>](../../../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md)|指定用于向服务验证客户端身份的凭据。|  
  
## 备注  
 摘要是使用算法和一组输入确定的哈希。  身份验证器和被验证方一致同意某种算法并交换用作输入的数据。  客户端可以计算哈希并将其发送给服务。  服务也可以计算哈希并比较值。  如果匹配，则客户端将通过验证。  
  
 必须使用 Windows 上的 Active Directory 和 Internet 信息服务 \(IIS\) 启用此功能。  [!INCLUDE[crdefault](../../../../../includes/crdefault-md.md)] [IIS 6.0 中的摘要式身份验证](http://go.microsoft.com/fwlink/?LinkId=88443)（可能为英文网页）。  
  
## 请参阅  
 <xref:System.ServiceModel.Configuration.ClientCredentialsElement>   
 <xref:System.ServiceModel.Configuration.ClientCredentialsElement.HttpDigest%2A>   
 <xref:System.ServiceModel.Description.ClientCredentials>   
 <xref:System.ServiceModel.Description.ClientCredentials.HttpDigest%2A>   
 <xref:System.ServiceModel.Configuration.HttpDigestClientElement>   
 <xref:System.ServiceModel.Security.HttpDigestClientCredential>   
 [安全行为](../../../../../docs/framework/wcf/feature-details/security-behaviors-in-wcf.md)   
 [保证客户端的安全](../../../../../docs/framework/wcf/securing-clients.md)   
 [使用证书](../../../../../docs/framework/wcf/feature-details/working-with-certificates.md)   
 [保护服务和客户端的安全](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)