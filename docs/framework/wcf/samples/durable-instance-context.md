---
title: "持久性实例上下文 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 97bc2994-5a2c-47c7-927a-c4cd273153df
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# 持久性实例上下文
此示例演示如何自定义 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 运行库以启用持久性实例上下文。它使用 SQL Server 2005 作为其后备存储（在本例中为 SQL Server 2005 Express）。但是，它还提供了一种访问自定义存储机制的方法。  
  
> [!NOTE]
>  本主题的末尾介绍了此示例的设置过程和生成说明。  
  
 此示例涉及对 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的通道层和服务模型层进行扩展。因此，有必要先了解基础概念再阅读实现细节。  
  
 持久性实例上下文在实际方案中相当常见。例如，购物车应用程序能够在中途暂停购物并在改天继续。因此，当我们改天访问购物车应用程序时，我们的原始上下文将得以还原。一定要注意的是，当我们断开连接时，购物车应用程序（在服务器上）不保持购物车实例，而是将其状态保持在持久性存储介质中，并使用它为还原后的上下文构造新实例。因此，可为同一个上下文服务的服务实例与上一个实例不同（即，这两个实例的内存地址不同）。  
  
 持久性实例上下文是由在客户端和服务之间交换上下文 ID 的小型协议来实现的。这个上下文 ID 是在客户端上创建的，然后传输到服务。在创建了服务实例之后，服务运行库将尝试加载所保持的状态，该状态与持久性存储（默认为 SQL Server 2005 数据库）中的这个上下文 ID 相对应。如果没有可用状态，则新实例将采用其默认状态。服务实现功能使用自定义属性来标记用于更改服务实现状态的操作，以便该运行库可以在调用这些操作之后保存服务实例。  
  
 根据上面的说明，可以通过方便地区分以下两个步骤来实现目标：  
  
1.  更改在网络上传递的消息，使其包含上下文 ID。  
  
2.  更改服务的本地行为，以便实现自定义实例化逻辑。  
  
 由于上述列表中的第一项会影响网络上的消息，因此它应当作为自定义通道来实现，而且应当挂钩到通道层。第二项会影响服务的本地行为，因此可以通过扩展几个服务扩展点来实现。随后的几节将分别讨论其中的每个扩展。  
  
## 持久性 InstanceContext 通道  
 要查看的第一项就是通道层扩展。编写自定义通道时的第一步就是确定通道的通信结构。因为引入了一个新的网络协议，所以该通道应当能够与通道堆栈中的几乎所有其他通道协作。因此它应当支持所有的消息交换模式。但是，无论通道的通信结构如何，其核心功能都是相同的。更具体地说，在客户端上，它应当将上下文 ID 写入消息中；在服务中，它应当从消息中读取这个上下文 ID 并将其传递到较高层。因此，创建了一个 `DurableInstanceContextChannelBase` 类，该类充当所有持久性实例上下文通道实现的抽象基类。该类中包含常见的状态机管理功能，以及两个用来将上下文信息应用于消息并从消息中读取上下文信息的受保护成员。  
  
