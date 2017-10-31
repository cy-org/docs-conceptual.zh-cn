---
title: "如何：使用自定义用户名和密码验证程序 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WCF, 用户名和密码"
ms.assetid: 8e08b74b-fa44-4018-b63d-0d0805f85e3f
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# 如何：使用自定义用户名和密码验证程序
默认情况下，当用户名和密码用于身份验证时，[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 会使用 Windows 来验证用户名和密码。不过，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 允许自定义用户名和密码身份验证方案，也称为“验证程序”。若要合并自定义用户名和密码验证程序，请创建一个从 <xref:System.IdentityModel.Selectors.UserNamePasswordValidator> 派生的类，然后对其进行配置。  
  
 有关示例应用程序，请参见 [用户名密码验证程序](../../../../docs/framework/wcf/samples/user-name-password-validator.md)。  
  
### 创建自定义用户名和密码验证程序  
  
1.  创建一个从 <xref:System.IdentityModel.Selectors.UserNamePasswordValidator> 派生的类。  
  
     [!code-csharp[C_CustomUsernameAndPasswordValidator#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customusernameandpasswordvalidator/cs/service.cs#3)]
     [!code-vb[C_CustomUsernameAndPasswordValidator#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customusernameandpasswordvalidator/vb/service.vb#3)]  
  
2.  通过重写 <xref:System.IdentityModel.Selectors.UserNamePasswordValidator.Validate%2A> 方法，实现自定义身份验证方案。  
  
     请不要使用下面示例中的代码在生产环境中重写 <xref:System.IdentityModel.Selectors.UserNamePasswordValidator.Validate%2A> 方法。请将该代码替换为您的自定义用户名和密码验证方案，这可能会涉及到从数据库检索用户名和密码对。  
  
     若要将身份验证错误返回到客户端，应在 <xref:System.IdentityModel.Selectors.UserNamePasswordValidator.Validate%2A> 方法中引发 <xref:System.ServiceModel.FaultException>。  
  
     [!code-csharp[C_CustomUsernameAndPasswordValidator#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customusernameandpasswordvalidator/cs/service.cs#4)]
     [!code-vb[C_CustomUsernameAndPasswordValidator#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customusernameandpasswordvalidator/vb/service.vb#4)]  
  
### 配置服务以使用自定义用户名和密码验证程序  
  
1.  配置一个绑定，该绑定在任何传输上使用消息安全，或者在 HTTP\(S\) 上使用传输级安全。  
  
     使用消息安全时，应添加系统提供的绑定之一，如 [\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md)或支持消息安全和 `UserName` 凭据类型的 [\<customBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)。  
  
     在 HTTP\(S\) 上使用传输级安全时，应添加 [\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md)或 [\<basicHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md)，或添加使用 HTTP\(S\) 和 `Basic` 身份验证方案的 [\<netTcpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/nettcpbinding.md) 或 [\<customBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)。  
  
    > [!NOTE]
    >  使用 [!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)] 或更高版本时，可将自定义用户名和密码验证程序与消息和传输安全一起使用。使用 [!INCLUDE[vstecwinfx](../../../../includes/vstecwinfx-md.md)] 时，自定义用户名和密码验证程序只能与消息安全一起使用。  
  
    > [!TIP]
    >  有关在此上下文中使用 \<netTcpBinding\> 的更多信息，请参见 [\<安全性\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-nettcpbinding.md)。  
  
    1.  在配置文件中，在 [\<system.serviceModel\>](../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md) 元素下面添加一个 [\<绑定\>](../../../../docs/framework/configure-apps/file-schema/wcf/bindings.md) 元素。  
  
    2.  向该绑定节添加 [\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md) 或 [\<basicHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md) 元素。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]创建 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 绑定元素的更多信息，请参见[如何：在配置中指定服务绑定](../../../../docs/framework/wcf/how-to-specify-a-service-binding-in-configuration.md)。  
  
    3.  将 [\<安全性\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-wshttpbinding.md)或 [\<安全性\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-basichttpbinding.md) 的 `mode` 属性设置为 `Message`、`Transport` 或`TransportWithMessageCredential`。  
  
    4.  设置 [\<消息\>](../../../../docs/framework/configure-apps/file-schema/wcf/message-of-wshttpbinding.md) 或 [\<传输\>](../../../../docs/framework/configure-apps/file-schema/wcf/transport-of-wshttpbinding.md) 的 `clientCredentialType` 属性。  
  
         使用消息安全时，将 [\<消息\>](../../../../docs/framework/configure-apps/file-schema/wcf/message-of-wshttpbinding.md)的 `clientCredentialType` 属性设置为 `UserName`。  
  
         在 HTTP\(S\) 上使用传输级安全时，将 [\<传输\>](../../../../docs/framework/configure-apps/file-schema/wcf/transport-of-wshttpbinding.md) 或 [\<传输\>](../../../../docs/framework/configure-apps/file-schema/wcf/transport-of-basichttpbinding.md) 的 `clientCredentialType` 属性设置为 `Basic`。  
  
        > [!NOTE]
        >  如果使用传输级安全在 Internet 信息服务\(IIS\) 中承载 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务，并且将 <xref:System.ServiceModel.Security.UserNamePasswordServiceCredential.UserNamePasswordValidationMode%2A> 属性设置为 <xref:System.ServiceModel.Security.UserNamePasswordValidationMode>，则自定义身份验证方案会使用 Windows 身份验证的子集。这是因为在此情况下，IIS 会在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 调用自定义验证器之前执行 Windows 身份验证。  
  
     [!INCLUDE[crabout](../../../../includes/crabout-md.md)]创建 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 绑定元素的更多信息，请参见[如何：在配置中指定服务绑定](../../../../docs/framework/wcf/how-to-specify-a-service-binding-in-configuration.md)。  
  
     下面的示例显示绑定的配置代码。  
  
    ```  
    <system.serviceModel>   
      <bindings>  
      <wsHttpBinding>  
          <binding name="Binding1">  
            <security mode="Message">  
              <message clientCredentialType="UserName" />  
            </security>  
          </binding>          
        </wsHttpBinding>  
      </bindings>  
    </system.serviceModel>  
    ```  
  
2.  配置一个行为，该行为指定使用自定义用户名和密码验证程序来验证传入的 <xref:System.IdentityModel.Tokens.UserNameSecurityToken> 安全令牌的用户名和密码对。  
  
    1.  添加一个 [\<行为\>](../../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md) 元素，将其作为 [\<system.serviceModel\>](../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md) 元素的子级。  
  
    2.  向 [\<行为\>](../../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md) 元素中添加一个 [\<serviceBehaviors\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicebehaviors.md)。  
  
    3.  添加一个 [\<行为\>](../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-servicebehaviors.md) 元素，并将 `name` 属性设置为适当的值。  
  
    4.  向 [\<行为\>](../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-servicebehaviors.md) 元素中添加一个 [\<serviceCredentials\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md)。  
  
    5.  向 [\<serviceCredentials\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md)中添加一个 [\<userNameAuthentication\>](../../../../docs/framework/configure-apps/file-schema/wcf/usernameauthentication.md)。  
  
    6.  将 `userNamePasswordValidationMode` 设置为 `Custom`。  
  
        > [!IMPORTANT]
        >  如果未设置 `userNamePasswordValidationMode` 值，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 会使用 Windows 身份验证而不是自定义用户名和密码验证程序。  
  
    7.  将 `customUserNamePasswordValidatorType` 设置为表示自定义用户名和密码验证程序的类型。  
  
     下面的示例演示至此为止的 `<serviceCredentials>` 片段。  
  
    ```  
    <serviceCredentials>  
      <userNameAuthentication userNamePasswordValidationMode="Custom" customUserNamePasswordValidatorType="Microsoft.ServiceModel.Samples.CalculatorService.CustomUserNameValidator, service" />  
    </serviceCredentials>  
    ```  
  
## 示例  
 下面的代码示例演示如何创建自定义用户名和密码验证程序。请不要使用代码重写生产环境中的 <xref:System.IdentityModel.Selectors.UserNamePasswordValidator.Validate%2A> 方法。请将该代码替换为您的自定义用户名和密码验证方案，这可能会涉及到从数据库检索用户名和密码对。  
  
 [!code-csharp[C_CustomUsernameAndPasswordValidator#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customusernameandpasswordvalidator/cs/service.cs#1)]
 [!code-vb[C_CustomUsernameAndPasswordValidator#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customusernameandpasswordvalidator/vb/service.vb#1)]  
[!code-csharp[C_CustomUsernameAndPasswordValidator#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customusernameandpasswordvalidator/cs/service.cs#2)]
[!code-vb[C_CustomUsernameAndPasswordValidator#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customusernameandpasswordvalidator/vb/service.vb#2)]  
  
## 请参阅  
 <xref:System.IdentityModel.Selectors.UserNamePasswordValidator>   
 [如何：使用 ASP.NET 成员资格提供程序](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-membership-provider.md)   
 [身份验证](../../../../docs/framework/wcf/feature-details/authentication-in-wcf.md)