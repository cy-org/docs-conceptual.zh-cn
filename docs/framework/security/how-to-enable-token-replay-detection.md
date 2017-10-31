---
title: "如何：启用令牌重播检测"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5a9f5771-f5f6-4100-8501-406aa20d731a
caps.latest.revision: 4
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: cde32407f072f3d29af4a8d1aae559e46057ae3a
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="how-to-enable-token-replay-detection"></a>如何：启用令牌重播检测
## <a name="applies-to"></a>适用于  
  
-   Microsoft® Windows® Identity Foundation (WIF)  
  
-   ASP.NET® Web 窗体  
  
## <a name="summary"></a>摘要  
 此“如何”主题提供了详细的分步过程，用于说明如何在使用 WIF 的 ASP.NET 应用程序中启用令牌重播检测。 还说明了如何测试应用程序，以验证是否启用令牌重播检测。 此“如何”主题未详细介绍如何创建安全令牌服务 (STS)，而是使用随标识和访问工具提供的开发 STS。 开发 STS 不执行实际的身份验证操作，只是用来进行测试。 你将需要安装标识和访问工具才能完成此“如何”主题。 此工具可以从下列位置下载：[标识和访问工具](http://go.microsoft.com/fwlink/?LinkID=245849)  
  
## <a name="contents"></a>内容  
  
-   目标  
  
-   概述  
  
-   步骤摘要  
  
-   步骤 1 – 创建简单的 ASP.NET Web 窗体应用程序，并启用重播检测  
  
-   步骤 2 - 测试解决方案  
  
## <a name="objectives"></a>目标  
  
-   创建一个简单的 ASP.NET 应用程序，该应用程序使用标识和访问工具中的 WIF 和开发 STS  
  
-   启用令牌重播检测并验证其是否正常运行  
  
## <a name="overview"></a>概述  
 客户端尝试向具有客户端已使用的 STS 令牌的信赖方进行身份验证时，出现重播攻击。 为防止这种攻击，WIF 包含以前用过的 STS 令牌的重播检测缓存。 启用后，重播检测会检查传入请求的令牌，并验证此令牌以前是否已使用过。 如果该令牌已使用过，则会拒绝请求，并引发 <xref:System.IdentityModel.Tokens.SecurityTokenReplayDetectedException> 异常。  
  
 以下步骤演示启用重播检测所需的配置更改。  
  
## <a name="summary-of-steps"></a>步骤摘要  
  
-   步骤 1 – 创建简单的 ASP.NET Web 窗体应用程序，并启用重播检测  
  
-   步骤 2 - 测试解决方案  
  
## <a name="step-1--create-a-simple-aspnet-web-forms-application-and-enable-replay-detection"></a>步骤 1 – 创建简单的 ASP.NET Web 窗体应用程序，并启用重播检测  
 此步骤将创建新的 ASP.NET Web 窗体应用程序并修改 Web.config 文件以启用重播检测。  
  
#### <a name="to-create-a-simple-aspnet-application"></a>创建一个简单 ASP.NET 应用程序  
  
1.  启动 Visual Studio，然后依次单击“文件”、“新建”和“项目”。  
  
2.  在“新建项目”窗口中，单击“ASP.NET Web 窗体应用程序”。  
  
3.  在“名称”中，输入 `TestApp`，然后按“确定”。  
  
4.  在“解决方案资源管理器”下，右键单击“TestApp”项目，然后选择“标识和访问”。  
  
5.  “标识和访问”窗口随即出现。 在“提供程序”下，选择“使用本地开发 STS 测试应用程序”，然后单击“应用”。  
  
6.  将以下 \<tokenReplayDetection> 元素添加至 Web.config 配置文件，并紧跟在 \<system.identityModel> 元素和 \<identityConfiguration> 元素之后，如下所示：  
  
    ```xml  
    <system.identityModel>  
        <identityConfiguration>  
            <tokenReplayDetection enabled="true"/>  
    ```  
  
## <a name="step-2--test-your-solution"></a>步骤 2 - 测试解决方案  
 此步骤将测试已启用 WIF 的 ASP.NET 应用程序，以验证是否已启用重播检测。  
  
#### <a name="to-test-your-wif-enabled-aspnet-application-for-replay-detection"></a>测试已启用 WIF 的 ASP.NET 应用程序，以进行重播检测  
  
1.  按 F5 键运行解决方案。 应显示默认 ASP.NET 主页，且你会通过用户名 Terry （这是由开发 STS 返回的默认用户名）进行自动身份验证。  
  
2.  按浏览器“返回”按钮。 “/”应用程序页应显示服务器错误，描述为：ID1062: 已检测到重播: 令牌: “System.IdentityModel.Tokens.SamlSecurityToken”，后跟 AssertionId 和颁发者。  
  
     会出现此错误页，因为检测到令牌重播时引发 <xref:System.IdentityModel.Tokens.SecurityTokenReplayDetectedException> 类型异常。 出现此错误的原因是第一次提供令牌时，你尝试重新发送初始 POST 请求。 对于服务器的后续请求，“返回”按钮不会引起此行为。

