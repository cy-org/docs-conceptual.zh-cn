---
title: "如何：转换传入声明"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2831d514-d9d8-4200-9192-954bb6da1126
caps.latest.revision: 4
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: bcf0e640e6b6b45ddb87070c7d6df2fa6dadc834
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="how-to-transform-incoming-claims"></a>如何：转换传入声明
## <a name="applies-to"></a>适用于  
  
-   Microsoft® Windows® Identity Foundation (WIF)  
  
-   ASP.NET® Web 窗体  
  
## <a name="summary"></a>摘要  
 本指南提供了创建简单的声明感知 ASP.NET Web 窗体应用程序和转换传入声明的详细分步过程。 它还提供关于如何测试应用程序的说明，以便验证当应用程序运行时是否呈现已转换声明。  
  
## <a name="contents"></a>内容  
  
-   目标  
  
-   概述  
  
-   步骤摘要  
  
-   步骤 1 – 创建简单的 ASP.NET Web 窗体应用程序  
  
-   步骤 2 – 使用自定义 ClaimsAuthenticationManager 实现声明转换  
  
-   步骤 3 - 测试你的解决方案  
  
## <a name="objectives"></a>目标  
  
-   配置 ASP.NET Web 窗体应用程序实现基于声明的身份验证  
  
-   通过添加管理员角色声明转换传入声明  
  
-   测试 ASP.NET Web 窗体应用程序，了解它是否正常工作  
  
## <a name="overview"></a>概述  
 WIF 公开名为 <xref:System.Security.Claims.ClaimsAuthenticationManager> 的类，使用户在声明呈现给信赖方 (RP) 应用程序之前能够进行修改。 <xref:System.Security.Claims.ClaimsAuthenticationManager> 可用于分离身份验证和基础应用程序代码之间的问题。 以下示例演示如何在传入的 <xref:System.Security.Claims.ClaimsPrincipal> 中向声明添加 RP 可能需要的角色。  
  
## <a name="summary-of-steps"></a>步骤摘要  
  
-   步骤 1 – 创建简单的 ASP.NET Web 窗体应用程序  
  
-   步骤 2 – 使用自定义 ClaimsAuthenticationManager 实现声明转换  
  
-   步骤 3 - 测试你的解决方案  
  
## <a name="step-1--create-a-simple-aspnet-web-forms-application"></a>步骤 1 – 创建简单的 ASP.NET Web 窗体应用程序  
 在此步骤中，将创建一个新的 ASP.NET Web 窗体应用程序。  
  
#### <a name="to-create-a-simple-aspnet-application"></a>创建一个简单 ASP.NET 应用程序  
  
1.  以管理员身份在提升模式下启动 Visual Studio。  
  
2.  在 Visual Studio 中，单击“文件”，再单击“新建”，然后单击“项目”。  
  
3.  在“新建项目”窗口中，单击“ASP.NET Web 窗体应用程序”。  
  
4.  在“名称”中，输入 `TestApp`，然后按“确定”。  
  
5.  在“解决方案资源管理器”下，右键单击“TestApp”项目，然后选择“标识和访问”。  
  
6.  “标识和访问”窗口随即出现。 在“提供程序”下，选择“使用本地开发 STS 测试应用程序”，然后单击“应用”。  
  
7.  在 Default.aspx 文件中，将现有标记替换为以下内容，然后保存文件：  
  
    ```  
    <%@ Page Title="Home Page" Language="C#" MasterPageFile="~/Site.Master" AutoEventWireup="true"  
        CodeBehind="Default.aspx.cs" Inherits="TestApp._Default" %>  
  
    <asp:Content runat="server" ID="BodyContent" ContentPlaceHolderID="MainContent">  
          <h3>Your Claims</h3>  
        <p>  
            <asp:GridView ID="ClaimsGridView" runat="server" CellPadding="3">  
                <AlternatingRowStyle BackColor="White" />  
                <HeaderStyle BackColor="#7AC0DA" ForeColor="White" />  
            </asp:GridView>  
        </p>  
    </asp:Content>  
    ```  
  
