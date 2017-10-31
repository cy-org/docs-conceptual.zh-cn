---
title: "DiscoveryClient 和 DynamicEndpoint | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7cd418f0-0eab-48d1-a493-7eb907867ec3
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# DiscoveryClient 和 DynamicEndpoint
<xref:System.ServiceModel.Discovery.DiscoveryClient> 和 <xref:System.ServiceModel.Discovery.DynamicEndpoint> 是两类在客户端端用来搜索服务。<xref:System.ServiceModel.Discovery.DiscoveryClient> 为您提供的与特定集的条件相匹配的服务列表，并允许您连接到的服务。<xref:System.ServiceModel.Discovery.DynamicEndpoint> 执行的操作相同，另外，会自动连接到一个被发现的服务。可以将任何终结点转换为 <xref:System.ServiceModel.Discovery.DynamicEndpoint>，也可以在配置中添加搜索条件。因此，如果您需要在解决方案中执行发现操作但不希望修改客户端逻辑，则 <xref:System.ServiceModel.Discovery.DynamicEndpoint> 会非常有用，此时您只需要修改终结点。<xref:System.ServiceModel.Discovery.DiscoveryClient> 另一方面可用于获得更好的控制您的搜索操作。下面对每个类的用途和优势加以详细说明。  
  
## DiscoveryClient  
 <xref:System.ServiceModel.Discovery.DiscoveryClient> 定义同步和异步 Find 方法以及 <xref:System.ServiceModel.Discovery.DiscoveryClient.FindCompleted> 和 <xref:System.ServiceModel.Discovery.DiscoveryClient.FindProgressChanged> 事件。它还定义了同步和异步 Resolve 方法以及 <xref:System.ServiceModel.Discovery.DiscoveryClient.ResolveCompleted> 事件。使用 <xref:System.ServiceModel.Discovery.DiscoveryClient.Find%2A> 或 <xref:System.ServiceModel.Discovery.DiscoveryClient.FindAsync%2A> 方法可以搜索服务。这两个方法都接受 <xref:System.ServiceModel.Discovery.FindCriteria> 实例，该实例可用于指定协定类型名称、作用域、最大请求结果数和作用域匹配规则。<xref:System.ServiceModel.Discovery.DiscoveryClient.FindCompleted> 和 <xref:System.ServiceModel.Discovery.DiscoveryClient.FindProgressChanged> 调用时，可以使用事件 <xref:System.ServiceModel.Discovery.DiscoveryClient.FindAsync%2A> 方法。<xref:System.ServiceModel.Discovery.DiscoveryClient.FindProgressChanged> 每当发射 <xref:System.ServiceModel.Discovery.DiscoveryClient> 从服务接收到响应。可使用该事件来显示指示查找操作进度的进度栏。它还可用来在接收到查找响应时对这些响应进行操作。查找操作完成时激发 <xref:System.ServiceModel.Discovery.DiscoveryClient.FindCompleted> 事件。如果已接收到最大响应数或 <xref:System.ServiceModel.Discovery.FindCriteria.Duration%2A> 已结束，则可能发生此情况。查找操作完成时，将在 <xref:System.ServiceModel.Discovery.FindResponse> 实例中返回结果。<xref:System.ServiceModel.Discovery.FindResponse> 包含 <xref:System.ServiceModel.Discovery.EndpointDiscoveryMetadata> 的集合，该集合包含地址、协定类型名称、扩展、侦听 URI 和匹配的服务的作用域。然后，您可以使用这些信息连接到匹配的服务并调用其中一个服务。下面的示例演示如何调用 [the M:System.ServiceModel.Discovery.DiscoveryClient.Find\(System.ServiceModel.Discovery.FindCriteria\)](assetId:///the M:System.ServiceModel.Discovery.DiscoveryClient.Find(System.ServiceModel.Discovery.FindCriteria)?qualifyHint=False&autoUpgrade=True) 方法并使用返回的元数据调用找到的服务。使用 <xref:System.ServiceModel.Discovery.DiscoveryClient> 的优势是可以缓存已找到的终结点列表并在以后使用这些终结点。通过此缓存，您可以构建自定义逻辑来处理各种失败情况。  
  
```  
DiscoveryClient dc = new DiscoveryClient(new UdpDiscoveryEndpoint());  
  
FindCriteria criteria = new FindCriteria(typeof(ICalculatorService));  
FindResponse fr = dc.Find(criteria);  
  
if (fr.Endpoints.Count > 0)  
{  
   EndpointAddress ep = fr.Endpoints[0].Address;  
   CalculatorServiceClient client = new CalculatorServiceClient();  
  
    // Connect to the discovered service endpoint  
   client.Endpoint.Address = endpointAddress;  
   Console.WriteLine("Invoking CalculatorService at {0}", endpointAddress);  
  
   double value1 = 100.00D;  
   double value2 = 15.99D;  
  
   // Call the Add service operation.  
   double result = client.Add(value1, value2);  
   Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);  
}  
else  
   Console.WriteLine(“No matching endpoints found”);  
  
```  
  
 下面的示例演示如何采用异步方式执行查找操作。  
  
```  
static void FindServiceAsync()  
{  
   DiscoveryClient dc = new DiscoveryClient(new UdpDiscoveryEndpoint());   
   dc.FindCompleted += new EventHandler<FindCompletedEventArgs>( discoveryClient_FindCompleted);  
   dc.FindProgressChanged += new EventHandler<FindProgressChangedEventArgs>(discoveryClient_FindProgressChanged);  
   dc.FindAsync(new FindCriteria(typeof(ICalculatorService)));   
}   
static void discoveryClient_FindProgressChanged(object sender, FindProgressChangedEventArgs e)  
{  
   Console.WriteLine("Found service at: " + e.EndpointDiscoveryMetadata.Address  
}   
  
static void discoveryClient_FindCompleted(object sender, FindCompletedEventArgs e)  
{    
      if (e.Result.Endpoints.Count > 0)  
            {  
                EndpointAddress ep = e.Result.Endpoints[0].Address;  
                CalculatorServiceClient client = new CalculatorServiceClient();  
  
                // Connect to the discovered service endpoint  
                client.Endpoint.Address = ep;  
                Console.WriteLine("Invoking CalculatorService at {0}", ep);  
  
                double value1 = 100.00D;  
                double value2 = 15.99D;  
  
                double result = client.Add(value1, value2);  
                Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);  
            }  
            else  
                Console.WriteLine("No matching endpoints found");  
  
        }  
  
```  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]执行异步查找调用的更多信息，请参见[异步查找](../../../../docs/framework/wcf/samples/asynchronous-find-sample.md)。  
  
 使用 <xref:System.ServiceModel.Discovery.DiscoveryClient.Resolve%2A> 和 <xref:System.ServiceModel.Discovery.ResolveAsync%28System.ServiceModel.Discovery.ResolveCriteria%29> 方法可以查找基于其终结点地址的服务。如果终结点地址不是网络可寻址地址，则此操作非常有用。Resolve 方法接受 <xref:System.ServiceModel.Discovery.ResolveCriteria> 的实例，该实例可用于指定要解析的服务终结点地址、解析操作的最大持续时间和一组扩展。下面的示例演示如何使用 <xref:System.ServiceModel.Discovery.DiscoveryClient.Resolve%2A> 方法来解析服务。  
  