```  
class DurableInstanceContextChannelBase  
{  
  //…  
  protected void ApplyContext(Message message)  
  {  
    //…              
  }  
  protected string ReadContextId(Message message)  
  {  
    //…              
  }  
}  
```  
  
 这两种方法使用 `IContextManager` 实现将上下文 ID 写入消息中或从消息中读取上下文 ID。（`IContextManager` 是一个用来为所有的上下文管理器定义协定的自定义接口。）通道可以将上下文 ID 包括在 SOAP 头中，也可以包括在 HTTP Cookie 头中。每个上下文管理器实现都继承自 `ContextManagerBase` 类，该类包含所有上下文管理器的常用功能。使用该类中的 `GetContextId` 方法，可以客户端中产生上下文 ID。首次产生某个上下文 ID 时，此方法会将该上下文 ID 保存到一个文本文件中，该文件的名称是由远程终结点地址构造的（典型 URI 中的无效文件名字符会替换为 @ 字符）。  
  
 以后，当需要针对同一个远程终结点使用该上下文 ID 时，此方法会检查是否存在相应的文件。如果存在的话，此方法会读取并返回该上下文 ID。否则，此方法会返回一个新生成的上下文 ID 并将其保存到文件中。使用默认配置时，这些文件会放在名为 ContextStore 的目录中，该目录位于当前用户的临时目录中。不过，可以使用绑定元素来配置此位置。  
  
 用来传输上下文 ID 的机制是可配置的。它可以写入 HTTP Cookie 头中，也可以写入自定义 SOAP 头中。自定义 SOAP 头方法允许将该协议与非 HTTP 协议（例如，TCP 或命名管道）一起使用。这两个选项由两个类（即 `MessageHeaderContextManager` 和 `HttpCookieContextManager`）来实现。  
  
 这两个类都将上下文 ID 写入相应的消息中。例如，`MessageHeaderContextManager` 类中的 `WriteContext` 方法将上下文 ID 写入 SOAP 头中。  
  
```  
public override void WriteContext(Message message)  
{  
  string contextId = this.GetContextId();  
  
  MessageHeader contextHeader =  
    MessageHeader.CreateHeader(DurableInstanceContextUtility.HeaderName,  
      DurableInstanceContextUtility.HeaderNamespace,  
      contextId,   
      true);  
  
  message.Headers.Add(contextHeader);  
}   
```  
  
 `DurableInstanceContextChannelBase` 类中的 `ApplyContext` 和 `ReadContextId` 方法分别都调用 `IContextManager.ReadContext` 和 `IContextManager.WriteContext`。但是，这些上下文管理器不是由 `DurableInstanceContextChannelBase` 类直接创建的，而是使用 `ContextManagerFactory` 类创建的。  
  
```  
IContextManager contextManager =  
                ContextManagerFactory.CreateContextManager(contextType,   
                this.contextStoreLocation,   
                this.endpointAddress);  
```  
  
 `ApplyContext` 方法由发送通道调用。它将上下文 ID 插入传出消息中。`ReadContextId` 方法由接收通道调用。此方法可确保上下文 ID 在传入消息中可用，并将上下文 ID 添加到 `Message` 类的 `Properties` 集合中。此方法还在无法读取上下文 ID 时引发 `CommunicationException`，从而导致通道中止。  
  
```  
message.Properties.Add(DurableInstanceContextUtility.ContextIdProperty, contextId);  
```  
  
 在继续操作之前，一定要先了解 `Message` 类的 `Properties` 集合的用法。通常，在将数据从较低的通道层传递到较高层时，将使用这个 `Properties` 集合。这样，无论协议细节如何，都可以按照一致的方式向较高层提供所需的数据。换言之，通道层可以将上下文 ID 作为 SOAP 头或 HTTP Cookie 头来收发。但是，较高层没有必要知道这些细节，因为通道层会使 `Properties` 集合中提供这些信息。  
  
 现在，`DurableInstanceContextChannelBase` 类已经就绪，必须实现全部十个必要的接口（IOutputChannel、IInputChannel、IOutputSessionChannel、IInputSessionChannel、IRequestChannel、IReplyChannel、IRequestSessionChannel、IReplySessionChannel、IDuplexChannel 和 IDuplexSessionChannel）。它们类似于每个可用的消息交换模式（数据报、单工、双工以及它们的会话变量）。其中的每个实现都继承上面描述的基类，并相应地调用 `ApplyContext` 和 `ReadContexId`。例如，用来实现 IOutputChannel 接口的 `DurableInstanceContextOutputChannel` 从发送消息的每种方法中调用 `ApplyContext` 方法。  
  
```  
public void Send(Message message, TimeSpan timeout)  
{  
    // Apply the context information before sending the message.  
    this.ApplyContext(message);  
    //…  
}   
```  
  
 另一方面，用来实现 `IInputChannel` 接口的 `DurableInstanceContextInputChannel` 在接收消息的每种方法中调用 `ReadContextId` 方法。  
  
