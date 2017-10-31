---
title: "行为安全 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 19710ae3-f197-4d28-ba9d-52e465006819
caps.latest.revision: 5
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 5
---
# 行为安全
本节包含演示服务行为的配置安全的示例。  
  
## 本节内容  
 [服务审核行为](../../../../docs/framework/wcf/samples/service-auditing-behavior.md)  
 此示例演示如何在服务操作过程中使用 <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior> 来启用对安全事件的审核。  
  
 [成员资格和角色提供程序](../../../../docs/framework/wcf/samples/membership-and-role-provider.md)  
 此示例演示服务如何使用 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 成员资格和角色提供程序来对客户端进行身份验证和授权。  
  
 [授予对服务操作的访问权限](../../../../docs/framework/wcf/samples/authorizing-access-to-service-operations.md)  
 本示例演示如何使用 [\<serviceAuthorization\>](../../../../docs/framework/configure-apps/file-schema/wcf/serviceauthorization-element.md)来启用 <xref:System.Security.Permissions.PrincipalPermissionAttribute> 特性以授予对服务操作的访问权限。  
  
 [模拟客户端](../../../../docs/framework/wcf/samples/impersonating-the-client.md)  
 此示例演示如何在服务中模拟调用方应用程序，以便服务可以代表调用方访问系统资源。