```  
DiscoveryClient dc = new DiscoveryClient(new UdpDiscoveryEndpoint());  
ResolveCriteria criteria = new ResolveCriteria(endpointAddress);  
ResolveResponse response = dc.Resolve(criteria);  
EndpointAddress newEp = response.EndpointDiscoveryMetadata.Address;  
  
```  
  
## DynamicEndpoint  
 <xref:System.ServiceModel.Discovery.DynamicEndpoint> 是一个标准终结点（[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][标准终结点](../../../../docs/framework/wcf/feature-details/standard-endpoints.md)），它执行发现操作并自动选择匹配的服务。只需要创建一个传入要搜索的协定和要使用的绑定的 <xref:System.ServiceModel.Discovery.DynamicEndpoint>，然后将 <xref:System.ServiceModel.Discovery.DynamicEndpoint> 实例传递给 WCF 客户端。下面的示例演示如何创建并使用 <xref:System.ServiceModel.Discovery.DynamicEndpoint> 来调用计算器服务。每次打开客户端时都会执行发现操作。还可以通过向终结点配置元素添加 `kind =”dynamicEndpoint”` 特性，将配置中定义的任何终结点转换为 <xref:System.ServiceModel.Discovery.DynamicEndpoint>。  
  
```  
  
DynamicEndpoint dynamicEndpoint = new DynamicEndpoint(ContractDescription.GetContract(typeof(ICalculatorService)), new WSHttpBinding());  
CalculatorServiceClient client = new CalculatorServiceClient(dynamicEndpoint);  
  
Console.WriteLine("Invoking CalculatorService");  
Console.WriteLine();  
  
double value1 = 100.00D;  
double value2 = 15.99D;  
  
double result = client.Add(value1, value2);  
Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);  
  
```  
  
## 请参阅  
 [通过范围进行发现](../../../../docs/framework/wcf/samples/discovery-with-scopes-sample.md)   
 [异步查找](../../../../docs/framework/wcf/samples/asynchronous-find-sample.md)   
 [Basic](../../../../docs/framework/wcf/samples/basic-sample.md)