```  
public Message Receive(TimeSpan timeout)  
{  
    //…  
      ReadContextId(message);  
      return message;  
}  
```  
  
 除此之外，这些通道实现还将方法调用委托给通道堆栈中位于其下方的通道。但是，会话变量有一个基本逻辑来确保上下文 ID 仅随导致创建会话的第一条消息发送和读取。  
  
```  
if (isFirstMessage)  
{  
//…  
    this.ApplyContext(message);  
    isFirstMessage = false;  
}  
```  
  
 这些通道实现随后会由 `DurableInstanceContextBindingElement` 类和 `DurableInstanceContextBindingElementSection` 类相应地添加到 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 通道运行库中。有关绑定元素和绑定元素节的更多详细信息，请参见 [HttpCookieSession](../../../../docs/framework/wcf/samples/httpcookiesession.md) 通道示例文档。  
  
## 服务模型层扩展  
 既然上下文 ID 已经穿过了通道层，可以实现服务行为来自定义实例化了。在该实例中，存储管理器用来从持久性存储中加载状态或将状态保存到持久性存储中。如上所述，该实例提供一个将 SQL Server 2005 用作其后备存储的存储管理器。但是，还可以向该扩展中添加自定义存储机制。为此，需要声明一个必须由所有的存储管理器实现的公共接口。  
  
```  
public interface IStorageManager  
{  
    object GetInstance(string contextId, Type type);  
    void SaveInstance(string contextId, object state);  
}  
```  
  
 `SqlServerStorageManager` 类包含默认的 `IStorageManager` 实现。在它的 `SaveInstance` 方法中，给定对象使用 XmlSerializer 进行序列化并保存到 SQL Server 数据库中。  
  
```  
XmlSerializer serializer = new XmlSerializer(state.GetType());  
string data;  
  
using (StringWriter writer = new StringWriter(CultureInfo.InvariantCulture))  
{  
    serializer.Serialize(writer, state);  
    data = writer.ToString();  
}  
  
using (SqlConnection connection = new SqlConnection(GetConnectionString()))  
{  
    connection.Open();  
  
    string update = @"UPDATE Instances SET Instance = @instance WHERE ContextId = @contextId";  
  
    using (SqlCommand command = new SqlCommand(update, connection))  
    {  
        command.Parameters.Add("@instance", SqlDbType.VarChar, 2147483647).Value = data;  
        command.Parameters.Add("@contextId", SqlDbType.VarChar, 256).Value = contextId;  
  
        int rows = command.ExecuteNonQuery();  
  
        if (rows == 0)  
        {  
            string insert = @"INSERT INTO Instances(ContextId, Instance) VALUES(@contextId, @instance)";  
            command.CommandText = insert;  
            command.ExecuteNonQuery();  
        }  
    }  
}  
```  
  
 在 `GetInstance` 方法中，会针对给定的上下文 ID 读取经过序列化的数据，并将根据该数据构造的对象返回到调用方。  
  
```  
object data;  
using (SqlConnection connection = new SqlConnection(GetConnectionString()))  
{  
    connection.Open();  
  
    string select = "SELECT Instance FROM Instances WHERE ContextId = @contextId";  
    using (SqlCommand command = new SqlCommand(select, connection))  
    {  
        command.Parameters.Add("@contextId", SqlDbType.VarChar, 256).Value = contextId;  
        data = command.ExecuteScalar();  
    }  
}  
  
if (data != null)  
{  
    XmlSerializer serializer = new XmlSerializer(type);  
    using (StringReader reader = new StringReader((string)data))  
    {  
        object instance = serializer.Deserialize(reader);  
        return instance;  
    }  
}  
```  
  
 这些存储管理器的用户不应当直接实例化它们，而是应当使用 `StorageManagerFactory` 类，该类从存储管理器的创建细节提取数据。该类有一个静态成员（即 `GetStorageManager`），该成员创建一个具有给定存储管理器类型的实例。如果类型参数是 `null`，此方法会创建默认 `SqlServerStorageManager` 类的一个实例并返回它。此方法还对给定类型进行验证，确保该类型能够实现 `IStorageManager` 接口。  
  
