---
title: "双工服务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 396b875a-d203-4ebe-a3a1-6a330d962e95
caps.latest.revision: 17
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 17
---
# 双工服务
双工服务协定是一种消息交换模式，其中双方终结点都可独立向对方发送消息。 因此，双工服务可以将消息发送回客户端终结点，从而提供类似事件的行为。 当客户端连接到服务并为服务提供可用来将消息发送回客户端的通道时，就会发生双工通信。 请注意，双工服务的类似事件的行为仅在会话中起作用。  
  
 若要创建双工协定，需要创建一对接口。 第一个接口是描述客户端可调用的操作的服务协定接口。 该服务协定必须指定*回调协定*中<xref:System.ServiceModel.ServiceContractAttribute.CallbackContract%2A?displayProperty=fullName>属性。 回调协定是定义服务可在客户端终结点上调用的操作的接口。 虽然系统提供的双工绑定利用了会话，但是双工协定不需要会话。  
  
 下面是双工协定的示例。  
  
 [!code-csharp[c_DuplexServices#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_duplexservices/cs/service.cs#0)]
 [!code-vb[c_DuplexServices#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_duplexservices/vb/service.vb#0)]  
  
 `CalculatorService` 类实现 `ICalculatorDuplex` 主接口。 服务使用<xref:System.ServiceModel.InstanceContextMode>实例模式来维护每个会话的结果。 名为 `Callback` 的私有属性访问指向客户端的回调通道。 服务使用该回调通过回调接口将消息返送给客户端，如下面的示例代码所示。  
  
 [!code-csharp[c_DuplexServices#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_duplexservices/cs/service.cs#1)]
 [!code-vb[c_DuplexServices#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_duplexservices/vb/service.vb#1)]  
  
 客户端必须提供一个实现双工协定回调接口的类，以便从服务接收消息。 下面的示例代码演示了一个实现 `CallbackHandler` 接口的 `ICalculatorDuplexCallback` 类。  
  
 [!code-csharp[c_DuplexServices#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_duplexservices/cs/client.cs#2)]
 [!code-vb[c_DuplexServices#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_duplexservices/vb/client.vb#2)]  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]为双工协定需要生成的客户端<xref:System.ServiceModel.InstanceContext>类，以在构造时提供。 这<xref:System.ServiceModel.InstanceContext>类用作实现回调接口并处理返回从服务发送的消息的对象的站点。 <xref:System.ServiceModel.InstanceContext>构造类时使用的一个实例`CallbackHandler`类。 此对象处理通过回调接口从服务发送到客户端的消息。  
  
 [!code-csharp[c_DuplexServices#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_duplexservices/cs/client.cs#3)]
 [!code-vb[c_DuplexServices#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_duplexservices/vb/client.vb#3)]  
  
 服务的配置必须设置为提供同时支持会话通信和双工通信的绑定。 `wsDualHttpBinding` 元素支持会话通信，并通过提供双 HTTP 连接（一个连接对应于一个方向）来允许进行双工通信。  
  
 在客户端，必须配置一个服务器可用来连接客户端的地址，如下面的示例配置所示。  
  
  
  
> [!NOTE]
>  未能通过身份验证通常使用安全对话的非双工客户端会引发<xref:System.ServiceModel.Security.MessageSecurityException>。 但是，如果使用安全对话的双工客户端未能通过身份验证，客户端收到<xref:System.TimeoutException>相反。  
  
 如果使用 `WSHttpBinding` 元素创建客户端/服务，并且不包含客户端回调终结点，您将收到以下错误。  
  
```  
HTTP could not register URL  
htp://+:80/Temporary_Listen_Addresses/<guid> because TCP port 80 is being used by another application.  
```  
  
 下面的示例代码演示了如何在代码中指定客户端终结点地址。  
  
```  
WSDualHttpBinding binding = new WSDualHttpBinding();  
EndpointAddress endptadr = new EndpointAddress("http://localhost:12000/DuplexTestUsingCode/Server");  
binding.ClientBaseAddress = new Uri("http://localhost:8000/DuplexTestUsingCode/Client/");  
```  
  
 下面的示例代码演示了如何在配置中指定客户端终结点地址。  
  
```  
<client>  
    <endpoint name ="ServerEndpoint"   
          address="http://localhost:12000/DuplexTestUsingConfig/Server"  
          bindingConfiguration="WSDualHttpBinding_IDuplexTest"   
            binding="wsDualHttpBinding"  
           contract="IDuplexTest" />  
</client>  
<bindings>  
    <wsDualHttpBinding>  
        <binding name="WSDualHttpBinding_IDuplexTest"    
          clientBaseAddress="http://localhost:8000/myClient/" >  
            <security mode="None"/>  
         </binding>  
    </wsDualHttpBinding>  
</bindings>  
  
```  
  
> [!WARNING]
>  双工模型不自动检测服务或客户端何时关闭其通道。 因此，如果客户端意外终止，默认情况下将不会通知该服务；或者，如果客户端意外终止，将不会通知该服务。 客户端和服务可以实现自己的协议以相互通知对方（如果它们这么选择）。  
  
## <a name="see-also"></a>另请参阅  
 [双工](../../../../docs/framework/wcf/samples/duplex.md)   
 [指定客户端运行时行为](../../../../docs/framework/wcf/specifying-client-run-time-behavior.md)   
 [如何︰ 创建通道工厂并用它创建和管理通道](../../../../docs/framework/wcf/feature-details/how-to-create-a-channel-factory-and-use-it-to-create-and-manage-channels.md)