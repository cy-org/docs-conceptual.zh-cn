---
title: "自定义多路分解器 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fc54065c-518e-4146-b24a-0fe00038bfa7
caps.latest.revision: 41
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 41
---
# 自定义多路分解器
本示例演示如何将 MSMQ 消息头映射到不同服务操作，以便使用 <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding> 的 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务不再像 [到 Windows Communication Foundation 的消息队列](../../../../docs/framework/wcf/samples/message-queuing-to-wcf.md) 和 [Windows Communication Foundation 到消息队列](../../../../docs/framework/wcf/samples/wcf-to-message-queuing.md) 示例中那样限于使用一个服务操作。  
  
 本示例中的服务是自承载控制台应用程序，通过它可以观察接收排队消息的服务。  
  
 此服务协定是 `IOrderProcessor`，它定义了适合与队列一起使用的单向服务。  
  
```  
[ServiceContract]  
[KnownType(typeof(PurchaseOrder))]  
[KnownType(typeof(String))]  
public interface IOrderProcessor  
{  
    [OperationContract(IsOneWay = true, Name = "SubmitPurchaseOrder")]  
    void SubmitPurchaseOrder(MsmqMessage<PurchaseOrder> msg);  
  
    [OperationContract(IsOneWay = true, Name = "CancelPurchaseOrder")]  
    void CancelPurchaseOrder(MsmqMessage<string> ponumber);  
}  
```  
  
 MSMQ 消息没有 Action 标头。  无法自动将不同的 MSMQ 消息映射到操作协定。  所以只能有一个操作协定。  为了克服此限制，服务实现 <xref:System.ServiceModel.Dispatcher.IDispatchOperationSelector> 接口的 <xref:System.ServiceModel.Dispatcher.IDispatchOperationSelector.SelectOperation%2A> 方法。  通过 <xref:System.ServiceModel.Dispatcher.IDispatchOperationSelector.SelectOperation%2A> 方法，服务可以将给定的消息头映射到特定服务操作。  在本示例中，将消息的标签标头映射到服务操作。  操作协定的 `Name` 参数确定必须为给定的消息标签调度哪个服务操作。  例如，如果消息的标签标头包含“SubmitPurchaseOrder”，则调用“SubmitPurchaseOrder”服务操作。  
  
```  
public class OperationSelector : IDispatchOperationSelector  
{  
    public string SelectOperation(ref System.ServiceModel.Channels.Message message)  
    {  
        MsmqIntegrationMessageProperty property = MsmqIntegrationMessageProperty.Get(message);  
        return property.Label;  
    }  
}  
```  
  
 服务必须实现 <xref:System.ServiceModel.Description.IContractBehavior> 接口的 <xref:System.ServiceModel.Description.IContractBehavior.ApplyDispatchBehavior%28System.ServiceModel.Description.ContractDescription%2CSystem.ServiceModel.Description.ServiceEndpoint%2CSystem.ServiceModel.Dispatcher.DispatchRuntime%29> 方法，如下面的示例代码所示。  这会将自定义 `OperationSelector` 应用于服务框架调度运行时。  
  
```  
void IContractBehavior.ApplyDispatchBehavior(ContractDescription description, ServiceEndpoint endpoint, DispatchRuntime dispatch)  
{  
    dispatch.OperationSelector = new OperationSelector();  
}  
```  
  
 在到达 OperationSelector 之前，消息必须通过调度程序的 <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.ContractFilter%2A>。  默认情况下，如果在由服务实现的任何协定上找不到消息操作，则会拒绝该消息。  为了避免这种阻碍的发生，我们实现了一个名为 `MatchAllFilterBehavior` 的 <xref:System.ServiceModel.Description.IEndpointBehavior>，它通过应用 <xref:System.ServiceModel.Dispatcher.MatchAllMessageFilter> 允许任何消息通过 `ContractFilter`，如下所示。  
  
```  
public void ApplyDispatchBehavior(ServiceEndpoint serviceEndpoint, EndpointDispatcher endpointDispatcher)  
{  
    endpointDispatcher.ContractFilter = new MatchAllMessageFilter();  
}  
```  
  
 当服务接收到消息时，会使用标签标头提供的信息调度相应的服务操作。  消息正文反序列化为 `PurchaseOrder` 对象，如下面的示例代码所示。  
  
```  
[OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = true)]  
public void SubmitPurchaseOrder(MsmqMessage<PurchaseOrder> msg)  
{  
    PurchaseOrder po = (PurchaseOrder)msg.Body;  
    Random statusIndexer = new Random();  
    po.Status = (OrderStates)statusIndexer.Next(3);  
    Console.WriteLine("Processing {0} ", po);  
}  
```  
  
 服务是自承载服务。  使用 MSMQ 时，必须提前创建所使用的队列。  可以手动或通过代码完成此操作。  在本示例中，服务包含用以检查队列是否存在的代码，并在队列不存在时创建该队列。  从配置文件中读取队列名称。  
  
