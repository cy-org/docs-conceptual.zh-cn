---
title: "ServiceSecurityAuditBehavior | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2c5809e7-5364-44ce-bc71-848be4672e2a
caps.latest.revision: 8
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 8
---
# ServiceSecurityAuditBehavior
ServiceSecurityAuditBehavior  
  
## 语法  
  
```  
class ServiceSecurityAuditBehavior : Behavior  
{  
  string AuditLogLocation;  
  string MessageAuthenticationAuditLevel;  
  string ServiceAuthorizationAuditLevel;  
  boolean SuppressAuditFailure;  
};  
```  
  
## 方法  
 ServiceSecurityAuditBehavior 类不定义任何方法。  
  
## 属性  
 ServiceSecurityAuditBehavior 类具有下列属性：  
  
### AuditLogLocation  
 数据类型：String  
  
 访问类型：只读  
  
 审核日志的位置。  
  
### MessageAuthenticationAuditLevel  
 数据类型：String  
  
 访问类型：只读  
  
 用于记录审核事件的消息身份验证级别的类型。  
  
### ServiceAuthorizationAuditLevel  
 数据类型：String  
  
 访问类型：只读  
  
 审核日志中记录的授权事件类型。  
  
### SuppressAuditFailure  
 数据类型：Boolean  
  
 访问类型：只读  
  
 一个 boolean 值，指定取消显示审核日志写入失败的行为。  
  
## 要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|------------------------------|  
|命名空间|已在 root\\ServiceModel 中定义|  
  
## 请参阅  
 <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior>