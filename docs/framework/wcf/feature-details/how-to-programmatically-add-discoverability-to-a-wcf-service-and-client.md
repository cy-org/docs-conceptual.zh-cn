---
title: "如何：以编程方式向 WCF 服务和客户端添加可检测性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4f7ae7ab-6fc8-4769-9730-c14d43f7b9b1
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# 如何：以编程方式向 WCF 服务和客户端添加可检测性
本主题说明如何检测到 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务。 它基于[自承载](http://go.microsoft.com/fwlink/?LinkId=145523)示例。  
  
### <a name="to-configure-the-existing-self-host-service-sample-for-discovery"></a>针对 Discovery 配置现有自承载服务示例  
  
1.  在 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 中打开自承载解决方案。 示例位于 TechnologySamples\Basic\Service\Hosting\SelfHost 目录中。  
  
2.  将对 `System.ServiceModel.Discovery.dll` 的引用添加到服务项目中。 您可能会看到一条错误消息： ServiceModel.Discovery.dll 或其依赖项之一要求更高版本的[!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]比项目中指定..." 如果您看到此消息，用鼠标右键单击解决方案资源管理器中的项目并选择**属性**。 在**项目属性**窗口中，请确保**目标框架**是[!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)]。  
  
3.  打开 Service.cs 文件并添加下面的 `using` 语句。  
  
    ```  
    using System.ServiceModel.Discovery;  
    ```  
  
4.  在`Main()`方法时，内部`using`语句中，添加<xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior>向服务主机的实例。  
  
    ```  
    public static void Main()  
    {  
        // Create a ServiceHost for the CalculatorService type.  
        using (ServiceHost serviceHost = new ServiceHost(typeof(CalculatorService)))  
        {  
            // Add a ServiceDiscoveryBehavior  
            serviceHost.Description.Behaviors.Add(new ServiceDiscoveryBehavior());                  
  
            // ...  
        }  
    }  
    ```  
  
     <xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior>指定应用于服务是可发现。  
  
5.  添加<xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>到服务主机添加的代码之后立即<xref:System.ServiceModel.Discovery.ServiceDiscoveryBehavior>。  
  
    ```  
    // Add ServiceDiscoveryBehavior  
    serviceHost.Description.Behaviors.Add(new ServiceDiscoveryBehavior());  
  
    // Add a UdpDiscoveryEndpoint  
    serviceHost.AddServiceEndpoint(new UdpDiscoveryEndpoint());  
    ```  
  
     此代码指定应将发现消息发送到标准 UDP 发现终结点。  
  
### <a name="to-create-a-client-application-that-uses-discovery-to-call-the-service"></a>创建使用发现功能调用服务的客户端应用程序  
  
1.  向名为 `DiscoveryClientApp` 的解决方案添加一个新控制台应用程序。  
  
2.  添加对 `System.ServiceModel.dll` 和 `System.ServiceModel.Discovery.dll` 的引用  
  
3.  将 GeneratedClient.cs 和 App.config 文件从现有客户端项目复制到新的 DiscoveryClientApp 项目。 要执行此操作，请右键单击中的文件**解决方案资源管理器**，选择**副本**，然后选择**DiscoveryClientApp**项目，用鼠标右键单击并选择**粘贴**。  
  
4.  打开 Program.cs。  
  
5.  添加下面的 `using` 语句。  
  
    ```  
    using System.ServiceModel;  
    using System.ServiceModel.Discovery;  
    using Microsoft.ServiceModel.Samples;  
  
    ```  
  
6.  将一个名为 `FindCalculatorServiceAddress()` 的静态方法添加到 `Program` 类。  
  
    ```  
    static EndpointAddress FindCalculatorServiceAddress()  
    {  
    }  
    ```  
  
     此方法使用发现功能搜索 `CalculatorService` 服务。  
  
7.  内部`FindCalculatorServiceAddress`方法中，创建一个新<xref:System.ServiceModel.Discovery.DiscoveryClient>实例，并在传入<xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>给构造函数。  
  
    ```  
    static EndpointAddress FindCalculatorServiceAddress()  
    {  
        // Create DiscoveryClient  
        DiscoveryClient discoveryClient = new DiscoveryClient(new UdpDiscoveryEndpoint());  
    }  
    ```  
  
     这将告知[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]， <xref:System.ServiceModel.Discovery.DiscoveryClient>类应使用标准 UDP 发现终结点来发送和接收发现消息。  
  
8.  在下一步的一行，调用<xref:System.ServiceModel.Discovery.DiscoveryClient.Find%2A>方法并指定<xref:System.ServiceModel.Discovery.FindCriteria>包含您想要搜索的服务协定的实例。 在本示例中，指定的是 `ICalculator`。  
  
    ```  
    // Find ICalculatorService endpoints              
    FindResponse findResponse = discoveryClient.Find(new FindCriteria(typeof(ICalculator)));  
    ```  
  
9. 在调用后<xref:System.ServiceModel.Discovery.DiscoveryClient.Find%2A>、 检查以查看是否至少一个匹配的服务，则返回<xref:System.ServiceModel.EndpointAddress>的第一个匹配的服务。 如果找不到匹配服务，则返回 `null`。  
  
    ```  
    if (findResponse.Endpoints.Count > 0)  
    {  
        return findResponse.Endpoints[0].Address;  
    }  
    else  
    {  
        return null;  
    }  
    ```  
  
10. 将名为 `InvokeCalculatorService` 的静态方法添加到 `Program` 类。  
  
    ```  
    static void InvokeCalculatorService(EndpointAddress endpointAddress)  
    {  
    }  
    ```  
  
     此方法使用从 `FindCalculatorServiceAddress` 返回的终结点地址调用计算器服务。  
  
11. 在 `InvokeCalculatorService` 方法的内部，创建 `CalculatorServiceClient` 类的实例。 此类定义由[自承载](http://go.microsoft.com/fwlink/?LinkId=145523)示例。 并且是使用 Svcutil.exe 生成的。  
  
    ```  
    // Create a client  
    CalculatorClient client = new CalculatorClient();  
    ```  
  
12. 在下一行，将客户端的终结点地址设置为从 `FindCalculatorServiceAddress()` 返回的终结点地址。  
  
    ```  
    // Connect to the discovered service endpoint  
    client.Endpoint.Address = endpointAddress;  
    ```  
  
13. 紧随上一步骤的代码之后，调用由计算器服务公开的方法。  
  
    ```  
    Console.WriteLine("Invoking CalculatorService at {0}", endpointAddress);  
  
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
    ```  
  
14. 将以下代码添加到 `Main()` 类中的 `Program` 方法以调用 `FindCalculatorServiceAddress`。  
  
    ```  
    public static void Main()  
    {  
        EndpointAddress endpointAddress = FindCalculatorServiceAddress();  
    }  
    ```  
  
15. 在下一行，调用 `InvokeCalculatorService()`，并传递由 `FindCalculatorServiceAddress()` 返回的终结点地址。  
  
    ```  
    if (endpointAddress != null)  
    {  
        InvokeCalculatorService(endpointAddress);  
    }  
  
    Console.WriteLine("Press <ENTER> to exit.");  
    Console.ReadLine();  
    ```  
  
### <a name="to-test-the-application"></a>测试应用程序  
  
1.  打开具有特权的命令提示符并运行 Service.exe。  
  
2.  打开命令提示符并运行 Discoveryclientapp.exe。  
  
3.  service.exe 的输出应类似于以下输出。  
  
    ```Output  
    Received Add(100,15.99)  
    Return: 115.99  
    Received Subtract(100,15.99)  
    Return: 84.01  
    Received Multiply(100,15.99)  
    Return: 1599  
    Received Divide(100,15.99)  
    Return: 6.25390869293308  
    ```  
  
4.  Discoveryclientapp.exe 的输出应类似于以下输出。  
  
    ```Output  
    Invoking CalculatorService at http://localhost:8000/ServiceModelSamples/service  
    Add(100,15.99) = 115.99  
    Subtract(100,15.99) = 84.01  
    Multiply(100,15.99) = 1599  
    Divide(100,15.99) = 6.25390869293308  
  
    Press <ENTER> to exit.  
    ```  
  
## <a name="example"></a>示例  
 下面是此示例的代码清单。 由于此代码基于[自承载](http://go.microsoft.com/fwlink/?LinkId=145523)示例，列出更改过的那些文件。 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]自承载示例，请参阅[安装说明进行操作](http://go.microsoft.com/fwlink/?LinkId=145522)。  
  
```  
  
// Service.cs  
using System;  
using System.Configuration;  
using System.ServiceModel;  
using System.ServiceModel.Discovery;  
  
namespace Microsoft.ServiceModel.Samples  
{  
    // See SelfHost sample for service contract and implementation  
    // ...  
  
        // Host the service within this EXE console application.  
        public static void Main()  
        {  
            // Create a ServiceHost for the CalculatorService type.  
            using (ServiceHost serviceHost = new ServiceHost(typeof(CalculatorService)))  
            {  
                // Add the ServiceDiscoveryBehavior to make the service discoverable  
                serviceHost.Description.Behaviors.Add(new ServiceDiscoveryBehavior());  
                serviceHost.AddServiceEndpoint(new UdpDiscoveryEndpoint());  
  
                // Open the ServiceHost to create listeners and start listening for messages.  
                serviceHost.Open();  
  
                // The service can now be accessed.  
                Console.WriteLine("The service is ready.");  
                Console.WriteLine("Press <ENTER> to terminate service.");  
                Console.WriteLine();  
                Console.ReadLine();  
            }  
        }  
    }  
}  
```  
  
```  
// Program.cs  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.ServiceModel;  
using System.ServiceModel.Discovery;  
using Microsoft.ServiceModel.Samples;  
using System.Text;  
  
namespace DiscoveryClientApp  
{  
    class Program  
    {  
        static EndpointAddress FindCalculatorServiceAddress()  
        {  
            // Create DiscoveryClient  
            DiscoveryClient discoveryClient = new DiscoveryClient(new UdpDiscoveryEndpoint());  
  
            // Find ICalculatorService endpoints              
            FindResponse findResponse = discoveryClient.Find(new FindCriteria(typeof(ICalculator)));  
  
            if (findResponse.Endpoints.Count > 0)  
            {  
                return findResponse.Endpoints[0].Address;  
            }  
            else  
            {  
                return null;  
            }  
        }  
  
        static void InvokeCalculatorService(EndpointAddress endpointAddress)  
        {  
            // Create a client  
            CalculatorClient client = new CalculatorClient();  
  
            // Connect to the discovered service endpoint  
            client.Endpoint.Address = endpointAddress;  
  
            Console.WriteLine("Invoking CalculatorService at {0}", endpointAddress);  
  
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
        static void Main(string[] args)  
        {  
            EndpointAddress endpointAddress = FindCalculatorServiceAddress();  
  
            if (endpointAddress != null)  
            {  
                InvokeCalculatorService(endpointAddress);  
            }  
  
            Console.WriteLine("Press <ENTER> to exit.");  
            Console.ReadLine();  
  
        }  
    }  
}  
```  
  
<!-- TODO: review snippet reference  [!CODE [Microsoft.Win32.RegistryKey#4](Microsoft.Win32.RegistryKey#4)]  -->  
  
## <a name="see-also"></a>另请参阅  
 [WCF Discovery 概述](../../../../docs/framework/wcf/feature-details/wcf-discovery-overview.md)   
 [WCF Discovery 对象模型](../../../../docs/framework/wcf/feature-details/wcf-discovery-object-model.md)