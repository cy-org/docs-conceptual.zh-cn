---
title: "如何：在服务上模拟客户端 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WCF, 模拟"
  - "模拟"
  - "WCF, 安全"
ms.assetid: 431db851-a75b-4009-9fe2-247243d810d3
caps.latest.revision: 33
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 33
---
# 如何：在服务上模拟客户端
如果在 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 服务上模拟客户端，则该服务可以代表该客户端执行操作。 对于受访问控制列表 \(ACL\) 检查的操作（例如，访问计算机上的目录和文件，或访问 SQL Server 数据库），ACL 检查针对的是客户端用户帐户。 本主题演示一些基本步骤，通过这些步骤，Windows 域中的客户端可以设置客户端模拟级别。 有关此操作的可运行示例，请参阅[模拟客户端](../../../docs/framework/wcf/samples/impersonating-the-client.md)。[!INCLUDE[crabout](../../../includes/crabout-md.md)]客户端模拟，请参阅 [委托和模拟](../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md)。  
  
> [!NOTE]
>  当客户端和服务运行在同一计算机上，客户端运行在系统帐户（即 `Local System` 或 `Network Service`）下时，如果安全会话是使用状态安全上下文令牌建立的，则不能模拟客户端。 WinForms 或控制台应用程序通常运行在当前登录的帐户下，因此，默认情况下可以模拟该帐户。 但是，如果客户端为 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 页并且该页承载在 [!INCLUDE[iis601](../../../includes/iis601-md.md)] 或 IIS 7.0 中，则默认情况下，客户端会在 `Network Service` 帐户下运行。 默认情况下，系统提供的所有支持安全会话的绑定都使用无状态安全上下文令牌。 但如果客户端是 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 页，并且使用了安全会话以及有状态的安全上下文令牌，则无法模拟该客户端。[!INCLUDE[crabout](../../../includes/crabout-md.md)]在安全会话中使用有状态的安全上下文令牌，请参阅[如何：为安全会话创建安全上下文令牌](../../../docs/framework/wcf/feature-details/how-to-create-a-security-context-token-for-a-secure-session.md)。  
  
### 根据缓存的 Windows 令牌在服务上启用客户端模拟  
  
1.  创建服务。 有关此基本过程的教程，请参阅[入门教程](../../../docs/framework/wcf/getting-started-tutorial.md)。  
  
2.  使用采用 Windows 身份验证并创建会话的绑定，例如 <xref:System.ServiceModel.NetTcpBinding> 或 <xref:System.ServiceModel.WSHttpBinding>。  
  
3.  在创建服务接口的实现时，将 <xref:System.ServiceModel.OperationBehaviorAttribute> 类应用于要求客户端模拟的方法。 将 <xref:System.ServiceModel.OperationBehaviorAttribute.Impersonation%2A> 属性设置为 <xref:System.ServiceModel.ImpersonationOption>。  
  
     [!code-csharp[c_SimpleImpersonation#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_simpleimpersonation/cs/source.cs#2)]
     [!code-vb[c_SimpleImpersonation#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_simpleimpersonation/vb/source.vb#2)]  
  
### 设置客户端允许的模拟级别  
  
1.  通过使用 [ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 创建服务客户端代码。[!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [使用 WCF 客户端访问服务](../../../docs/framework/wcf/accessing-services-using-a-wcf-client.md).  
  
2.  创建 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端后，将 <xref:System.ServiceModel.Security.WindowsClientCredential.AllowedImpersonationLevel%2A> 类的 <xref:System.ServiceModel.Security.WindowsClientCredential> 属性设置为 <xref:System.Security.Principal.TokenImpersonationLevel> 枚举值之一。  
  
    > [!NOTE]
    >  若要使用 <xref:System.Security.Principal.TokenImpersonationLevel>，则必须使用协商 Kerberos 身份验证（有时称为“多段”或“多步”Kerberos）。 有关如何实现此操作的说明，请参阅 [安全性的最佳做法](../../../docs/framework/wcf/feature-details/best-practices-for-security-in-wcf.md)。  
  
     [!code-csharp[c_SimpleImpersonation#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_simpleimpersonation/cs/source.cs#1)]
     [!code-vb[c_SimpleImpersonation#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_simpleimpersonation/vb/source.vb#1)]  
  
## 请参阅  
 <xref:System.ServiceModel.OperationBehaviorAttribute>   
 <xref:System.Security.Principal.TokenImpersonationLevel>   
 [模拟客户端](../../../docs/framework/wcf/samples/impersonating-the-client.md)   
 [委托和模拟](../../../docs/framework/wcf/feature-details/delegation-and-impersonation-with-wcf.md)