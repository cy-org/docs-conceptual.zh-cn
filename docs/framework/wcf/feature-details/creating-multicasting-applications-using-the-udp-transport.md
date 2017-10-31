---
title: "创建使用 UDP 传输的多播应用程序 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7485154a-6e85-4a67-a9d4-9008e741d4df
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# 创建使用 UDP 传输的多播应用程序
多播应用程序在同一时间向大量的收件人发送小消息，而无需建立点到点的连接。此类应用程序的重点在速度而非可靠性。换句话说，它更重要的是要发送及时的数据，以确保实际收到任何特定的消息。现在，WCF 支持使用 <xref:System.ServiceModel.UdpBinding> 编写多播应用程序。此传输在服务需要将小消息同时发送到大量客户端的方案中非常有用。股票行情自动收录器应用程序是这类服务的一个示例。  
  
## 实现多播应用程序  
 要实现多播应用程序，定义服务协定并对需要响应多播消息的每个软件组件实现服务协定。例如，股票行情自动收录器应用程序可以定义服务协定：  
  
```  
// Shared contracts between the client and the service  
    [ServiceContract]  
    interface IStockTicker  
    {  
        [OperationContract(IsOneWay = true)]  
        void SendStockInfo(StockInfo[] stockInfo);  
    }  
  
    [DataContract]  
    class StockInfo  
    {  
        [DataMember]  
        public string Symbol;  
  
        [DataMember]  
        public float Price;  
  
        public StockInfo(string symbol, float price)  
        {  
            this.Symbol = symbol;  
            this.Price = price;  
        }  
    }  
  
```  
  
 每个想要接收多播消息的应用程序必须承载公开此接口的服务。例如，下面的代码示例演示如何接收多播消息：  
  
```  
// Service Address  
            string serviceAddress = "soap.udp://224.0.0.1:40000";  
            // Binding  
            UdpBinding myBinding = new UdpBinding();  
            // Host  
            ServiceHost host = new ServiceHost(typeof  
                (StockTickerService), new Uri(serviceAddress));  
            // Add service endpoint  
            host.AddServiceEndpoint(typeof(IStockTicker), myBinding, string.Empty);  
            // Openup the service host  
            host.Open();  
  
            Console.WriteLine("Start receiving stock information");  
            Console.ReadLine();  
  
```  
  
 应用程序指定所有服务都侦听的 UDP 地址。创建一个新的<xref:System.ServiceModel.ServiceHost>，使用 <xref:System.ServiceModel.UdpBinding> 公开服务终结点.然后打开 <xref:System.ServiceModel.ServiceHost>，并开始侦听传入的消息。  
  
 在这种类型的方案中，实际是由客户端发送多播消息。正在正确的 UDP 地址侦听的每个服务都将接收多播消息。下面是发送多播消息的客户端的一个示例：  
  
```  
// Multicast Address  
            string serviceAddress = "soap.udp://224.0.0.1:40000";  
  
            // Binding  
            UdpBinding myBinding = new UdpBinding();  
  
            // Channel factory  
            ChannelFactory<IStockTicker> factory  
                = new ChannelFactory<IStockTicker>(myBinding,  
                            new EndpointAddress(serviceAddress));  
  
            // Call service  
            IStockTicker proxy = factory.CreateChannel();  
  
            while (true)  
            {  
                // This will continue to mulicast stock information   
                proxy.SendStockInfo(GetStockInfo());  
                Console.WriteLine(String.Format("sent stock info at {0}", DateTime.Now));  
                // Wait for one second before sending another update  
                System.Threading.Thread.Sleep(new TimeSpan(0, 0, 1));  
            }  
  
```  
  
 此代码将生成股票信息，然后使用服务协定 IStockTicker 发送多播，以调用正确的 UDP 地址上的服务侦听。  
  
### UDP 可靠消息传送  
 UDP 绑定不支持可靠消息，原因是 UDP 协议的轻型性质。如果您需要确认远程终结点已接收消息，请使用支持可靠消息传送的传输，如 HTTP 或 TCP。有关可靠消息传送的更多信息，请参见 http:\/\/go.microsoft.com\/fwlink\/?LinkId\=231830  
  
### 双向多播消息传送  
 多播的消息通常是单向的，UdpBinding 不支持请求\/答复消息交换。使用 UDP 传输发送的消息包含发件人地址和收件人地址。使用发件人地址是必须消息，因为它可能在路由过程中被恶意更改。可以使用下面的代码来检查地址：  
  
```  
if (address.AddressFamily == AddressFamily.InterNetwork)  
          {  
              // IPv4  
              byte[] addressBytes = address.GetAddressBytes();  
              return ((addressBytes[0] & 0xE0) == 0xE0);  
          }  
          else  
          {  
              // IPv6   
              return address.IsIPv6Multicast;  
          }  
  
```  
  
 此代码检查发件人地址的第一个字节，以查看它是否包含 0xE0，这标志着该地址是一个多播的地址。  
  
### 安全注意事项  
 侦听多播消息时，ICMP 数据包发送到路由器，通知它您在多播地址上侦听。本地子网上具有权限的任何人都可以侦听这些类型的数据包，并确定正在侦听的多播的地址和端口。  
  
 请勿出去任何安全目的使用发件人的 IP 地址。此信息可以伪造，并可以导致应用程序发送响应到错误的计算机。减轻这种威胁的一种方法是启用消息级别的安全性。 在网络级，还可使用 IPSec（Internet 协议安全性） 和\/或 NAP（网络访问保护）。