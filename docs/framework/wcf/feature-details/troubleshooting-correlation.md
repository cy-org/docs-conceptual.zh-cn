---
title: "针对相关的疑难解答 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 98003875-233d-4512-a688-4b2a1b0b5371
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# 针对相关的疑难解答
相关用于在工作流服务消息之间和工作流服务消息与正确的工作流实例之间建立关联，如果未正确配置相关，则将接收不到消息，且应用程序无法正常运行。本主题概述了对相关问题进行疑难解答的几种方法，还列出了使用相关时可能出现的一些常见问题。  
  
## 处理 UnknownMessageReceived 事件  
 服务接收到未知消息（包括无法与现有实例关联的消息）时，将发生 <xref:System.ServiceModel.ServiceHostBase.UnknownMessageReceived> 事件。对于自承载服务，可在宿主应用程序中处理此事件。  
  
```csharp  
host.UnknownMessageReceived += delegate(object sender, UnknownMessageReceivedEventArgs e)  
{  
    Console.WriteLine("Unknown Message Received:");  
    Console.WriteLine(e.Message);  
};  
```  
  
 对于 Web 承载的服务，可通过从 <xref:System.ServiceModel.Activities.Activation.WorkflowServiceHostFactory> 派生类并重写  <xref:System.ServiceModel.Activities.Activation.WorkflowServiceHostFactory.CreateWorkflowServiceHost%2A> 来处理此事件。  
  
```csharp  
class CustomFactory : WorkflowServiceHostFactory  
{  
    protected override WorkflowServiceHost CreateWorkflowServiceHost(Activity activity, Uri[] baseAddresses)  
    {  
        // Create the WorkflowServiceHost.  
        WorkflowServiceHost host = new WorkflowServiceHost(activity, baseAddresses);  
  
        // Handle the UnknownMessageReceived event.  
        host.UnknownMessageReceived += delegate(object sender, UnknownMessageReceivedEventArgs e)  
        {  
            Console.WriteLine("Unknown Message Received:");  
            Console.WriteLine(e.Message);  
        };  
  
        return host;  
    }  
}  
```  
  
 随后可在服务的 `svc` 文件中指定此自定义 <xref:System.ServiceModel.Activities.Activation.WorkflowServiceHostFactory>。  
  
```  
<% @ServiceHost Language="C#" Service="OrderServiceWorkflow" Factory="CustomFactory" %>  
```  
  
 调用此处理程序时，消息可以使用 <xref:System.ServiceModel.UnknownMessageReceivedEventArgs> 的 <xref:System.ServiceModel.UnknownMessageReceivedEventArgs.Message%2A> 属性进行检索，并且类似于下面的消息。  
  
```Output  
<s:Envelope xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">  
  <s:Header>  
    <To s:mustUnderstand="1" xmlns="http://schemas.microsoft.com/ws/2005/05/addressing/none">http://localhost:8080/OrderService</To>  
    <Action s:mustUnderstand="1" xmlns="http://schemas.microsoft.com/ws/2005/05/addressing/none">http://tempuri.org/IService/AddItem</Action>  
  </s:Header>  
  <s:Body>  
    <AddItem xmlns="http://tempuri.org/">  
      <Item>Books</Item>  
    </AddItem>  
  </s:Body>  
</s:Envelope>  
  
```  
  
 检查调度到 <xref:System.ServiceModel.ServiceHostBase.UnknownMessageReceived> 处理程序的消息可能会提供有关消息未与工作流服务实例关联的原因的线索。  
  
