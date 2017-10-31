---
title: "如何：使用 Windows 身份验证生成声明感知 ASP.NET 应用程序"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 11c53d9d-d34a-44b4-8b5e-22e3eaeaee93
caps.latest.revision: 5
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 676a03678cbdf6fe08e628806df2a1853fb71718
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="how-to-build-claims-aware-aspnet-application-using-windows-authentication"></a>如何：使用 Windows 身份验证生成声明感知 ASP.NET 应用程序
## <a name="applies-to"></a>适用于  
  
-   Microsoft® Windows® Identity Foundation (WIF)  
  
-   ASP.NET® Web 窗体  
  
## <a name="summary"></a>摘要  
 本操作说明提供了创建使用 Windows 身份验证的简单声明感知 ASP.NET Web 窗体应用程序的详细分步过程。 还提供关于如何测试应用程序以验证用户使用 Windows 身份验证登录时是否呈现声明的说明。  
  
## <a name="contents"></a>内容  
  
-   目标  
  
-   概述  
  
-   步骤摘要  
  
-   步骤 1 – 创建简单的 ASP.NET Web 窗体应用程序  
  
-   步骤 2 – 为使用 Windows 身份验证的声明配置 ASP.NET Web 窗体应用程序  
  
-   步骤 3 - 测试你的解决方案  
  
## <a name="objectives"></a>目标  
  
-   为使用 Windows 身份验证的声明配置 ASP.NET Web 窗体应用程序  
  
-   测试 ASP.NET Web 窗体应用程序，了解它是否正常工作  
  
## <a name="overview"></a>概述  
 在 .NET 4.5 中，已将 WIF 及其基于声明的授权作为 Framework 的重要组成部分包括在内。 以前，如果想要来自 ASP.NET 用户的声明，需要安装 WIF，然后将接口转换为如 `Thread.CurrentPrincipal` 或 `HttpContext.Current.User` 的主体对象。 现在，声明由这些主体对象自动提供。  
  
 Windows 身份验证受益于 .NET 4.5 对 WIF 的纳入，因为所有通过 Windows 凭据进行身份验证的用户会自动拥有与之关联的声明。 如本操作说明所示，可在使用 Windows 身份验证的 ASP.NET 应用程序中开始立即使用这些声明。  
  
## <a name="summary-of-steps"></a>步骤摘要  
  
-   步骤 1 – 创建简单的 ASP.NET Web 窗体应用程序  
  
-   步骤 2 – 为使用 Windows 身份验证的声明配置 ASP.NET Web 窗体应用程序  
  
-   步骤 3 - 测试你的解决方案  
  
## <a name="step-1--create-a-simple-aspnet-web-forms-application"></a>步骤 1 – 创建简单的 ASP.NET Web 窗体应用程序  
 在此步骤中，将创建一个新的 ASP.NET Web 窗体应用程序。  
  
#### <a name="to-create-a-simple-aspnet-application"></a>创建一个简单 ASP.NET 应用程序  
  
1.  启动 Visual Studio，然后依次单击“文件”、“新建”和“项目”。  
  
2.  在“新建项目”窗口中，单击“ASP.NET Web 窗体应用程序”。  
  
3.  在“名称”中，输入 `TestApp`，然后按“确定”。  
  
4.  创建 TestApp 项目后，在“解决方案资源管理器”中单击它。 项目的属性会在“解决方案资源管理器”下的“属性面板”窗格中显示。 将“Windows 身份验证”属性设置为“启用”。  
  
    > [!WARNING]
    >  新的 ASP.NET 应用程序中默认禁用 Windows 身份验证，因此必须手动启用它。  
  
## <a name="step-2--configure-aspnet-web-forms-application-for-claims-using-windows-authentication"></a>步骤 2 – 为使用 Windows 身份验证的声明配置 ASP.NET Web 窗体应用程序  
 在此步骤中，将配置条目添加到 Web.config 配置文件，并修改 Default.aspx 文件以显示帐户的声明信息。  
  
#### <a name="to-configure-aspnet-application-for-claims-using-windows-authentication"></a>为使用 Windows 身份验证的声明配置 ASP.NET 应用程序  
  
1.  在 TestApp 项目的 Default.aspx 文件中，将现有标记替换为以下内容：  
  
    ```  
    <%@ Page Title="Home Page" Language="C#" MasterPageFile="~/Site.Master" AutoEventWireup="true"  
        CodeBehind="Default.aspx.cs" Inherits="TestApp._Default" %>  
  
    <asp:Content runat="server" ID="BodyContent" ContentPlaceHolderID="MainContent">  
        <p>  
            This page displays the claims associated with a Windows authenticated user.          
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
  
     此步骤将 GridView 控件添加到“Default.aspx”页，该页将填充从 Windows 身份验证中检索的声明。  
  
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
                this.ClaimsGridView.DataSource = claimsPrincipal.Claims;  
                this.ClaimsGridView.DataBind();  
            }  
        }  
    }  
    ```  
  
     上方的代码将显示有关已经过身份验证的用户的声明。  
  
3.  若要更改应用程序的身份验证类型，请修改项目的 Web.config 根文件的 \<system.web> 节中的 \<authentication> 块，使其只包括以下配置条目：  
  
    ```xml  
    <authentication mode="Windows" />  
    ```  
  
4.  最后，修改同一 Web.config 文件的 \<system.web> 节中的 \<authorization> 块以强制身份验证：  
  
    ```xml  
    <authorization>  
        <deny users="?" />  
    </authorization>  
    ```  
  
## <a name="step-3--test-your-solution"></a>步骤 3 - 测试你的解决方案  
 此步骤中将测试 ASP.NET Web 窗体应用程序，并验证用户使用 Windows 身份验证登录时是否呈现声明。  
  
#### <a name="to-test-your-aspnet-web-forms-application-for-claims-using-windows-authentication"></a>为使用 Windows 身份验证的声明测试 ASP.NET Web 窗体应用程序  
  
1.  按 F5 生成并运行该应用程序。 应当会显示 Default.aspx，且你的 Windows 帐户名（包括域名）应在页面的右上角显示为已经过身份验证的用户。 页面内容应包括一个表，其中填充有从你的 Windows 帐户检索的声明。

