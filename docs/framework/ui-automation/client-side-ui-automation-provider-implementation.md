---
title: "Client-Side UI Automation Provider Implementation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "UI Automation, client-side provider implementation"
  - "client-side UI Automation provider, implementation"
  - "provider implementation, UI Automation"
ms.assetid: 3584c0a1-9cd0-4968-8b63-b06390890ef6
caps.latest.revision: 14
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 13
---
# Client-Side UI Automation Provider Implementation
> [!NOTE]
>  本文档适用于想要使用 <xref:System.Windows.Automation> 命名空间中定义的托管 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 类的 .NET Framework 开发人员。 有关 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 的最新信息，请参阅 [Windows 自动化 API：UI 自动化](http://go.microsoft.com/fwlink/?LinkID=156746)。  
  
 几种不同的 [!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)] 框架在 [!INCLUDE[TLA#tla_ms](../../../includes/tlasharptla-ms-md.md)] 操作系统内部使用，包括 [!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)]、[!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)] 和 [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)]。[!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)]向客户公开有关 UI 元素的信息。 但是，[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]本身并不了解存在于这些框架中的不同类型的控件以及从中提取信息所需的技术。 而是将此任务留给称为提供程序的对象。 一个提供程序从特定控件中提取信息，并将该信息传递给 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]，后者随后以一致的方式将其呈现给客户端。  
  
 提供程序可以存在于服务器端或客户端上。 服务器端提供程序由控件本身实现。[!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] 元素实现提供程序，正如可以在考虑到 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]的情况下写入第三方控件一样。  
  
 但较旧的控件（例如 [!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)] 和 [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)] 中的控件）不直接支持 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]。 这些控件都将改为由存在于客户端进程中的提供程序提供，并且使用跨进程通信获取有关控件的信息；例如，通过监视在窗口与控件之间来回的消息。 此类客户端提供程序有时称为代理。  
  
 [!INCLUDE[TLA2#tla_winvista](../../../includes/tla2sharptla-winvista-md.md)] 为标准的 [!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)] 和 [!INCLUDE[TLA2#tla_winforms](../../../includes/tla2sharptla-winforms-md.md)]控件提供提供程序。 此外，回退提供程序为任何不由另一个服务器端提供程序或代理提供、但具有 [!INCLUDE[TLA#tla_aa](../../../includes/tlasharptla-aa-md.md)] 实现的控件提供部分 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]支持。 所有这样的提供程序均已自动加载，并且可供客户端应用程序使用。  
  
 有关 [!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)] 和 [!INCLUDE[TLA2#tla_winforms](../../../includes/tla2sharptla-winforms-md.md)]控件支持的详细信息，请参阅 [UI Automation Support for Standard Controls](../../../docs/framework/ui-automation/ui-automation-support-for-standard-controls.md)。  
  
 应用程序还可以注册其他客户端提供程序。  
  
<a name="Distributing_Client-Side_Providers"></a>   
## 分布客户端提供程序  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]预期在托管代码程序集中查找客户端提供程序。 此程序集中命名空间的名称应与程序集名称相同。 例如，名为 ContosoProxies.dll 的程序集将包含 ContosoProxies 命名空间。 在命名空间内创建一个 <xref:UIAutomationClientsideProviders.UIAutomationClientSideProviders> 类。 在静态 <xref:UIAutomationClientsideProviders.UIAutomationClientSideProviders.ClientSideProviderDescriptionTable> 字段的实现中，创建一个描述提供程序的 <xref:System.Windows.Automation.ClientSideProviderDescription> 结构数组。  
  
<a name="Registering_and_Configuring_Client-Side_Providers"></a>   
## 注册并配置客户端提供程序  
 [!INCLUDE[TLA#tla_dll](../../../includes/tlasharptla-dll-md.md)] 中的客户端提供程序通过调用 <xref:System.Windows.Automation.ClientSettings.RegisterClientSideProviderAssembly%2A> 加载。 客户端应用程序不需要任何进一步的操作即可使用提供程序。  
  
 在客户端自己的代码中实现的提供程序通过使用 <xref:System.Windows.Automation.ClientSettings.RegisterClientSideProviders%2A> 注册。 此方法将 <xref:System.Windows.Automation.ClientSideProviderDescription> 结构数组作为参数，每个结构均指定以下属性：  
  
-   创建提供程序对象的回调函数。  
  
-   提供程序将提供的控件的类名。  
  
-   提供程序将提供的应用程序（通常为可执行文件的完整名称）的映像名称。  
  
-   控制如何将类名与在目标应用程序中找到的窗口类进行匹配的标志。  
  
 最后两个参数为可选。 当客户端需要为不同的应用程序使用不同的提供程序时，它可能会指定目标应用程序的映像名称。 例如，客户端可能会为支持“多视图”模式的已知应用程序中的 [!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)] 列表视图控件使用一个提供程序，为不支持“多视图”模式的另一个已知应用程序中的类似控件使用另一个提供程序。  
  
## 请参阅  
 [Create a Client\-Side UI Automation Provider](../../../docs/framework/ui-automation/create-a-client-side-ui-automation-provider.md)   
 [Implement UI Automation Providers in a Client Application](../../../docs/framework/ui-automation/implement-ui-automation-providers-in-a-client-application.md)