---
title: "使用 WCF 客户端访问服务 | Microsoft Docs"
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
  - "客户端 [WCF], 访问服务"
ms.assetid: d780af9f-73c5-42db-9e52-077a5e4de7fe
caps.latest.revision: 36
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 36
---
# 使用 WCF 客户端访问服务
创建服务之后，下一步是创建 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端代理。  客户端应用程序使用 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端代理与服务进行通信。  客户端应用程序通常导入服务的元数据来生成可用来调用该服务的 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端代码。  
  
 创建 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端的基本步骤包括：  
  
1.  编译服务代码。  
  
2.  生成 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端代理。  
  
3.  实例化 WCF 客户端代理。  
  
 可通过使用服务模块元数据实用工具 \(SvcUtil.exe\) 手动生成 WCF 客户端代理。有关更多信息，请参见 [ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)。  还可以使用“添加服务引用”功能在 Visual Studio 内生成 WCF 客户端代理。  若要使用上述两种方法中的一种生成 WCF 客户端代理，必须运行该服务。  如果服务是自承载服务，则必须运行主机。  如果服务是在 IIS\/WAS 中承载的，则无需执行任何其他操作。  
  
## ServiceModel 元数据实用工具  
 [ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 是一个用于从元数据生成代码的命令行工具。  下面是一个基本 Svcutil.exe 命令示例。  
  
```  
Svcutil.exe <service's Metadata Exchange (MEX) address or HTTP GET address>   
```  
  
 另外，还可以使用 Svcutil.exe 来处理文件系统中的 Web 服务描述语言 \(WSDL\) 和 XML 架构定义语言 \(XSD\) 文件。  
  
```  
Svcutil.exe <list of WSDL and XSD files on file system>  
```  
  
 结果是一个包含 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端代码的代码文件，客户端应用程序可以使用这些客户端代码来调用服务。  
  
 您还可以使用该工具生成配置文件。  
  
```  
Svcutil.exe <file1 [,file2]>  
```  
  
 如果仅提供了一个文件名，则该文件名是输出文件的名称。  如果提供了两个文件名，则第一个文件是输入配置文件，其内容将与生成的配置合并，然后写出到第二个文件中。  [!INCLUDE[crabout](../../../includes/crabout-md.md)]配置的更多信息，请参见[为服务配置绑定](../../../docs/framework/wcf/configuring-bindings-for-wcf-services.md)。  
  
> [!IMPORTANT]
>  与任何未受保护的网络请求一样，未受保护的元数据请求也会带来一定的风险：如果您不能确定您正在与其进行通信的终结点身份属实，那么您检索的信息有可能是来自于恶意服务的元数据。  
  
## Visual Studio 中的“添加服务引用”功能  
 在服务运行的情况下，右击将包含 WCF 客户端代理的项目，然后选择**“添加服务引用”**。  在**“添加服务引用”**对话框中，键入要调用的服务的 URL，然后单击**“转到”**按钮。  该对话框将显示在您指定的地址上提供的服务列表。  双击该服务可看到可用协定和操作，为生成的代码指定命名空间，然后单击**“确定”**按钮。  
  
## 示例  
 下面的代码示例演示为服务创建的一个服务协定。  
  
```csharp  
// Define a service contract.  
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public interface ICalculator  
{  
    [OperationContract]  
    double Add(double n1, double n2);  
    // Other methods are not shown here.  
}  
```  
  
```vb  
' Define a service contract.  
<ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")> _  
Public Interface ICalculator  
    <OperationContract()>  _  
    Function Add(ByVal n1 As Double, ByVal n2 As Double) As Double   
    ' Other methods are not shown here.  
End Interface   
```  
  
 ServiceModel 元数据实用工具以及 Visual Studio 中的“添加服务引用”功能生成以下 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端类。  该类从 <xref:System.ServiceModel.ClientBase%601> 泛型类继承，并实现 `ICalculator` 接口。  该工具还生成 `ICalculator` 接口（此处未演示）。  
  
```csharp  
public partial class CalculatorClient : System.ServiceModel.ClientBase<ICalculator>, ICalculator  
{  
    public CalculatorClient(){}  
  
    public CalculatorClient(string configurationName) :   
            base(configurationName)  
    {}  
  
    public CalculatorClient(System.ServiceModel.Binding binding) :   
            base(binding)  
    {}  
  
    public CalculatorClient(System.ServiceModel.EndpointAddress address,  
    System.ServiceModel.Binding binding) :   
            base(address, binding)  
    {}  
  
    public double Add(double n1, double n2)  
    {  
        return base.InnerChannel.Add(n1, n2);  
    }  
}  
  
```  
  
```vb  
Partial Public Class CalculatorClient  
    Inherits System.ServiceModel.ClientBase(Of ICalculator)  
    Implements ICalculator  
  
    Public Sub New()  
        MyBase.New  
    End Sub  
  
    Public Sub New(ByVal configurationName As String)  
        MyBase.New(configurationName)  
    End Sub  
  
    Public Sub New(ByVal binding As System.ServiceModel.Binding)  
        MyBase.New(binding)  
    End Sub  
  
    Public Sub New(ByVal address As _  
    System.ServiceModel.EndpointAddress, _  
    ByVal binding As System.ServiceModel.Binding)  
        MyBase.New(address, binding)  
    End Sub  
  
    Public Function Add(ByVal n1 As Double, ByVal n2 As Double) As _  
    Double Implements ICalculator.Add  
        Return MyBase.InnerChannel.Add(n1, n2)  
    End Function   
End Class  
  
```  
  
## 使用 WCF 客户端  
 若要使用 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端，请创建 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端的一个实例，然后调用其方法，如下面的代码所示。  
  
```csharp  
// Create a client object with the given client endpoint configuration.  
CalculatorClient calcClient = new CalculatorClient("CalculatorEndpoint"));  
// Call the Add service operation.  
double value1 = 100.00D;  
double value2 = 15.99D;  
double result = calcClient.Add(value1, value2);  
Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);  
  
```  
  
```vb  
' Create a client object with the given client endpoint configuration.  
Dim calcClient As CalculatorClient = _  
New CalculatorClient("CalculatorEndpoint")  
  
' Call the Add service operation.  
Dim value1 As Double = 100.00D  
Dim value2 As Double = 15.99D  
Dim result As Double = calcClient.Add(value1, value2)  
Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result)  
  
```  
  
## 调试客户端引发的异常  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 客户端所引发的许多异常是由服务上的异常所导致的。  以下是这种情况的一些示例：  
  
-   <xref:System.Net.Sockets.SocketException>: 现有连接被远程主机强行关闭。  
  
-   <xref:System.ServiceModel.CommunicationException>: 基础连接意外关闭。  
  
-   <xref:System.ServiceModel.CommunicationObjectAbortedException>: 套接字连接已中止。  这可能是由于处理消息时出错或远程主机超过接收超时或者潜在的网络资源问题导致的。  
  
 当发生这些类型的异常时，解决问题的最佳方式是在服务端启用跟踪并确定服务端发生了何种异常。  [!INCLUDE[crabout](../../../includes/crabout-md.md)]跟踪的更多信息，请参见[跟踪](../../../docs/framework/wcf/diagnostics/tracing/index.md)和[使用跟踪来排除应用程序故障](../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)。  
  
## 请参阅  
 [如何：创建客户端](../../../docs/framework/wcf/how-to-create-a-wcf-client.md)   
 [如何：使用双工协定访问服务](../../../docs/framework/wcf/feature-details/how-to-access-services-with-a-duplex-contract.md)   
 [如何：以异步方式调用服务操作](../../../docs/framework/wcf/feature-details/how-to-call-wcf-service-operations-asynchronously.md)   
 [如何：使用单向和请求\-答复协定访问服务](../../../docs/framework/wcf/feature-details/how-to-access-wcf-services-with-one-way-and-request-reply-contracts.md)   
 [如何：访问 WSE 3.0 服务](../../../docs/framework/wcf/feature-details/how-to-access-a-wse-3-0-service-with-a-wcf-client.md)   
 [了解生成的客户端代码](../../../docs/framework/wcf/feature-details/understanding-generated-client-code.md)   
 [如何：使用 XmlSerializer 改善 WCF 客户端应用程序的启动时间](../../../docs/framework/wcf/feature-details/startup-time-of-wcf-client-applications-using-the-xmlserializer.md)   
 [指定客户端运行时行为](../../../docs/framework/wcf/specifying-client-run-time-behavior.md)   
 [配置客户端行为](../../../docs/framework/wcf/configuring-client-behaviors.md)