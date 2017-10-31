---
title: "终结点创建概述 | Microsoft Docs"
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
  - "终结点 [WCF], 概述"
ms.assetid: f4dce0fb-6f54-47e6-8054-86d7f574b91c
caps.latest.revision: 40
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 40
---
# 终结点创建概述
与 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 服务的所有通信是通过该服务的终结点进行的。  终结点为客户端提供对 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务所提供的功能的访问权。  本节描述终结点的结构，并概述如何在配置和代码中定义终结点。  
  
## 终结点的结构  
 每个终结点包含一个指示可在何处找到此终结点的地址、一个指定客户端如何与此终结点进行通信的绑定和一个标识可用方法的协定。  
  
-   **地址**。  地址唯一标识终结点并告知潜在客户服务的所在位置。  在 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 对象模型中，地址由 <xref:System.ServiceModel.EndpointAddress> 地址表示，该地址包含统一资源标识符 \(URI\) 和地址属性，而地址属性包括标识、一些 Web 服务描述语言 \(WSDL\) 元素和可选标头的集合。  可选标头提供用于标识终结点或与终结点交互的其他详细寻址信息。  [!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [指定终结点地址](../../../docs/framework/wcf/specifying-an-endpoint-address.md).  
  
-   **绑定**。  绑定指定如何与终结点进行通信。  绑定指定终结点如何与世界通信，包括使用哪种传输协议（例如，TCP 或 HTTP）、对消息使用何种编码（例如，文本或二进制），以及需要何种安全要求（例如，安全套接字层 \[SSL\] 或 SOAP 消息安全）。  [!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [使用绑定配置服务和客户端](../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md).  
  
-   **服务协定**。  服务协定概述了终结点向客户端公开的功能。  协定指定客户端可以调用的操作、消息的形式、输入参数的类型或调用操作所需的数据，以及客户端应收到的处理消息或响应消息的种类。  三种基本的协定类型与基本消息交换模式 \(MEP\) 相对应：数据报（单向）、请求\/答复和双工（双向）。  当访问服务协定时，服务协定也可以采用数据和消息协定要求特定的数据类型和消息格式。  [!INCLUDE[crabout](../../../includes/crabout-md.md)]如何定义服务协定的更多信息，请参见[设计服务协定](../../../docs/framework/wcf/designing-service-contracts.md)。  请注意，也可以要求客户端实现服务定义的协定（称为回调协定），以便在双工 MEP 下接收服务的消息。  [!INCLUDE[crdefault](../../../includes/crdefault-md.md)] [双工服务](../../../docs/framework/wcf/feature-details/duplex-services.md).  
  
 指定服务的终结点有两种方式，通过使用代码的强制方式或通过配置的声明方式。  如果未指定任何终结点，则运行时通过为该服务实现的每个服务协定的每个基地址添加一个默认终结点，来提供默认终结点。  在代码中定义终结点通常是不可行的，因为已部署服务的绑定和地址通常与在部署服务时所用的绑定和地址不同。  一般而言，使用配置定义服务终结点比使用代码更为可行。  通过将绑定和寻址信息放置在代码之外，可以在更改这些信息之后不必重新编译和重新部署应用程序。  
  
> [!NOTE]
>  添加执行模拟的服务终结点时，必须使用 <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%2A> 方法之一或 <xref:System.ServiceModel.Description.ContractDescription.GetContract%28System.Type%2CSystem.Type%29> 方法来将协定正确加载到新的 <xref:System.ServiceModel.Description.ServiceDescription> 对象。  
  
## 在代码中定义终结点  
 下面的示例说明如何在代码中指定终结点，如下所示：  
  
-   定义 `IEcho` 类型的服务协定，该服务接受某人的名字并做出响应“Hello \<名字\>\!”。  
  
-   实现由 `IEcho` 协定定义的该类型的 `Echo` 服务。  
  
-   为服务指定一个终结点地址：http:\/\/localhost:8000\/Echo。  
  
-   使用 <xref:System.ServiceModel.WSHttpBinding> 绑定配置 `Echo` 服务。  
  
```csharp  
Namespace Echo  
{  
   // Define the contract for the IEcho service   
   [ServiceContract]  
   public interface IEcho  
   {  
       [OperationContract]  
       String Hello(string name)  
   }  
  
   // Create an Echo service that implements IEcho contract  
   class Echo : IEcho  
   {  
      public string Hello(string name)  
      {  
         return "Hello" + name + "!";  
      }  
      public static void Main ()  
      {  
          //Specify the base address for Echo service.  
          Uri echoUri = new Uri("http://localhost:8000/");  
  
          //Create a ServiceHost for the Echo service.  
          ServiceHost serviceHost = new ServiceHost(typeof(Echo),echoUri);  
  
          // Use a predefined WSHttpBinding to configure the service.  
          WSHttpBinding binding = new WSHttpBinding();  
  
          // Add the endpoint for this service to the service host.  
          serviceHost.AddServiceEndpoint(  
             typeof(IEcho),   
             binding,   
             echoUri  
           );  
  
          // Open the service host to run it.  
          serviceHost.Open();  
     }  
  }  
}  
```  
  
```vb  
' Define the contract for the IEcho service  
    <ServiceContract()> _  
    Public Interface IEcho  
        <OperationContract()> _  
        Function Hello(ByVal name As String) As String  
    End Interface  
  
' Create an Echo service that implements IEcho contract  
    Public Class Echo   
        Implements IEcho  
        Public Function Hello(ByVal name As String) As String _  
 Implements ICalculator.Hello  
            Dim result As String = "Hello" + name + "!"  
            Return result  
        End Function  
  
' Specify the base address for Echo service.  
Dim echoUri As Uri = New Uri("http://localhost:8000/")  
  
' Create a ServiceHost for the Echo service.  
Dim svcHost As ServiceHost = New ServiceHost(GetType(HelloWorld), echoUri)  
  
' Use a predefined WSHttpBinding to configure the service.  
Dim binding As New WSHttpBinding()  
  
' Add the endpoint for this service to the service host.  
serviceHost.AddServiceEndpoint(GetType(IEcho), binding, echoUri)  
  
' Open the service host to run it.  
serviceHost.Open()  
```  
  
> [!NOTE]
>  使用基址创建服务主机，然后将与基址相关的其余地址指定为终结点的一部分。  这样划分地址可以更加方便地为主机上的服务定义多个终结点。  
  
> [!NOTE]
>  不能在 <xref:System.ServiceModel.ServiceHostBase> 上的 <xref:System.ServiceModel.Channels.CommunicationObject.OnOpening%2A> 方法之后修改服务应用程序中的 <xref:System.ServiceModel.Description.ServiceDescription> 的属性。  如果修改通过该点的某些成员（如 <xref:System.ServiceModel.ServiceHostBase.Credentials%2A> 属性以及 <xref:System.ServiceModel.ServiceHostBase> 和 <xref:System.ServiceModel.ServiceHost> 上的 `AddServiceEndpoint` 方法），则将引发异常。  允许修改其他成员，但结果不可确定。  
>   
>  同样，在调用 <xref:System.ServiceModel.ChannelFactory> 上的 <xref:System.ServiceModel.Channels.CommunicationObject.OnOpening%2A> 之后不能在客户端上修改 <xref:System.ServiceModel.Description.ServiceEndpoint> 值。  如果修改通过该点的 <xref:System.ServiceModel.ChannelFactory.Credentials%2A> 属性，则此属性将引发异常。  可以对其他客户端说明值进行修改而不会出现错误，但结果不可确定。  
>   
>  无论是对于服务还是客户端，建议您在调用 <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A> 之前修改说明。  
  
## 在配置中定义终结点  
 创建应用程序时，经常需要将一些决策交给部署该应用程序的管理员。  例如，通常没有办法预先知道将使用什么服务地址（一个 URI）。  最好允许管理员在创建服务后指定地址，而不是对地址进行硬编码。  这种灵活性是通过配置实现的。  有关详细信息，请参阅[正在配置服务](../../../docs/framework/wcf/configuring-services.md)。  
  
> [!NOTE]
>  使用带有 `/config:`*文件名*`[,`*文件名*`]` 开关的 [ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 可以快速创建配置文件。  
  
## 使用默认终结点  
 如果在代码或配置中未指定任何终结点，则运行时通过为该服务实现的每个服务协定的每个基地址添加一个默认终结点，来提供默认终结点。  可以在代码或配置中指定基地址，默认终结点是在 <xref:System.ServiceModel.ServiceHost> 上调用 <xref:System.ServiceModel.ServiceHost.Open%2A> 时添加的。  此示例是上一节中的同一示例，但由于未指定任何终结点，因此添加了默认终结点。  
  
```csharp  
Namespace Echo  
{  
   // Define the contract for the IEcho service   
   [ServiceContract]  
   Interface IEcho  
   {  
       [OperationContract]  
       String Hello(string name)  
   }  
  
   // Create an Echo service that implements IEcho contract  
   Class Echo : IEcho  
   {  
      Public string Hello(string name)  
      {  
         return "Hello" + name + "!";  
      }  
      static void Main ()  
      {  
          //Specify the base address for Echo service.  
          Uri echoUri = new Uri("http://localhost:8000/");  
  
          //Create a ServiceHost for the Echo service.  
          ServiceHost serviceHost = new ServiceHost(typeof(Echo),echoUri);  
  
          // Open the service host to run it. Default endpoints  
          // are added when the service is opened.  
          serviceHost.Open();  
     }  
  }  
}  
```  
  
```vb  
' Define the contract for the IEcho service  
    <ServiceContract()> _  
    Public Interface IEcho  
        <OperationContract()> _  
        Function Hello(ByVal name As String) As String  
    End Interface  
  
' Create an Echo service that implements IEcho contract  
    Public Class Echo   
        Implements IEcho  
        Public Function Hello(ByVal name As String) As String _  
 Implements ICalculator.Hello  
            Dim result As String = "Hello" + name + "!"  
            Return result  
        End Function  
  
' Specify the base address for Echo service.  
Dim echoUri As Uri = New Uri("http://localhost:8000/")  
  
' Open the service host to run it. Default endpoints  
' are added when the service is opened.  
serviceHost.Open()  
```  
  
 如果显式提供了终结点，则仍可以添加默认终结点，方法是先在 <xref:System.ServiceModel.ServiceHostBase.AddDefaultEndpoints%2A> 上调用 <xref:System.ServiceModel.ServiceHost>，然后调用 <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A>。  [!INCLUDE[crabout](../../../includes/crabout-md.md)]默认终结点的更多信息，请参见[简化配置](../../../docs/framework/wcf/simplified-configuration.md)和 [WCF 服务的简化配置](../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md)。  
  
## 请参阅  
 [实现服务协定](../../../docs/framework/wcf/implementing-service-contracts.md)