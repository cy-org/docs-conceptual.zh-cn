---
title: "基本示例 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c1910bc1-3d0a-4fa6-b12a-4ed6fe759620
caps.latest.revision: 17
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 17
---
# 基本示例
此示例演示如何使服务可发现以及如何搜索和调用可发现服务。  此示例由两个项目组成：服务项目和客户端项目。  
  
> [!NOTE]
>  此示例在代码中实现发现。  有关在配置中实现发现的示例，请参见[配置](../../../../docs/framework/wcf/samples/configuration-sample.md)。  
  
## 服务  
 这是一个简单计算器服务实现。  与发现相关的代码可以在 `Main` 中找到，其中向服务主机添加了一个 <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior>，并且添加了一个 <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>，如下面的代码所示。  
  
```  
using (ServiceHost serviceHost = new ServiceHost(typeof(CalculatorService), baseAddress))  
{  
    serviceHost.AddServiceEndpoint(typeof(ICalculatorService), new   
      WSHttpBinding(), String.Empty);  
  
    // Make the service discoverable over UDP multicast  
    serviceHost.Description.Behaviors.Add(new ServiceDiscoveryBehavior());                  
    serviceHost.AddServiceEndpoint(new UdpDiscoveryEndpoint());  
  
    serviceHost.Open();  
    // ...  
}  
```  
  
## 客户端  
 客户端使用 <xref:System.ServiceModel.Discovery.DynamicEndpoint> 定位服务。  标准终结点 <xref:System.ServiceModel.Discovery.DynamicEndpoint> 在打开客户端时解析服务的终结点。  在本例中，<xref:System.ServiceModel.Discovery.DynamicEndpoint> 基于服务协定查找服务。  默认情况下，<xref:System.ServiceModel.Discovery.DynamicEndpoint> 对 <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint> 进行搜索。  定位到服务终结点后，客户端便通过指定绑定连接到服务。  
  
```csharp  
public static void Main()  
{  
   DynamicEndpoint dynamicEndpoint = new DynamicEndpoint( ContractDescription.GetContract(typeof(ICalculatorService)), new WSHttpBinding());  
   // ...  
}              
```  
  
 客户端定义一个名为 `InvokeCalculatorService` 方法，该方法使用 <xref:System.ServiceModel.Discovery.DiscoveryClient> 类搜索服务。  <xref:System.ServiceModel.Discovery.DynamicEndpoint> 继承自 <xref:System.ServiceModel.Description.ServiceEndpoint>，因此可以传递给 `InvokeCalculatorService` 方法。  本示例随后使用 <xref:System.ServiceModel.Discovery.DynamicEndpoint> 创建 `CalculatorServiceClient` 的实例并调用计算器服务的各个操作。  
  
```csharp  
static void InvokeCalculatorService(ServiceEndpoint serviceEndpoint)  
{  
   // Create a client  
   CalculatorServiceClient client = new CalculatorServiceClient(serviceEndpoint);  
  
   Console.WriteLine("Invoking CalculatorService");  
   Console.WriteLine();  
  
   double value1 = 100.00D;  
   double value2 = 15.99D;  
  
   // Call the Add service operation.  
   double result = client.Add(value1, value2);  
   Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);  
  
   // Call the Subtract service operation.  
   result = client.Subtract(value1, value2);  
   Console.WriteLine("Subtract({0},{1}) = {2}", value1, value2, result);  
  
   // Call the Multiply service operation.  
   result = client.Multiply(value1, value2);  
   Console.WriteLine("Multiply({0},{1}) = {2}", value1, value2, result);  
  
   // Call the Divide service operation.  
   result = client.Divide(value1, value2);  
   Console.WriteLine("Divide({0},{1}) = {2}", value1, value2, result);  
   Console.WriteLine();  
  
   //Closing the client gracefully closes the connection and cleans up resources  
   client.Close();  
}  
  
```  
  
#### 使用此示例  
  
1.  此示例使用 HTTP 终结点，若要运行此示例，必须添加正确的 URL ACL。  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][配置 HTTP 和 HTTPS](http://go.microsoft.com/fwlink/?LinkId=70353)（可能为英文网页）。  使用提升的特权执行下面的命令应添加相应的 ACL。  如果该命令无效，则可能需要使用您的域和用户名替换以下参数。  `netsh http add urlacl url=http://+:8000/ user=%DOMAIN%\%UserName%`  
  
2.  使用 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 打开 Basic.sln 并生成示例。  
  
3.  运行 service.exe 应用程序。  
  
4.  服务启动后，运行 client.exe。  
  
5.  观察客户端是否能够在不知道服务地址的情况下找到服务。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。  在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。  此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\Discovery\Basic`  
  
## 请参阅