```  
public static IStorageManager GetStorageManager(Type storageManagerType)  
{  
IStorageManager storageManager = null;  
  
if (storageManagerType == null)  
{  
    return new SqlServerStorageManager();  
}  
else  
{  
    object obj = Activator.CreateInstance(storageManagerType);  
  
    // Throw if the specified storage manager type does not  
    // implement IStorageManager.  
    if (obj is IStorageManager)  
    {  
        storageManager = (IStorageManager)obj;  
    }  
    else  
    {  
        throw new InvalidOperationException(  
                  ResourceHelper.GetString("ExInvalidStorageManager"));  
    }  
  
    return storageManager;  
}                  
}   
```  
  
 我们已经实现了要在持久性存储中读写实例的必要基础结构，现在必须采取必要的步骤来更改服务行为。  
  
 作为此过程的第一步，我们必须保存已通过通道层到达当前 InstanceContext 的上下文 ID。InstanceContext 是一个运行库组件，它充当 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 调度程序和服务实例之间的链接，可用来向服务实例提供其他状态和行为。这是必不可少的，因为在会话通信中，上下文 ID 仅随第一条消息发送。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 允许扩展它的 InstanceContext 运行库组件，方法是使用它的可扩展对象模式来添加新的状态和行为。在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中的可扩展对象模式下，可以用新功能来扩展现有的运行库类，或者向对象中添加新的状态功能。可扩展对象模式中有三个接口（即 IExtensibleObject\<T\>、IExtension\<T\> 和 IExtensionCollection\<T\>）：  
  
-   IExtensibleObject\<T\> 接口由允许进行扩展的对象来实现，这些扩展可用来自定义对象功能。  
  
-   IExtension\<T\> 接口由作为扩展的对象来实现，这些扩展是对类型为 T 的类的扩展。  
  
-   IExtensionCollection\<T\> 接口是 IExtension 的集合，它允许按类型来检索 IExtension。  
  
 因此，应当创建一个 InstanceContextExtension 类，该类实现 IExtension 接口并定义保存上下文 ID 所必需的状态。此类还提供用来存放正使用的存储管理器的状态。在保存了新状态之后，就无法对其进行修改。因此，状态是在构造实例时提供并保存到实例中的，之后，只能使用只读属性来进行访问。  
  
```  
// Constructor  
public DurableInstanceContextExtension(string contextId,   
            IStorageManager storageManager)  
{  
    this.contextId = contextId;  
    this.storageManager = storageManager;              
}  
  
// Read only properties  
public string ContextId  
{  
    get { return this.contextId; }  
}  
  
public IStorageManager StorageManager  
{  
    get { return this.storageManager; }              
}   
```  
  
 InstanceContextInitializer 类实现 IInstanceContextInitializer 接口，并将实例上下文扩展添加到所构造的 InstanceContext 的 Extensions 集合中。  
  
```  
public void Initialize(InstanceContext instanceContext, Message message)  
{  
    string contextId =   
  (string)message.Properties[DurableInstanceContextUtility.ContextIdProperty];  
  
    DurableInstanceContextExtension extension =  
                new DurableInstanceContextExtension(contextId,   
                     storageManager);  
    instanceContext.Extensions.Add(extension);  
}  
```  
  
 如上所述，上下文 ID 读取自 `Message` 类的 `Properties` 集合并传递到扩展类的构造函数。这演示了如何以一致的方式在层之间交换信息。  
  
 下一个重要的步骤是重写服务实例的创建过程。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 允许使用 IInstanceProvider 接口来实现自定义实例化行为并将它们挂钩到运行库。这可以通过实现新的 `InstanceProvider` 类来完成。在构造函数中，可以接受来自实例提供程序的服务类型。以后，可以使用此服务类型来创建新实例。在 `GetInstance` 实现中，创建了一个存储管理器实例并查找持久性实例。如果返回的是 `null`，则会实例化此服务类型的新实例并将其返回到调用方。  
  
