---
title: "如何：为 WCF Web 服务应用程序启用 WIF"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bfc64b3d-64e9-4093-a6a4-72e933917af7
caps.latest.revision: 6
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 7db69de994770e122dd4a4233b9a44d572c32344
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="how-to-enable-wif-for-a-wcf-web-service-application"></a>如何：为 WCF Web 服务应用程序启用 WIF
## <a name="applies-to"></a>适用于  
  
-   Microsoft® Windows® Identity Foundation (WIF)  
  
-   Microsoft® Windows® Communication Foundation (WCF)  
  
## <a name="summary"></a>摘要  
 此“如何”主题提供了详细的分步过程，用于说明如何在 WCF 服务中启用 WIF。 它还提供关于如何测试应用程序的说明，以便验证 Web 服务在应用程序运行时正确呈现声明。 此“如何”主题未详细介绍如何创建安全令牌服务 (STS)，而是使用随标识和访问工具提供的开发 STS。 开发 STS 不执行实际的身份验证操作，只是用来进行测试。 你将需要安装标识和访问工具才能完成此“如何”主题。 此工具可以从下列位置下载：[标识和访问工具](http://go.microsoft.com/fwlink/?LinkID=245849)  
  
## <a name="contents"></a>内容  
  
-   目标  
  
-   概述  
  
-   步骤摘要  
  
-   步骤 1 – 创建一个简单的 WCF 服务  
  
-   步骤 2 - 为 WCF 服务创建一个客户端应用程序  
  
-   步骤 3 - 测试你的解决方案  
  
## <a name="objectives"></a>目标  
  
-   创建一个需要使用颁发令牌的 WCF 服务  
  
-   创建一个 WCF 客户端，用于从 STS 请求令牌并将其传递给 WCF 服务  
  
## <a name="overview"></a>概述  
 此“如何”主题旨在演示开发人员在开发 WCF 服务时可以如何使用联合身份验证。 在 WCF 服务中使用联合方法的部分优势包括：  
  
1.  将 WCF 服务代码之外的身份验证逻辑纳入在内  
  
2.  重复使用现有的标识管理解决方案  
  
3.  与其他标识解决方案实现互操作  
  
4.  灵活、弹性地适应未来更改  
  
 借助 WIF 和关联的标识和访问工具，可以更轻松地开发和测试采用联合身份验证的 WCF 服务，如下列步骤所示。  
  
## <a name="summary-of-steps"></a>步骤摘要  
  
-   步骤 1 – 创建一个简单的 WCF 服务  
  
-   步骤 2 - 为 WCF 服务创建一个客户端应用程序  
  
-   步骤 3 - 测试你的解决方案  
  
## <a name="step-1--create-a-simple-wcf-service"></a>步骤 1 – 创建一个简单的 WCF 服务  
 在此步骤中，你将创建一个新的 WCF 服务，此服务使用标识和访问工具中包含的开发 STS。  
  
#### <a name="to-create-a-simple-wcf-service"></a>创建一个简单的 WCF 服务  
  
1.  以管理员身份在提升模式下启动 Visual Studio。  
  
2.  在 Visual Studio 中，单击“文件”，再单击“新建”，然后单击“项目”。  
  
3.  在“新建项目”窗口中，单击“WCF 服务应用程序”。  
  
4.  在“名称”中，输入 `TestService`，然后按“确定”。  
  
5.  右键单击“解决方案资源管理器”下的“TestService”项目，然后选择“标识和访问”。  
  
6.  “标识和访问”窗口随即出现。 在“提供程序”下，选择“使用本地开发 STS 测试应用程序”，然后单击“应用”。 标识和访问工具可以向 Web.config 文件添加配置元素，从而将服务配置为使用 WIF，并将身份验证外包给本地开发 STS (LocalSTS) 来执行。  
  
7.  在 Service1.svc.cs 文件中，为 System.Security.Claims 命名空间添加一个 `using` 指令，并使用下面的代码替换现有代码，然后保存文件：  
  
    ```csharp  
    public class Service1 : IService1  
    {  
        public string ComputeResponse(string input)  
        {  
            // Get the caller's identity from ClaimsPrincipal.Current  
            ClaimsPrincipal claimsPrincipal = OperationContext.Current.ClaimsPrincipal;  
  
            // Start generating the output  
            StringBuilder builder = new StringBuilder();  
            builder.AppendLine("Computed by ClaimsAwareWebService");  
            builder.AppendLine("Input received from client:" + input);  
  
            if (claimsPrincipal != null)  
            {  
                // Display the claims from the caller. Do not use this code in a production application.  
                ClaimsIdentity identity = claimsPrincipal.Identity as ClaimsIdentity;  
                builder.AppendLine("Client Name:" + identity.Name);  
                builder.AppendLine("IsAuthenticated:" + identity.IsAuthenticated);  
                builder.AppendLine("The service received the following issued claims of the client:");  
  
                // Iterate over the caller’s claims and append to the output  
                foreach (Claim claim in claimsPrincipal.Claims)  
                {  
                    builder.AppendLine("ClaimType :" + claim.Type + "   ClaimValue:" + claim.Value);  
                }  
            }  
  
            return builder.ToString();  
        }  
    }  
    ```  
  
     `ComputeResponse` 方法可以显示由 LocalSTS 发出的各个声明的属性。  
  
8.  在 IService1.cs 文件中，使用下面的代码替换现有代码，然后保存文件：  
  
    ```csharp  
    [ServiceContract]  
    public interface IService1  
    {  
        [OperationContract]  
        string ComputeResponse(string input);  
    }  
    ```  
  
9. 生成项目。  
  
10. 按“Ctrl-F5”运行服务，而不启动调试器。 此时应该会为此服务打开一个网页，可查看通知区域（系统栏），验证 LocalSTS 是否正在运行。  
  
    > [!IMPORTANT]
    >  当在下一个步骤中向客户端应用程序添加服务引用时，TestService 和 LocalSTS 都必须处于运行状态。  
  
## <a name="step-2--create-a-client-application-for-the-wcf-service"></a>步骤 2 - 为 WCF 服务创建一个客户端应用程序  
 在此步骤中，你将创建一个控制台应用程序，此应用程序使用开发 STS 来对上一个步骤中创建的 WCF 服务进行身份验证。  
  
#### <a name="to-create-a-client-application"></a>创建客户端应用程序  
  
1.  在 Visual Studio 中，右键单击解决方案，单击“添加”，然后单击“新建项目”。  
  
2.  在“添加新项目”窗口中，选择 Visual C# 模板列表中的“控制台应用程序”，输入 `Client`，然后按“确定”。 系统将在你的解决方案文件夹中创建新项目。  
  
3.  右键单击“客户端”项目下的“引用”，然后单击“添加服务引用”。  
  
4.  在“添加服务引用”窗口中，单击“发现”按钮上的下拉箭头，然后单击“解决方案中的服务”。 “地址”将自动填充之前创建的 WCF 服务，而“命名空间”将设置为“ServiceReference1”。 单击“确定”。  
  
    > [!IMPORTANT]
    >  向客户端添加服务引用时，TestService 和 LocalSTS 都必须处于运行状态。  
  
5.  Visual Studio 将生成 WCF 服务的代理类，然后添加所有必要的引用信息。 还将向 App.config 文件添加元素，以便将客户端配置为从 STS 获取令牌，然后对服务进行身份验证。 当此过程完成之后，将打开 Program.cs 文件。 分别为 System.ServiceModel 和 Client.ServiceReference1 添加一个 `using` 指令，使用下面的代码替换 Main 方法，然后保存文件：  
  
    ```csharp  
    static void Main(string[] args)  
    {  
        // Create the client for the service  
        Service1Client client = new Service1Client();  
        Console.WriteLine("-------------WCF Client Application--------------\n");  
  
        while (!ShouldQuitApplication())  
        {  
            try  
            {  
                Console.WriteLine(client.ComputeResponse("Hello World"));  
            }  
            catch (CommunicationException e)  
            {  
                Console.WriteLine(e.Message);  
                Console.WriteLine(e.StackTrace);  
                Exception ex = e.InnerException;  
                while (ex != null)  
                {  
                    Console.WriteLine("===========================");  
                    Console.WriteLine(ex.Message);  
                    Console.WriteLine(ex.StackTrace);  
                    ex = ex.InnerException;  
                }  
            }  
            catch (TimeoutException)  
            {  
                Console.WriteLine("Timed out...");  
            }  
            catch (Exception e)  
            {  
                Console.WriteLine("An unexpected exception occurred.");  
                Console.WriteLine(e.StackTrace);  
            }  
        }  
  
        client.Close();  
  
        if (client != null)  
        {  
            client.Abort();  
        }  
    }  
  
    static bool ShouldQuitApplication()  
    {  
        Console.WriteLine("---------------------------------------------------------------------");  
        Console.WriteLine("Press Enter key to invoke service, any other key to quit application:");  
        Console.WriteLine("----------------------------------------------------------------------");  
  
        ConsoleKeyInfo keyInfo = Console.ReadKey();  
        if (keyInfo.Key == ConsoleKey.Enter)  
            return false;  
        return true;  
    }  
    ```  
  
6.  打开 App.config 文件并添加下面的 XML，将其作为 `<system.serviceModel>` 元素下的第一个子元素，然后保存文件：  
  
    ```xml  
    <behaviors>  
       <endpointBehaviors>  
         <behavior>  
           <clientCredentials>  
             <serviceCertificate>  
               <authentication certificateValidationMode="None"/>  
             </serviceCertificate>  
           </clientCredentials>  
         </behavior>  
       </endpointBehaviors>  
     </behaviors>  
    ```  
  
     这样会禁用证书验证。  
  
7.  右键单击“TestService”解决方案，然后单击“设置启动项目”。 “启动项目”属性页便随即打开。 在“启动项目”属性页中，选择“多启动项目”，然后单击每个项目的“操作”字段，并从下拉菜单中选择“启动”。 单击“确定”保存这些设置。  
  
8.  生成解决方案。  
  
## <a name="step-3--test-your-solution"></a>步骤 3 - 测试你的解决方案  
 在此步骤中，你将测试已启用 WIF 的 WCF 应用程序并验证正确呈现声明。  
  
#### <a name="to-test-your-wif-enabled-wcf-application-for-claims"></a>对已启用 WIF 的 WCF 应用程序进行声明测试  
  
1.  按 F5 生成并运行该应用程序。 应会看到一个控制台窗口，以及以下文本：按“Enter”可调用服务，按其他键可退出应用程序：  
  
2.  按“Enter”，然后控制台应会显示以下声明信息：  
  
    ```  
    Computed by Service1  
    Input received from client: Hello World  
    Client Name: Terry  
    IsAuthenticated: True  
    The service received the following issued claims of the client:  
    ClaimType :http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name    ClaimValue:Terry  
    ClaimType :http://schema.xmlsoap.org/ws/2005/05/identity/claims/surname    ClaimValue:Adams  
    ClaimType :http://schemas.microsoft.com/ws/2008/06/identity/claims/role    ClaimValue:developer  
    ClaimType :http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress    ClaimValue:terry@contoso.com  
    ```  
  
    > [!IMPORTANT]
    >  在按“Enter”之前，TestService 和 LocalSTS 都必须处于运行状态。 此时应该会为此服务打开一个网页，可查看通知区域（系统栏），验证 LocalSTS 是否正在运行。  
  
3.  如果这些声明出现在控制台中，表示你已成功通过 STS 身份验证，可以显示 WCF 服务的声明。

