---
title: "WCF 服务和 ASP.NET | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b980496a-f0b0-4319-8e55-a0f0fa32da70
caps.latest.revision: 24
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 24
---
# WCF 服务和 ASP.NET
本主题讨论如何与 ASP.NET 并行承载 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务以及在 ASP.NET 兼容模式中承载它们。  
  
## 与 ASP.NET 并行承载 WCF  
 Internet 信息服务 \(IIS\) 中承载的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务可以与 .ASPX 页和 ASMX Web 服务一起位于单个公共应用程序域内。  ASP.NET 提供公共基础结构服务，例如 AppDomain 管理以及 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 与 ASP.NET HTTP 运行库的动态编译。  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的默认配置与 ASP.NET 是并行的。  
  
 ![WCF 服务和 ASP .NET：共享状态](../../../../docs/framework/wcf/feature-details/media/hostingwcfwithaspnet.gif "HostingWCFwithASPNET")  
  
 ASP.NET HTTP 运行库处理 ASP.NET 请求但不参与发送到 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务的请求处理，即使这些服务与 ASP.NET 内容一样承载在相同的 AppDomain 中，也是如此。  而 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务模型会截获发送到 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务的消息，并且通过 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 传输协议\/通道堆栈来路由这些消息。  
  
 并行模型的结果如下：  
  
-   ASP.NET 和 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务可以共享 AppDomain 状态。  由于两个框架可以在同一 AppDomain 中共存，因此，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 还可以与 ASP.NET 共享 AppDomain 状态（包括静态变量、事件，等等）。  
  
