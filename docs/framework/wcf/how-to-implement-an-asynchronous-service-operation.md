---
title: "如何：实现异步服务操作 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4e5d2ea5-d8f8-4712-bd18-ea3c5461702c
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# 如何：实现异步服务操作
在 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 应用程序中，服务操作可以按同步方式或异步方式实现，而无需指示客户端如何调用它。例如，异步服务操作可以同步调用，而同步服务操作可以异步调用。有关如何在客户端应用程序中异步调用操作的示例，请参见[如何：以异步方式调用服务操作](../../../docs/framework/wcf/feature-details/how-to-call-wcf-service-operations-asynchronously.md)。[!INCLUDE[crabout](../../../includes/crabout-md.md)]同步操作和异步操作的更多信息，请参见[设计服务协定](../../../docs/framework/wcf/designing-service-contracts.md)和[同步和异步操作](../../../docs/framework/wcf/synchronous-and-asynchronous-operations.md)。本主题介绍异步服务操作的基本结构，代码并不完整。有关服务与客户端方面的完整示例，请参见[Asynchronous](http://msdn.microsoft.com/zh-cn/833db946-f511-4f64-a26f-2759a11217c7)。  
  
### 按异步方式实现服务操作  
  
1.  在服务协定中，按照 .NET 异步设计准则声明一个异步方法对。`Begin` 方法采用一个参数、一个回调对象和一个状态对象作为参数，并且返回一个 <xref:System.IAsyncResult?displayProperty=fullName> 和一个匹配的 `End` 方法，该方法采用一个 <xref:System.IAsyncResult?displayProperty=fullName> 作为参数并将返回值返回。关于异步调用的详细信息，请参见[异步编程设计模式](http://go.microsoft.com/fwlink/?LinkId=248221)。  
  
2.  使用 <xref:System.ServiceModel.OperationContractAttribute?displayProperty=fullName> 属性 \(attribute\) 标记该异步方法对的 `Begin` 方法，并将 <xref:System.ServiceModel.OperationContractAttribute.AsyncPattern%2A?displayProperty=fullName> 属性 \(property\) 设置为 `true`。例如，下面的代码执行步骤 1 和 2。  
  
     [!code-csharp[C_SyncAsyncClient#6](../../../samples/snippets/csharp/VS_Snippets_CFX/c_syncasyncclient/cs/services.cs#6)]
     [!code-vb[C_SyncAsyncClient#6](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_syncasyncclient/vb/services.vb#6)]  
  
3.  按照异步设计准则在服务类中实现 `Begin/End` 方法对。例如，下面的代码示例演示一个实现，在此实现中，异步服务操作的 `Begin` 和 `End` 部分都向控制台写入一个字符串，并且将 `End` 操作的返回值返回到客户端。有关完整的代码示例，请参见“示例”部分。  
  
     [!code-csharp[C_SyncAsyncClient#3](../../../samples/snippets/csharp/VS_Snippets_CFX/c_syncasyncclient/cs/services.cs#3)]
     [!code-vb[C_SyncAsyncClient#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_syncasyncclient/vb/services.vb#3)]  
  
## 示例  
 下面的代码示例演示以下各项：  
  
1.  与下列各项之间的服务协定接口：  
  
    1.  同步 `SampleMethod` 操作。  
  
    2.  异步 `BeginSampleMethod` 操作。  
  
    3.  异步 `BeginServiceAsyncMethod`\/`EndServiceAsyncMethod` 操作对。  
  
2.  使用 <xref:System.IAsyncResult?displayProperty=fullName> 对象的服务实现。  
  
 [!code-csharp[C_SyncAsyncClient#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_syncasyncclient/cs/services.cs#1)]
 [!code-vb[C_SyncAsyncClient#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_syncasyncclient/vb/services.vb#1)]  
  
## 请参阅  
 [设计服务协定](../../../docs/framework/wcf/designing-service-contracts.md)   
 [同步和异步操作](../../../docs/framework/wcf/synchronous-and-asynchronous-operations.md)