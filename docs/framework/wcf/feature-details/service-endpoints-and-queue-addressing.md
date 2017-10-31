---
title: "服务终结点和队列寻址 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7d2d59d7-f08b-44ed-bd31-913908b83d97
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 18
---
# 服务终结点和队列寻址
本主题讨论客户端如何对从队列中读取的服务进行寻址以及服务终结点如何映射到队列。作为提示，下图演示传统 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 排队应用程序部署。  
  
 ![排队应用程序关系图](../../../../docs/framework/wcf/feature-details/media/distributed-queue-figure.jpg "Distributed\-Queue\-Figure")  
  
 客户端为了将消息发送到服务，需要确定该消息在目标队列中的地址。服务为了从队列中读取消息，需要在目标队列中设置它的侦听地址。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中的寻址基于统一资源标识符 \(URI\)，而消息队列 \(MSMQ\) 队列名称不是基于 URI。因此，必须了解如何使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 对在 MSMQ 中创建的队列进行寻址。  
  
## MSMQ 寻址  
 MSMQ 使用路径和格式名来标识队列。路径指定一个主机名称和一个 `QueueName`。可以根据需要在主机名称和 `QueueName` 之间添加一个 `Private$`，以指示不是在 Active Directory 目录服务中发布的专用队列。  
  
 路径名映射到“FormatNames”以确定地址的其他方面，包括路由和队列管理器传输协议。队列管理器支持两种传输协议：本机 MSMQ 协议和 SOAP 可靠消息协议 \(SRMP\)。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] MSMQ 路径和格式名的更多信息，请参见 [About Message Queuing](http://go.microsoft.com/fwlink/?LinkId=94837)（关于消息队列）。  
  
## NetMsmqBinding 和服务寻址  
 在将消息发送到服务中的目标地址时，将根据用于通信的传输协议选择 URI 中的方案。[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中的每个传输协议都有唯一的方案。此方案必须反映用于通信的传输协议的性质。例如，net.tcp、net.pipe、HTTP 等等。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中的 MSMQ 排队传输协议公开 net.msmq 方案。使用 net.msmq 方案寻址的任何消息都使用 MSMQ 排队传输协议通道上的 `NetMsmqBinding` 发送。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中的队列寻址基于下面的模式：  
  
 net.msmq: \/\/ \<*host\-name*\> \/ \[private\/\] \<*queue\-name*\>  
  
 其中：  
  
-   \<*host\-name*\> 是承载目标队列的计算机的名称。  
  
-   \[private\] 可选。它在对作为专用队列的目标队列寻址时使用。若要对公共队列寻址，不能指定 private。请注意，与 MSMQ 路径不同，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] URI 形式中不包含“$”。  
  
-   \<*queue\-name*\>是队列的名称。队列名还可以引用子队列。因此，\<*queue\-name*\> \= \<*name\-of\-queue*\>\[;*sub\-queue\-name*\]。  
  
 示例 1：若要对计算机 abc atadatum.com 上承载的专用队列 PurchaseOrders 寻址，URI 将为 net.msmq:\/\/abc.adatum.com\/private\/PurchaseOrders。  
  
 示例 2：若要对计算机 def atadatum.com 上承载的公共队列 AccountsPayable 寻址，URI 将为 net.msmq:\/\/def.adatum.com\/AccountsPayable。  
  
 队列地址用作侦听器从中读取消息的侦听 URI。换言之，队列地址等效于 TCP 套接字的侦听端口。  
  
 从队列中读取消息的终结点必须使用以前在打开 ServiceHost 时指定的同一方案指定队列地址。有关示例，请参见 [网络 MSMQ 绑定](../../../../docs/framework/wcf/samples/net-msmq-binding.md)和[Message Queuing Integration Binding Samples](http://msdn.microsoft.com/zh-cn/997d11cb-f2c5-4ba0-9209-92843d4d0e1a)。  
  
### 队列中存在多个协定  
 队列中的消息可以实现不同的协定。在这种情况下，下列条件中必须有一个成立才能成功读取并处理所有消息：  
  
-   为服务指定一个实现所有协定的终结点。此为推荐方法。  
  
-   指定多个具有不同协定的终结点，但要确保所有终结点都使用相同的 `NetMsmqBinding` 对象。ServiceModel 中的调度逻辑使用一个消息泵，它从传输通道中读取消息以进行调度，并最终根据相应的协定将消息多路分解到不同的终结点。消息泵是为侦听 URI\/绑定对创建的。队列地址被排队侦听器用作侦听 URI。通过让所有终结点使用相同的绑定对象，可以确保使用单个消息泵来读取消息，并且根据协定将消息多路分解到相关终结点。  
  
### SRMP 消息传递  
 如前所述，可以使用 SRMP 协议进行队列到队列的传输。当 HTTP 传输协议在传输队列和目标队列之间传输消息时，经常使用这一协议。  
  
 若要使用 SRMP 传输协议，请使用 net.msmq URI 方案对消息进行寻址（如前所述），并在 `NetMsmqBinding` 的 `QueueTransferProtocol` 属性中指定选择 SRMP 还是 Secured SRMP。  
  
 指定 `QueueTransferProtocol` 属性只具有发送的功能。这是客户端发出的有关要使用哪种队列传输协议的指示。  
  
### 使用 Active Directory  
 MSMQ 带有 Active Directory 集成支持。安装带有 Active Directory 集成的 MSMQ 时，计算机必须属于 Windows 域。Active Directory 用于发布可供发现的队列，此类队列称为“公共队列”。对队列进行寻址时，可以使用 Active Directory 对队列进行解析。这与使用域名系统 \(DNS\) 解析网络名称的 IP 地址的方式相似。`NetMsmqBinding` 中的 `UseActiveDirectory` 属性是一个布尔值，该值指示排队通道是否必须使用 Active Directory 来解析队列 URI。默认情况下，此属性设置为 `false`。如果 `UseActiveDirectory` 属性设置为 `true`，则排队通道使用 Active Directory 将 net.msmq:\/\/ URI 转换为格式名。  
  
 `UseActiveDirectory` 属性仅对发送消息的客户端有意义，因为它用于在发送消息时解析队列的地址。  
  
### 将 net.msmq URI 映射到消息队列格式名  
 排队通道负责将提供给通道的 net.msmq URI 名称映射到 MSMQ 格式名。下表总结了用于在它们之间进行映射的规则。  
  
|基于 WCF URI 的队列地址|使用 Active Directory 属性|队列传输协议属性|得到的 MSMQ 格式名|  
|----------------------|----------------------------|--------------|------------------|  
|Net.msmq:\/\/\<计算机名\>\/private\/abc|False（默认值）|Native（默认值）|DIRECT\=OS:计算机名\\private$\\abc|  
|Net.msmq:\/\/\<计算机名\>\/private\/abc|False|SRMP|DIRECT\=http:\/\/machine\/msmq\/private$\/abc|  
|Net.msmq:\/\/\<计算机名\>\/private\/abc|True|Native|PUBLIC\=some\-guid（队列的 GUID）|  
  
### 从死信队列或病毒消息队列读取消息  
 若要从作为目标队列子队列的病毒消息队列中读取消息，请打开具有子队列地址的 `ServiceHost`。  
  
 示例：从本地计算机的 PurchaseOrders 专用队列的病毒消息队列中读取消息的服务将按 net.msmq:\/\/localhost\/private\/PurchaseOrders;poison 寻址。  
  
 若要从系统的事务性死信队列中读取消息，URI 必须采用以下形式：net.msmq:\/\/localhost\/system$;DeadXact。  
  
 若要从系统的非事务性死信队列中读取消息，URI 必须采用以下形式：net.msmq:\/\/localhost\/system$;DeadLetter。  
  
 在使用自定义死信队列时，请注意，死信队列必须驻留在本地计算机上。因此，死信队列的 URI 被限制为以下形式：  
  
 net.msmq: \/\/localhost\/ \[private\/\]  \<*custom\-dead\-letter\-queue\-name*\>.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务验证它接收到的消息的目标队列是否都是它正在侦听的特定队列。如果消息的目标队列与它所在的队列不匹配，服务不会处理该消息。这存在一个问题：侦听死信队列的服务必须寻址，因为死信队列中的任何消息都需要传递到别处。若要从死信队列或病毒队列中读取消息，必须使用带有 <xref:System.ServiceModel.AddressFilterMode> 参数的 `ServiceBehavior`。有关示例，请参见[死信队列](../../../../docs/framework/wcf/samples/dead-letter-queues.md)。  
  
## MsmqIntegrationBinding 和服务寻址  
 `MsmqIntegrationBinding` 用于与传统 MSMQ 应用程序进行通信。为了便于与现有 MSMQ 应用程序进行互操作，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 仅支持格式名寻址。因此，使用此绑定发送的消息必须符合 URI 方案。  
  
 msmq.formatname:\<*MSMQ\-format\-name*\>\>  
  
 MSMQ 格式名采用 MSMQ 在 [About Message Queuing](http://go.microsoft.com/fwlink/?LinkId=94837)（关于消息队列）中指定的形式。  
  
 请注意，当使用 `MsmqIntegrationBinding` 从队列接收消息时，只能使用直接格式名以及公共和专用格式名（需要 Active Directory 集成）。但是，建议您使用直接格式名。例如，在 [!INCLUDE[wv](../../../../includes/wv-md.md)] 上，使用任何其他格式名都将导致错误，因为系统会尝试打开一个子队列，而该子队列只能使用直接格式名打开。  
  
 在使用 `MsmqIntegrationBinding` 对 SRMP 进行寻址时，不需要在直接格式名中添加 \/msmq\/ 来帮助 Internet 信息服务 \(IIS\) 进行调度。例如：在使用 SRMP 协议对队列 abc 进行寻址时，应使用 DIRECT\=http:\/\/adatum.com\/private$\/abc 而不是 DIRECT\=http:\/\/adatum.com\/msmq\/private$\/abc。  
  
 请注意，对于 `MsmqIntegrationBinding`，不能使用 net.msmq:\/\/ 寻址。因为 `MsmqIntegrationBinding` 支持任意形式的 MSMQ 格式名寻址，所以您可以使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务，该服务使用此绑定来使用 MSMQ 中的多路广播和通讯组列表功能。一个例外是在使用 `MsmqIntegrationBinding` 时指定 `CustomDeadLetterQueue`。它必须采用 net.msmq:\/\/ 形式，这与使用 `NetMsmqBinding` 进行指定的方式相似。  
  
## 请参阅  
 [承载排队应用程序的 Web](../../../../docs/framework/wcf/feature-details/web-hosting-a-queued-application.md)