---
title: "使用 NetHttpBinding | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fe134acf-ceca-49de-84a9-05a37e3841f1
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# 使用 NetHttpBinding
<xref:System.ServiceModel.NetHttpBinding> 是为使用 HTTP 或 WebSocket 服务设计的绑定，默认情况下使用二进制编码。  <xref:System.ServiceModel.NetHttpBinding> 将检测它是否与请求\-答复协定或双工协定结合使用，并更改其行为以进行匹配 ― 它将针对请求\-答复协定使用 HTTP，并针对双工协定使用 WebSocket。  可使用 <xref:System.ServiceModel.NetHttpBinding.WebSocketTransportUsage%2A> 设置来重写此行为：  
  
1.  始终 \- 甚至对于请求\-答复协定，也会强制使用 WebSocket。  
  
2.  从不 \- 阻止使用 WebSocket。  尝试使用具有此设置的双工协定将导致异常。  
  
3.  双工时 \- 这是默认值，其行为如前所述。  
  
 <xref:System.ServiceModel.NetHttpBinding> 支持 HTTP 模式和 WebSocket 模式下的可靠会话。  在 WebSocket 模式下，会话由传输来提供。  
  
> [!WARNING]
>  在使用 <xref:System.ServiceModel.NetHttpBinding> 且该绑定的 TransferMode 设置为 TransferMode.Streamed 时，较大的流可能会造成死锁，调用将会超时。  若要解决此问题，请发送较小的流，或使用 TransferMode.Buffered。  
  
## 将服务配置为使用 NetHttpBinding  
 The <xref:System.ServiceModel.NetHttpBinding> 的配置方式与任何其他绑定的配置方式相同。  以下配置代码段说明了如何通过 <xref:System.ServiceModel.NetHttpBinding> 配置 WCF 服务。  
  
```xml  
<system.serviceModel>  
    <services>  
      <service name="WcfService1.Service1">  
        <endpoint address=""  
                  binding="netHttpBinding"  
                  contract="WcfService1.IService1"/>  
        <endpoint address="mex"  
                  binding="mexHttpBinding"  
                  contract="IMetadataExchange"/>  
      </service>  
    </services>  
    <bindings>  
      <netHttpBinding>  
        <binding name="My_NetHttpBindingConfig">  
          <webSocketSettings transportUsage="WhenDuplex"/>  
        </binding>  
      </netHttpBinding>  
    </bindings>  
    <!- ... -->   
  </system.serviceModel>  
```  
  
 下面的代码段演示如何用代码添加 <xref:System.ServiceModel.NetHtttpBinding>。  
  
```csharp  
ServiceHost svchost = new ServiceHost(typeof(Service1), baseAddress);  
            NetHttpBinding binding = new NetHttpBinding();  
            svchost.AddServiceEndpoint(typeof(IService1), binding, address);   
        }  
```  
  
## 请参阅  
 [为服务配置绑定](../../../../docs/framework/wcf/configuring-bindings-for-wcf-services.md)   
 [绑定](../../../../docs/framework/wcf/feature-details/bindings.md)   
 [系统提供的绑定](../../../../docs/framework/wcf/system-provided-bindings.md)   
 [双工服务](../../../../docs/framework/wcf/feature-details/duplex-services.md)