-   [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务的行为保持一致，不受宿主环境和传输协议的影响。  ASP.NET HTTP 运行库与 IIS\/ASP.NET 宿主环境和 HTTP 通信是有意耦合在一起的。  相反，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 旨在跨宿主环境保持行为一致（[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 在 IIS 的内部和外部的行为保持一致）以及跨传输协议保持行为一致（IIS 7.0 和更高版本中承载的服务在其公开的所有终结点之间保持行为一致，即使其中一些终结点使用 HTTP 之外的协议也是如此）。  
  
-   在 AppDomain 中，由 HTTP 运行库实现的功能适用于 ASP.NET 内容而不适用于 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]。  ASP.NET 应用程序平台的许多 HTTP 特定功能不适用于包含 ASP.NET 内容的 AppDomain 内承载的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务。  这些功能的示例包括：  
  
    -   HttpContext：从 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 内部进行访问时，<xref:System.Web.HttpContext.Current%2A> 始终为 `null`。  请改用 <xref:System.ServiceModel.OperationContext.Current.RequestContext>。  
  
    -   基于文件的授权：在确定是否对服务请求进行授权时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 安全模型不允许使用应用于服务的 .svc 文件的访问控制列表 \(ACL\)。  
  
    -   基于配置的 URL 授权：同样，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 安全模型不符合 System.Web 的 \<authorization\> 配置元素中指定的任何基于 URL 的授权规则。  如果服务驻留在由 ASP.NET 的 URL 授权规则提供保护的 URL 空间内，则对 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 请求将忽略这些设置。  
  
    -   HttpModule 扩展性：当引发 <xref:System.Web.HttpApplication.PostAuthenticateRequest> 事件且未将处理返回到 ASP.NET HTTP 管道时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 宿主基础结构截获 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 请求。  编码为在管道的后期截获请求的模块不截获 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 请求。  
  
    -   ASP.NET 模拟：默认情况下，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 请求总是作为 IIS 进程标识运行，即使将 ASP.NET 设置为使用 System.Web 的 \<identity impersonate\=”true” \/\> 配置选项来启用模拟也是如此。  
  
 这些限制仅应用于 IIS 应用程序中承载的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务。  ASP.NET 内容的行为不受 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 存在的影响。  
  
 需要由 HTTP 管道传统上提供的功能的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序应考虑使用独立于主机和传输协议的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 等效项：  
  
-   <xref:System.ServiceModel.OperationContext>，而不是 <xref:System.Web.HttpContext>。  
  
-   <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior>，而不是 ASP.NET 的文件\/URL 授权。  
  
-   <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector> 或自定义分层通道，而不是 HTTP 模块。  
  
-   使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的每个操作的模拟，而不是 System.Web 模拟。  
  
 或者，可以考虑在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的 ASP.NET 兼容模式中运行服务。  
  
## 在 ASP.NET 兼容模式中承载 WCF 服务  
 尽管 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 模型旨在跨宿主环境和传输保持行为的一致性，但经常在一些方案中，应用程序中不要求这种程度的灵活性。  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的 ASP.NET 兼容模式适用于具有以下特点的方案：不需要具有在 IIS 外部承载或通过 HTTP 之外的协议进行通信的能力，但使用 ASP.NET Web 应用程序平台的所有功能。  
  
 在默认的并行配置中，承载基础结构的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 截获 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 消息并将其路由到 HTTP 管道之外；与此不同的是，在 ASP.NET 兼容模式中运行的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务完全参与 ASP.NET HTTP 请求生命周期。  在兼容模式中，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务通过 <xref:System.Web.IHttpHandler> 实现来使用 HTTP 管道，其方式类似于处理 ASPX 页和 ASMX Web 服务的请求。  因此，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的行为在以下 ASP.NET 功能方面与 ASMX 相同：  
  
-   在 ASP.NET 兼容模式中运行的 <xref:System.Web.HttpContext>: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务可以访问 <xref:System.Web.HttpContext.Current%2A> 以及与其关联的状态。  
  
-   基于文件的授权：在 ASP.NET 兼容模式中运行的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务可以通过将文件系统访问控制列表 \(ACL\) 附加到服务的 .svc 文件来获得保护。  
  
-   可配置的 URL 授权：当 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务在 ASP.NET 兼容模式中运行时，将对 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 请求强制执行 ASP.NET 的 URL 授权规则。  
  
-   <xref:System.Web.HttpModuleCollection> 扩展性：由于在 ASP.NET 兼容模式中运行的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务完全参与 ASP.NET HTTP 请求生命周期，因此在 HTTP 管道中配置的任何 HTTP 模块能够在服务调用前后的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 请求上进行操作。  
  
-   ASP.NET 模拟：[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务使用 ASP.NET 模拟线程的当前标识来运行，如果已为应用程序启用 ASP.NET 模拟，则该标识可能与 IIS 进程标识不同。  如果为某个特定服务操作同时启用 ASP.NET 模拟和 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 模拟，则服务模拟最终使用从 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 获得的标识来运行。  
  
 可通过下面的配置（位于应用程序的 Web.config 文件中）在应用程序级别上启用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的 ASP.NET 兼容模式：  
  
```  
<system.serviceModel>  
    <serviceHostingEnvironment aspNetCompatibilityEnabled="true" />  
</system.serviceModel>  
```  
  
 如果没有指定，则此值默认为“`true`”。  若将此值设置为“`false`”，则指示在应用程序中运行的所有 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务将不在 ASP.NET 兼容模式中运行。  
  
 由于 ASP.NET 兼容模式暗含的请求处理语义与 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 默认值完全不同，因此单独的服务实现能够控制其是否在已启用 ASP.NET 兼容模式的应用程序内运行。  服务可以使用 <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsAttribute> 来指示其是否支持 ASP.NET 兼容模式。  此特性的默认值为 <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode>。  
  
 `[AspNetCompatibilityRequirements(RequirementsMode = AspNetCompatibilityRequirementsMode.Allowed)]`  
  
 `public class CalculatorService : ICalculatorSession`  
  
 `{//Implement calculator service methods.}`  
  
 下表演示应用程序范围的兼容模式设置如何与单独服务指定的支持级别交互：  
  
|应用程序范围的兼容模式设置|\[AspNetCompatibilityRequirementsMode\]<br /><br /> 设置|观察到的结果|  
|-------------------|----------------------------------------------------|------------|  
|aspNetCompatibilityEnabled \= “`true`”|<xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode>|服务成功激活。|  
|aspNetCompatibilityEnabled \= “`true`”|<xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode>|服务成功激活。|  
|aspNetCompatibilityEnabled \= “`true`”|<xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode>|服务接收消息时发生激活错误。|  
|aspNetCompatibilityEnabled \= “`false`”|<xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode>|服务接收消息时发生激活错误。|  
|aspNetCompatibilityEnabled \= “`false`”|<xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode>|服务成功激活。|  
|aspNetCompatibilityEnabled \= “`false`”|<xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode>|服务成功激活。|  
  
> [!NOTE]
>  IIS 7.0 和 WAS 允许 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务通过 HTTP 之外的协议进行通信。  但是，在已启用 ASP.NET 兼容模式的应用程序中运行的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务不允许公开非 HTTP 终结点。  在服务接收其第一条消息时，这种配置会生成激活异常。  
  
 有关为 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务启用 ASP.NET 兼容模式的更多信息，请参见 <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode> 和 [ASP.NET 兼容性](../../../../docs/framework/wcf/samples/aspnet-compatibility.md)示例。  
  
## 请参阅  
 <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsAttribute>   
 [Windows Server App Fabric 承载功能 （可能为英文网页）](http://go.microsoft.com/fwlink/?LinkId=201276)