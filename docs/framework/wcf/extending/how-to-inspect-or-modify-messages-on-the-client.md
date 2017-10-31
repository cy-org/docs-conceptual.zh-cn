---
title: "如何：检查或修改客户端的消息 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b8256335-f1c2-419f-b862-9f220ccad84c
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 如何：检查或修改客户端的消息
通过实现 <xref:System.ServiceModel.Dispatcher.IClientMessageInspector?displayProperty=fullName> 并将其插入客户端运行时，可以检查或修改通过 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端的传入或传出消息。  有关详细信息，请参阅[扩展客户端](../../../../docs/framework/wcf/extending/extending-clients.md)。  服务上的等效功能为 <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector?displayProperty=fullName>。  有关完整的代码示例，请参见[消息检查器](../../../../docs/framework/wcf/samples/message-inspectors.md)示例。  
  
### 检查或修改消息  
  
1.  实现 <xref:System.ServiceModel.Dispatcher.IClientMessageInspector?displayProperty=fullName> 接口。  
  
2.  实现 <xref:System.ServiceModel.Description.IEndpointBehavior?displayProperty=fullName> 或 <xref:System.ServiceModel.Description.IContractBehavior?displayProperty=fullName>，具体取决于您希望在其中插入客户端消息检查器的作用域。  <xref:System.ServiceModel.Description.IEndpointBehavior?displayProperty=fullName> 允许您在终结点级别更改行为。  <xref:System.ServiceModel.Description.IContractBehavior?displayProperty=fullName> 允许您在协定级别更改行为。  
  
3.  在 <xref:System.ServiceModel.ChannelFactory%601?displayProperty=fullName> 上调用 <xref:System.ServiceModel.ClientBase%601.Open%2A?displayProperty=fullName> 或 <xref:System.ServiceModel.ICommunicationObject.Open%2A?displayProperty=fullName> 方法前，插入行为。  有关详细信息，请参阅[使用行为配置和扩展运行时](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md)。  
  
## 示例  
 下面的代码示例按顺序演示以下各项：  
  
-   客户端检查器实现。  
  
-   插入检查器的终结点行为。  
  
-   一个 <xref:System.ServiceModel.Configuration.BehaviorExtensionElement> 派生类，允许您在配置文件中添加行为。  
  
-   一个配置文件，它添加终结点行为，以便在客户端运行时中插入客户端消息检查器。  
  
```csharp  
// Client message inspector  
public class SimpleMessageInspector : IClientMessageInspector  
{  
    public void AfterReceiveReply(ref System.ServiceModel.Channels.Message reply, object correlationState)  
    {  
        // Implement this method to inspect/modify messages after a message  
        // is received but prior to passing it back to the client   
        Console.WriteLine("AfterReceiveReply called");  
    }  
  
    public object BeforeSendRequest(ref System.ServiceModel.Channels.Message request, IClientChannel channel)  
    {  
        // Implement this method to inspect/modify messages before they   
        // are sent to the service  
        Console.WriteLine("BeforeSendRequest called");  
        return null;  
    }  
}  
  
```  
  
```csharp  
// Endpoint behavior  
public class SimpleEndpointBehavior : IEndpointBehavior  
{  
    public void AddBindingParameters(ServiceEndpoint endpoint, System.ServiceModel.Channels.BindingParameterCollection bindingParameters)  
    {  
         // No implementation necessary  
    }  
  
    public void ApplyClientBehavior(ServiceEndpoint endpoint, ClientRuntime clientRuntime)  
    {  
        clientRuntime.MessageInspectors.Add(new SimpleMessageInspector());  
    }  
  
    public void ApplyDispatchBehavior(ServiceEndpoint endpoint, EndpointDispatcher endpointDispatcher)  
    {  
         // No implementation necessary  
    }  
  
    public void Validate(ServiceEndpoint endpoint)  
    {  
         // No implementation necessary  
    }  
}  
```  
  
```csharp  
// Configuration element   
public class SimpleBehaviorExtensionElement : BehaviorExtensionElement  
{  
    public override Type BehaviorType  
    {  
        get { return typeof(SimpleEndpointBehavior); }  
    }  
  
    protected override object CreateBehavior()  
    {  
         // Create the  endpoint behavior that will insert the message  
         // inspector into the client runtime  
        return new SimpleEndpointBehavior();  
    }  
}  
  
```  
  
```vb  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
    <system.serviceModel>  
        <client>  
            <endpoint address="http://localhost:8080/SimpleService/"   
                      binding="wsHttpBinding"  
                      contract="ServiceReference1.IService1"  
                      name="WSHttpBinding_IService1"/>  
        </client>  
  
      <behaviors>  
        <endpointBehaviors>  
          <behavior name="clientInspectorsAdded">  
            <simpleBehaviorExtension />  
          </behavior>  
        </endpointBehaviors>  
      </behaviors>  
      <extensions>  
        <behaviorExtensions>  
          <add  
            name="simpleBehaviorExtension"  
            type="SimpleServiceLib.SimpleBehaviorExtensionElement, Host, Version=0.0.0.0, Culture=neutral, PublicKeyToken=null"/>  
        </behaviorExtensions>  
      </extensions>  
    </system.serviceModel>  
</configuration>  
  
```  
  
## 请参阅  
 <xref:System.ServiceModel.Dispatcher.IClientMessageInspector?displayProperty=fullName>   
 <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector?displayProperty=fullName>   
 [使用行为配置和扩展运行时](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md)