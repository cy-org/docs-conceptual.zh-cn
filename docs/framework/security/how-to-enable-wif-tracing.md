---
title: "如何：启用 WIF 跟踪"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 271b6889-3454-46ff-96ab-9feb15e742ee
caps.latest.revision: 3
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 516e065bc360538e7b62807a5492c0c6c9d16e69
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="how-to-enable-wif-tracing"></a>如何：启用 WIF 跟踪
## <a name="applies-to"></a>适用于  
  
-   Microsoft® Windows® Identity Foundation (WIF)  
  
-   ASP.NET® Web 窗体  
  
## <a name="summary"></a>摘要  
 此“如何”主题提供了详细的分步过程，用于说明如何在 ASP.NET 应用程序中启用 WIF 跟踪。 还说明了如何测试应用程序，以验证跟踪侦听器和日志是否正常工作。 此“如何”主题未详细介绍如何创建安全令牌服务 (STS)，而是使用随标识和访问工具提供的开发 STS。 开发 STS 不执行实际的身份验证操作，只是用来进行测试。 你将需要安装标识和访问工具才能完成此“如何”主题。 此工具可以从下列位置下载：[标识和访问工具](http://go.microsoft.com/fwlink/?LinkID=245849)  
  
> [!IMPORTANT]
>  为被动应用程序（即使用 WS 联合身份验证协议的应用程序）启用 WIF 跟踪有可能使应用程序受到拒绝服务 (DoS) 攻击或使信息泄漏给恶意方。 这包括被动 RP 和被动 STS。 因此，我们建议不要在生产环境中为被动 RP 和被动 STS 启用 WIF 跟踪。  
  
## <a name="contents"></a>内容  
  
-   目标  
  
-   概述  
  
-   步骤摘要  
  
-   步骤 1 – 创建简单的 ASP.NET Web 窗体应用程序，并启用跟踪  
  
-   步骤 2 - 测试解决方案  
  
## <a name="objectives"></a>目标  
  
-   创建一个简单的 ASP.NET 应用程序，该应用程序使用标识和访问工具中的 WIF 和开发 STS  
  
-   启用跟踪，并验证其是否正常工作  
  
## <a name="overview"></a>概述  
 跟踪可通过 WIF 调试和解决许多问题类型，包括令牌、cookie、声明、协议消息等。 WIF 跟踪类似于 WCF 跟踪；例如，可选择跟踪的详细级别，显示从关键消息到所有消息的一切内容。 可以在 .xml 文件或 .svclog 文件中生成 WIF 跟踪，可通过使用服务跟踪查看器工具查看。 此工具位于计算机上 Windows SDK 安装路径的 bin 目录中，例如：C:\Program Files\Microsoft SDKs\Windows\v7.1\Bin\SvcTraceViewer.exe。  
  
## <a name="summary-of-steps"></a>步骤摘要  
  
-   步骤 1 – 创建简单的 ASP.NET Web 窗体应用程序，并启用跟踪  
  
-   步骤 2 - 测试解决方案  
  
## <a name="step-1--create-a-simple-aspnet-web-forms-application-and-enable-tracing"></a>步骤 1 – 创建简单的 ASP.NET Web 窗体应用程序，并启用跟踪  
 此步骤将创建新的 ASP.NET Web 窗体应用程序并修改 Web.config 文件以启用跟踪。  
  
#### <a name="to-create-a-simple-aspnet-application"></a>创建一个简单 ASP.NET 应用程序  
  
1.  启动 Visual Studio，然后依次单击“文件”、“新建”和“项目”。  
  
2.  在“新建项目”窗口中，单击“ASP.NET Web 窗体应用程序”。  
  
3.  在“名称”中，输入 `TestApp`，然后按“确定”。  
  
4.  在“解决方案资源管理器”下，右键单击“TestApp”项目，然后选择“标识和访问”。  
  
5.  “标识和访问”窗口随即出现。 在“提供程序”下，选择“使用本地开发 STS 测试应用程序”，然后单击“应用”。  
  
6.  在 C: 驱动器的根目录中创建一个名为 logs 的新文件夹，如：C:\logs  
  
7.  将以下 \<system.diagnostics > 元素添加到 Web.config 配置文件中，紧跟在 \</configSections > 元素之后，如下所示：  
  
    ```xml  
    <configuration>  
        <configSections>  
        …  
        </configSections>  
        <system.diagnostics>  
            <sources>  
                <source name="System.IdentityModel" switchValue="Verbose">  
                    <listeners>  
                        <add name="xml" type="System.Diagnostics.XmlWriterTraceListener" initializeData="C:\logs\WIF.xml" />  
                    </listeners>  
                </source>  
            </sources>  
            <trace autoflush="true" />  
        </system.diagnostics>  
    ```  
  
    > [!NOTE]
    >  在 initializeData 属性中指定的目录位置必须存在，才可开始日志记录。 如果位置不存在，则无法创建任何日志。  
  
     上面的配置设置将启用 WIF 的详细跟踪，并将生成的日志保存在 C:logsWIF.xml 文件中。  
  
## <a name="step-2--test-your-solution"></a>步骤 2 - 测试解决方案  
 此步骤将测试已启用 WIF 的 ASP.NET 应用程序，以验证是否正在记录日志。  
  
#### <a name="to-test-your-wif-enabled-aspnet-application-for-successful-tracing"></a>测试是否成功跟踪已启用 WIF 的 ASP.NET 应用程序  
  
1.  按 F5 键运行解决方案。 应显示默认 ASP.NET 主页，且你会通过用户名 Terry （这是由开发 STS 返回的默认用户名）进行自动身份验证。  
  
2.  关闭浏览器窗口，然后导航到 C:\logs 文件夹。 使用文本编辑器打开 C:\logs\WIF.xml 文件。  
  
3.  检查 WIF.xml 文件并验证该文件是否包含以 \<E2ETraceEvent> 开头的项。 这些跟踪将包含 \<TraceRecord > 元素，其中包含对跟踪活动的描述，如验证 SecurityToken。

