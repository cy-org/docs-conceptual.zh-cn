---
title: "自定义生存期 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 52806c07-b91c-48fe-b992-88a41924f51f
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# 自定义生存期
此示例演示如何编写 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 扩展，以便为共享的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务实例提供自定义生存期服务。  
  
> [!NOTE]
>  本主题的最后提供了此示例的设置过程和生成说明。  
  
## 共享实例化  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 为服务实例提供了多种实例化模式。本主题中介绍的共享实例化模式提供了一种用于在多个通道之间共享一个服务实例的方法。客户端可以在本地解析实例的终结点地址，或与该服务中的工厂方法联系，以获取正在运行的实例的终结点地址。在客户端获取终结点地址后，它就可以创建一个新通道并开始通信。以下代码段演示客户端应用程序如何向现有服务实例创建一个新通道。  
  
```  
// Create the first channel.  
IEchoService proxy = channelFactory.CreateChannel();  
  
// Resolve the instance.  
EndpointAddress epa = ((IClientChannel)proxy).ResolveInstance();  
  
// Create new channel factory with the endpoint address resolved by   
// previous statement.  
ChannelFactory<IEchoService> channelFactory2 =  
                new ChannelFactory<IEchoService>("echoservice",  
                epa);  
  
// Create the second channel to the same instance.  
IEchoService proxy2 = channelFactory2.CreateChannel();  
  
```  
  
 与其他实例化模式不同，共享实例化模式拥有一种释放服务实例的独特方式。当一个实例的所有通道都关闭时，服务 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 运行时将启动一个计时器。如果在超时值已到之前没有人进行连接，则 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 将释放该实例并认领这些资源。作为拆卸过程的一部分，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 将在释放该实例之前调用所有 <xref:System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime> 实现的 <xref:System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime.IsIdle%2A> 方法。如果它们全都返回 `true`，则释放该实例。否则，<xref:System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime> 实现负责通过回调方法来通知处于空闲状态的 `Dispatcher`。  
  
 默认情况下，<xref:System.ServiceModel.InstanceContext> 的空闲超时值为一分钟。但是，此示例演示如何使用自定义扩展来对此进行扩展。  
  