## 使用跟踪监视工作流进度  
 通过跟踪可监视工作流的进度。默认情况下，将针对工作流生命周期事件、活动生命周期事件、错误传播以及书签恢复发出跟踪记录。此外，自定义活动也可以发出自定义跟踪记录。对相关问题进行疑难解答时，活动跟踪记录、书签恢复记录以及错误传播记录是最有用的。活动跟踪记录可用于确定工作流的当前进度，并有助于识别当前正等待消息的消息传递活动。书签恢复记录很有用是因为这些记录可指示工作流已接收到消息，而错误传播记录则提供工作流中所有错误的记录。若要启用跟踪，请在 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 的 <xref:System.ServiceModel.Activities.WorkflowServiceHost.WorkflowExtensions%2A> 中指定所需 <xref:System.Activities.Tracking.TrackingParticipant>。在下面的示例中，使用默认跟踪配置文件配置了 `ConsoleTrackingParticipant`（来自[自定义跟踪](../../../../docs/framework/windows-workflow-foundation/samples/custom-tracking.md)示例）。  
  
```csharp  
host.WorkflowExtensions.Add(new ConsoleTrackingParticipant());  
```  
  
 跟踪参与者（如 ConsoleTrackingParticipant）对于具有控制台窗口的自承载工作流服务很有用。对于 Web 承载的服务，应使用将跟踪信息记录到持久存储区的跟踪参与者，如内置 <xref:System.Activities.Tracking.EtwTrackingParticipant> 或使用将信息记录到文件的自定义跟踪参与者（如[使用文本文件跟踪](../../../../docs/framework/windows-workflow-foundation/samples/tracking-using-a-text-file.md)示例中的 `TextWriterTrackingParticpant`）。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]跟踪以及为 Web 承载的工作流服务配置跟踪的更多信息，请参见[工作流跟踪](../../../../docs/framework/windows-workflow-foundation//workflow-tracking-and-tracing.md)、[为工作流配置跟踪](../../../../docs/framework/windows-workflow-foundation//configuring-tracking-for-a-workflow.md)和[跟踪 &#91;WF 示例&#93;](../../../../docs/framework/windows-workflow-foundation/samples/tracking.md)示例。  
  
## 使用 WCF 跟踪  
 WCF 跟踪提供对发往和来自工作流服务的消息流的跟踪。对相关问题（尤其是基于内容的相关）进行疑难解答时，此跟踪信息很有用。若要启用跟踪，对于 Web 承载的工作流服务，请在 `web.config` 文件的 `system.diagnostics` 节中指定所需跟踪侦听器，对于自承载的工作流服务，请在 `app.config` 文件中指定所需跟踪侦听器。若要在跟踪文件中包括消息内容，请在 `system.serviceModel` 的 `diagnostics` 节的 `messageLogging` 元素中将 `logEntireMessage` 指定为 `true`。在下面的示例中，将包括消息内容的跟踪信息配置为写入名为 `service.svclog` 的文件。  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
  <system.diagnostics>  
    <sources>  
      <source name="System.ServiceModel" switchValue="Information" propagateActivity="true">  
        <listeners>  
          <add name="corr"/>  
        </listeners>  
      </source>  
      <source name="System.ServiceModel.MessageLogging">  
        <listeners>  
          <add name="corr"/>  
        </listeners>  
      </source>  
    </sources>  
  
    <sharedListeners>  
      <add name="corr" type="System.Diagnostics.XmlWriterTraceListener" initializeData="c:\logs\service.svclog">  
      </add>  
    </sharedListeners>  
  </system.diagnostics>  
  
  <system.serviceModel>  
    <diagnostics>  
      <messageLogging logEntireMessage="true" logMalformedMessages="false"  
         logMessagesAtServiceLevel="false" logMessagesAtTransportLevel="true" maxSizeOfMessageToLog="2147483647">  
      </messageLogging>  
    </diagnostics>  
  </system.serviceModel>  
</configuration>  
```  
  
 若要查看 `service.svclog` 中包含的跟踪信息，请使用[服务跟踪查看器工具 \(SvcTraceViewer.exe\)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md)。对基于内容的相关问题进行疑难解答时，此工具尤其有用，因为您可查看消息内容，并准确了解传递的内容以及它是否与基于内容的相关的 <xref:System.ServiceModel.CorrelationQuery> 匹配。有关 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] WCF 跟踪的更多信息，请参见[服务跟踪查看器工具 \(SvcTraceViewer.exe\)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md)、[配置跟踪](../../../../docs/framework/wcf/diagnostics/tracing/configuring-tracing.md)和[使用跟踪来排除应用程序故障](../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)。  
  
## 常见上下文交换相关问题  
 某些类型的相关需要使用特定类型的绑定才能正常工作。例如需要双向绑定（如 <xref:System.ServiceModel.BasicHttpBinding>）的请求\-答复相关和需要基于上下文的绑定（如 <xref:System.ServiceModel.BasicHttpContextBinding>）的上下文交换相关。大多数绑定支持双向操作，因此这对于请求\-答复相关并不是常见问题，但是只有几种基于上下文的绑定，包括 <xref:System.ServiceModel.BasicHttpContextBinding>、<xref:System.ServiceModel.WSHttpContextBinding> 和 <xref:System.ServiceModel.NetTcpContextBinding>。如果未使用这些绑定中的一种，则对工作流服务的初次调用会成功，但是后续调用会失败并出现下面的 <xref:System.ServiceModel.FaultException>。  
  
```Output  
没有上下文附加到服务的传入消息，  
并且当前操作未标有“CanCreateInstance = true”。  
若要与此服务通信，请检查传入绑定是否  
支持上下文协议并已初始化了有效的上下文。  
```  
  
 用于上下文相关的上下文信息可由 <xref:System.ServiceModel.Activities.SendReply> 返回到 <xref:System.ServiceModel.Activities.Receive> 活动，该活动在使用双向操作时初始化上下文相关，如果操作是单向的，则上下文信息也可由调用方指定。如果调用方未发送上下文，或工作流服务未返回上下文，则当调用后续操作时，会返回前面介绍的 <xref:System.ServiceModel.FaultException>。  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [上下文交换](../../../../docs/framework/wcf/feature-details/context-exchange-correlation.md).  
  
## 常见请求\-答复相关问题  
 将请求\-答复相关与 <xref:System.ServiceModel.Activities.Receive>\/<xref:System.ServiceModel.Activities.SendReply> 对配合使用可以在工作流服务中实现双向操作，而与 <xref:System.ServiceModel.Activities.Send>\/<xref:System.ServiceModel.Activities.ReceiveReply> 对配合使用可以在其他 Web 服务中调用双向操作。在 WCF 服务中调用双向操作时，该服务可以是传统的基于命令性代码的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务，也可以是工作流服务。若要使用请求\-答复相关，必须使用双向绑定（如 <xref:System.ServiceModel.BasicHttpBinding>），且操作则必须是双向的。  
  
 如果工作流服务具有并行的双向操作，或具有重叠的 <xref:System.ServiceModel.Activities.Receive>\/<xref:System.ServiceModel.Activities.SendReply> 或 <xref:System.ServiceModel.Activities.Send>\/<xref:System.ServiceModel.Activities.ReceiveReply> 对，则 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 提供的隐式相关句柄管理可能不足（尤其是在高压力方案中），并且可能无法正确路由消息。若要防止此问题发生，我们建议您在使用请求\-答复相关时，始终显式指定 <xref:System.ServiceModel.Activities.CorrelationHandle>。从工作流设计器的**“工具箱”**的“消息传递”部分使用**“SendAndReceiveReply”**和**“ReceiveAndSendReply”**模板时，默认情况下将显式配置 <xref:System.ServiceModel.Activities.CorrelationHandle>。使用代码生成工作流时，将在对中第一个活动的 <xref:System.ServiceModel.Activities.Receive.CorrelationInitializers%2A> 中指定 <xref:System.ServiceModel.Activities.CorrelationHandle>。在下面的示例中，使用 <xref:System.ServiceModel.Activities.RequestReplyCorrelationInitializer> 中指定的显式 <xref:System.ServiceModel.Activities.CorrelationInitializer.CorrelationHandle%2A> 来配置 <xref:System.ServiceModel.Activities.Receive> 活动。  
  
```csharp  
Variable<CorrelationHandle> RRHandle = new Variable<CorrelationHandle>();  
  
Receive StartOrder = new Receive  
{  
    CanCreateInstance = true,  
    ServiceContractName = OrderContractName,  
    OperationName = "StartOrder",  
    CorrelationInitializers =  
    {  
        new RequestReplyCorrelationInitializer  
        {  
            CorrelationHandle = RRHandle  
        }  
    }  
};  
  
SendReply ReplyToStartOrder = new SendReply  
{  
    Request = StartOrder,  
    Content = ... // Contains the return value, if any.  
};  
  
// Construct a workflow using StartOrder and ReplyToStartOrder.  
```  
  
 在 <xref:System.ServiceModel.Activities.Receive>\/<xref:System.ServiceModel.Activities.SendReply> 对或 <xref:System.ServiceModel.Activities.Send>\/<xref:System.ServiceModel.Activities.ReceiveReply> 对之间不允许存在持久性。会创建一个非永久性区域，该区域会持续到两个活动都已完成。如果某个活动（如延迟活动）处于此非永久性区域中，并使工作流成为空闲状态，则工作流不会持久，即使主机配置为在工作流成为空闲状态时保持工作流也是如此。如果某个活动（如 Persist 活动）尝试在非永久性区域中显式保持，则会引发严重异常，工作流会中止，并将 <xref:System.ServiceModel.FaultException> 返回给调用方。严重异常消息为“System.InvalidOperationException: 非永久性块内不能包含 Persist 活动”。此异常不会返回给调用方，但是可以观察到（如果启用了跟踪）。返回给调用方的 <xref:System.ServiceModel.FaultException> 消息为“无法执行操作，因为 WorkflowInstance‘5836145b\-7da2\-49d0\-a052\-a49162adeab6’已完成”。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]请求\-答复相关的更多信息，请参见[请求\-答复](../../../../docs/framework/wcf/feature-details/request-reply-correlation.md)。  
  
## 常见内容相关问题  
 当工作流服务接收到多个消息，且交换的消息中的一段数据标识了所需实例时，会使用基于内容的相关。基于内容的相关使用消息中的此数据（如客户编号或订单 ID）将消息路由到正确的工作流实例。本节描述使用基于内容的相关时可能出现的几个常见问题。  
  
### 确保标识数据唯一  
 用于标识实例的数据经过哈希运算之后即可成为相关键。必须小心确保用于相关的数据是唯一的，否则经过哈希运算的键中可能会出现冲突，从而导致错误路由消息。例如，仅基于客户姓名的相关可能会导致冲突，因为可能存在多个具有相同姓名的客户。在使消息彼此相关所采用的数据中，不得使用冒号 \(:\)，因为冒号已用于分隔消息查询的键和值以便构成将在随后进行哈希运算的字符串。如果使用持久性，请确保以前保留的实例未使用当前标识数据。暂时禁用持久性可有助于确定此问题。WCF 跟踪可用于查看计算出的相关键，对于调试此类问题十分有用。  
  
### 争用条件  
 在服务接收消息到实际初始化相关之间有一小段时间间隙，在这段时间内将忽略后续的消息。如果工作流服务使用通过单向操作从客户机传递的数据来初始化基于内容的相关，且调用方立即发送后续消息，则在这段时间间隔内会忽略这些消息。可通过使用双向操作初始化相关，或通过使用 <xref:System.ServiceModel.Activities.TransactedReceiveScope> 来避免发生这种情况。  
  
### 相关查询问题  
 相关查询用于指定消息中的哪些数据用于使消息相关。这些数据使用 XPath 查询进行指定。如果即使看起来一切正常，但仍未调度传递给服务的消息，则一种疑难解答策略是指定与消息数据的值匹配的文本值（而不是 XPath 查询）。若要指定文本值，请使用 `string` 函数。在下面的示例中，<xref:System.ServiceModel.MessageQuerySet> 配置为对 `OrderId` 使用文本值 `11445`，而注释掉 XPath 查询。  
  
```csharp  
MessageQuerySet = new MessageQuerySet  
{  
    {  
        "OrderId",   
        //new XPathMessageQuery("sm:body()/tempuri:StartOrderResponse/tempuri:OrderId")  
        new XPathMessageQuery("string('11445')")  
    }  
}  
```  
  
 如果 XPath 查询配置不正确，从而未检索到任何相关数据，则会返回错误，同时显示下面的消息：“相关查询生成了空结果集。请确保正确配置了终结点的相关查询。”解决此问题的一种快速方式是将 XPath 查询替换为文本值，如上一节中所述。如果在**“添加相关初始值设定项”**或**“CorrelatesOn 定义”**对话框中使用 XPath 查询生成器且工作流服务使用消息协定，则可能会发生此问题。下面的示例定义了一个消息协定类。  
  
```csharp  
[MessageContract]  
public class AddItemMessage  
{  
    [MessageHeader]  
    public string CartId;  
  
    [MessageBodyMember]  
    public string Item;  
}  
  
```  
  
 此消息协定由 <xref:System.ServiceModel.Activities.Receive> 活动在工作流中使用。消息标头中的 `CartId` 用于将消息与正确实例相关。如果使用工作流设计器中的相关对话框创建检索 `CartId` 的 XPath 查询，则会生成以下不正确的 XPath 查询。  
  
```  
sm:body()/xg0:AddItemMessage/xg0:CartId  
  
```  
  
 如果 <xref:System.ServiceModel.Activities.Receive> 活动使用数据的参数，则此 XPath 查询是正确的，但是由于它使用消息协定，因此是不正确的。下面的 XPath 查询是用于从标头检索 `CartId` 的正确 XPath 查询。  
  
```  
sm:header()/tempuri:CartId  
  
```  
  
 可以通过检查消息正文确认此情况。  
  
```xml  
<s:Envelope xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">  
  <s:Header>  
    <Action s:mustUnderstand="1" xmlns="http://schemas.microsoft.com/ws/2005/05/addressing/none">http://tempuri.org/IService/AddItem</Action>  
    <h:CartId xmlns:h="http://tempuri.org/">80c95b41-c98d-4660-a6c1-99412206e54c</h:CartId>  
  </s:Header>  
  <s:Body>  
    <AddItemMessage xmlns="http://tempuri.org/">  
      <Item>Books</Item>  
    </AddItemMessage>  
  </s:Body>  
</s:Envelope>  
  
```  
  
 下面的示例演示一个 <xref:System.ServiceModel.Activities.Receive> 活动，该活动针对使用以前的消息协定检索数据的 `AddItem` 操作而配置。XPath 查询进行了正确配置。  
  
```xaml  
<Receive CorrelatesWith="[CCHandle] OperationName="AddItem" ServiceContractName="p:IService">  
  <Receive.CorrelatesOn>  
    <XPathMessageQuery x:Key="key1">  
      <XPathMessageQuery.Namespaces>  
        <ssx:XPathMessageContextMarkup>  
          <x:String x:Key="xg0">http://schemas.datacontract.org/2004/07/MessageContractWFService</x:String>  
        </ssx:XPathMessageContextMarkup>  
      </XPathMessageQuery.Namespaces>sm:header()/tempuri:CartId</XPathMessageQuery>  
  </Receive.CorrelatesOn>  
  <ReceiveMessageContent DeclaredMessageType="m:AddItemMessage">  
    <p1:OutArgument x:TypeArguments="m:AddItemMessage">[AddItemMessage]</p1:OutArgument>  
  </ReceiveMessageContent>  
</Receive>  
  
```  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]基于内容的相关的更多信息，请参见[基于内容](../../../../docs/framework/wcf/feature-details/content-based-correlation.md)和[相关计算器](../../../../docs/framework/windows-workflow-foundation/samples/correlated-calculator.md)示例。