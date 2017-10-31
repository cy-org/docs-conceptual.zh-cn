---
title: "How to: Register Callbacks for Cancellation Requests | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "cancellation, how to register callbacks"
ms.assetid: 8838dd75-18ed-4b8b-b322-cd4531faac64
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# How to: Register Callbacks for Cancellation Requests
下面的示例演示如何注册委托，该委托将在 <xref:System.Threading.CancellationToken.IsCancellationRequested%2A> 属性因调用创建标记的对象上的 <xref:System.Threading.CancellationTokenSource.Cancel%2A> 而变为 True 时进行调用。  使用此技术可取消本地不支持统一取消框架的异步操作，也可取消阻止可能等待异步操作结束的方法。  
  
> [!NOTE]
>  某些情况下，当启用“仅我的代码”后，Visual Studio 会在引发异常的行中断运行并显示一条错误消息，该消息显示“用户代码未处理异常”。 此错误是良性的。  可以按 F5 继续运行，并请参阅下面示例中所示的异常处理行为。  若要阻止 Visual Studio 在出现第一个错误时中断运行，只需在“工具”、“选项”、“调试”、“常规”下取消选中“仅我的代码”复选框即可。  
  
## 示例  
 在下面的示例中，<xref:System.Net.WebClient.CancelAsync%2A> 方法注册为在通过取消标记请求取消时要调用的方法。  
  
 [!code-csharp[Conceptual.Cancellation.Callback#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.cancellation.callback/cs/howtoexample1.cs#1)]
 [!code-vb[Conceptual.Cancellation.Callback#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.cancellation.callback/vb/howtoexample1.vb#1)]  
  
 如果注册回调时已经请求了取消，那么仍然要保证调用回调。  在此特定情况下，如果当前未执行异步操作，则 <xref:System.Net.WebClient.CancelAsync%2A> 方法将不进行任何操作，因此调用此方法始终是安全的。  
  
## 请参阅  
 [Cancellation in Managed Threads](../../../docs/standard/threading/cancellation-in-managed-threads.md)