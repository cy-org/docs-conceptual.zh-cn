---
title: "如何：在托管应用程序中承载 WCF 服务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: 5eb29db0-b6dc-4e77-8c68-0a62f79d743b
caps.latest.revision: 42
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 42
---
# 如何：在托管应用程序中承载 WCF 服务
若要在托管应用程序中承载某项服务，请在托管应用程序代码内嵌入该服务的代码，在代码中强制定义、通过配置以声明的方式定义或者使用默认终结点定义该服务的终结点，然后创建 <xref:System.ServiceModel.ServiceHost> 的实例。  
  
 若要开始接收消息，请调用 <xref:System.ServiceModel.ServiceHost> 上的 <xref:System.ServiceModel.ICommunicationObject.Open%2A>。这样即可创建并打开服务的侦听器。以这种方式承载服务的做法通常称为“自承载”，原因是托管的应用程序会自己处理承载工作。若要关闭服务，请调用在 <xref:System.ServiceModel.ServiceHost> 上的 <xref:System.ServiceModel.Channels.CommunicationObject.Close%2A?displayProperty=fullName>。  
  
 在托管的 Windows 服务中、在 Internet 信息服务 \(IIS\) 中或在 Windows 进程激活服务 \(WAS\) 中也可以承载服务。[!INCLUDE[crabout](../../../includes/crabout-md.md)]服务的承载选项的更多信息，请参见[承载服务](../../../docs/framework/wcf/hosting-services.md).  
  
 在托管应用程序中承载服务是一个非常灵活的选项，因为这种做法在部署时所需的基础结构最少[!INCLUDE[crabout](../../../includes/crabout-md.md)] 在托管应用程序中承载服务的更多信息，请参见[在托管应用程序中承载](../../../docs/framework/wcf/feature-details/hosting-in-a-managed-application.md).  
  
 下面的过程演示如何在控制台应用程序中实现自承载的服务。  
  
### 创建自承载服务  
  
1.  打开 [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)]，然后在**“文件”**菜单中依次选择**“新建”**和**“项目…”**。  
  
2.  在**“已安装的模板”**列表中，依次选择**“Visual C\#”**和**“Windows”**或依次选择**“Visual Basic”**和**“Windows”**。根据您的 [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] 设置，**“已安装的模板”**列表中的**“其他语言”**节点下可能会显示其中一种语言或者同时显示这两种语言。  
  
3.  从**“Windows”**列表中选择**“控制台应用程序”**。在**“名称”**框中键入 `SelfHost`，然后单击**“确定”**。  
  
4.  在**“解决方案资源管理器”**中右击**“SelfHost”**，然后选择**“添加引用…”**。从**“.NET”**选项卡中选择**“System.ServiceModel”**，然后单击**“确定”**。  
  
    > [!TIP]
    >  如果**“解决方案资源管理器”**窗口不可见，请从**“视图”**菜单中选择**“解决方案资源管理器”**。  
  
