---
title: "如何：创建自定义授权策略 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 05b0549b-882d-4660-b6f0-5678543e5475
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# 如何：创建自定义授权策略
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 中的标识模型基础结构支持基于声明的授权模型。声明从令牌中提取，并可以选择由自定义授权策略进行处理，然后放入 <xref:System.IdentityModel.Policy.AuthorizationContext> 中，之后进行检查以做出授权决定。可以使用自定义策略将声明从传入令牌转换成应用程序需要的声明。这样，可以将应用程序层从 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 支持的不同令牌类型所提供的不同声明的详细信息中隔离出来。本主题演示如何实现自定义授权策略和如何将该策略添加到服务所使用的策略集中。  
  
### 实现自定义授权策略  
  
1.  定义一个从 <xref:System.IdentityModel.Policy.IAuthorizationPolicy> 中派生的新类。  
  
2.  实现只读 <xref:System.IdentityModel.Policy.IAuthorizationComponent.Id%2A> 属性，方法是在该类的构造函数中生成唯一字符串并在访问此属性时返回该字符串。  
  
3.  通过返回表示策略颁发者的 <xref:System.IdentityModel.Claims.ClaimSet>，实现只读 <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Issuer%2A> 属性。它可能是表示应用程序的 `ClaimSet`，也可能是内置的 `ClaimSet`（例如，由静态 <xref:System.IdentityModel.Claims.ClaimSet.System%2A> 属性返回的 `ClaimSet`）。  
  
4.  按照下面过程中的说明，实现 <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%28System.IdentityModel.Policy.EvaluationContext%2CSystem.Object%40%29> 方法。  
  
### 实现 Evaluate 方法  
  
1.  需要向此方法传递两个参数：<xref:System.IdentityModel.Policy.EvaluationContext> 类的一个实例和一个对象引用。  
  
2.  如果自定义授权策略添加 <xref:System.IdentityModel.Claims.ClaimSet> 实例，而不考虑 <xref:System.IdentityModel.Policy.EvaluationContext> 的当前内容，则通过调用 <xref:System.IdentityModel.Policy.EvaluationContext.AddClaimSet%28System.IdentityModel.Policy.IAuthorizationPolicy%2CSystem.IdentityModel.Claims.ClaimSet%29> 方法添加每个 `ClaimSet`，并从 <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%2A> 方法返回 `true`。返回 `true` 可向授权基础结构指示授权策略已执行其工作，不需要重新调用。  
  
3.  如果自定义授权策略仅在 `EvaluationContext` 中已经存在特定的声明时才添加声明集，则通过检查由 `ClaimSet` 属性返回的 <xref:System.IdentityModel.Policy.EvaluationContext.ClaimSets%2A> 实例，查找这些声明。如果声明已存在，则通过调用 <xref:System.IdentityModel.Policy.EvaluationContext.AddClaimSet%28System.IdentityModel.Policy.IAuthorizationPolicy%2CSystem.IdentityModel.Claims.ClaimSet%29> 方法添加新声明集，如果不再需要添加其他声明集，则返回 `true`，向授权基础结构指示授权策略已完成其工作。如果声明不存在，则返回 `false`，指示如果其他授权策略向 `EvaluationContext` 添加更多声明集，则应该重新调用授权策略。  
  
4.  对于更为复杂的处理方案，可以使用 <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%28System.IdentityModel.Policy.EvaluationContext%2CSystem.Object%40%29> 方法的第二个参数来存储一个状态变量，在对 <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%28System.IdentityModel.Policy.EvaluationContext%2CSystem.Object%40%29> 方法的每个后续调用过程中，授权基础结构均将传回该变量以便进行特定的评估。  
  
### 通过配置指定自定义授权策略  
  
1.  在 `serviceAuthorization` 元素的 `authorizationPolicies` 元素的 `add` 元素的 `policyType` 属性中指定自定义授权策略的类型。  
  
    ```  
    <configuration>  
     <system.serviceModel>  
      <behaviors>  
        <serviceAuthorization serviceAuthorizationManagerType=  
                  "Samples.MyServiceAuthorizationManager" >  
          <authorizationPolicies>         
            <add policyType="Samples.MyAuthorizationPolicy"  
          </authorizationPolicies>  
        </serviceAuthorization>  
      </behaviors>  
     </system.serviceModel>  
    </configuration>  
    ```  
  
### 通过代码指定自定义授权策略  
  
1.  创建 <xref:System.IdentityModel.Policy.IAuthorizationPolicy> 的一个 <xref:System.Collections.Generic.List%601>。  
  
2.  创建自定义授权策略的一个实例。  
  
3.  将该授权策略实例添加到列表中。  
  
4.  对每个自定义授权策略重复步骤 2 和 3。  
  
5.  将列表的一个只读版本分配给 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior.ExternalAuthorizationPolicies%2A> 属性。  
  
     [!code-csharp[c_CustomAuthPol#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customauthpol/cs/c_customauthpol.cs#8)]
     [!code-vb[c_CustomAuthPol#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customauthpol/vb/source.vb#8)]  
  
## 示例  
 下面的示例演示完整的 <xref:System.IdentityModel.Policy.IAuthorizationPolicy> 实现。  
  
 [!code-csharp[c_CustomAuthPol#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customauthpol/cs/c_customauthpol.cs#5)]
 [!code-vb[c_CustomAuthPol#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customauthpol/vb/source.vb#5)]  
  
## 请参阅  
 <xref:System.ServiceModel.ServiceAuthorizationManager>   
 [如何：比较声明](../../../../docs/framework/wcf/extending/how-to-compare-claims.md)   
 [如何：为服务创建自定义授权管理器](../../../../docs/framework/wcf/extending/how-to-create-a-custom-authorization-manager-for-a-service.md)   
 [授权策略](../../../../docs/framework/wcf/samples/authorization-policy.md)