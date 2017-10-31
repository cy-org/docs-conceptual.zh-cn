---
title: "管理数据服务上下文（WCF 数据服务） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 15b19d09-7de7-4638-9556-6ef396cc45ec
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 管理数据服务上下文（WCF 数据服务）
<xref:System.Data.Services.Client.DataServiceContext> 类封装针对指定数据服务支持的操作。  尽管 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 服务是无状态的，但上下文不是。  因此，可使用 <xref:System.Data.Services.Client.DataServiceContext> 类在数据服务的各个交互之间保持客户端的状态，以支持诸如更改管理之类的功能。  该类还对更改的标识和跟踪进行管理。  
  
## 合并选项和标识解析  
 当执行 <xref:System.Data.Services.Client.DataServiceQuery%601> 时，响应源中的实体将具体化为对象。  有关详细信息，请参阅[对象具体化](../../../../docs/framework/data/wcf/object-materialization-wcf-data-services.md)。  将响应消息中的项具体化为对象所采用的方式将基于标识解析，并且依赖于执行查询时所依据的合并选项。  在单一 <xref:System.Data.Services.Client.DataServiceContext> 范围内执行多个查询或加载请求时，[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]客户端将只跟踪具有特定键值的单个对象实例。  用于执行标识解析的此键唯一地标识一个实体。  
  
 默认情况下，客户端只针对 <xref:System.Data.Services.Client.DataServiceContext> 尚未跟踪的实体，将响应源中的项具体化为对象。  这意味着不会覆盖缓存中已存在的对象更改。  此行为通过为查询和加载操作指定 <xref:System.Data.Services.Client.MergeOption> 值进行控制。  通过设置 <xref:System.Data.Services.Client.DataServiceContext> 的 <xref:System.Data.Services.Client.DataServiceContext.MergeOption%2A> 属性可指定此选项。  默认的合并选项值为 <xref:System.Data.Services.Client.MergeOption>。  这样将只为尚未进行跟踪的实体具体化对象，这意味着不会覆盖现有对象。  防止数据服务中的更新覆盖客户端上的对象更改的另一种方式是指定 <xref:System.Data.Services.Client.MergeOption>。  当指定 <xref:System.Data.Services.Client.MergeOption> 时，客户端上对象的值将替换为响应源中对应项的最新值，即使已对这些对象进行了更改也是如此。  当使用 <xref:System.Data.Services.Client.MergeOption> 合并选项时，<xref:System.Data.Services.Client.DataServiceContext> 无法将对客户端对象所做的更改发送到数据服务。  使用此选项时，将始终用数据服务中的值覆盖更改。  
  
## 管理并发  
 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 支持使数据服务能够检测更新冲突的乐观并发。  可以按这种方式配置数据服务提供程序，使得数据服务能够使用并发标记检查实体是否更改。  此标记包含实体类型的一个或多个属性，数据服务通过验证这些属性来确定某个资源是否已更改。  并发标记包含在发送给数据服务的请求和从数据服务发出的响应的 eTag 标头中，由 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]客户端进行管理。有关更多信息，请参见[更新数据服务](../../../../docs/framework/data/wcf/updating-the-data-service-wcf-data-services.md)。  
  
 <xref:System.Data.Services.Client.DataServiceContext> 通过使用 <xref:System.Data.Services.Client.DataServiceContext.AddObject%2A>、<xref:System.Data.Services.Client.DataServiceContext.UpdateObject%2A> 和 <xref:System.Data.Services.Client.DataServiceContext.DeleteObject%2A> 或通过 <xref:System.Data.Services.Client.DataServiceCollection%601> 跟踪已手动报告的对对象所做的更改。  当调用 <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> 方法时，客户端将更改发送回数据服务。  如果客户端中的数据更改与数据服务中的更改冲突，则 <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> 会失败。  当发生这种情况时，您必须再次查询实体资源以接收更新数据。  若要覆盖数据服务中的更改，请使用 <xref:System.Data.Services.Client.MergeOption> 合并选项执行查询。  再次调用 <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> 时，只要尚未对数据服务中的资源进行其他更改，客户端上保留的更改将永久保存到数据服务。  
  