5.  如果文件尚未打开，请在**“解决方案资源管理器”**中双击**“Program.cs”**或**“Module1.vb”**，以在代码窗口中打开它。将下面的语句添加到文件的顶部。  
  
     [!code-csharp[CFX_SelfHost4#1](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_selfhost4/cs/program.cs#1)]
     [!code-vb[CFX_SelfHost4#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/cfx_selfhost4/vb/module1.vb#1)]  
  
6.  定义和实现服务协定。此示例定义了一个 `HelloWorldService`，它基于对服务的输入返回消息。  
  
     [!code-csharp[CFX_SelfHost4#2](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_selfhost4/cs/program.cs#2)]
     [!code-vb[CFX_SelfHost4#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/cfx_selfhost4/vb/module1.vb#2)]  
  
    > [!NOTE]
    >  [!INCLUDE[crabout](../../../includes/crabout-md.md)]如何定义和实现服务接口的更多信息，请参见[如何：定义服务协定](../../../docs/framework/wcf/how-to-define-a-wcf-service-contract.md)和[如何：实现服务协定](../../../docs/framework/wcf/how-to-implement-a-wcf-contract.md)。  
  
7.  在 `Main` 方法的顶部，使用该服务的基址创建 <xref:System.Uri> 类的实例。  
  
     [!code-csharp[CFX_SelfHost4#3](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_selfhost4/cs/program.cs#3)]
     [!code-vb[CFX_SelfHost4#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/cfx_selfhost4/vb/module1.vb#3)]  
  
8.  创建 <xref:System.ServiceModel.ServiceHost> 类的实例，并将表示服务类型的 <xref:System.Type> 和基址统一资源标识符 \(URI\) 传递到 [ServiceHost\(Type, Uri\<xref:System.ServiceModel.ServiceHost.%23ctor%28System.Type%2CSystem.Uri%5B%5D%29>。启用元数据发布，然后调用 <xref:System.ServiceModel.ServiceHost> 上的 <xref:System.ServiceModel.ICommunicationObject.Open%2A> 方法，以初始化服务并使其准备好接收消息。  
  
     [!code-csharp[CFX_SelfHost4#4](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_selfhost4/cs/program.cs#4)]
     <!-- TODO: review snippet reference [!code-vb[CFX_SelfHost4#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/cfx_selfhost4/vb/module1.vb#4)]  -->  
  
    > [!NOTE]
    >  此示例使用默认终结点，且该服务不需要任何配置文件。如果未配置任何终结点，则运行时会为该服务实现的每个服务协定的每个基地址创建一个终结点[!INCLUDE[crabout](../../../includes/crabout-md.md)]默认终结点的更多信息，请参见[简化配置](../../../docs/framework/wcf/simplified-configuration.md)和 [WCF 服务的简化配置](../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md)。  
  
9. 按 Ctrl\+Shift\+B 生成解决方案。  
  
### 测试服务  
  
1.  按 Ctrl\+F5 运行服务。  
  
2.  打开**“WCF 测试客户端”**。  
  
    > [!TIP]
    >  若要打开**“WCF 测试客户端”**，请打开 [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] 命令提示符，然后执行**“WcfTestClient.exe”**。  
  
3.  从**“文件”**菜单中选择**“添加服务...”**。  
  
4.  在地址框中键入 `http://localhost:8080/hello`，然后单击**“确定”**。  
  
    > [!TIP]
    >  确保服务正在运行，否则此步骤将失败。如果已经更改了代码中的基址，则在此步骤中使用修改后的基址。  
  
5.  双击**“我的服务项目”**节点下的**“SayHello”**。在**“请求”**列表的**“值”**列中，键入您的姓名，然后单击**“调用”**。此时，**“响应”**列表中将显示一条答复消息。  
  
## 示例  
 下面的示例创建 <xref:System.ServiceModel.ServiceHost> 对象以承载 `HelloWorldService` 类型的服务，然后调用 <xref:System.ServiceModel.ServiceHost> 上的 <xref:System.ServiceModel.ICommunicationObject.Open%2A> 方法。在代码中提供基址，启用元数据发布，并使用默认终结点。  
  
 [!code-csharp[CFX_SelfHost4#5](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_selfhost4/cs/program.cs#5)]
 [!code-vb[CFX_SelfHost4#5](../../../samples/snippets/visualbasic/VS_Snippets_CFX/cfx_selfhost4/vb/module1.vb#5)]  
  
## 请参阅  
 <xref:System.Uri>   
 <xref:System.Configuration.ConfigurationManager.AppSettings%2A>   
 <xref:System.Configuration.ConfigurationManager>   
 [如何：在 IIS 中承载 WCF 服务](../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-iis.md)   
 [自承载](../../../docs/framework/wcf/samples/self-host.md)   
 [承载服务](../../../docs/framework/wcf/hosting-services.md)   
 [如何：定义服务协定](../../../docs/framework/wcf/how-to-define-a-wcf-service-contract.md)   
 [如何：实现服务协定](../../../docs/framework/wcf/how-to-implement-a-wcf-contract.md)   
 [ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)   
 [使用绑定配置服务和客户端](../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)   
 [系统提供的绑定](../../../docs/framework/wcf/system-provided-bindings.md)