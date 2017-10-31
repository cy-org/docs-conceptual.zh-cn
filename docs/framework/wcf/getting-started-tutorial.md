---
title: "入门教程 | Microsoft Docs"
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
  - "入门 [WCF]"
  - "WCF [WCF], 入门"
  - "Windows Communication Foundation [WCF], 入门"
ms.assetid: df939177-73cb-4440-bd95-092a421516a1
caps.latest.revision: 47
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 47
---
# 入门教程
本节中包含的主题旨在帮助您快速了解 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 编程体验。  这些主题要根据本主题底部的列表中的顺序完成。  通过学习本教程，您可以初步了解创建 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务和客户端应用程序所需的步骤。  服务公开一个或多个终结点，其中每个终结点都公开一项或多项服务操作。  服务的终结点指定下列信息：服务所在的位置；一个绑定，其中包含描述客户端必须如何与服务进行通信的信息；一个协定，用于定义服务向其客户端提供的功能。  
  
 在完成本教程中的系列主题之后，您将会得到一个正在运行的服务，以及一个可以调用该服务的客户端。  前三个主题描述如何定义服务协定、如何实现服务协定以及如何承载服务。  创建的服务自承载在控制台应用程序中。  服务还可在 Internet Information Services \(IIS\) 下承载。  [!INCLUDE[crabout](../../../includes/crabout-md.md)]如何进行此操作的更多信息，请参见[如何：在 IIS 中承载 WCF 服务](../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-iis.md)。  在代码中配置服务；不过，也可以在配置文件中配置服务。  [!INCLUDE[crabout](../../../includes/crabout-md.md)]使用配置文件的更多信息，请参见[使用配置文件配置服务](../../../docs/framework/wcf/configuring-services-using-configuration-files.md)。  
  
 后三个主题描述如何创建客户端代理，如何配置客户端应用程序，以及如何使用客户端代理调用由服务公开的操作。  服务发布定义客户端应用程序与服务进行通信所需信息的元数据。  [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] 自动化访问此元数据的过程，并使用它来构建和配置服务的客户端应用程序。  如果您没有使用 [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)]，则可以使用 [ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 构建和配置服务的客户端应用程序。  
  
 本节中的所有主题均假定您使用 Visual Studio 2011 作为开发环境。  如果您使用的是其他开发环境，请忽略特定于 [!INCLUDE[vs_current_short](../../../includes/vs-current-short-md.md)] 的说明。  
  
> [!NOTE]
>  如果运行的是 [!INCLUDE[wv](../../../includes/wv-md.md)] 或 Windows 操作系统的更高版本，则必须通过在“开始”菜单上右击 Microsoft Visual Studio 2011，然后选择**“以管理员身份运行”**的方式来启动 [!INCLUDE[vs_current_short](../../../includes/vs-current-short-md.md)]。  若要始终以管理员身份启动 Visual Studio 2011，可以创建一个快捷方式，右击该快捷方式，选择“属性”，选择**“兼容性”**选项卡，然后选中**“请以管理员身份运行该程序”**复选框。  在使用此快捷方式启动 Visual Studio 2011 时，会总是以管理员身份运行。  
  
 有关可以下载到硬盘中并运行的示例应用程序，请参见 [Windows Communication Foundation Samples](http://msdn.microsoft.com/zh-cn/8ec9d192-5d81-4f64-bfd3-90c5e5858c91)中的主题。  有关专门针对本主题的示例，请参见[入门](../../../docs/framework/wcf/samples/getting-started-sample.md)。  
  
 有关创建服务和客户端的更深入信息，请参见[基本 WCF 编程](../../../docs/framework/wcf/basic-wcf-programming.md)。  
  
## 本节内容  
 [如何：定义服务协定](../../../docs/framework/wcf/how-to-define-a-wcf-service-contract.md)  
 描述如何使用用户定义的接口创建 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 协定。  协定定义服务所公开的功能。  
  
 [如何：实现服务协定](../../../docs/framework/wcf/how-to-implement-a-wcf-contract.md)  
 描述如何实现服务协定。  一旦定义了某一协定后，必须使用某一服务类实现该协定。  
  
 [如何：承载和运行基本的服务](../../../docs/framework/wcf/how-to-host-and-run-a-basic-wcf-service.md)  
 描述如何在代码中配置服务的终结点，以及如何在控制台应用程序内承载服务。  若要激活服务，必须在运行时环境中配置和承载服务。  此环境将创建服务并控制其上下文和生存期。  
  
 [如何：创建客户端](../../../docs/framework/wcf/how-to-create-a-wcf-client.md)  
 描述如何从 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务检索用于创建 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端代理的元数据。  此进程使用 Visual Studio 2011 中的“添加服务引用”功能。  
  
 [如何：配置客户端](../../../docs/framework/wcf/how-to-configure-a-basic-wcf-client.md)  
 描述如何配置 WCF 客户端。配置客户端需要指定客户端用于访问服务的终结点。  
  
 [如何：使用客户端](../../../docs/framework/wcf/how-to-use-a-wcf-client.md)  
 描述如何使用 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端代理调用服务操作。  
  
## 参考  
 <xref:System.ServiceModel.ServiceContractAttribute>  
  
 <xref:System.ServiceModel.OperationContractAttribute>  
  
## 相关章节  
 [Windows Communication Foundation Samples](http://msdn.microsoft.com/zh-cn/8ec9d192-5d81-4f64-bfd3-90c5e5858c91)  
  
 [基本编程生命周期](../../../docs/framework/wcf/basic-programming-lifecycle.md)  
  
## 请参阅  
 [概念概述](../../../docs/framework/wcf/conceptual-overview.md)   
 [文档指南](../../../docs/framework/wcf/guide-to-the-documentation.md)   
 [什么是 Windows Communication Foundation](../../../docs/framework/wcf/whats-wcf.md)   
 [WCF 功能详细信息](../../../docs/framework/wcf/feature-details/index.md)