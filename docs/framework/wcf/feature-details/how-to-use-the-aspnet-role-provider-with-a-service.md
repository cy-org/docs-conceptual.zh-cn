---
title: "如何：将 ASP.NET 角色提供程序与服务一起使用 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 88d33a81-8ac7-48de-978c-5c5b1257951e
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 如何：将 ASP.NET 角色提供程序与服务一起使用
[!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 角色提供程序（与 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 成员资格提供程序一起提供）是一种可供 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 开发人员创建网站的功能，这些网站允许用户通过网站创建帐户并向用户分配用于授权的角色。借助此功能，任何用户都可以通过网站建立帐户，并登录以获取该网站及其服务的独占访问权。这与要求用户在 Windows 域中具有帐户的 Windows 安全完全不同。所有提供凭据（用户名\/密码组合）的用户都可以使用该站点及其服务。  
  
 有关示例应用程序，请参见[成员资格和角色提供程序](../../../../docs/framework/wcf/samples/membership-and-role-provider.md)。[!INCLUDE[crabout](../../../../includes/crabout-md.md)][!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 成员资格提供程序功能的更多信息，请参见[如何：使用 ASP.NET 成员资格提供程序](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-membership-provider.md)。  
  
 角色提供程序功能使用 SQL Server 数据库存储用户信息。[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 开发人员可以出于安全目的利用这些功能。当集成到 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序中时，用户必须向 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端应用程序提供用户名\/密码组合。若要让 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 使用该数据库，您必须创建 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior> 类的一个实例，将其 <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior.PrincipalPermissionMode%2A> 属性设置为 <xref:System.ServiceModel.Description.PrincipalPermissionMode>，并将行为集合的实例添加到承载服务的 <xref:System.ServiceModel.ServiceHost> 中。  
  
### 配置角色提供程序  
  
1.  在 Web.config 文件中的 \<`system.web`\> 元素下，添加 \<`roleManager`\> 元素，并将其 `enabled` 属性设置为 `true`。  
  
2.  将 `defaultProvider` 属性设置为 `SqlRoleProvider`。  
  
3.  添加一个 \<`providers`\> 元素，将其作为 \<`roleManager`\> 元素的子级。  
  
4.  按照下面的示例所示，添加 \<`add`\> 元素（其 `name`、`type`、`connectionStringName` 和 `applicationName` 属性设置为相应的值），将其作为 \<`providers`\> 元素的子级。  
  
    ```  
    <!-- Configure the Sql Role Provider. -->  
    <roleManager enabled ="true"   
     defaultProvider ="SqlRoleProvider" >  
       <providers>  
         <add name ="SqlRoleProvider"   
           type="System.Web.Security.SqlRoleProvider"   
           connectionStringName="SqlConn"   
           applicationName="MembershipAndRoleProviderSample"/>  
       </providers>  
    </roleManager>  
    ```  
  
### 将服务配置为使用角色提供程序  
  
1.  在 Web.config 文件中，添加 [\<system.serviceModel\>](../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md) 元素。  
  
2.  向 \<`system.ServiceModel`\> 元素中添加一个 [\<行为\>](../../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md) 元素。  
  
3.  向 \<`behaviors`\> 元素中添加一个 [\<serviceBehaviors\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicebehaviors.md)。  
  
4.  添加 [\<行为\>](../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md) 元素并将 `name` 属性设置为适当的值。  
  
5.  向 \<`behavior`\> 元素中添加一个 [\<serviceAuthorization\>](../../../../docs/framework/configure-apps/file-schema/wcf/serviceauthorization-element.md)。  
  
6.  将 `principalPermissionMode` 属性设置为 `UseAspNetRoles`。  
  
7.  将 `roleProviderName` 属性设置为 `SqlRoleProvider`。下面的示例演示此配置的一个片段。  
  
    ```  
    <behaviors>  
     <serviceBehaviors>  
      <behavior name="CalculatorServiceBehavior">  
       <serviceAuthorization principalPermissionMode ="UseAspNetRoles"  
                             roleProviderName ="SqlRoleProvider" />  
      </behavior>  
     </serviceBehaviors>  
    </behaviors>  
    ```  
  
## 请参阅  
 [成员资格和角色提供程序](../../../../docs/framework/wcf/samples/membership-and-role-provider.md)   
 [如何：使用 ASP.NET 成员资格提供程序](../../../../docs/framework/wcf/feature-details/how-to-use-the-aspnet-membership-provider.md)