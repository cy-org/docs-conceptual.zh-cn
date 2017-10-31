---
title: "WCF 服务主机 (WcfSvcHost.exe) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8643a63d-a357-4c39-bd6c-cdfdf71e370e
caps.latest.revision: 27
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 27
---
# WCF 服务主机 (WcfSvcHost.exe)
[!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 服务主机 \(WcfSvcHost.exe\) 允许您启动 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 调试器 \(F5\) 以自动承载和测试已实现的服务。然后可以使用 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 测试客户端 \(WcfTestClient.exe\) 或您自己的客户端来测试服务，以查找并解决任何潜在错误。  
  
## WCF 服务主机  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务主机将枚举 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务项目中的服务、加载项目的配置并为它所找到的每项服务对主机进行实例化。此工具通过 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务模板集成到 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 中，在您开始调试项目时将会调用此工具。  
  
 使用 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务主机可以承载 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务（在 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务库项目中），而无需在开发过程中额外编写代码或提交到特定的主机。  
  
> [!NOTE]
>  [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务主机不支持部分信任。如果想要在部分信任中使用 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务，请不要使用 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 中的 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务库项目模板生成服务。而应通过选择 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务网站模板在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 中创建新的网站。该网站可以在支持 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 部分信任的 WebServer 中承载服务。  
  
## WCF 服务主机承载的项目类型  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务主机可以承载以下 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务库项目类型：[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务库、顺序工作流服务库、状态机工作流服务库和联合服务库。[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务主机也可以承载那些使用**“添加项”**功能添加到服务库项目中的服务。这包括 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务、WF 状态机服务、WF 顺序服务、XAML WF 状态机服务和 XAML WF 顺序服务。  
  
 但是，应该注意到该工具将不会帮助您配置主机。对于此项任务，必须手动编辑 App.config 文件。另外，此工具也不会验证用户定义的配置文件。  
  
> [!CAUTION]
>  不应该使用 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务主机在生产环境中承载服务，因为其设计初衷并不是为了执行此操作。[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务主机无法满足此类环境的可靠性、安全性和可管理性要求。请改用 IIS，因为它可以提供卓越的可靠性和监视功能，并且是承载服务的首选解决方案。在服务开发完成后，应该将服务从 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务主机迁移到 IIS。  
  
## 在 Visual Studio 中使用 WCF 服务主机的方案  
 下表列出了**“命令行参数”**对话框中的所有参数，通过在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 的**“解决方案资源管理器”**中右击您的项目，选择**“属性”**，然后选择**“调试”**选项卡并单击**“启动项目”**，可以找到该对话框。这些参数可用于配置 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务主机。  
  
|参数|含义|  
|--------|--------|  
|`/client`|一个可选参数，用于指定要在承载服务后运行的可执行文件的路径。这将在承载后启动 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 测试客户端。|  
|`/clientArg`|将字符串指定为传递给自定义客户端应用程序的参数。|  
|`/?`|显示帮助文本。|  
  
#### 使用 WCF 测试客户端  
 在创建新的 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务项目并按 F5 启动调试器后，[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务主机将开始承载它在项目中找到的所有服务。[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 测试客户端将会自动打开，并显示在配置文件中定义的服务终结点列表。可以从主窗口中测试参数并调用服务。  
  
 为了确保使用 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 测试客户端，请在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 的**“解决方案资源管理器”**中右击您的项目，并选择**“属性”**，然后选择**“调试”**选项卡。单击**“启动项目”**并确保**“命令行参数”**对话框中显示以下内容。  
  
 `/client:WcfTestClient.exe`  
  
#### 使用自定义客户端  
 若要使用自定义客户端，请在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 的**“解决方案资源管理器”**中右击您的项目，并选择**“属性”**，然后选择**“调试”**选项卡。单击**“启动项目”**并在**“命令行参数”**对话框中按照以下示例中的指示编辑 `/client` 参数以指向自定义客户端。  
  
 `/client:"path/CustomClient.exe"`  
  
 如果按 F5 再次启动服务，则 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务主机将在您启动调试器时自动启动您的自定义客户端。  
  
 也可以按照以下示例中的指示使用 `/clientArg:` 形参将字符串指定为传递给自定义客户端应用程序的实参。  
  
 `/client:"path/CustomClient.exe" /clientArg:"arguments that are passed to Client"`  
  
 例如，如果使用的是联合服务库模板，则可以使用以下命令行参数。  
  
 `/client:iexplore.exe /clientArgs:http://localhost:8731/Design_Time_Addresses/Feed1/`  
  
#### 指定无客户端  
 若要指定在 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务承载之后将不使用客户端，请在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 的**“解决方案资源管理器”**中右击您的项目，并选择**“属性”**，然后选择**“调试”**选项卡。单击**“启动项目”**并将**“命令行参数”**对话框留空。  
  
#### 使用自定义主机  
 若要使用自定义主机，请在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 的**“解决方案资源管理器”**中右击您的项目，并选择**“属性”**，然后选择**“调试”**选项卡。单击**“启动外部程序”**并输入自定义主机的完整路径。也可以使用**“命令行参数”**对话框指定要传递给主机的参数。  
  
## WCF 服务主机用户界面  
 在最初调用 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务主机（通过在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 内按 F5 来调用）时，**“WCF 服务主机”**窗口将自动打开。当正在运行 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务主机时，此程序的图标将出现在通知区域中。双击该图标可以打开**“WCF 服务主机”**窗口  
  
 如果在承载服务过程中出错，则将打开“[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务主机”对话框以显示相关信息。  
  
 **“WCF 服务主机”**主窗口包含以下两个菜单：  
  
-   **“文件”**：包含**“关闭”**和**“退出”**命令。单击**“关闭”**时，**“WCF 服务主机”**对话框将关闭，但会继续承载服务。当单击**“退出”**时，[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务主机也将关闭。这还将停止所有承载的服务。  
  
-   **“帮助”**：包含**“关于”**命令，该命令包含版本信息。此菜单还包含可打开帮助文件的**“帮助”**命令。  
  
 **“WCF 服务主机”**主窗口包含以下两个区域：  
  
-   第一个区域为**“服务”**。该区域包含一个显示所有服务基本信息的列表。这些信息包括：  
  
    -   **“服务”**：列出所有服务。  
  
    -   **“状态”**：列出服务的状态。有效值为“已开始”、“已停止”和“错误”。  
  
    -   **“元数据地址”**：显示服务的元数据地址。  
  
-   第二个区域为**“附加信息”**。如果在**“服务”**区域中选择了特定的服务行，则该区域将显示服务状态的详细说明。如果状态为“错误”，则可以在屏幕上查看完整的错误消息。  
  
## 停止 WCF 服务主机  
 可以通过以下四种方法关闭 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务主机：  
  
-   在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 中停止调试会话。  
  
-   从**“WCF 服务主机”**窗口内的**“文件”**菜单中选择**“退出”**。  
  
-   从系统通知区域内 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务主机任务栏图标的上下文菜单中选择**“退出”**。  
  
-   退出正在使用的 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]。  
  
## 在无管理员权限的情况下使用服务主机  
 为了使没有管理员权限的用户能够开发 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务，在安装 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 的过程中为命名空间“http:\/\/\+:8731\/Design\_Time\_Addresses”创建了一个 ACL（访问控制列表）。该 ACL 被设置为“\(UI\)”，这将包括登录到此计算机的所有交互用户。管理员可以在此 ACL 中添加或移除用户，或者打开其他端口。此 ACL 使用户可以在无管理员权限的情况下使用 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务自动主机 \(wcfSvcHost.exe\)。  
  
 可以使用提升的管理员帐户在 [!INCLUDE[wv](../../../includes/wv-md.md)] 中通过 netsh.exe 工具来修改访问权限。下面是使用 netsh.exe 的示例。  
  
```  
netsh http add urlacl url=http://+:8001/MyService user=<domain>\<user>  
```  
  
 有关 netsh.exe 的更多信息，请参见[如何使用 Netsh.exe 工具和命令行开关](http://go.microsoft.com/fwlink/?LinkId=97877)（可能为英文网页）。  
  
## 请参阅  
 [WCF 测试客户端 \(WcfTestClient.exe\)](../../../docs/framework/wcf/wcf-test-client-wcftestclient-exe.md)