```  
public static void Main()  
{  
    // Get MSMQ queue name from app settings in configuration  
    string queueName = ConfigurationManager.AppSettings["orderQueueName"];  
  
    // Create the transacted MSMQ queue if necessary.  
    if (!MessageQueue.Exists(queueName))  
        MessageQueue.Create(queueName, true);  
  
    // Create a ServiceHost for the CalculatorService type.  
    using (ServiceHost serviceHost = new ServiceHost(typeof(OrderProcessorService)))  
    {                 
        ServiceEndpoint endpoint = serviceHost.Description.Endpoints[0];  
        endpoint.Behaviors.Add(new MatchAllFilterBehavior());  
  
        //Open the ServiceHost to create listeners and start listening for messages.  
        serviceHost.Open();  
  
        // The service can now be accessed.  
        Console.WriteLine("The service is ready.");  
        Console.WriteLine("Press <ENTER> to terminate service.");  
        Console.ReadLine();  
  
        // Close the ServiceHost to shutdown the service.  
        serviceHost.Close();  
    }  
}  
```  
  
 MSMQ 队列名称是在配置文件的 appSettings 节中指定的。  
  
> [!NOTE]
>  队列名称为本地计算机使用圆点 \(.\)，并在其路径中使用反斜杠分隔符。  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 终结点地址指定 msmq.formatname 方案，并为本地计算机使用 localhost。  方案后面是根据 MSMQ 格式名寻址指南正确格式化的队列地址。  
  
```  
<appSettings>  
    <!-- Use appSetting to configure the MSMQ queue name. -->  
    <add key="queueName" value=".\private$\Orders" />  
</appSettings>  
  
```  
  
> [!NOTE]
>  此示例要求安装[消息队列](http://go.microsoft.com/fwlink/?LinkId=95143)（可能为英文网页）。  
  
 启动服务并运行客户端。  
  
 下面的输出显示在客户端上。  
  
```  
Placed the order:Purchase Order: 28fc457a-1a56-4fe0-9dde-156965c21ed6  
        Customer: somecustomer.com  
        OrderDetails  
                Order LineItem: 54 of Blue Widget @unit price: $29.99  
                Order LineItem: 890 of Red Widget @unit price: $45.89  
        Total cost of this order: $42461.56  
        Order status: Pending  
Canceled the Order: 28fc457a-1a56-4fe0-9dde-156965c21ed6  
Press <ENTER> to terminate client.  
```  
  
 下面的输出必须显示在服务上。  
  
```  
The service is ready.  
Press <ENTER> to terminate service.  
Processing Purchase Order: 28fc457a-1a56-4fe0-9dde-156965c21ed6  
        Customer: somecustomer.com  
        OrderDetails  
                Order LineItem: 54 of Blue Widget @unit price: $29.99  
                Order LineItem: 890 of Red Widget @unit price: $45.89  
        Total cost of this order: $42461.56  
        Order status: Shipped  
Purchase Order 28fc457a-1a56-4fe0-9dde-156965c21ed6 is canceled  
```  
  
### 设置、生成和运行示例  
  
1.  确保已经执行了[Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2.  如果先运行服务，则它将检查以确保队列存在。  如果队列不存在，则服务将创建一个队列。  可以先运行服务以创建队列或通过 MSMQ 队列管理器创建一个队列。  执行下面的步骤来在 Windows 2008 中创建队列。  
  
    1.  在 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 中打开服务器管理器。  
  
    2.  展开**“功能”**选项卡。  
  
    3.  右击**“私有消息队列”**，然后选择**“新建”**和**“专用队列”**。  
  
    4.  选中**“事务性”**框。  
  
    5.  输入 `ServiceModelSamplesTransacted` 作为新队列的名称。  
  
3.  若要生成 C\# 或 Visual Basic .NET 版本的解决方案，请按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明进行操作。  
  
4.  若要用单机配置或跨计算机配置来运行示例，请按照[运行 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/running-the-samples.md)中的说明进行操作。  
  
### 跨计算机运行示例  
  
1.  将 \\service\\bin\\ 文件夹（在语言特定文件夹内）中的服务程序文件复制到服务计算机上。  
  
2.  将 \\client\\bin\\ 文件夹（在语言特定文件夹内）中的客户端程序文件复制到客户端计算机上。  
  
3.  在 Client.exe.config 文件中，更改 orderQueueName 以指定服务计算机名称，而不是使用“.”。  
  
4.  在服务计算机上，在命令提示符下启动 Service.exe。  
  
5.  在客户端计算机上，在命令提示符下启动 Client.exe。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。  在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。  此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\Binding\MSMQIntegration\CustomDemux`  
  
## 请参阅  
 [在 WCF 中排队](../../../../docs/framework/wcf/feature-details/queuing-in-wcf.md)   
 [消息队列 （可能为英文网页）](http://go.microsoft.com/fwlink/?LinkId=95143)