## 扩展 InstanceContext  
 在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]中， <xref:System.ServiceModel.InstanceContext>是服务实例和`Dispatcher`之间的链接[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 允许您通过使用可扩展对象模式添加新状态或行为来扩展此运行时组件。该可扩展的对象模式将在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中使用，以便使用新功能来扩展现有运行时类，或者向对象添加新的状态功能。可扩展对象模式中有三个接口：`IExtensibleObject<T>`、`IExtension<T>` 和 `IExtensionCollection<T>`。  
  
 `IExtensibleObject<T>` 接口由对象实现，以允许进行自定义其功能的扩展。  
  
 `IExtension<T>` 接口由可作为类型为 `T` 的类扩展的对象来实现。  
  
 最后，`IExtensionCollection<T>` 接口是允许按类型检索 `IExtensions` 的 `IExtensions` 集合。  
  
 因此，为了扩展 <xref:System.ServiceModel.InstanceContext>，必须实现 `IExtension` 接口。在此示例项目中，`CustomLeaseExtension` 类包含此实现。  
  
```  
class CustomLeaseExtension : IExtension<InstanceContext>  
{  
}  
  
```  
  
 `IExtension` 接口具有 `Attach` 和 `Detach` 两个方法。顾名思义，当运行时将扩展附加到 <xref:System.ServiceModel.InstanceContext> 类的实例以及将扩展从该类的实例分离时，将会调用这两个方法。在此示例中，`Attach` 方法用于跟踪属于当前扩展实例的 <xref:System.ServiceModel.InstanceContext> 对象。  
  
```  
InstanceContext owner;  
  
public void Attach(InstanceContext owner)  
{  
  this.owner = owner;   
}  
```  
  
 此外，还必须将必要的实现添加到该扩展以提供扩展的生存期支持。因此，将使用所需的方法来声明 `ICustomLease` 接口，并在 `CustomLeaseExtension` 类中实现该接口。  
  
```  
interface ICustomLease  
{  
    bool IsIdle { get; }          
    InstanceContextIdleCallback Callback { get; set; }  
}  
  
class CustomLeaseExtension : IExtension<InstanceContext>, ICustomLease  
{  
}  
  
```  
  
 当 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 调用 <xref:System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime> 实现中的 <xref:System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime.IsIdle%2A> 方法时，此调用将路由到 `CustomLeaseExtension` 的 <xref:System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime.IsIdle%2A> 方法。然后，`CustomLeaseExtension` 将检查其私有状态，以查看 <xref:System.ServiceModel.InstanceContext> 是否处于空闲状态。如果它处于空闲状态，则返回 `true`。否则，它将针对指定的扩展生存期启动一个计时器。  
  
```  
public bool IsIdle  
{  
  get  
  {  
    lock (thisLock)  
    {  
      if (isIdle)  
      {  
        return true;  
      }  
      else  
      {  
        StartTimer();  
        return false;  
      }  
    }  
  }  
}  
  
```  
  
 在该计时器的 `Elapsed` 事件中，将调用调度程序中的回调功能以启动另一个清理周期。  
  
```  
void idleTimer_Elapsed(object sender, ElapsedEventArgs args)  
{  
    idleTimer.Stop();  
    isIdle = true;    
    callback(owner);  
}  
  
```  
  
 对于转为空闲状态的实例，当有新消息到达时，将无法续订正在运行的计时器。  
  
 此示例实现 <xref:System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime> 以截获对 <xref:System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime.IsIdle%2A> 方法的调用，并将这些调用路由到 `CustomLeaseExtension`。<xref:System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime> 实现包含在 `CustomLifetimeLease` 类中。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 要释放此服务实例时，将会调用 <xref:System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime.IsIdle%2A> 方法。但是，在 ServiceBehavior 的 <xref:System.ServiceModel.Dispatcher.DispatchRuntime.InstanceContextLifetimes%2A> 集合中，只有特定 `ISharedSessionInstance` 实现的一个实例。这意味着在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 检查 <xref:System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime.IsIdle%2A> 方法时，将无法识别关闭的 <xref:System.ServiceModel.InstanceContext>。因此，此示例使用线程锁定将请求序列化到 <xref:System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime.IsIdle%2A> 方法。  
  
> [!IMPORTANT]
>  由于序列化可能会严重影响应用程序的性能，因此不推荐使用线程锁定方法。  
  
 私有成员变量将在 `CustomLeaseExtension` 类中使用以跟踪 `IsIdle` 值。每次检索 <xref:System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime> 的值时，`IsIdle` 私有成员都会返回并重置为 `false`。必须将此值设置为 `false`，以确保调度程序调用 <xref:System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime.NotifyIdle%2A> 方法。  
  
```  
public bool IsIdle  
{  
    get   
    {  
       lock (thisLock)  
       {  
           bool idleCopy = isIdle;  
           isIdle = false;  
           return idleCopy;  
       }  
    }  
}  
  
```  
  
 如果 `ISharedSessionLifetime.IsIdle` 属性返回 `false`，则调度程序会使用 `NotifyIdle` 方法来注册一个回调函数。此方法将接收对所释放的 <xref:System.ServiceModel.InstanceContext> 的引用。因此，该示例代码可查询 `ICustomLease` 类型扩展，并检查处于扩展状态的 `ICustomLease.IsIdle` 属性。  
  
```  
public void NotifyIdle(InstanceContextIdleCallback callback,   
            InstanceContext instanceContext)  
{  
    lock (thisLock)  
    {  
       ICustomLease customLease =  
           instanceContext.Extensions.Find<ICustomLease>();  
       customLease.Callback = callback;   
       isIdle = customLease.IsIdle;  
       if (isIdle)  
       {  
             callback(instanceContext);  
       }  
    }   
}  
  
```  
  
 在检查 `ICustomLease.IsIdle` 属性之前，需要设置 Callback 属性，否则，`CustomLeaseExtension` 变为空闲状态后就无法通知调度程序。如果 `ICustomLease.IsIdle` 返回 `true`，则 `isIdle` 私有成员仅在 `CustomLifetimeLease` 中设置为 `true`，并调用该回调方法。由于该代码持有一个锁，因此其他线程无法更改此私有成员的值。调度程序下次检查 `ISharedSessionLifetime.IsIdle` 时，它将返回 `true`，并让调度程序释放该实例。  
  
 由于自定义扩展的基础工作已完成，因此必须将其挂钩到服务模型。为了将 `CustomLeaseExtension` 实现挂钩到 <xref:System.ServiceModel.InstanceContext>，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 提供了 <xref:System.ServiceModel.Dispatcher.IInstanceContextInitializer> 接口以执行 <xref:System.ServiceModel.InstanceContext> 的引导。在此示例中，`CustomLeaseInitializer` 类实现此接口，并将 `CustomLeaseExtension` 的一个实例从仅方法初始化添加到 <xref:System.ServiceModel.InstanceContext.Extensions%2A> 集合。此方法在初始化 <xref:System.ServiceModel.InstanceContext> 时由调度程序调用。  
  
```  
public void Initialize(InstanceContext instanceContext, Message message)  
{  
  IExtension<InstanceContext> customLeaseExtension =  
    new CustomLeaseExtension(timeout);  
  instanceContext.Extensions.Add(customLeaseExtension);  
}  
```  
  
 最后，<xref:System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime> 和 <xref:System.ServiceModel.Dispatcher.IInstanceContextInitializer> 实现通过使用 <xref:System.ServiceModel.Description.IServiceBehavior> 实现挂钩到服务模型。此实现将放置在 `CustomLeaseTimeAttribute` 类中，它还派生自 `Attribute` 基类，以将此行为作为特性公开。在 `IServiceBehavior.ApplyBehavior` 方法中，<xref:System.ServiceModel.Dispatcher.IInstanceContextInitializer> 和 <xref:System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime> 实现的实例分别添加到 <xref:System.ServiceModel.Dispatcher> 的 <xref:System.ServiceModel.Dispatcher.DispatchRuntime.InstanceContextLifetimes%2A> 和 <xref:System.ServiceModel.Dispatcher.DispatchRuntime.InstanceContextInitializers%2A> 集合。  
  
```  
public void ApplyBehavior(ServiceDescription description,   
           ServiceHostBase serviceHostBase,   
           Collection<DispatchBehavior> behaviors,  
           Collection<BindingParameterCollection> parameters)  
{  
    CustomLifetimeLease customLease = new CustomLifetimeLease();  
    CustomLeaseInitializer initializer =   
                new CustomLeaseInitializer(timeout);  
  
    foreach (DispatchBehavior dispatchBehavior in behaviors)  
    {  
        dispatchBehavior.InstanceContextLifetimes.Add(customLease);  
        dispatchBehavior.InstanceContextInitializers.Add(initializer);  
    }  
}  
  
```  
  
 可使用 `CustomLeaseTime` 特性对此行为进行批注，以将其添加到示例服务类中。  
  
```  
[ServiceBehavior(InstanceContextMode=InstanceContextMode.Shareable)]  
[CustomLeaseTime(Timeout = 20000)]  
public class EchoService : IEchoService  
{  
  //…  
}  
```  
  
 运行示例时，操作请求和响应将显示在服务和客户端控制台窗口中。在每个控制台窗口中按 Enter 可以关闭服务和客户端。  
  
#### 设置、生成和运行示例  
  
1.  请确保已经执行了 [Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2.  若要生成 C\# 或 Visual Basic .NET 版本的解决方案，请按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明进行操作。  
  
3.  若要用单机配置或跨计算机配置来运行示例，请按照[运行 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/running-the-samples.md)中的说明进行操作。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录。  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Extensibility\Instancing\Lifetime`  
  
## 请参阅