---
title: "自定义令牌处理程序"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5062669f-8bfc-420a-a25d-d8ab992ab10e
caps.latest.revision: 4
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: d471e860e74c9a01770c95671401bdbbc23643cb
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="custom-token-handlers"></a>自定义令牌处理程序
本主题讨论 WIF 中的令牌处理程序，以及如何使用它们处理令牌。 还介绍为 WIF 中默认不支持的令牌类型创建自定义令牌处理程序所需的内容。  
  
## <a name="introduction-to-token-handlers-in-wif"></a>WIF 中的令牌处理程序简介  
 WIF 依赖安全令牌处理程序为信赖方 (RP) 应用程序或安全令牌服务 (STS) 创建、读取、写入和验证令牌。 令牌处理程序是扩展点，用于在 WIF 管道中添加自定义令牌处理程序，或自定义现有令牌处理程序管理令牌的方式。 为了根据需要更改功能，WIF 提供九个可以修改或完全替代的内置安全令牌处理程序。  
  
## <a name="built-in-security-token-handlers-in-wif"></a>WIF 中的内置安全令牌处理程序  
 WIF 4.5 包括九个从抽象基类 <xref:System.IdentityModel.Tokens.SecurityTokenHandler> 派生的安全令牌处理程序类：  
  
-   <xref:System.IdentityModel.Tokens.EncryptedSecurityTokenHandler>  
  
-   <xref:System.IdentityModel.Tokens.KerberosSecurityTokenHandler>  
  
-   <xref:System.IdentityModel.Tokens.RsaSecurityTokenHandler>  
  
-   <xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler>  
  
-   <xref:System.IdentityModel.Tokens.Saml2SecurityTokenHandler>  
  
-   <xref:System.IdentityModel.Tokens.SessionSecurityTokenHandler>  
  
-   <xref:System.IdentityModel.Tokens.UserNameSecurityTokenHandler>  
  
-   <xref:System.IdentityModel.Tokens.WindowsUserNameSecurityTokenHandler>  
  
-   <xref:System.IdentityModel.Tokens.X509SecurityTokenHandler>  
  
## <a name="adding-a-custom-token-handler"></a>添加自定义令牌处理程序  
 一些令牌类型（例如，简单 Web 令牌 (SWT) 和 JSON Web 令牌 (JWT)）没有 WIF 提供的内置令牌处理程序。 对于这些令牌类型以及其他没有内置处理程序的令牌类型，必须执行以下步骤来创建自定义令牌处理程序。  
  
#### <a name="adding-a-custom-token-handler"></a>添加自定义令牌处理程序  
  
1.  创建一个从 <xref:System.IdentityModel.Tokens.SecurityTokenHandler> 派生的新类。  
  
2.  重写以下方法，提供自己的实现：  
  
    -   <xref:System.IdentityModel.Tokens.SecurityTokenHandler.CanReadToken%2A>  
  
    -   <xref:System.IdentityModel.Tokens.SecurityTokenHandler.ReadToken%2A>  
  
    -   <xref:System.IdentityModel.Tokens.SecurityTokenHandler.CanWriteToken%2A>  
  
    -   <xref:System.IdentityModel.Tokens.SecurityTokenHandler.WriteToken%2A>  
  
    -   <xref:System.IdentityModel.Tokens.SecurityTokenHandler.CanValidateToken%2A>  
  
    -   <xref:System.IdentityModel.Tokens.SecurityTokenHandler.ValidateToken%2A>  
  
3.  在应用于 WIF 的 \<system.identityModel> 部分内的 Web.config 或 App.config 文件中，添加对新自定义令牌处理程序的引用。 例如，以下配置标记指定了位于 CustomToken 命名空间中名为 MyCustomTokenHandler 的新令牌处理程序。  
  
    ```xml  
    <system.identityModel>  
        <identityConfiguration saveBootstrapContext="true">  
            <securityTokenHandlers>  
                <add type="CustomToken.MyCustomTokenHandler, CustomToken" />  
            </securityTokenHandlers>  
        </identityConfiguration>  
    </system.identityModel>  
    ```  
  
     请注意，如果提供自己的令牌处理程序来处理已有内置令牌处理程序的令牌类型，必须添加 \<remove> 元素，才能删除默认处理程序和改用自定义处理程序。 例如，以下配置将使用自定义令牌处理程序替换默认 <xref:System.IdentityModel.Tokens.SamlSecurityTokenHandler>：  
  
    ```xml  
    <system.identityModel>  
        <identityConfiguration saveBootstrapContext="true">  
            <securityTokenHandlers>  
                <remove type="System.IdentityModel.Tokens.SamlSecurityTokenHandler, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=abcdefg123456789">  
                <add type="CustomToken.MyCustomTokenHandler, CustomToken" />  
            </securityTokenHandlers>  
        </identityConfiguration>  
    </system.identityModel>  
    ```

