---
title: "异步操作（WCF 数据服务） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "异步操作 [WCF 数据服务]"
  - "WCF 数据服务, 异步操作"
  - "WCF 数据服务, 客户端库"
ms.assetid: 679644c7-e3fc-422c-b14a-b44b683900d0
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 异步操作（WCF 数据服务）
与内部网络中运行的应用程序相比，Web 应用程序必须适应客户端与服务器之间更长时间的延迟。  若要优化应用程序的性能和用户体验，建议您在通过 Web 访问 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 服务器时使用 <xref:System.Data.Services.Client.DataServiceContext> 和 <xref:System.Data.Services.Client.DataServiceQuery%601> 类的异步方法。  
  
 尽管 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 服务器异步处理 HTTP 请求，但是 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 客户端库的某些方法是同步的，并且会一直等到整个请求\-响应交换完成后才会继续执行。  [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 客户端库的异步方法不会等待此交换完成，并且允许应用程序同时保持具有响应能力的用户界面。  
  
 通过使用 <xref:System.Data.Services.Client.DataServiceContext> 和 <xref:System.Data.Services.Client.DataServiceQuery%601> 类的一对方法（分别以 *Begin* 和 *End* 开头），可以执行异步操作。  *Begin* 方法注册一个委托，服务将在操作完成时调用该委托。  应在注册的委托中调用 *End* 方法以处理来自已完成操作的回调。  在调用 *End* 方法以完成异步操作时，必须从用于开始该操作的那个 <xref:System.Data.Services.Client.DataServiceQuery%601> 或 <xref:System.Data.Services.Client.DataServiceContext> 实例进行调用。  每个 *Begin* 方法采用一个 `state` 参数，该参数可将一个状态对象传递给回调。  此状态对象是从 <xref:System.IAsyncResult> 中检索的，后者随回调提供，用于调用对应的 *End* 方法以完成异步操作。  例如，如果在对 <xref:System.Data.Services.Client.DataServiceQuery%601> 实例调用 <xref:System.Data.Services.Client.DataServiceQuery%601.BeginExecute%2A> 方法时提供该实例作为 `state` 参数，那么 <xref:System.IAsyncResult> 将返回同一个 <xref:System.Data.Services.Client.DataServiceQuery%601> 实例。  随后将使用 <xref:System.Data.Services.Client.DataServiceQuery%601> 的这个实例调用 <xref:System.Data.Services.Client.DataServiceQuery%601.EndExecute%2A> 方法以完成查询操作。  有关详细信息，请参阅[如何：执行异步数据服务查询](../../../../docs/framework/data/wcf/how-to-execute-asynchronous-data-service-queries-wcf-data-services.md)。  
  
> [!NOTE]
>  .NET Framework for Silverlight 中提供的客户端库仅支持异步操作。  有关更多信息，请参见 [WCF 数据服务 \(Silverlight\)](http://go.microsoft.com/fwlink/?LinkID=143149)（可能为英文网页）。  
  
 .NET Framework 客户端库支持下列异步操作：  
  
|操作|方法|  
|--------|--------|  
|执行 <xref:System.Data.Services.Client.DataServiceQuery%601>。|-   <xref:System.Data.Services.Client.DataServiceQuery%601.BeginExecute%2A><br />-   <xref:System.Data.Services.Client.DataServiceQuery%601.EndExecute%2A>|  
|从 <xref:System.Data.Services.Client.DataServiceContext> 执行查询。|-   <xref:System.Data.Services.Client.DataServiceContext.BeginExecute%2A><br />-   <xref:System.Data.Services.Client.DataServiceContext.EndExecute%2A>|  
|从 <xref:System.Data.Services.Client.DataServiceContext> 执行批查询。|-   <xref:System.Data.Services.Client.DataServiceContext.BeginExecuteBatch%2A><br />-   <xref:System.Data.Services.Client.DataServiceContext.EndExecuteBatch%2A>|  
|将相关实体加载到 <xref:System.Data.Services.Client.DataServiceContext> 中。|-   <xref:System.Data.Services.Client.DataServiceContext.BeginLoadProperty%2A><br />-   <xref:System.Data.Services.Client.DataServiceContext.EndLoadProperty%2A>|  
|保存对 <xref:System.Data.Services.Client.DataServiceContext> 中对象的更改|-   <xref:System.Data.Services.Client.DataServiceContext.BeginSaveChanges%2A><br />-   <xref:System.Data.Services.Client.DataServiceContext.EndSaveChanges%2A>|  
  
## 异步操作的线程注意事项  
 在多线程应用程序中，不一定会在用于调用 *Begin* 方法的那个线程（即创建初始请求的线程）中调用针对异步操作注册为回调的委托。  对于必须在特定线程中调用回调的应用程序，必须将处理响应的 *End* 方法的执行显式封送至所需线程。  例如，在基于 Windows Presentation Foundation \(WPF\) 的应用程序和基于 Silverlight 的应用程序中，必须通过对 <xref:System.Windows.Threading.Dispatcher> 对象使用 <xref:System.Windows.Threading.Dispatcher.BeginInvoke%2A> 方法，将响应封送回 UI 线程。  有关详细信息，请参阅[Querying the Data Service \(WCF Data Services\/Silverlight\)](http://msdn.microsoft.com/zh-cn/3a7cdc07-c37e-4da2-b98b-c3763fd0970b)。  
  
## 请参阅  
 [WCF 数据服务客户端库](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)