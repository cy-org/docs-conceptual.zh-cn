---
title: "如何：创建使用自定义证书验证程序的服务 | Microsoft Docs"
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
  - "WCF, Authentication — 身份验证"
ms.assetid: bb0190ff-0738-4e54-8d22-c97d343708bf
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# 如何：创建使用自定义证书验证程序的服务
本主题介绍如何实现自定义证书验证程序，以及如何配置客户端或服务凭据以使用自定义证书验证程序替换默认证书验证逻辑。  
  
 如果使用 X.509 证书对客户端或服务进行身份验证，则默认情况下，[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 使用 Windows 证书存储区和加密 API 来验证该证书并确保它是受信任的。  有时，内置证书验证功能并不足够且必须更改。  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 提供了一种简单的方法，允许用户添加自定义证书验证程序来更改验证逻辑。  如果指定了自定义证书验证程序，则 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 不使用内置证书验证逻辑，而是依靠自定义验证程序。  
  
## 过程  
  
#### 创建自定义证书验证程序  
  
1.  定义一个从 <xref:System.IdentityModel.Selectors.X509CertificateValidator> 派生的新类。  
  
2.  实现抽象 <xref:System.IdentityModel.Selectors.X509CertificateValidator.Validate%2A> 方法。  将必须验证的证书作为参数传递给该方法。  如果根据验证逻辑，传递的证书无效，则此方法引发 <xref:System.IdentityModel.Tokens.SecurityTokenValidationException>。  如果证书有效，则此方法返回到调用方。  
  
    > [!NOTE]
    >  若要将身份验证错误返回到客户端，应在 <xref:System.IdentityModel.Selectors.UserNamePasswordValidator.Validate%2A> 方法中引发 <xref:System.ServiceModel.FaultException>。  
  
 [!code-csharp[c_CustomCertificateValidator#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customcertificatevalidator/cs/source.cs#2)]
 [!code-vb[c_CustomCertificateValidator#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customcertificatevalidator/vb/source.vb#2)]  
  
#### 指定服务配置中的自定义证书验证程序  
  
1.  向 [\<system.serviceModel\>](../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md) 元素添加一个 [\<行为\>](../../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md) 元素和一个 [\<serviceBehaviors\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicebehaviors.md)。  
  
2.  添加一个 [\<行为\>](../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)并将 `name` 属性设置为适当的值。  
  
3.  向 `<behavior>` 元素中添加一个 [\<serviceCredentials\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecredentials.md)。  
  
4.  向 `<serviceCredentials>` 元素中添加一个 `<clientCertificate>` 元素。  
  
5.  向 `<clientCertificate>` 元素添加一个 [\<authentication\>](../../../../docs/framework/configure-apps/file-schema/wcf/authentication-of-clientcertificate-element.md)。  
  
6.  将 `customCertificateValidatorType` 属性设置为验证程序类型。  下面的示例将该属性设置为类型的命名空间和名称。  
  
7.  将 `certificateValidationMode` 属性设置为 `Custom`。  
  
    ```  
    <configuration>  
     <system.serviceModel>  
      <behaviors>  
       <serviceBehaviors>  
        <behavior name="ServiceBehavior">  
         <serviceCredentials>  
          <clientCertificate>  
          <authentication certificateValidationMode="Custom" customCertificateValidatorType="Samples.MyValidator, service" />  
          </clientCertificate>  
         </serviceCredentials>  
        </behavior>  
       </serviceBehaviors>  
      </behaviors>  
    </system.serviceModel>  
    </configuration>  
    ```  
  
#### 使用客户端上的配置指定自定义证书验证程序  
  
1.  向 [\<system.serviceModel\>](../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md) 元素添加一个 [\<行为\>](../../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md) 元素和一个 [\<serviceBehaviors\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicebehaviors.md)。  
  
2.  添加一个 [\<endpointBehaviors\>](../../../../docs/framework/configure-apps/file-schema/wcf/endpointbehaviors.md) 元素。  
  
3.  添加一个 `<behavior>` 元素，并将 `name` 属性设置为适当的值。  
  
4.  添加一个 [\<clientCredentials\>](../../../../docs/framework/configure-apps/file-schema/wcf/clientcredentials.md) 元素。  
  
5.  添加一个 [\<serviceCertificate\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicecertificate-of-clientcredentials-element.md)。  
  
6.  添加一个 [\<Authentication — 身份验证\>](../../../../docs/framework/configure-apps/file-schema/wcf/authentication-of-servicecertificate-element.md)，如下面的示例所示。  
  
7.  将 `customCertificateValidatorType` 属性设置为验证程序类型。  
  
8.  将 `certificateValidationMode` 属性设置为 `Custom`。  下面的示例将该属性设置为类型的命名空间和名称。  
  
    ```  
    <configuration>  
     <system.serviceModel>  
      <behaviors>  
       <endpointBehaviors>  
        <behavior name="clientBehavior">  
         <clientCredentials>  
          <serviceCertificate>  
           <authentication certificateValidationMode="Custom"   
                  customCertificateValidatorType=  
             "Samples.CustomX509CertificateValidator, client"/>  
          </serviceCertificate>  
         </clientCredentials>  
        </behavior>  
       </endpointBehaviors>  
      </behaviors>  
     </system.serviceModel>  
    </configuration>  
    ```  
  
#### 使用服务上的代码指定自定义证书验证程序  
  
1.  指定 <xref:System.ServiceModel.Description.ServiceCredentials.ClientCertificate%2A> 属性的自定义证书验证程序。  您可以使用 <xref:System.ServiceModel.ServiceHostBase.Credentials%2A> 属性访问服务凭据。  
  
2.  将 <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication.CertificateValidationMode%2A> 属性设置为 <xref:System.ServiceModel.Security.X509CertificateValidationMode>。  
  
 [!code-csharp[c_CustomCertificateValidator#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customcertificatevalidator/cs/source.cs#1)]
 [!code-vb[c_CustomCertificateValidator#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customcertificatevalidator/vb/source.vb#1)]  
  
#### 使用客户端上的代码指定自定义证书验证程序  
  
1.  使用 <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication.CustomCertificateValidator%2A> 属性指定自定义证书验证程序。  您可以使用 <xref:System.ServiceModel.ServiceHostBase.Credentials%2A> 属性访问客户端凭据。  （由 [ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 生成的客户端类始终是从 <xref:System.ServiceModel.ClientBase%601> 类派生而来的。）  
  
2.  将 <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication.CertificateValidationMode%2A> 属性设置为 <xref:System.ServiceModel.Security.X509CertificateValidationMode>。  
  
## 示例  
  
### 描述  
 下面的示例演示自定义证书验证程序的实现及其在服务上的用法。  
  
### 代码  
 [!code-csharp[c_CustomCertificateValidator#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customcertificatevalidator/cs/source.cs#3)]
 [!code-vb[c_CustomCertificateValidator#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customcertificatevalidator/vb/source.vb#3)]  
  
## 请参阅  
 <xref:System.IdentityModel.Selectors.X509CertificateValidator>