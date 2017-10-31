---
title: "如何：创建 Windows Communication Foundation 客户端 | Microsoft Docs"
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
helpviewer_keywords: 
  - "客户端 [WCF], 运行"
  - "WCF 客户端 [WCF], 运行"
ms.assetid: a67884cc-1c4b-416b-8c96-5c954099f19f
caps.latest.revision: 64
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 64
---
# 如何：创建 Windows Communication Foundation 客户端
这是创建 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 应用程序所需的六项任务中的第四项任务。有关全部六项任务的概述，请参见[入门教程](../../../docs/framework/wcf/getting-started-tutorial.md)主题。  
  
 本主题描述如何检索 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务中的元数据，以及如何使用这些元数据创建可以访问该服务的 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 代理。通过使用 Visual Studio 提供的添加服务引用功能完成此任务。此工具从服务的 MEX 终结点获取元数据，并以所选语言（默认情况下为 C\#）为客户端代理生成托管源代码文件。除了创建客户端代理外，该工具还会为客户端创建或更新客户端配置文件，以使客户端应用程序能够连接至其某个终结点上的服务。  
  
> [!NOTE]
>  您还可以使用[ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)工具生成代理类和配置，而不使用 Visual Studio 内的添加服务引用。  
  
> [!WARNING]
>  当在 [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] 中从某个类库项目调用 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务时，可以使用添加服务引用功能自动生成代理和关联配置文件。该类库项目不会使用配置文件。需要将生成的配置文件中的设置添加到将调用该类库的可执行 app.config 文件中。  
  
 客户端应用程序使用生成的代理类与服务通信。[如何：使用客户端](../../../docs/framework/wcf/how-to-use-a-wcf-client.md)中对此过程进行了描述。  
  
### 创建 Windows Communication Foundation 客户端  
  
1.  通过右击入门解决方案，依次选择**“添加”**、**“新项目”**，创建新的控制台应用程序项目。在对话框左侧的**“添加新项目”** 对话框中，在**“C\#”**或**“VB”**下选择**“Windows”**。在对话框中的中心部分中选择**“控制台应用程序”**。为项目 `GettingStartedClient` 命名。  
  
2.  通过右击解决方案资源管理器中的**“GettingStartedClient”** 并选择**“属性”**，将 GettingStartedClient 项目的目标框架设置为 .NET Framework 4.5在标记的**“目标框架”**下拉框中，选择**“.NET Framework 4.5”**。设置 VB 项目的目标框架稍有不同，在 GettingStartedClient 项目属性对话框中，单击屏幕左侧的**“编译”**选项卡，然后单击对话框左下角的**“高级编译选项”**按钮。然后在标记的**“目标框架”**中选择**“.NET Framework 4.5”**。  
  
     设置目标框架将导致 Visual Studio 2011 重新加载解决方案，在提示时按**“确定”**。  
  
3.  通过右击解决方案资源管理器中 GettingStartedClient 项目下的**“引用”**文件夹，并选择**“添加”**引用，将对 System.ServiceModel 的引用添加到 GettingStartedClient 项目。在**“添加引用”**对话框中，选择对话框左侧的**“框架”**。请在搜索程序集文本框中，键入 `System.ServiceModel`。在对话框中的中心部分，选择**“System.ServiceModel”**，单击**“添加”**按钮，然后单击**“关闭”**按钮。在主菜单中单击**“全部保存”**按钮保存解决方案。  
  
4.  接下来，将计算器服务添加到服务引用。在此之前，必须先启动 GettingStartedHost 控制台应用程序。主机运行后，可在解决方案资源管理器中的 GettingStartedClient 项目下右击引用文件夹，选择添加服务引用，并在添加服务引用对话框的地址框中键入以下 URL： http:\/\/localhost:8000\/ServiceModelSamples\/Service，然后单击**“转到”**按钮。然后，CalculatorService 应显示在服务列表框中，双击 CalculatorService，然后它将展开并显示由该服务实现的服务协定。原样保留默认命名空间，并单击**“确定”**按钮。  
  
     使用 Visual Studio 将引用添加到服务时，解决方案资源管理器中 GettingStartedClient 项目下的服务引用文件夹下将显示新项。如果使用[ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 工具将，将生成一个源代码文件和 app.config 文件。  
  
     也可将命令行工具[ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 与适当的开关一起使用以创建客户端代码。下面的示例生成服务的代码文件和配置文件。第一个示例显示如何以 VB 生成代理，第二个示例显示如何以 C\# 生成代理：  
  
    ```  
    svcutil.exe /language:vb /out:generatedProxy.vb /config:app.config http://localhost:8000/ServiceModelSamples/service  
  
    ```  
  
    ```csharp  
    svcutil.exe /language:cs /out:generatedProxy.cs /config:app.config http://localhost:8000/ServiceModelSamples/service  
  
    ```  
  
 现在，您已创建了客户端应用程序将用于调用计数器服务的代理。继续该系列中的下一主题：[如何：配置客户端](../../../docs/framework/wcf/how-to-configure-a-basic-wcf-client.md)  
  
## 请参阅  
 [ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)   
 [入门](../../../docs/framework/wcf/samples/getting-started-sample.md)   
 [自承载](../../../docs/framework/wcf/samples/self-host.md)   
 [如何：使用配置文件发布服务的元数据](../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-a-configuration-file.md)   
 [如何：使用 Svcutil.exe 下载元数据文档](../../../docs/framework/wcf/feature-details/how-to-use-svcutil-exe-to-download-metadata-documents.md)