## 保存更改  
 在 <xref:System.Data.Services.Client.DataServiceContext> 实例中对更改进行跟踪，但不会将更改立即发送到服务器。  在完成对指定活动的所需更改后，调用 <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> 以将所有更改提交给数据服务。  <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> 操作完成后，会返回 <xref:System.Data.Services.Client.DataServiceResponse> 对象。  <xref:System.Data.Services.Client.DataServiceResponse> 对象包括一系列 <xref:System.Data.Services.Client.OperationResponse> 对象，这些对象依次又包含一系列表示已保留或尝试的更改的 <xref:System.Data.Services.Client.EntityDescriptor> 或 <xref:System.Data.Services.Client.LinkDescriptor> 实例。  在数据服务中创建或修改实体之后，<xref:System.Data.Services.Client.EntityDescriptor> 包含对已更新实体的引用，其中包括所有服务器生成的属性值，例如上面示例中生成的 `ProductID` 值。  客户端库将使用这些新值自动更新 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 对象。  
  
 对于成功的插入和更新操作，与操作关联的 <xref:System.Data.Services.Client.EntityDescriptor> 或 <xref:System.Data.Services.Client.LinkDescriptor> 对象的状态属性设置为 <xref:System.Data.Services.Client.EntityStates>，并通过使用 <xref:System.Data.Services.Client.MergeOption> 合并新值。  如果数据服务中的插入、更新或删除操作失败，则实体状态保持在调用 <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> 之前的状态，并且 <xref:System.Data.Services.Client.OperationResponse> 的 <xref:System.Data.Services.Client.OperationResponse.Error%2A> 属性设置为包含有关该错误的信息的 <xref:System.Data.Services.Client.DataServiceRequestException>。  有关详细信息，请参阅[更新数据服务](../../../../docs/framework/data/wcf/updating-the-data-service-wcf-data-services.md)。  
  
### 为更新设置 HTTP 方法  
 默认情况下，.NET Framework 客户端库将更新作为 MERGE 请求发送至现有实体。  MERGE 请求将更新实体的选定属性；但客户端始终会在 MERGE 请求中包含所有属性，即使是未更改的属性也包含在内。  [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 协议还支持发送 PUT 请求以更新实体。  在 PUT 请求中，现有实体实际上将替换为该实体的一个新实例，新实例具有来自客户端的属性值。  要使用 PUT 请求，请在调用 <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> 时为 <xref:System.Data.Services.Client.SaveChangesOptions> 枚举设置 <xref:System.Data.Services.Client.SaveChangesOptions> 标志。  
  
> [!NOTE]
>  当客户端不知道实体的所有属性时，PUT 请求的行为会与 MERGE 请求不同。  当将某个实体类型投影到客户端上的新类型时，可能会发生这种情况。  当新属性已经添加到服务数据模型中的实体中，同时 <xref:System.Data.Services.Client.DataServiceContext> 的 <xref:System.Data.Services.Client.DataServiceContext.IgnoreMissingProperties%2A> 属性设置为 `true` 以忽略这类客户端映射错误时，也会发生这种情况。  在这种情况下，PUT 请求会将客户端未知的任何属性重置为默认值。  
  
### POST 隧道  
 默认情况下，客户端库通过使用 POST、GET、PUT\/MERGE\/PATCH 和 DELETE 等 HTTP 方法相应地向 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 服务发送创建、读取、更新和删除请求。  这保持了具象状态传输 \(REST\) 的基本原则。  不过，不是每个 Web 服务器实现都支持完整的 HTTP 方法集。  在某些情况下，支持的方法可能仅限 GET 和 POST。  在中介（如防火墙）用某些方法阻止请求时，可能会发生这种情况。  因为 GET 和 POST 方法是支持最多的方法，所以 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 指定了一种方法，通过使用 POST 请求执行任何不受支持的 HTTP方法。  这种方法称为“方法隧道”或“POST 隧道”，使客户端能够发送 POST 请求，而在自定义 `X-HTTP-Method` 标头中指定实际方法。  要为请求启用 POST 隧道，请将 <xref:System.Data.Services.Client.DataServiceContext> 实例上的 <xref:System.Data.Services.Client.DataServiceContext.UsePostTunneling%2A> 属性设置为 `true`。  
  
## 请参阅  
 [WCF 数据服务客户端库](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)   
 [更新数据服务](../../../../docs/framework/data/wcf/updating-the-data-service-wcf-data-services.md)   
 [异步操作](../../../../docs/framework/data/wcf/asynchronous-operations-wcf-data-services.md)   
 [批处理操作](../../../../docs/framework/data/wcf/batching-operations-wcf-data-services.md)