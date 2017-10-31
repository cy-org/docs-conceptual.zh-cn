---
title: "如何：使用 WIF 生成声明感知 ASP.NET Web 窗体应用程序"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: efb264dd-f47b-49a9-85ee-9f45d4425765
caps.latest.revision: 7
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: d5b81e20ed1b39c7750329718729905484eb7fa1
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="how-to-build-claims-aware-aspnet-web-forms-application-using-wif"></a>如何：使用 WIF 生成声明感知 ASP.NET Web 窗体应用程序
## <a name="applies-to"></a>适用于  
  
-   Microsoft® Windows® Identity Foundation (WIF)  
  
-   ASP.NET® Web 窗体  
  
## <a name="summary"></a>摘要  
 本操作说明提供了创建简单的声明感知 ASP.NET Web 窗体应用程序的详细分步过程。 还提供关于如何测试简单声明感知 ASP.NET Web 窗体应用程序以确保成功实现联合身份验证的说明。 本操作说明不包括如何创建安全令牌服务 (STS) 的详细说明，且假定你已配置 STS。  
  
## <a name="contents"></a>内容  
  
-   目标  
  
-   步骤摘要  
  
-   步骤 1 – 创建简单的 ASP.NET Web 窗体应用程序  
  
-   第 2 步 – 为基于声明的身份验证配置 ASP.NET Web 窗体应用程序  
  
-   步骤 3 - 测试你的解决方案  
  
## <a name="objectives"></a>目标  
  
-   为基于声明的身份验证配置 ASP.NET Web 窗体应用程序  
  
-   测试成功的声明感知 ASP.NET Web 窗体应用程序  
  
## <a name="summary-of-steps"></a>步骤摘要  
  
-   步骤 1 – 创建简单的 ASP.NET Web 窗体应用程序  
  
-   步骤 2 – 为联合身份验证配置 ASP.NET Web 窗体应用程序  
  
-   步骤 3 - 测试你的解决方案  
  
## <a name="step-1--create-a-simple-aspnet-web-forms-application"></a>步骤 1 – 创建简单的 ASP.NET Web 窗体应用程序  
 在此步骤中，将创建一个新的 ASP.NET Web 窗体应用程序。  
  
#### <a name="to-create-a-simple-aspnet-application"></a>创建一个简单 ASP.NET 应用程序  
  
1.  启动 Visual Studio，然后依次单击“文件”、“新建”和“项目”。  
  
2.  在“新建项目”窗口中，单击“ASP.NET Web 窗体应用程序”。  
  
3.  在“名称”中，输入 `TestApp`，然后按“确定”。  
  
## <a name="step-2--configure-aspnet-web-forms-application-for-claims-based-authentication"></a>第 2 步 – 为基于声明的身份验证配置 ASP.NET Web 窗体应用程序  
 在此步骤中，将配置条目添加到 ASP.NET Web 窗体应用程序的 Web.config 配置文件中，以使其可感知声明。  
  
#### <a name="to-configure-aspnet-application-for-claims-based-authentication"></a>为基于声明的身份验证配置 ASP.NET Web 应用程序  
  
1.  将以下配置节条目紧随添加到 Web.config 配置文件中的 \<configuration> 起始元素后：  
  
    ```xml  
    <configSections>  
      <section name="system.identityModel" type="System.IdentityModel.Configuration.SystemIdentityModelSection, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089" />  
      <section name="system.identityModel.services" type="System.IdentityModel.Services.Configuration.SystemIdentityModelServicesSection, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=B77A5C561934E089" />  
    </configSections>  
    ```  
  
2.  添加 \<location> 元素，用于启用对应用程序的联合元数据的访问权限：  
  
    ```xml  
    <location path="FederationMetadata">  
      <system.web>  
        <authorization>  
          <allow users="*" />  
        </authorization>  
      </system.web>  
    </location>  
    ```  
  
3.  在 \<system.web> 元素内添加以下配置条目以拒绝用户、禁用本机身份验证并启用 WIF 来管理身份验证。  
  
    ```xml  
    <authorization>  
      <deny users="?" />  
    </authorization>  
    <authentication mode="None" />  
    ```  
  
4.  添加 \<system.webServer> 元素，用于为联合身份验证定义模块。 请注意，PublicKeyToken 特性必须与之前为 \<configSections > 条目添加的 PublicKeyToken 特性相同：  
  
    ```xml  
    <system.webServer>  
      <modules>  
        <add name="WSFederationAuthenticationModule" type="System.IdentityModel.Services.WSFederationAuthenticationModule, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" preCondition="managedHandler" />  
        <add name="SessionAuthenticationModule" type="System.IdentityModel.Services.SessionAuthenticationModule, System.IdentityModel.Services, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" preCondition="managedHandler" />  
      </modules>  
    </system.webServer>  
    ```  
  
