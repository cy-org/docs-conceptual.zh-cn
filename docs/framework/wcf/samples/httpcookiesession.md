---
title: "HttpCookieSession | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 101cb624-8303-448a-a3af-933247c1e109
caps.latest.revision: 31
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 31
---
# HttpCookieSession
此示例演示如何生成自定义协议通道，以便使用 HTTP Cookie 进行会话管理。通过此通道可以在 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务和 ASMX 客户端或者 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端和 ASMX 服务之间进行通信。  
  
 当客户端在基于会话的 ASMX Web 服务中调用 Web 方法时，[!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 引擎将执行以下操作：  
  
-   生成一个唯一的 ID（会话 ID）。  
  
-   生成会话对象并将其与该唯一 ID 相关联。  
  
-   将该唯一 ID 添加到 Set\-Cookie HTTP 响应头中并发送给客户端。  
  
-   根据它发送给客户端的会话 ID 在后续调用中标识客户端。  
  
 客户端将此会话 ID 包含在发送给服务器的后续请求中。服务器使用来自客户端的会话 ID 为当前 HTTP 上下文加载相应的会话对象。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Extensibility\Channels\HttpCookieSession`  
  
## HttpCookieSession 通道消息交换模式  
 此示例为类似 ASMX 的方案启用会话。在通道堆栈的底部，我们使用了支持 <xref:System.ServiceModel.Channels.IRequestChannel> 和 <xref:System.ServiceModel.Channels.IReplyChannel> 的 HTTP 传输。通道的任务是向通道堆栈中的更高层提供会话。此示例实现了两个支持会话的通道（<xref:System.ServiceModel.Channels.IRequestSessionChannel> 和 <xref:System.ServiceModel.Channels.IReplySessionChannel>）。  
  
## 服务通道  
 此示例在 `HttpCookieReplySessionChannelListener` 类中提供服务通道。此类实现 <xref:System.ServiceModel.Channels.IChannelListener> 接口，并将通道堆栈中位于较低层的 <xref:System.ServiceModel.Channels.IReplyChannel> 通道转换为 <xref:System.ServiceModel.Channels.IReplySessionChannel>。此过程可以分为以下几部分：  
  
-   当通道侦听器打开时，它接受来自其内部侦听器的内部通道。因为内部侦听器是一个数据报侦听器，而被接受的通道的生存期与该侦听器的生存期相分离，所以我们可以关闭内部侦听器，只保留内部通道。  
  
    ```  
                this.innerChannelListener.Open(timeoutHelper.RemainingTime());  
    this.innerChannel = this.innerChannelListener.AcceptChannel(timeoutHelper.RemainingTime());  
    this.innerChannel.Open(timeoutHelper.RemainingTime());  
    this.innerChannelListener.Close(timeoutHelper.RemainingTime());  
    ```  
  
-   当打开进程完成后，我们设置一个消息循环，以接收来自内部通道的消息。  
  
    ```  
    IAsyncResult result = BeginInnerReceiveRequest();  
    if (result != null && result.CompletedSynchronously)  
    {  
       // do not block the user thread  
       if (this.completeReceiveCallback == null)  
       {  
          this.completeReceiveCallback = new WaitCallback(CompleteReceiveCallback);  
       }  
       ThreadPool.QueueUserWorkItem(this.completeReceiveCallback, result);  
    }  
    ```  
  
-   当消息到达后，服务通道检查会话标识符并多路分解到相应的会话通道。通道侦听器维护一个字典，该字典将会话标识符映射到会话通道实例。  
  
    ```  
    Dictionary<string, IReplySessionChannel> channelMapping;  
    ```  
  
 `HttpCookieReplySessionChannel` 类实现 <xref:System.ServiceModel.Channels.IReplySessionChannel>。通道堆栈的较高层调用 <xref:System.ServiceModel.Channels.IReplyChannel.ReceiveRequest%2A> 方法来读取此会话的请求。每个会话通道具有一个专用的消息队列，该消息队列由服务通道进行填充。  
  
```  
InputQueue<RequestContext> requestQueue;  
```  
  
 当有人调用 <xref:System.ServiceModel.Channels.IReplyChannel.ReceiveRequest%2A> 方法，而消息队列中没有消息时，通道将等待指定的时间量，然后自行关闭。这样将清除为非 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端创建的会话通道。  
  
 我们使用 `channelMapping` 跟踪 `ReplySessionChannels`，并且在所有已接受的通道全部关闭之前不会关闭基础 `innerChannel`。这样使 `HttpCookieReplySessionChannel` 的生存期可以超过 `HttpCookieReplySessionChannelListener`。我们也无需担心侦听器会在我们下面收集垃圾，因为已接受的通道通过 `OnClosed` 回调保留对其侦听器的引用。  
  
## 客户端通道  
 对应的客户端通道位于 `HttpCookieSessionChannelFactory` 类中。在创建通道的过程中，通道工厂使用 `HttpCookieRequestSessionChannel` 包装内部请求通道。`HttpCookieRequestSessionChannel` 类将调用转发给基础请求通道。当客户端关闭代理时，`HttpCookieRequestSessionChannel` 向服务发送一条指明该通道正在关闭的消息。因此，服务通道堆栈可以正常关闭正在使用的会话通道。  
  
## 绑定和绑定元素  
 创建服务通道和客户端通道后，下一步是将它们与 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 运行库集成。通道通过绑定和绑定元素公开给 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]。由一个或多个绑定元素组成的绑定 。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 提供了多个系统定义的绑定；例如，BasicHttpBinding 或 WSHttpBinding。`HttpCookieSessionBindingElement` 类包含绑定元素的实现。它重写通道侦听器和通道工厂创建方法，以进行必要的通道侦听器或通道工厂实例化。  
  
 此示例使用策略断言作为服务说明。这使得此示例能够将其通道要求发布给其他可以使用服务的客户端。例如，此绑定元素发布策略断言，以使潜在的客户端知道它支持会话。因为此示例在绑定元素配置中启用了 `ExchangeTerminateMessage` 属性，它增加了必要断言，以表明服务支持通过额外的消息交换操作终止会话对话。客户端然后可以使用此操作。下面的 WSDL 代码演示了从 `HttpCookieSessionBindingElement` 中创建的策略断言。  
  
```  
<wsp:Policy wsu:Id="HttpCookieSessionBinding_IWcfCookieSessionService_policy" xmlns:wsp="http://schemas.xmlsoap.org/ws/2004/09/policy" xmlns:wsu="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">  
<wsp:ExactlyOne>  
<wsp:All>  
<wspe:Utf816FFFECharacterEncoding xmlns:wspe="http://schemas.xmlsoap.org/ws/2004/09/policy/encoding"/>  
<mhsc:httpSessionCookie xmlns:mhsc="http://samples.microsoft.com/wcf/mhsc/policy"/>  
</wsp:All>  
</wsp:ExactlyOne>  
</wsp:Policy>  
```  
  
 `HttpCookieSessionBinding` 类是一个系统提供的绑定，它使用上面介绍的绑定元素。  
  
## 向配置系统中添加通道  
 此示例提供了两个类，它们通过配置公开示例通道。第一个类是适用于 `HttpCookieSessionBindingElement` 的 <xref:System.ServiceModel.Configuration.BindingElementExtensionElement>。批量实现委派给从 <xref:System.ServiceModel.Configuration.StandardBindingElement> 派生的 `HttpCookieSessionBindingConfigurationElement`。`HttpCookieSessionBindingConfigurationElement` 的属性与 `HttpCookieSessionBindingElement` 上的属性相对应。  
  
### 绑定元素扩展节  
 `HttpCookieSessionBindingElementSection` 节是一个 <xref:System.ServiceModel.Configuration.BindingElementExtensionElement>，它向配置系统公开 `HttpCookieSessionBindingElement`。通过对配置节名称进行一些重写，可以定义绑定元素的类型以及如何创建绑定元素。然后，我们可以按如下方式注册配置文件中的扩展节：  
  
```  
<configuration>        
    <system.serviceModel>        
      <extensions>          
        <bindingElementExtensions>            
          <add name="httpCookieSession"   
               type=  
"Microsoft.ServiceModel.Samples.HttpCookieSessionBindingElementElement,   
                    HttpCookieSessionExtension, Version=1.0.0.0,   
                    Culture=neutral, PublicKeyToken=null"/>  
        </bindingElementExtensions >  
      </extensions>  
  
      <bindings>  
      <customBinding>  
        <binding name="allowCookiesBinding">  
          <textMessageEncoding messageVersion="Soap11WSAddressing10" />  
          <httpCookieSession sessionTimeout="10" exchangeTerminateMessage="true" />  
          <httpTransport allowCookies="true" />  
        </binding>  
      </customBinding>  
      </bindings>        
    </system.serviceModel>    
</configuration>  
```  
  
## 测试代码  
 使用此示例传输的测试代码位于 Client 和 Service 目录中。它包含两个测试 \- 一个测试在客户端使用 `allowCookies` 设置为 `true` 的绑定。第二个测试在该绑定上实现显式关闭（使用终止消息交换）。  
  
 运行该示例时，应看到以下输出：  
  
```  
Simple binding:  
AddItem(10000,2): ItemCount=2  
AddItem(10550,5): ItemCount=7  
RemoveItem(10550,2): ItemCount=5  
Items  
10000, 2  
10550, 3  
Smart binding:  
AddItem(10000,2): ItemCount=2  
AddItem(10550,5): ItemCount=7  
RemoveItem(10550,2): ItemCount=5  
Items  
10000, 2  
10550, 3  
  
Press <ENTER> to terminate client.  
```  
  
#### 设置、生成和运行示例  
  
1.  使用以下命令安装 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 4.0。  
  
    ```  
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable  
  
    ```  
  
2.  请确保已执行 [Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
3.  若要生成解决方案，请按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明进行操作。  
  
4.  若要用单机配置或跨计算机配置来运行示例，请按照[运行 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/running-the-samples.md)中的说明进行操作。  
  
## 请参阅