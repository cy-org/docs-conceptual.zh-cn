---
title: "事务处理批处理 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ecd328ed-332e-479c-a894-489609bcddd2
caps.latest.revision: 23
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 23
---
# 事务处理批处理
本示例演示如何通过使用消息队列 \(MSMQ\) 来批处理事务处理读取。  事务处理批处理是排队通信中事务处理读取的一种性能优化功能。  
  
> [!NOTE]
>  本主题的最后介绍了此示例的设置过程和生成说明。  
  
 在排队通信中，客户端使用队列与服务进行通信。  更确切地说，客户端向队列发送消息。  服务从队列接收消息。  因此不必同时运行服务和客户端便可使用队列进行通信。  
  
 本示例演示事务处理批处理。  事务处理批处理是一种行为，通过该行为可以在读取队列中的多个消息并处理这些消息时使用单个事务。  
  
### 设置、生成和运行示例  
  
1.  确保已经执行了[Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2.  如果先运行服务，则它将检查以确保队列存在。  如果队列不存在，则服务将创建一个队列。  可以先运行服务以创建队列或通过 MSMQ 队列管理器创建一个队列。  执行下面的步骤来在 Windows 2008 中创建队列。  
  
    1.  在 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 中打开服务器管理器。  
  
    2.  展开**“功能”**选项卡。  
  
    3.  右击**“私有消息队列”**，然后选择**“新建”**和**“专用队列”**。  
  
    4.  选中**“事务性”**框。  
  
    5.  输入 `ServiceModelSamplesTransacted` 作为新队列的名称。  
  
    > [!NOTE]
    >  在此示例中，客户端将数以百计的消息作为批的一部分发送。  通常，服务应用程序会花一些时间处理这些消息。  
  
3.  若要生成 C\# 或 Visual Basic .NET 版本的解决方案，请按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明进行操作。  
  
4.  若要用单机配置或跨计算机配置来运行示例，请按照[运行 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/running-the-samples.md)中的说明进行操作。  
  
### 在加入到工作组或在没有 Active Directory 集成的计算机上运行示例  
  
1.  默认情况下使用 <xref:System.ServiceModel.NetMsmqBinding> 启用传输安全。  MSMQ 传输安全性有两个相关的属性，即 <xref:System.ServiceModel.MsmqTransportSecurity.MsmqAuthenticationMode%2A> 和 <xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A>。默认情况下，身份验证模式设置为 `Windows`，保护级别设置为 `Sign`。  为了使 MSMQ 提供身份验证和签名功能，MSMQ 必须是域的一部分，并且必须安装 MSMQ 的 Active Directory 集成选项。  如果在不满足这些条件的计算机上运行此示例，将会收到错误。  
  
2.  如果计算机不是域成员或尚未安装 Active Directory 集成，请将身份验证模式和保护级别设置为 `None` 以关闭传输安全性，如下面的示例配置所示：  
  
    ```  
    <system.serviceModel>  
      <behaviors>  
        <serviceBehaviors>  
          <behavior name="ThrottlingBehavior">  
            <serviceMetadata httpGetEnabled="true"/>  
            <serviceThrottling maxConcurrentCalls="5"/>  
          </behavior>  
        </serviceBehaviors>  
  
        <endpointBehaviors>  
          <behavior name="BatchingBehavior">  
            <transactedBatching maxBatchSize="100"/>  
          </behavior>  
        </endpointBehaviors>  
      </behaviors>  
      <services>  
        <service   
            behaviorConfiguration="ThrottlingBehavior"   
            name="Microsoft.ServiceModel.Samples.OrderProcessorService">  
          <host>  
            <baseAddresses>  
              <add baseAddress="http://localhost:8000/orderProcessor/transactedBatchingSample"/>  
            </baseAddresses>  
          </host>  
          <!-- Define NetMsmqEndpoint -->  
          <endpoint address="net.msmq://localhost/private/ServiceModelSamplesTransactedBatching"  
                    binding="netMsmqBinding"  
                    bindingConfiguration="Binding1"   
                    behaviorConfiguration="BatchingBehavior"   
                    contract="Microsoft.ServiceModel.Samples.IOrderProcessor" />  
          <endpoint address="mex"  
                    binding="mexHttpBinding"  
                    contract="IMetadataExchange" />  
        </service>  
      </services>  
  
      <bindings>  
        <netMsmqBinding>  
          <binding name="Binding1">  
            <security mode="None" />  
          </binding>  
        </netMsmqBinding>  
      </bindings>  
  
    </system.serviceModel>  
  
    ```  
  
3.  确保在运行示例前更改服务器和客户端上的配置。  
  
    > [!NOTE]
    >  将 `security` `mode` 设置为 `None` 等效于将 <xref:System.ServiceModel.MsmqTransportSecurity.MsmqAuthenticationMode%2A>、<xref:System.ServiceModel.MsmqTransportSecurity.MsmqProtectionLevel%2A> 和 `Message` 安全设置为 `None`。  
  
4.  若要在远程计算机上运行数据库，请更改连接字符串，使其指向数据库所在的计算机。  
  
## 要求  
 若要运行此示例，必须安装 MSMQ 并需要使用 SQL 或 SQL Express。  
  
## 演示  
 本示例演示事务处理批处理行为。  事务处理批处理是随 MSMQ 排队传输一起提供的一种性能优化功能。  
  
 当使用事务来发送和接收消息时，实际上有两个单独的事务。  当客户端在事务范围内发送消息时，事务相对于客户端和客户端队列管理器来说是本地事务。  当服务在事务范围内接收消息时，事务相对于服务和接收队列管理器来说是本地事务。  务必要记住的是，客户端和服务不会参与同一个事务；实际上，它们在对队列执行操作（如发送和接收）时使用的是不同的事务。  
  
 在本示例中，我们将使用单个事务来执行多个服务操作。  这仅作为一种性能优化功能，并不影响应用程序的语义。  本示例基于[已经过事务处理的 MSMQ 绑定](../../../../docs/framework/wcf/samples/transacted-msmq-binding.md)。  
  
## 注释  
 在本示例中，客户端在事务范围内向服务发送一批消息。  为了演示性能优化，我们将发送大量消息，在本例中，最多达 2500 条消息。  
  
 然后，服务在服务定义的事务范围内接收发送到队列的消息。  如果不进行批处理，这将导致每次调用服务操作都会产生 2500 个事务。  这会影响系统的性能。  由于涉及到两个资源管理器（MSMQ 队列和 `Orders` 数据库），因此，每个这样的事务都是一个 DTC 事务。  我们通过使用数量少得多的事务确保在单个事务中处理一批消息并进行服务操作调用，以此来进行优化。  
  
 我们通过以下方式使用批处理功能：  
  
-   在配置中指定事务处理批处理行为。  
  
-   按照要使用单个事务读取的消息的数量来指定批次大小。  
  
-   指定要运行的并发批次的最大数量。  
  
 在本示例中，我们通过减少事务数量，确保在提交事务之前在单个事务中调用 100 次服务操作，以此来演示性能的提升。  
  
 服务行为通过将 `TransactionScopeRequired` 设置为 `true` 来定义操作行为。  这可确保此方法所访问的任何资源管理器都使用相同的事务范围从队列中检索消息。  在此示例中，我们使用一个基本数据库来存储消息中包含的采购订单信息。  事务范围还可保证该方法引发异常时，消息将返回到队列。  如果不设置此操作行为，则队列通道会创建一个从队列中读取消息的事务，并在调度消息前自动提交事务，因此，如果操作失败，消息将丢失。  最常见的方案是在用于从队列中读取消息的事务中登记服务操作，如下面的代码所示。  
  
 请注意，`ReleaseServiceInstanceOnTransactionComplete` 设置为 `false`。  这是批处理的一个重要要求。  `ServiceBehaviorAttribute` 上的 `ReleaseServiceInstanceOnTransactionComplete` 属性指示事务完成后对服务实例执行什么操作。  默认情况下，事务一旦完成即释放服务实例。  批处理的核心方面是使用单个事务来读取和调度队列中的许多消息。  因此，释放服务实例会导致事务结束，从而过早地取消批处理的真正使用。  如果此属性设置为 `true`，并且将事务处理批处理行为添加到终结点，则批处理验证行为将引发异常。  
  
```  
// Service class that implements the service contract.  
// Added code to write output to the console window.  
[ServiceBehavior(ReleaseServiceInstanceOnTransactionComplete=false,   
TransactionIsolationLevel=  
System.Transactions.IsolationLevel.Serializable, ConcurrencyMode=ConcurrencyMode.Multiple)]  
public class OrderProcessorService : IOrderProcessor  
{  
    [OperationBehavior(TransactionScopeRequired = true,  
                       TransactionAutoComplete = true)]  
    public void SubmitPurchaseOrder(PurchaseOrder po)  
    {  
        Orders.Add(po);  
        Console.WriteLine("Processing {0} ", po);  
    }  
    …  
}  
  
```  
  
 `Orders` 类包装了订单处理。  在此示例中，它用采购订单信息更新数据库。  
  
```  
// Order Processing Logic  
public class Orders  
{  
    public static void Add(PurchaseOrder po)  
    {  
        // Insert purchase order.  
        SqlCommand insertPurchaseOrderCommand =   
        new SqlCommand(  
        "insert into PurchaseOrders(poNumber, customerId)   
                               values(@poNumber, @customerId)");  
        insertPurchaseOrderCommand.Parameters.Add("@poNumber",   
                                           SqlDbType.VarChar, 50);  
        insertPurchaseOrderCommand.Parameters.Add("@customerId",   
                                         SqlDbType.VarChar, 50);  
  
        // Insert product line item.  
        SqlCommand insertProductLineItemCommand =   
             new SqlCommand("insert into ProductLineItems(productId,   
                    unitCost, quantity, poNumber) values(@productId,   
                    @unitCost, @quantity, @poNumber)");  
        insertProductLineItemCommand.Parameters.Add("@productId",   
                                           SqlDbType.VarChar, 50);  
        insertProductLineItemCommand.Parameters.Add("@unitCost",   
                                                  SqlDbType.Float);  
        insertProductLineItemCommand.Parameters.Add("@quantity",   
                                                     SqlDbType.Int);  
        insertProductLineItemCommand.Parameters.Add("@poNumber",   
                                           SqlDbType.VarChar, 50);  
        int rowsAffected = 0;  
        using (TransactionScope scope =   
              new TransactionScope(TransactionScopeOption.Required))  
        {  
             using (SqlConnection conn = new   
                 SqlConnection(  
                 ConfigurationManager.AppSettings["connectionString"]))  
             {  
                 conn.Open();  
  
                // Insert into purchase order table.  
               insertPurchaseOrderCommand.Connection = conn;  
               insertPurchaseOrderCommand.Parameters["@poNumber"].Value   
                                                       = po.PONumber;  
             insertPurchaseOrderCommand.Parameters["@customerId"].Value   
                                                    =po.CustomerId;  
             insertPurchaseOrderCommand.ExecuteNonQuery();  
  
            // Insert into product line item table.  
            insertProductLineItemCommand.Connection = conn;  
            foreach (PurchaseOrderLineItem orderLineItem in   
                                        po.orderLineItems) {  
            insertProductLineItemCommand.Parameters["@poNumber"].Value   
                                                          =po.PONumber;  
            insertProductLineItemCommand.Parameters["@productId"].Value   
                                             = orderLineItem.ProductId;  
            insertProductLineItemCommand.Parameters["@unitCost"].Value   
                                             = orderLineItem.UnitCost;  
            insertProductLineItemCommand.Parameters["@quantity"].Value   
                                             = orderLineItem.Quantity;  
            rowsAffected +=   
            insertProductLineItemCommand.ExecuteNonQuery();  
            }  
            scope.Complete();  
        }  
     }  
     Console.WriteLine(  
     "Updated database with {0} product line items  for purchase order   
                                     {1} ", rowsAffected, po.PONumber);  
    }  
}  
```  
  
 批处理行为及其配置在服务应用程序配置中指定。  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
  <appSettings>  
    <!-- Use appSetting to configure MSMQ queue name. -->  
    <add key="queueName"   
     value=".\private$\ServiceModelSamplesTransactedBatching" />  
    <add key="baseAddress"   
     value=  
     "http://localhost:8000/orderProcessor/transactedBatchingSample"/>  
    <add key="connectionString" value="Data Source=.\SQLEXPRESS;AttachDbFilename=|DataDirectory|orders.mdf;Integrated Security=True;User Instance=True;" />  
  </appSettings>  
  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="ThrottlingBehavior">  
          <serviceThrottling maxConcurrentCalls="5"/>  
        </behavior>  
      </serviceBehaviors>  
  
      <endpointBehaviors>  
        <behavior name="BatchingBehavior">  
          <transactedBatching maxBatchSize="100"/>  
        </behavior>  
      </endpointBehaviors>  
    </behaviors>  
    <services>  
      <service   
          behaviorConfiguration="ThrottlingBehavior"   
          name="Microsoft.ServiceModel.Samples.OrderProcessorService">  
        <!-- Define NetMsmqEndpoint -->  
        <endpoint address=  
"net.msmq://localhost/private/ServiceModelSamplesTransactedBatching"  
                  binding="netMsmqBinding"  
                  behaviorConfiguration="BatchingBehavior"   
                  contract=  
                    "Microsoft.ServiceModel.Samples.IOrderProcessor" />  
      </service>  
    </services>  
  </system.serviceModel>  
</configuration>  
```  
  
> [!NOTE]
>  批次大小是一种系统提示。  例如，如果将批次大小指定为 20，则会使用单个事务读取和调度 20 条消息，然后提交事务。  但在有些情况下可能会在达到批次大小之前提交事务。  
>   
>  每个事务都有一个与之关联的超时，事务创建后，超时就开始计时。  当此超时过期时，事务就会中止。  在达到批次大小之前，此超时有可能过期。  为了避免因中止而重新执行该批次，`TransactedBatchingBehavior` 会检查事务上剩余多少时间。  如果已经用完事务超时的 80%，则会提交事务。  
>   
>  如果队列中已没有其他消息，则 <xref:System.ServiceModel.Description.TransactedBatchingBehavior> 将会提交事务而不等待达到批次大小。  
>   
>  批次大小的选择取决于应用程序。  如果批次大小过小，则可能无法获得所需的性能。  另一方面，如果批次大小过大，则可能会使性能下降。  例如，事务的生存期可能较长并对数据库保持锁定，或者事务可能会变为死锁状态，这会导致批处理回滚并重做工作。  
  
 客户端创建事务范围。  与队列的通信发生在事务范围之内，从而可将该事务范围视为原子单元，其中所有消息均将发送到队列或者没有任何消息发送到队列。  通过在事务范围上调用 <xref:System.Transactions.TransactionScope.Complete%2A> 可以提交事务。  
  
```  
//Client implementation code.  
class Client  
{  
    static void Main()  
    {  
        Random randomGen = new Random();  
        for (int i = 0; i < 2500; i++)  
        {  
            // Create a client with given client endpoint configuration.  
            OrderProcessorClient client = new OrderProcessorClient("OrderProcessorEndpoint");  
  
            // Create the purchase order.  
            PurchaseOrder po = new PurchaseOrder();  
            po.CustomerId = "somecustomer" + i + ".com";  
            po.PONumber = Guid.NewGuid().ToString();  
  
            PurchaseOrderLineItem lineItem1 = new PurchaseOrderLineItem();  
            lineItem1.ProductId = "Blue Widget";  
            lineItem1.Quantity = randomGen.Next(1, 100);  
            lineItem1.UnitCost = (float)randomGen.NextDouble() * 10;  
  
            PurchaseOrderLineItem lineItem2 = new PurchaseOrderLineItem();  
            lineItem2.ProductId = "Red Widget";  
            lineItem2.Quantity = 890;  
            lineItem2.UnitCost = 45.89F;  
  
            po.orderLineItems = new PurchaseOrderLineItem[2];  
            po.orderLineItems[0] = lineItem1;  
            po.orderLineItems[1] = lineItem2;  
  
            //Create a transaction scope.  
            using (TransactionScope scope = new TransactionScope(TransactionScopeOption.Required))  
            {  
                // Make a queued call to submit the purchase order.  
                client.SubmitPurchaseOrder(po);  
                // Complete the transaction.  
                scope.Complete();  
            }  
  
            client.Close();  
        }  
        Console.WriteLine();  
        Console.WriteLine("Press <ENTER> to terminate client.");  
        Console.ReadLine();  
    }  
}  
```  
  
 运行示例时，客户端和服务活动将显示在服务和客户端控制台窗口中。  您可以看到服务从客户端接收消息。  在每个控制台窗口中按 Enter 可以关闭服务和客户端。  请注意：由于正在使用队列，因此不必同时启动和运行客户端和服务。  可以先运行客户端，再将其关闭，然后启动服务，这样服务仍然会收到客户端的消息。  在批次中读取和处理消息时，可以看到滚动输出。  
  
```  
The service is ready.  
Press <ENTER> to terminate service.  
  
Updated database with 2 product line items for purchase order 493ac832-d216-4e94-b2a5-d7f492fb5e39  
Processing Purchase Order: 8b567f5b-0661-4662-aae2-6cef1bd6d278  
        Customer: somecustomer849.com  
        OrderDetails  
               Order LineItem: 80 of Blue Widget @unit price: $9.751623  
               Order LineItem: 890 of Red Widget @unit price: $45.89  
        Total cost of this order: $41622.23  
        Order status: Pending  
  
Updated database with 2 product line items for purchase order 41130b95-4ea8-40a9-91c3-2e129117fcb8  
Processing Purchase Order: 5ce2699d-9a31-4cc2-a8c5-64cda614b3c7  
        Customer: somecustomer850.com  
        OrderDetails  
               Order LineItem: 89 of Blue Widget @unit price: $6.369128  
               Order LineItem: 890 of Red Widget @unit price: $45.89  
        Total cost of this order: $41408.95  
        Order status: Pending  
  
Updated database with 2 product line items for purchase order 8b567f5b-0661-4662-aae2-6cef1bd6d278  
Processing Purchase Order: ea94486b-7c86-4309-a42d-2f06c00656cd  
        Customer: somecustomer851.com  
        OrderDetails  
             Order LineItem: 47 of Blue Widget @unit price: $0.9391424  
             Order LineItem: 890 of Red Widget @unit price: $45.89  
        Total cost of this order: $40886.24  
        Order status: Pending  
```  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。  在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。  此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\Binding\Net\MSMQ\Batching`  
  
## 请参阅