```  
public object GetInstance(InstanceContext instanceContext, Message message)  
{  
    object instance = null;  
  
    DurableInstanceContextExtension extension =  
    instanceContext.Extensions.Find<DurableInstanceContextExtension>();  
  
    string contextId = extension.ContextId;  
    IStorageManager storageManager = extension.StorageManager;              
  
    instance = storageManager.GetInstance(contextId, serviceType);          
  
    if (instance == null)  
    {  
        instance = Activator.CreateInstance(serviceType);  
    }  
  
    return instance;  
}  
```  
  
 下一个重要的步骤是将 `InstanceContextExtension`, `InstanceContextInitializer` 和 `InstanceProvider` 类安装到服务模型运行库中。自定义属性可用来标记服务实现类以安装该行为。`DurableInstanceContextAttribute` 包含对该属性的实现，它实现了用来扩展整个服务运行库的 `IServiceBehavior` 接口。  
  
 此类有一个接受要使用的存储管理器类型的属性。这样，该实现允许用户将其各自的 `IStorageManager` 实现指定为此属性的参数。  
  
 在 `ApplyDispatchBehavior` 实现中，会对当前 `ServiceBehavior` 属性的 `InstanceContextMode` 进行验证。如果此属性设置为 Singleton，则将无法启用持久性实例化，而且将引发 `InvalidOperationException` 以通知主机。  
  
```  
ServiceBehaviorAttribute serviceBehavior =  
    serviceDescription.Behaviors.Find<ServiceBehaviorAttribute>();  
  
if (serviceBehavior != null &&  
     serviceBehavior.InstanceContextMode == InstanceContextMode.Single)  
{  
    throw new InvalidOperationException(  
       ResourceHelper.GetString("ExSingeltonInstancingNotSupported"));  
}  
```  
  
 在此之后，会创建存储管理器的实例、实例上下文初始值设定项和实例提供程序，并将它们安装在为每个终结点创建的 `DispatchRuntime` 中。  
  
```  
IStorageManager storageManager =   
    StorageManagerFactory.GetStorageManager(storageManagerType);  
  
InstanceContextInitializer contextInitializer =  
    new InstanceContextInitializer(storageManager);  
  
InstanceProvider instanceProvider =  
    new InstanceProvider(description.ServiceType);  
  
foreach (ChannelDispatcherBase cdb in serviceHostBase.ChannelDispatchers)  
{  
    ChannelDispatcher cd = cdb as ChannelDispatcher;  
  
    if (cd != null)  
    {  
        foreach (EndpointDispatcher ed in cd.Endpoints)  
        {  
            ed.DispatchRuntime.InstanceContextInitializers.Add(contextInitializer);  
            ed.DispatchRuntime.InstanceProvider = instanceProvider;  
        }  
    }  
}  
```  
  
 总之，到目前为止，此示例已经生成了一个针对自定义上下文 ID 交换启用了自定义网络协议的通道，而且还覆盖了默认实例化行为，以便从持久性存储中加载实例。  
  
 剩下的就是通过某种方法来将服务实例保存到持久性存储中。如上所述，已经有一个必需的功能来将状态保存在 `IStorageManager` 实现中。现在，我们必须将该功能与 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 运行库集成在一起。需要另一个适用于服务实现类中的方法的属性。此属性假设应用于对服务实例的状态进行更改的方法。  
  
 `SaveStateAttribute` 类实现了此功能。它还实现了 `IOperationBehavior` 类以针对每个操作修改 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 运行库。如果某个方法是用该属性标记的，那么，在构造相应的 `DispatchOperation` 时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 运行库会调用 `ApplyBehavior` 方法。在该方法实现中，有下面的一行代码：  
  
```  
dispatch.Invoker = new OperationInvoker(dispatch.Invoker);  
```  
  
 此指令会创建 `OperationInvoker` 类型的一个实例并将它分配给正构造的 `DispatchOperation` 的 `Invoker` 属性。`OperationInvoker` 类是一个包装，它面向为 `DispatchOperation` 创建的默认操作调用程序。此类实现 `IOperationInvoker` 接口。在 `Invoke` 方法实现中，实际方法调用委托给内部操作调用程序。但是，在返回结果之前，会使用 `InstanceContext` 中的存储管理器来保存服务实例。  
  
