---
title: "如何：使用基于表单的身份验证生成声明感知 ASP.NET 应用程序"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 98a3e029-1a9b-4e0c-b5d0-29d3f23f5b15
caps.latest.revision: 6
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 987157bc3663330d9c610c1016787890e9dc6137
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="how-to-build-claims-aware-aspnet-application-using-forms-based-authentication"></a>如何：使用基于表单的身份验证生成声明感知 ASP.NET 应用程序
## <a name="applies-to"></a>适用于  
  
-   Microsoft® Windows® Identity Foundation (WIF)  
  
-   ASP.NET® Web 窗体  
  
## <a name="summary"></a>摘要  
 本操作说明提供了创建使用 Forms 身份验证的简单声明感知 ASP.NET Web 窗体应用程序的详细分步程序。 它还提供关于如何测试应用程序以验证用户使用 Forms 身份验证登录时是否呈现声明的说明。  
  
## <a name="contents"></a>内容  
  
-   目标  
  
-   概述  
  
-   步骤摘要  
  
-   步骤 1 – 创建简单的 ASP.NET Web 窗体应用程序  
  
-   步骤 2 – 为使用 Forms 身份验证的声明配置 ASP.NET Web 窗体应用程序  
  
-   步骤 3 - 测试你的解决方案  
  
## <a name="objectives"></a>目标  
  
-   为使用 Forms 身份验证的声明配置 ASP.NET Web 窗体应用程序  
  
-   测试 ASP.NET Web 窗体应用程序，了解它是否正常工作  
  
## <a name="overview"></a>概述  
 在 .NET 4.5 中，已将 WIF 及其基于声明的授权作为 Framework 的重要组成部分包括在内。 以前，如果想要来自 ASP.NET 用户的声明，需要安装 WIF，然后将接口转换为如 `Thread.CurrentPrincipal` 或 `HttpContext.Current.User` 的主体对象。 现在，声明由这些主体对象自动提供。  
  
 Forms 身份验证已因包括在 .NET 4.5 中而获益，因为所有通过窗体进行身份验证的用户都自动具有与他们相关的声明。 如本操作说明所示，可在使用 Forms 身份验证的 ASP.NET 应用程序中立即开始使用这些声明。  
  
## <a name="summary-of-steps"></a>步骤摘要  
  
-   步骤 1 – 创建简单的 ASP.NET Web 窗体应用程序  
  
-   步骤 2 – 为使用 Forms 身份验证的声明配置 ASP.NET Web 窗体应用程序  
  
-   步骤 3 - 测试你的解决方案  
  
## <a name="step-1--create-a-simple-aspnet-web-forms-application"></a>步骤 1 – 创建简单的 ASP.NET Web 窗体应用程序  
 在此步骤中，将创建一个新的 ASP.NET Web 窗体应用程序。  
  
#### <a name="to-create-a-simple-aspnet-application"></a>创建一个简单 ASP.NET 应用程序  
  
1.  启动 Visual Studio，然后依次单击“文件”、“新建”和“项目”。  
  
2.  在“新建项目”窗口中，单击“ASP.NET Web 窗体应用程序”。  
  
3.  在“名称”中，输入 `TestApp`，然后按“确定”。  
  
## <a name="step-2--configure-aspnet-web-forms-application-for-claims-using-forms-authentication"></a>步骤 2 – 为使用 Forms 身份验证的声明配置 ASP.NET Web 窗体应用程序  
 在此步骤中，将向“Web.config”配置文件添加一个配置项并编辑“Default.aspx”文件，以便显示帐户的声明信息。  
  
#### <a name="to-configure-aspnet-application-for-claims-using-forms-authentication"></a>为使用 Forms 身份验证的声明配置 ASP.NET 应用程序  
  
1.  在“Default.aspx”文件中，将现有标记替换为以下内容：  
  
    ```  
    <%@ Page Title="Home Page" Language="C#" MasterPageFile="~/Site.Master" AutoEventWireup="true" CodeBehind="Default.aspx.cs" Inherits="TestApp._Default" %>  
  
    <asp:Content runat="server" ID="BodyContent" ContentPlaceHolderID="MainContent">  
        <p>  
            This page displays the claims associated with a Forms authenticated user.          
        </p>  
        <h3>Your Claims</h3>  
        <p>  
            <asp:GridView ID="ClaimsGridView" runat="server" CellPadding="3">  
                <AlternatingRowStyle BackColor="White" />  
                <HeaderStyle BackColor="#7AC0DA" ForeColor="White" />  
            </asp:GridView>  
        </p>  
    </asp:Content>  
    ```  
  
     此步骤将向“Default.aspx”页添加 GridView 控件，该页将填充从 Forms 身份验证检索的声明。  
  
2.  保存 Default.aspx 文件，然后打开名为 Default.aspx.cs 的代码隐藏文件。 将现有代码替换为以下代码：  
  
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
  
                if (claimsPrincipal != null)  
                {  
                    this.ClaimsGridView.DataSource = claimsPrincipal.Claims;  
                    this.ClaimsGridView.DataBind();  
                }  
            }  
        }  
    }  
    ```  
  
     以上代码将显示有关已通过身份验证的用户（包括由 Forms 身份验证标识的用户）的声明。  
  
## <a name="step-3--test-your-solution"></a>步骤 3 - 测试你的解决方案  
 此步骤中将测试 ASP.NET Web 窗体应用程序，并验证用户使用 Forms 身份验证登录时是否呈现声明。  
  
#### <a name="to-test-your-aspnet-web-forms-application-for-claims-using-forms-authentication"></a>为使用 Forms 身份验证的声明测试 ASP.NET Web 窗体应用程序  
  
1.  按 F5 生成并运行该应用程序。 将显示“Default.aspx”，其页面右上角具有“注册”和“登录”链接。 单击“注册”。  
  
2.  在“注册”页上，创建用户帐户，然后单击“注册”。 将使用 Forms 身份验证创建帐户，并将使你自动登录。  
  
3.  已重定向到主页后，将看到一个位于标题“你的声明”下方的表格，它包含有关帐户的“颁发者”、“原始颁发者”、“类型”、“值”和“值类型”声明信息。

