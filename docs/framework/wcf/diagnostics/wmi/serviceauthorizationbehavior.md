---
title: "ServiceAuthorizationBehavior | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 77dad8e8-fea4-4d1c-b366-2f01a2a87f78
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# ServiceAuthorizationBehavior
ServiceAuthorizationBehavior  
  
## 语法  
  
```  
class ServiceAuthorizationBehavior : Behavior  
{  
  boolean ImpersonateCallerForAllOperations;  
  string PrincipalPermissionMode;  
  string RoleProvider;  
  string ServiceAuthorizationManager;  
};  
```  
  
## 方法  
 ServiceAuthorizationBehavior 类未定义任何方法。  
  
## 属性  
 ServiceAuthorizationBehavior 类具有下列属性：  
  
### ImpersonateCallerForAllOperations  
 数据类型：Boolean  
  
 访问类型：只读  
  
 一个值，控制服务是否尝试使用传入消息所提供的凭据进行模拟。  
  
### PrincipalPermissionMode  
 数据类型：String  
  
 访问类型：只读  
  
 用于在服务器上执行操作的主体。  
  
### RoleProvider  
 数据类型：String  
  
 访问类型：只读  
  
 ASP.NET 角色提供程序的名称。  
  
### ServiceAuthorizationManager  
 数据类型：String  
  
 访问类型：只读  
  
 用于自定义授权的授权管理器。  
  
## 要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|------------------------------|  
|命名空间|已在 root\\ServiceModel 中定义|  
  
## 请参阅  
 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior>