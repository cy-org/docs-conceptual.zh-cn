---
title: "启用事务流 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "事务 [WCF], 启用流"
ms.assetid: a03f5041-5049-43f4-897c-e0292d4718f7
caps.latest.revision: 17
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 17
---
# 启用事务流
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 提供用于控制事务流的灵活性较高的选项。服务事务流设置可以使用属性与配置的组合来表示。  
  
## 事务流设置  
 服务终结点的事务流设置根据下列三个值的交集生成：  
  
-   为服务协定中的每个方法指定的 <xref:System.ServiceModel.TransactionFlowAttribute> 属性。  
  
-   特定绑定中的 `TransactionFlow` 绑定属性。  
  
-   特定绑定中的 `TransactionFlowProtocol` 绑定属性。`TransactionFlowProtocol` 绑定属性允许您在可用于流动事务的两个不同事务协议之间进行选择。后面几节将对这些协议逐一进行简要描述。  
  
### WS\-AtomicTransaction 协议  
 WS\-AtomicTransaction \(WS\-AT\) 协议对于要求第三方协议堆栈具有互操作性时的情形非常有用。  
  
### OleTransactions 协议  
 OleTransactions 协议对于如下的情形非常有用：即不要求第三方协议堆栈具有互操作性，并且服务部署人员预先知道 WS\-AT 协议服务将在本地禁用或者现有网络拓扑不支持使用 WS\-AT。  
  
 下表列出了可以使用这些不同组合生成的不同类型的事务流。  
  
|TransactionFlow<br /><br /> 绑定|TransactionFlow 绑定属性|TransactionFlowProtocol 绑定协议|事务流的类型|  
|----------------------------|--------------------------|----------------------------------|------------|  
|Mandatory|true|WS\-AT|事务必须以可以互操作的 WS\-AT 格式流动。|  
|Mandatory|true|OleTransactions|事务必须以 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] OleTransactions 格式流动。|  
|Mandatory|false|不适用|不适用，因为这是无效的配置。|  
|Allowed|true|WS\-AT|事务可以以可互操作的 WS\-AT 格式流动。|  
|Allowed|true|OleTransactions|事务可以以 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] OleTransactions 格式流动。|  
|Allowed|false|任意值|不流动事务。|  
|NotAllowed|任意值|任意值|不流动事务。|  
  
 下表对消息处理结果做了总结。  
  
|传入消息|TransactionFlow 设置|事务标头|消息处理结果|  
|----------|------------------------|----------|------------|  
|事务与预期的协议格式匹配|Allowed 或 Mandatory|`MustUnderstand` 等于 `true`。|处理|  
|事务不与预期的协议格式匹配|Mandatory|`MustUnderstand` 等于 `false`。|因要求一个事务而拒绝|  
|事务不与预期的协议格式匹配|Allowed|`MustUnderstand` 等于 `false`。|因无法理解标头而拒绝|  
|使用任何协议格式的事务|NotAllowed|`MustUnderstand` 等于 `false`。|因无法理解标头而拒绝|  
|无事务|Mandatory|N\/A|因要求一个事务而拒绝|  
|无事务|Allowed|不可用|处理|  
|无事务|NotAllowed|不可用|进程|  
  
 虽然协定上的每个方法都有不同的事务流要求，但事务流协议设置的范围处于绑定级别。这意味着，共享同一个终结点（并因此共享同一绑定）的所有方法也共享允许或要求事务流的同一个策略以及同一个事务协议（如果适用）。  
  
## 在方法级别启用事务流  
 对于服务协定中的所有方法，事务流要求并不总是相同。因此，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 还提供基于属性的机制以允许表示每个方法的事务流首选项。这通过指定服务操作接受事务标头所处的级别的 <xref:System.ServiceModel.TransactionFlowAttribute> 来实现。如果需要启用事务流，则应使用此属性标记服务协定方法。此属性采用 <xref:System.ServiceModel.TransactionFlowOption> 枚举值之一，其中默认值为 <xref:System.ServiceModel.TransactionFlowOption>。如果指定除 <xref:System.ServiceModel.TransactionFlowOption> 以外的任何值，则要求该方法不要成为单向方法。开发人员可以使用此属性在设计时指定方法级别的事务流要求或约束。  
  
## 在终结点级别启用事务流  
 除了 <xref:System.ServiceModel.TransactionFlowAttribute> 属性提供的方法级别的事务流设置以外，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 也为事务流提供终结点范围的设置，以允许管理员可以在较高级别控制事务流。  
  
 这可以通过 <xref:System.ServiceModel.Channels.TransactionFlowBindingElement> 来实现，该类允许您在终结点绑定设置中启用或禁用传入事务流，并允许指定传入事务所需的事务协议格式。  
  
 如果该绑定已禁用事务流，但对服务协定的操作之一要求一个传入事务，则将在服务启动时引发验证异常。  
  
 大多数持续绑定 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 都提供某些 `transactionFlow` 和 `transactionProtocol` 特性，以允许您将特定的绑定配置为接受传入事务。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]设置配置元素的更多信息，请参见 [\<绑定\>](../../../../docs/framework/misc/binding.md) 。  
  
 管理员或部署人员可以使用终结点级别的事务流在部署时使用配置文件来配置事务流要求或约束。  
  
## 安全性  
 若要确保系统的安全性和完整性，您必须在应用程序之间流动事务时保护消息交换。您不应向无资格参与某一事务的任何应用程序流动或透露该事务的详细信息。  
  
 在使用元数据交换向未知或不受信任的 Web 服务生成 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端时，对这些 Web 服务上的操作的调用应取消当前的事务（如可能）。下面的示例演示如何执行此操作。  
  
```  
//client code which has an ambient transaction  
using (TransactionScope scope = new TransactionScope(TransactionScopeOption.Suppress))  
{  
    // No transaction will flow to this operation  
    untrustedProxy.Operation1(...);  
    scope.Complete();  
}  
//remainder of client code  
```  
  
 此外，还应将这些服务配置为仅接受来自它们已对其进行身份验证和授权的客户端的传入事务。如果传入事务来自高度受信任的客户端，则应仅接受传入事务。  
  
## 策略断言  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 使用策略断言来控制事务流。可以在服务的策略文档中找到策略断言，该断言是通过聚合协定、配置和属性而生成的。客户端可以使用 HTTP GET 或 WS\-MetadataExchange 请求\-回复来获取服务的策略文档。然后，客户端可以通过处理策略文档来确定服务协定上的哪些操作可以支持或要求事务流。  
  
 事务流策略断言通过指定客户端应发送给服务以表示事务的 SOAP 标头来影响事务流。所有事务标头都必须标记为 `MustUnderstand` 等于 `true`。以其他方式标记标头的任何消息都将被拒绝，并出现 SOAP 错误。  
  
 一个操作上只能出现一个与事务相关的策略断言。在一个操作上具有多个事务断言的策略文档将被视为无效，并且将被 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 拒绝。此外，每个端口类型内仅可出现一个事务协议。操作在一个端口类型内引用多个事务协议的策略文档将被视为无效，并将被 [ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)拒绝。事务断言出现在输出消息或单向输入消息上的策略文档也将被视为无效。