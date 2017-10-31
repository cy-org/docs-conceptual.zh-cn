---
title: "如何：使用 WIF 显示登录状态"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4d1174e4-5397-4962-9a5f-3b1ad7b3fc14
caps.latest.revision: 6
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 494e67b39187a2a38f29f994e17051430d90f708
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="how-to-display-signed-in-status-using-wif"></a>如何：使用 WIF 显示登录状态
## <a name="applies-to"></a>适用于  
  
-   Microsoft® Windows® Identity Foundation (WIF) 4.5  
  
-   ASP.NET® Web 窗体  
  
## <a name="summary"></a>摘要  
 本主题介绍如何在已启用 WIF 的 ASP.NET 应用程序中显示登录状态。 WIF 提供的机制可使应用程序声明感知、管理应用程序资源的身份验证和授权。  
  
## <a name="contents"></a>内容  
  
-   概述  
  
-   步骤摘要  
  
-   步骤 1 – 安装标识和访问扩展  
  
-   步骤 2 – 创建信赖方 ASP.NET 应用程序  
  
-   步骤 3 – 启用本地开发 STS 以验证用户身份  
  
-   步骤 4 – 修改 ASP.NET 应用程序以显示登录状态  
  
-   步骤 5 - 测试 WIF 和 ASP.NET 应用程序之间的集成  
  
## <a name="overview"></a>概述  
 本主题演示如何使用 WIF 创建简单的声明感知应用程序，以及如何轻松显示用户是否已登录。 以下步骤使用的本地开发 STS 包含在标识和访问 Visual Studio 扩展中。 本地开发 STS 专门用于测试和开发环境，提供一种简单的方法将声明集成到应用程序中。 它不可用于生产环境，因为它不执行实际的身份验证，也不需要凭据。 但以下步骤中的指令性代码与使用实际身份验证的生产就绪应用程序的相同。  
  
## <a name="summary-of-steps"></a>步骤摘要  
  
-   步骤 1 – 安装标识和访问扩展  
  
-   步骤 2 – 创建信赖方 ASP.NET 应用程序  
  
-   步骤 3 – 启用本地开发 STS 以验证用户身份  
  
-   步骤 4 – 修改 ASP.NET 应用程序以显示登录状态  
  
-   步骤 5 - 测试 WIF 和 ASP.NET 应用程序之间的集成  
  
## <a name="step-1--install-the-identity-and-access-extension"></a>步骤 1 – 安装标识和访问扩展  
 此步骤介绍如何为 Visual Studio 2012 配置标识和访问扩展。 此扩展会自动启动配置应用程序过程，以与 STS 终结点进行通信。  
  
#### <a name="to-install-the-identity-and-access-extension"></a>安装标识和访问扩展  
  
1.  以管理员身份在提升模式下启动 Visual Studio。  
  
2.  在 Visual Studio 中，单击“工具”，然后单击“展开管理器”。 此时将打开“扩展管理器”窗口。  
  
3.  在“扩展管理器”中，单击左侧菜单中的“联机扩展”，然后选择“Visual Studio 库”。  
  
4.  在“扩展管理器”的右上角，搜索“标识和访问”。  
  
5.  此时将在搜索结果中显示“标识和访问”项。 单击该项，然后单击“下载”。  
  
6.  此时将打开“下载并安装”对话框。 如果同意许可条款，请单击“安装”。  
  
7.  “标识和访问”扩展安装完成后，在管理员模式下重启 Visual Studio。  
  
## <a name="step-2--create-a-relying-party-aspnet-application"></a>步骤 2 – 创建信赖方 ASP.NET 应用程序  
 此步骤介绍如何创建与 WIF 集成的信赖方 ASP.NET Web 窗体应用程序。  
  
#### <a name="to-create-a-simple-aspnet-application"></a>创建一个简单 ASP.NET 应用程序  
  
1.  启动 Visual Studio，然后依次单击“文件”、“新建”和“项目”。  
  
2.  在“新建项目”窗口中，单击“ASP.NET Web 窗体应用程序”。  
  
3.  在“名称”中，输入 `TestApp`，然后按“确定”。  
  
## <a name="step-3--enable-local-development-sts-to-authenticate-users"></a>步骤 3 – 启用本地开发 STS 以验证用户身份  
 此步骤介绍如何在应用程序中启用本地开发 STS。 使用 Visual Studio 的标识和访问扩展可启用本地开发 STS。  
  
#### <a name="to-enable-local-development-sts-in-your-aspnet-application"></a>在 ASP.NET 应用程序中启用本地开发 STS  
  
1.  在 Visual Studio 中，右键单击“解决方案资源管理器”下的“TestApp”项目，然后选择“标识和访问”。  
  
2.  “标识和访问”窗口随即出现。 在“提供程序”下，选择“使用本地开发 STS 测试应用程序”，然后单击“应用”。  
  
## <a name="step-4--modify-your-aspnet-application-to-display-sign-in-status"></a>步骤 4 – 修改 ASP.NET 应用程序以显示登录状态  
 此步骤介绍如何修改 ASP.NET 应用程序，以动态显示当前用户是否已登录。 配置 STS 提供程序后，WIF 将处理传入的声明。 现在，需要配置应用程序代码，以显示身份验证的结果。  
  
#### <a name="to-display-sign-in-status"></a>显示登录状态  
  
1.  在 Visual Studio 中，打开“Default.aspx”文件下的“TestApp”项目。  
  
2.  在“Default.aspx”文件中，将现有标记替换为以下标记：  
  
    ```  
    <%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="_Default" %>  
  
    <!DOCTYPE html>  
  
    <html>  
    <head runat="server">  
        <title>Logged In Status</title>  
    </head>  
    <body>  
        <asp:label ID="myLabel" runat="server" />  
    </body>  
    </html>  
    ```  
  
3.  保存 Default.aspx 文件，然后打开名为 Default.aspx.cs 的代码隐藏文件。  
  
    > [!NOTE]
    >  在解决方案资源管理器中，Default.aspx.cs 文件可能隐藏在 Default.aspx 文件下。 如果 Default.aspx.cs 文件不可见，请单击文件旁边的三角形，展开 Default.aspx。  
  
4.  在 Default.aspx 文件中，将现有代码替换为以下代码：  
  
    ```csharp  
    using System;  
    using System.Web.UI;  
    using System.Security.Claims;  
  
    namespace TestApp  
    {  
        protected void Page_Load(object sender, EventArgs e)  
        {  
            ClaimsPrincipal claimsPrincipal = Thread.CurrentPrincipal as ClaimsPrincipal;  
  
            if (claimsPrincipal != null)  
            {  
                myLabel.Text = "You are signed in.";  
            }  
            else  
            {  
                myLabel.Text = "You are not signed in.";  
            }  
        }  
    }  
    ```  
  
5.  保存 Default.aspx.cs，并生成该应用程序。  
  
## <a name="step-5--test-the-integration-between-wif-and-your-aspnet-application"></a>步骤 5 - 测试 WIF 和 ASP.NET 应用程序之间的集成  
 此步骤介绍如何测试 WIF 和 ASP.NET 应用程序之间的集成。  
  
#### <a name="to-test-the-integration-between-wif-and-aspnet"></a>测试 WIF 和 ASP.NET 之间的集成  
  
1.  在 Visual Studio 中，按“F5”开始调试应用程序。 如果未发现任何错误，将打开一个新的浏览器窗口。  
  
2.  你可能会注意到，浏览器会以无提示方式将请求重定向到 STS，然后打开 Default.aspx 页。 如果 WIF 配置正确，站点应会显示以下文本：“你已登录”。

