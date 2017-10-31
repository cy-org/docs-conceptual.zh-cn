---
title: "如何：为服务创建自定义授权管理器 | Microsoft Docs"
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
  - "OperationRequirement 类"
  - "Windows Communication Foundation, 扩展"
ms.assetid: 6214afde-44c1-4bf5-ba07-5ad6493620ea
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# 如何：为服务创建自定义授权管理器
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 中的标识模型基础结构支持基于声明的可扩展授权模型。声明是从令牌中提取的，自定义授权策略将有选择地对其进行处理，然后放入 <xref:System.IdentityModel.Policy.AuthorizationContext> 中。授权管理器检查 <xref:System.IdentityModel.Policy.AuthorizationContext> 中的声明，从而作出授权决策。  
  
 默认情况下，授权决策由 <xref:System.ServiceModel.ServiceAuthorizationManager> 类作出；但是，可通过创建自定义授权管理器来覆盖这些决策。若要创建自定义授权管理器，请创建一个从 <xref:System.ServiceModel.ServiceAuthorizationManager> 派生的类，并实现 <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccessCore%2A> 方法。授权决策是在 <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccessCore%2A> 方法中作出的，如果允许访问，该方法返回 `true`，如果拒绝访问，则返回 `false`。  
  
 如果授权决策取决于消息正文的内容，请使用 <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccess%2A> 方法。  
  
 由于性能问题，如有可能，应重新设计应用程序，使授权决策不需要访问消息正文。  
  
 在代码或配置中，可以进行服务的自定义授权管理器注册。  
  
### 创建自定义授权管理器  
  
1.  从 <xref:System.ServiceModel.ServiceAuthorizationManager> 类派生一个类。  
  
     [!code-csharp[c_CustomAuthMgr#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customauthmgr/cs/c_customauthmgr.cs#5)]
     [!code-vb[c_CustomAuthMgr#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customauthmgr/vb/c_customauthmgr.vb#5)]  
  
2.  重写 <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccessCore%28System.ServiceModel.OperationContext%29> 方法。  
  
     使用传给 <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccessCore%28System.ServiceModel.OperationContext%29> 方法的 <xref:System.ServiceModel.OperationContext> 进行授权决策。  
  
     下面的代码示例使用 <xref:System.IdentityModel.Claims.ClaimSet.FindClaims%28System.String%2CSystem.String%29> 方法查找自定义声明 `http://www.contoso.com/claims/allowedoperation`，从而做出授权决策。  
  
     [!code-csharp[c_CustomAuthMgr#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customauthmgr/cs/c_customauthmgr.cs#6)]
     [!code-vb[c_CustomAuthMgr#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customauthmgr/vb/c_customauthmgr.vb#6)]  
  
### 使用代码注册自定义授权管理器  
  
1.  创建自定义授权管理器的一个实例，然后将其分配给 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior.ServiceAuthorizationManager%2A> 属性。  
  
     使用 <xref:System.ServiceModel.ServiceHostBase.Authorization%2A> 属性可以访问 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior>。  
  
     下面的代码示例注册 `MyServiceAuthorizationManager` 自定义授权管理器。  
  
     [!code-csharp[c_CustomAuthMgr#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customauthmgr/cs/c_customauthmgr.cs#4)]
     [!code-vb[c_CustomAuthMgr#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customauthmgr/vb/c_customauthmgr.vb#4)]  
  
### 使用配置注册自定义授权管理器  
  
1.  打开服务的配置文件。  
  
2.  将一个 [\<serviceAuthorization\>](../../../../docs/framework/configure-apps/file-schema/wcf/serviceauthorization-element.md)添加到 [\<行为\>](../../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md)中。  
  
     在 [\<serviceAuthorization\>](../../../../docs/framework/configure-apps/file-schema/wcf/serviceauthorization-element.md)中，添加一个 `serviceAuthorizationManagerType` 属性，并将其值设置为表示自定义授权管理器的类型。  
  
3.  添加一个保护客户端和服务之间的通信的绑定。  
  
     为此通信选择的绑定决定了添加到 <xref:System.IdentityModel.Policy.AuthorizationContext> 的声明，自定义授权管理器使用这些声明来进行授权决策。有关系统提供的绑定的更多信息，请参见[系统提供的绑定](../../../../docs/framework/wcf/system-provided-bindings.md)。  
  
4.  将行为与服务终结点关联，具体方法是，添加一个 [\<service\>](../../../../docs/framework/configure-apps/file-schema/wcf/service.md) 元素，并将 `behaviorConfiguration` 属性的值设置为 [\<行为\>](../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-servicebehaviors.md) 元素的名称属性的值。  
  
     有关配置服务终结点的更多信息，请参见[如何：在配置中创建服务终结点](../../../../docs/framework/wcf/feature-details/how-to-create-a-service-endpoint-in-configuration.md)。  
  
     下面的代码示例注册自定义授权管理器 `Samples.MyServiceAuthorizationManager`。  
  
    ```  
    <configuration>  
      <system.serviceModel>  
        <services>  
          <service   
              name="Microsoft.ServiceModel.Samples.CalculatorService"  
              behaviorConfiguration="CalculatorServiceBehavior">  
            <host>  
              <baseAddresses>  
                <add baseAddress="http://localhost:8000/ServiceModelSamples/service"/>  
              </baseAddresses>  
            </host>  
            <endpoint address=""  
                      binding="wsHttpBinding_Calculator"  
                      contract="Microsoft.ServiceModel.Samples.ICalculator" />  
          </service>  
        </services>  
        <bindings>  
          <WSHttpBinding>  
           <binding name = "wsHttpBinding_Calculator">  
             <security mode="Message">  
               <message clientCredentialType="Windows"/>  
             </security>  
            </binding>  
          </WSHttpBinding>  
    </bindings>  
        <behaviors>  
          <serviceBehaviors>  
            <behavior name="CalculatorServiceBehavior">  
              <serviceAuthorization serviceAuthorizationManagerType="Samples.MyServiceAuthorizationManager,MyAssembly" />  
             </behavior>  
         </serviceBehaviors>  
       </behaviors>  
      </system.serviceModel>  
    </configuration>  
    ```  
  
    > [!WARNING]
    >  请注意，当您指定了 serviceAuthorizationManagerType 后，字符串必须包含完全限定的类型名称。一个逗号，以及在其中定义类型的程序集的名称。如果你忽略了程序集的名称，WCF 会尝试从 System.ServiceModel.dll 加载类型。  
  
## 示例  
 下面的代码示例演示 <xref:System.ServiceModel.ServiceAuthorizationManager> 类的一个基本实现，包括重写 <xref:System.ServiceModel.ServiceAuthorizationManager.CheckAccessCore%2A> 方法。该示例代码检查某个自定义声明的 <xref:System.IdentityModel.Policy.AuthorizationContext>，如果该自定义声明的资源与 <xref:System.ServiceModel.OperationContext> 中的操作值匹配，则返回 `true`。有关 <xref:System.ServiceModel.ServiceAuthorizationManager> 类的更完整实现，请参见[授权策略](../../../../docs/framework/wcf/samples/authorization-policy.md)。  
  
 [!code-csharp[c_CustomAuthMgr#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customauthmgr/cs/c_customauthmgr.cs#2)]
 [!code-vb[c_CustomAuthMgr#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customauthmgr/vb/c_customauthmgr.vb#2)]  
  
## 请参阅  
 <xref:System.ServiceModel.ServiceAuthorizationManager>   
 [授权策略](../../../../docs/framework/wcf/samples/authorization-policy.md)   
 [授权策略](../../../../docs/framework/wcf/samples/authorization-policy.md)