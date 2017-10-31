---
title: "通过范围进行发现的示例 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6a37a754-6b8c-4ebe-bdf2-d4f0520271d5
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# 通过范围进行发现的示例
此示例演示如何使用范围对可发现的终结点进行分类，以及如何使用 <xref:System.ServiceModel.Discovery.DiscoveryClient> 来执行终结点的异步搜索。对于服务，此示例演示如何通过以下方法为每个终结点自定义发现：添加一个终结点发现行为并使用它将一个范围添加到该终结点，以及控制该终结点的可发现性。对于客户端，此示例演示客户端如何创建 <xref:System.ServiceModel.Discovery.DiscoveryClient>，以及如何通过将范围添加到 <xref:System.ServiceModel.Discovery.FindCriteria> 对搜索参数进行精细调整以包含范围。此示例还演示客户端如何通过添加终止条件来限制响应。  
  
## 服务功能  
 此项目演示添加到 <xref:System.ServiceModel.ServiceHost> 的两个服务终结点。每个终结点都具有一个与之关联的 <xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior>。此行为用于添加这两个终结点的 URI 范围。范围用于区分每个终结点，以便客户端可以对搜索进行精细调整。对于第二个终结点，可通过将 <xref:System.ServiceModel.Discovery.EndpointDiscoveryBehavior.Enabled%2A> 属性设置为 `false` 来禁用可发现性。这将确保与此终结点关联的发现元数据不会作为任何发现消息的一部分发送。  
  
## 客户端功能  
 `FindCalculatorServiceAddress()` 方法演示如何使用 <xref:System.ServiceModel.Discovery.DiscoveryClient> 并传入具有两个限制的 <xref:System.ServiceModel.Discovery.FindCriteria>。将一个范围添加到条件，并将 <xref:System.ServiceModel.Discovery.FindCriteria.MaxResults%2A> 属性设置为 1。此范围将结果限制为仅发布相同范围的服务。将 <xref:System.ServiceModel.Discovery.FindCriteria.MaxResults%2A> 设置为 1 可将 <xref:System.ServiceModel.Discovery.DiscoveryClient> 等待的响应限制为最多 1 个终结点。<xref:System.ServiceModel.Discovery.DiscoveryClient.Find%2A> 调用是一个同步操作，在达到超时或找到一个终结点之前，该同步操作将阻止该线程。  
  
#### 使用此示例  
  
1.  此示例使用 HTTP 终结点，若要运行此示例，必须添加正确的 URL ACL。有关详细信息，请参见[配置 HTTP 和 HTTPS](http://go.microsoft.com/fwlink/?LinkId=70353)（可能为英文网页）。使用提升的特权执行下面的命令应添加相应的 ACL。如果该命令无效，则可能需要使用您的域和用户名替换以下参数：`netsh http add urlacl url=http://+:8000/ user=%DOMAIN%\%UserName%`  
  
2.  生成解决方案。  
  
3.  从生成目录运行服务可执行文件。  
  
4.  运行客户端可执行文件。请注意，客户端能够查找该服务。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录。  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\Discovery\DiscoveryWithScopes`  
  
## 请参阅