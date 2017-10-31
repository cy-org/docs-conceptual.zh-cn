---
title: "如何：在企业中锁定终结点 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1b7eaab7-da60-4cf7-9d6a-ec02709cf75d
caps.latest.revision: 21
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 21
---
# 如何：在企业中锁定终结点
大企业往往要求开发的应用程序符合企业安全策略。  下面的主题讨论如何开发和安装可用于验证安装在计算机上的所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 客户端应用程序的客户端终结点验证程序。  
  
 在这种情况中，验证程序是客户端验证程序，因为此终结点行为是被添加到 machine.config 文件中的客户端 [\<commonBehaviors\>](../../../../docs/framework/configure-apps/file-schema/wcf/commonbehaviors.md) 部分的。  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 仅针对客户端应用程序加载常见的终结点行为，并仅针对服务应用程序加载常见服务行为。  若要为服务应用程序安装此相同验证程序，验证程序必须为服务行为。  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][\<commonBehaviors\>](../../../../docs/framework/configure-apps/file-schema/wcf/commonbehaviors.md) 部分。  
  
> [!IMPORTANT]
>  在部分信任环境中运行应用程序时，如果未标记 <xref:System.Security.AllowPartiallyTrustedCallersAttribute> 属性 \(APTCA\) 的服务行为或终结点行为已添加到配置文件中的 [\<commonBehaviors\>](../../../../docs/framework/configure-apps/file-schema/wcf/commonbehaviors.md) 部分，则不会运行这些服务行为或终结点行为。在这种情况下，不会引发任何异常。  若要强制运行公共行为（如验证程序），必须执行以下任一操作：  
>   
>  \-\- 使用 <xref:System.Security.AllowPartiallyTrustedCallersAttribute> 属性标记公共行为，使其可在部署为部分信任应用程序时运行。  请注意，可以在计算机上设置注册表项，以防运行标有 APTCA 的程序集。  
>   
>  \-\- 确保如果应用程序是作为完全受信任的应用程序部署的，则用户不能修改代码访问安全设置，从而无法在部分信任环境中运行该应用程序。  如果用户可以这样做，则自定义验证程序不会运行，且不引发任何异常。  有关确保实现这种方式的一种方法，请参阅 `levelfinal` 选项（使用[代码访问安全策略工具 \(Caspol.exe\)](http://go.microsoft.com/fwlink/?LinkId=248222)）。  
>   
>  有关详细信息，请参阅[部分信任最佳实践](../../../../docs/framework/wcf/feature-details/partial-trust-best-practices.md)和[支持的部署方案](../../../../docs/framework/wcf/feature-details/supported-deployment-scenarios.md)。  
  
### 创建终结点验证程序  
  
1.  使用 <xref:System.ServiceModel.Description.IEndpointBehavior> 方法中所需的验证步骤创建一个 <xref:System.ServiceModel.Description.IEndpointBehavior.Validate%2A>。  下面的代码提供了一个示例。  （`InternetClientValidatorBehavior` 取自[安全性验证](../../../../docs/framework/wcf/samples/security-validation.md)示例。）  
  
     [!code-csharp[LockdownValidation#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/internetclientvalidatorbehavior.cs#2)]  
  
2.  创建用于注册步骤 1 中创建的终结点验证程序的新 <xref:System.ServiceModel.Configuration.BehaviorExtensionElement>。  下面的代码示例演示了此过程。  （此示例的原始代码包含在[安全性验证](../../../../docs/framework/wcf/samples/security-validation.md)示例中。）  
  
     [!code-csharp[LockdownValidation#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/internetclientvalidatorelement.cs#3)]  
  
3.  确保用强名称对编译的程序集签名。  有关详细信息，请参阅[强名称工具 \(SN.EXE\)](http://go.microsoft.com/fwlink/?LinkId=248217)和适用于你所用语言的编译器命令。  
  
### 将验证程序安装到目标计算机中  
  
1.  使用恰当的机制安装终结点验证程序。  在企业中，可以使用组策略和 Systems Management Server \(SMS\)。  
  
2.  使用 [Gacutil.exe（全局程序集缓存工具）](http://msdn.microsoft.com/library/ex0ss12c\(v=vs.110\).aspx)将强名称程序集安装到全局程序集缓存中。  
  
3.  使用 <xref:System.Configuration?displayProperty=fullName> 命名空间类型执行以下操作：  
  
    1.  使用完全限定的类型名称将扩展名添加到 [\<behaviorExtensions\>](../../../../docs/framework/configure-apps/file-schema/wcf/behaviorextensions.md) 节并锁定该元素。  
  
         [!code-csharp[LockdownValidation#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/hostapplication.cs#5)]  
  
    2.  将行为元素添加到 [\<commonBehaviors\>](../../../../docs/framework/configure-apps/file-schema/wcf/commonbehaviors.md) 节的 `EndpointBehaviors` 属性并锁定该元素。  （若要在服务上安装验证程序，该验证程序必须是 <xref:System.ServiceModel.Description.IServiceBehavior>，并已添加到 `ServiceBehaviors` 属性。） 下面的代码示例演示执行步骤 a.  和 b. 之后的适当配置，唯一例外是有没有强名称。  
  
         [!code-csharp[LockdownValidation#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/hostapplication.cs#6)]  
  
    3.  保存 machine.config 文件。  下面的代码示例执行步骤 3 中的所有任务，但在本地保存已修改的 machine.config 文件的副本。  
  
         [!code-csharp[LockdownValidation#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/hostapplication.cs#7)]  
  
## 示例  
 下面的代码示例演示如何将公共行为添加到 machine.config 文件并将副本保存到磁盘。  `InternetClientValidatorBehavior` 取自[安全性验证](../../../../docs/framework/wcf/samples/security-validation.md)示例。  
  
 [!code-csharp[LockdownValidation#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/lockdownvalidation/cs/hostapplication.cs#1)]  
  
## .NET Framework 安全性  
 您可能还需要对配置文件元素进行加密。  有关更多信息，请参见“另请参见”部分。  
  
## 请参阅  
 [使用 DPAPI 对配置文件元素进行加密](http://go.microsoft.com/fwlink/?LinkId=94954)   
 [使用 RSA 对配置文件元素进行加密](http://go.microsoft.com/fwlink/?LinkId=94955)