```  
object result = innerOperationInvoker.Invoke(instance,  
    inputs, out outputs);  
  
// Save the instance using the storage manager saved in the   
// current InstanceContext.  
InstanceContextExtension extension =  
    OperationContext.Current.InstanceContext.Extensions.Find<InstanceContextExtension>();  
  
extension.StorageManager.SaveInstance(extension.ContextId, instance);  
return result;  
```  
  
## 使用扩展  
 现在，完成了通道层扩展和服务模型层扩展，可以在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序中使用它们了。服务必须使用自定义绑定将通道添加到通道堆栈中，然后使用相应的属性来标记服务实现类。  
  
```  
[DurableInstanceContext]  
[ServiceBehavior(InstanceContextMode=InstanceContextMode.PerSession)]  
public class ShoppingCart : IShoppingCart  
{  
//…  
     [SaveState]  
     public int AddItem(string item)  
     {  
         //…  
     }  
//…  
 }  
```  
  
 客户端应用程序必须使用自定义绑定将 DurableInstanceContextChannel 添加到通道堆栈中。若要以声明方式在配置文件中配置通道，必须将绑定元素节添加到绑定元素扩展集合中。  
  
```  
<system.serviceModel>  
 <extensions>  
   <bindingElementExtensions>  
     <add name="durableInstanceContext"  
type="Microsoft.ServiceModel.Samples.DurableInstanceContextBindingElementSection, DurableInstanceContextExtension, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null"/>  
   </bindingElementExtensions>  
 </extensions>  
```  
  
 现在，可以像其他标准绑定元素那样，将该绑定元素用于自定义绑定：  
  
```  
<bindings>  
 <customBinding>  
   <binding name="TextOverHttp">  
     <durableInstanceContext contextType="HttpCookie"/>             
     <reliableSession />  
     <textMessageEncoding />  
     <httpTransport />  
   </binding>  
 </customBinding>  
</bindings>  
```  
  
## 结论  
 此示例演示了如何创建自定义协议通道以及如何通过自定义服务行为来启用该通道。  
  
 用户可以使用配置节来指定 `IStorageManager` 实现，从而进一步改进扩展。这会允许在不重新编译服务代码的情况下修改后备存储。  
  
 而且，您可以尝试实现一个用来封装实例状态的类（例如，`StateBag`）。无论何时状态发生变化，该类都负责保持状态。这样，就可以避免使用 `SaveState` 属性，并能够更准确地执行保持工作（例如，可以在状态实际发生变化时保持状态，而不是在每次调用具有 `SaveState` 属性的方法时保存状态）。  
  
 运行示例时，会显示下面的输出。客户端会向其购物车中添加两项，之后将从服务中获取其购物车中各项的列表。在每个控制台窗口中按 Enter 可以关闭服务和客户端。  
  
```  
Enter the name of the product: apples  
Enter the name of the product: bananas  
  
Shopping cart currently contains the following items.  
apples  
bananas  
Press ENTER to shut down client  
```  
  
> [!NOTE]
>  重新生成服务会覆盖数据库文件。如果要使状态在多个示例运行之间得以保持，请确保在不同的运行之间不重新生成示例。  
  
#### 设置、生成和运行示例  
  
1.  请确保已经执行了 [Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2.  若要生成解决方案，请按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明进行操作。  
  
3.  若要用单机配置或跨计算机配置来运行示例，请按照[运行 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/running-the-samples.md)中的说明进行操作。  
  
> [!NOTE]
>  必须运行 SQL Server 2005 或 SQL Express 2005 才能运行此示例。如果您运行的是 SQL Server 2005，则必须修改服务连接字符串的配置。在跨计算机运行时，只需要在服务器计算机上安装 SQL Server。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录。  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录。  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Extensibility\Instancing\Durable`  
  
## 请参阅