5.  添加以下 Windows Identity Foundation 相关配置条目，并确保 ASP.NET 应用程序的 URL 和端口号与 \<audienceUris> 条目、\<wsFederation> 元素的“realm”特性和 \<wsFederation> 元素的“reply”特性中的值相匹配。 还需确保“issuer”值与安全令牌服务 (STS) URL 相适应。  
  
    ```xml  
    <system.identityModel>  
        <identityConfiguration>  
            <audienceUris>  
                <add value="http://localhost:28503/" />  
            </audienceUris>  
            <issuerNameRegistry type="System.IdentityModel.Tokens.ConfigurationBasedIssuerNameRegistry, System.IdentityModel, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089">  
                <trustedIssuers>  
                    <add thumbprint="1234567890ABCDEFGHIJKLMNOPQRSTUVWXYZ1234" name="YourSTSName" />  
                </trustedIssuers>   
            </issuerNameRegistry>  
            <certificateValidation certificateValidationMode="None" />  
        </identityConfiguration>  
    </system.identityModel>  
    <system.identityModel.services>  
        <federationConfiguration>  
            <cookieHandler requireSsl="false" />  
            <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:13922/wsFederationSTS/Issue" realm="http://localhost:28503/" reply="http://localhost:28503/" requireHttps="false" />  
        </federationConfiguration>  
    </system.identityModel.services>  
    ```  
  
6.  将引用添加到 <xref:System.IdentityModel> 程序集。  
  
7.  编译此解决方案，确保没有任何错误。  
  
## <a name="step-3--test-your-solution"></a>步骤 3 - 测试你的解决方案  
 在此步骤中，将测试为基于声明的身份验证配置的 ASP.NET Web 窗体应用程序。 若要执行基本测试，需添加用于在安全令牌服务 (STS) 颁发的令牌中显示声明的代码。  
  
#### <a name="to-test-your-aspnet-web-form-application-for-claims-based-authentication"></a>为基于声明的身份验证测试 ASP.NET Web 窗体应用程序  
  
1.  打开 TestApp 项目下的 Default.aspx 文件，并将现有标记替换为以下标记：  
  
    ```  
    %@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>  
  
    <!DOCTYPE html>  
  
    <html>  
    <head id="Head1" runat="server">  
        <title></title>  
    </head>  
    <body>  
        <h1><asp:label ID="signedIn" runat="server" /></h1>  
        <asp:label ID="claimType" runat="server" />  
        <asp:label ID="claimValue" runat="server" />  
        <asp:label ID="claimValueType" runat="server" />  
        <asp:label ID="claimSubjectName" runat="server" />  
        <asp:label ID="claimIssuer" runat="server" />  
    </body>  
    </html>  
    ```  
  
2.  保存 Default.aspx 文件，然后打开名为 Default.aspx.cs 的代码隐藏文件。  
  
    > [!NOTE]
    >  在解决方案资源管理器中，Default.aspx.cs 文件可能隐藏在 Default.aspx 文件下。 如果 Default.aspx.cs 文件不可见，请单击文件旁边的三角形，展开 Default.aspx。  
  
3.  将 Default.aspx.cs 的 Page_Load 方法中的现有代码替换为以下代码：  
  
    ```csharp  
    using System;  
    using System.IdentityModel;  
    using System.Security.Claims;  
    using System.Threading;  
    using System.Web.UI;  
  
    namespace TestApp  
    {  
        public partial class _Default : System.Web.UI.Page  
        {  
            protected void Page_Load(object sender, EventArgs e)  
            {  
                ClaimsPrincipal claimsPrincipal = Thread.CurrentPrincipal as ClaimsPrincipal;  
  
                if (claimsPrincipal != null)  
                {  
                    signedIn.Text = "You are signed in.";  
  
                    foreach (Claim claim in claimsPrincipal.Claims)  
                    {  
                        claimType.Text = claim.Type;  
                        claimValue.Text = claim.Value;  
                        claimValueType.Text = claim.ValueType;  
                        claimSubjectName.Text = claim.Subject.Name;  
                        claimIssuer.Text = claim.Issuer;  
                    }  
                }  
                else  
                {  
                    signedIn.Text = "You are not signed in.";  
                }  
            }  
        }  
    }  
    ```  
  
4.  保存 Default.aspx.cs，并生成解决方案。  
  
5.  按 F5 键运行解决方案。  
  
6.  应当会看到在安全令牌服务颁发给你的令牌中显示声明的页面。