8.  打开名为 Default.aspx.cs 的代码隐藏文件。 用以下内容替换现有代码，然后保存文件：  
  
    ```csharp  
    using System;  
    using System.Web.UI;  
    using System.Security.Claims;  
  
    namespace TestApp  
    {  
        public partial class _Default : Page  
        {  
            protected void Page_Load(object sender, EventArgs e)  
            {  
                ClaimsPrincipal claimsPrincipal = Page.User as ClaimsPrincipal;  
                this.ClaimsGridView.DataSource = claimsPrincipal.Claims;  
                this.ClaimsGridView.DataBind();  
            }  
        }  
    }  
    ```  
  
## <a name="step-2--implement-claims-transformation-using-a-custom-claimsauthenticationmanager"></a>步骤 2 – 使用自定义 ClaimsAuthenticationManager 实现声明转换  
 此步骤将覆盖 <xref:System.Security.Claims.ClaimsAuthenticationManager> 类中的默认功能，向传入主体添加管理员角色。  
  
#### <a name="to-implement-claims-transformation-using-a-custom-claimsauthenticationmanager"></a>使用自定义 ClaimsAuthenticationManager 实现声明转换  
  
1.  在 Visual Studio 中，右键单击解决方案，单击“添加”，然后单击“新建项目”。  
  
2.  在“添加新建项目”窗口中从“Visual C#”模板列表选择“类库”，输入 `ClaimsTransformation`，然后按“确定”。 系统将在你的解决方案文件夹中创建新项目。  
  
3.  在“ClaimsTransformation”项目下右键单击“引用”，然后单击“添加引用”。  
  
4.  在“引用管理器”窗口选择“System.IdentityModel”，然后单击“确定”。  
  
5.  打开“Class1.cs”或若它不存在，右键单击“ClaimsTransformation”，再依次单击“添加”、“类…”  
  
6.  使用指令将以下内容添加到代码文件：  
  
    ```csharp  
    using System.Security.Claims;  
    using System.Security.Principal;  
    ```  
  
7.  在代码文件中添加以下类和方法。  
  
    > [!WARNING]
    >  以下代码仅用于演示目的；请确保验证了生产代码中的预期权限。  
  
    ```csharp  
    public class ClaimsTransformationModule : ClaimsAuthenticationManager  
    {  
        public override ClaimsPrincipal Authenticate(string resourceName, ClaimsPrincipal incomingPrincipal)  
        {  
            if (incomingPrincipal != null && incomingPrincipal.Identity.IsAuthenticated == true)  
            {  
               ((ClaimsIdentity)incomingPrincipal.Identity).AddClaim(new Claim(ClaimTypes.Role, "Admin"));  
            }  
  
            return incomingPrincipal;  
        }  
    }  
    ```  
  
8.  保存文件并生成 ClaimsTransformation 项目。  
  
9. 在 TestApp ASP.NET 项目中，右键单击“引用”，然后单击“添加引用”。  
  
10. 在“引用管理器”窗口中从左侧菜单选择“解决方案”，然后从填充选项中选择“ClaimsTransformation”，再单击“确定”。  
  
11. 在根目录 Web.config 文件中，导航到 \<system.identityModel> 条目。 在 \<identityConfiguration> 元素内，添加以下行并保存文件：  
  
    ```xml  
    <claimsAuthenticationManager type="ClaimsTransformation.ClaimsTransformationModule, ClaimsTransformation" />  
    ```  
  
## <a name="step-3--test-your-solution"></a>步骤 3 - 测试你的解决方案  
 此步骤中将测试 ASP.NET Web 窗体应用程序，并验证用户使用 Forms 身份验证登录时是否呈现声明。  
  
#### <a name="to-test-your-aspnet-web-forms-application-for-claims-using-forms-authentication"></a>为使用 Forms 身份验证的声明测试 ASP.NET Web 窗体应用程序  
  
1.  按 F5 生成并运行该应用程序。 将看到 Default.aspx。  
  
2.  在 Default.aspx 页，在“你的声明”标题下应看到一个表格，包括有关帐户的颁发者、原始颁发者、类型、值以及值类型声明信息。 最后一行应以下面的方式显示：  
  
    ||||||  
    |-|-|-|-|-|  
    |本地机构|本地机构|http://schemas.microsoft.com/ws/2008/06/identity/claims/role|管理|http://www.w3.org/2001/XMLSchema#string|

