---
title: "ServiceCredentials | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9c780793-4785-46f7-add9-ac1ebeadb614
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# ServiceCredentials
ServiceCredentials  
  
## 语法  
  
```  
class ServiceCredentials : Behavior  
{  
  string ClientCertificate;  
  string IssuedTokenAuthentication;  
  string Peer;  
  string SecureConversationAuthentication;  
  string ServiceCertificate;  
  string UserNameAuthentication;  
  string WindowsAuthentication;  
};  
```  
  
## 方法  
 ServiceCredentials 类不定义任何方法。  
  
## 属性  
 ServiceCredentials 类具有下列属性：  
  
### ClientCertificate  
 数据类型：String  
  
 访问类型：只读  
  
 此服务的客户端证书身份验证和配置设置。  
  
### IssuedTokenAuthentication  
 数据类型：String  
  
 访问类型：只读  
  
 当前颁发的此服务的令牌身份验证设置。  
  
### 对等  
 数据类型：String  
  
 访问类型：只读  
  
 对等传输终结点要使用的当前凭据身份验证和配置设置。  
  
### SecureConversationAuthentication  
 数据类型：String  
  
 访问类型：只读  
  
 指定当前安全对话设置。  
  
### ServiceCertificate  
 数据类型：String  
  
 访问类型：只读  
  
 与此服务关联的证书。  
  
### UserNameAuthentication  
 数据类型：String  
  
 访问类型：只读  
  
 此服务的用户名\/密码设置。  
  
### WindowsAuthentication  
 数据类型：String  
  
 访问类型：只读  
  
 此服务的 Windows 身份验证设置。  
  
## 要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|------------------------------|  
|命名空间|已在 root\\ServiceModel 中定义|  
  
## 请参阅  
 <xref:System.ServiceModel.Description.ServiceCredentials>