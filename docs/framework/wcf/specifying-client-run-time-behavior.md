---
title: "指定客户端运行时行为 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "系统提供的客户端的行为 [WCF]"
ms.assetid: d16d3405-be70-4edb-8f62-b5f614ddeca5
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 指定客户端运行时行为
与 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 服务相似，可以对 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 客户端进行配置以修改运行时行为，以便适合客户端应用程序的需要。 有三个属性可用于指定客户端运行时行为。 双工客户端回调对象可以使用<xref:System.ServiceModel.CallbackBehaviorAttribute>和<xref:System.ServiceModel.Description.CallbackDebugBehavior>属性来修改其运行时行为。 另一个属性<xref:System.ServiceModel.Description.ClientViaBehavior>，可用来将逻辑目标与直接网络目标分开。 此外，双工客户端回调类型可以使用某些服务端行为。 [!INCLUDE[crdefault](../../../includes/crdefault-md.md)][指定服务运行时行为](../../../docs/framework/wcf/specifying-service-run-time-behavior.md)。  
  
## <a name="using-the-callbackbehaviorattribute"></a>使用 CallbackBehaviorAttribute  
 你可以配置或通过使用扩展的客户端应用程序中回调协定实现的执行行为<xref:System.ServiceModel.CallbackBehaviorAttribute>类。 此属性为回调类和执行类似的功能<xref:System.ServiceModel.ServiceBehaviorAttribute>类处在于实例化行为和事务设置。  
  
 <xref:System.ServiceModel.CallbackBehaviorAttribute>类必须应用于实现回调协定的类。 如果将应用于非双工协定实现， <xref:System.InvalidOperationException>在运行时引发异常。 下面的代码示例演示<xref:System.ServiceModel.CallbackBehaviorAttribute>类使用了回调对象上的<xref:System.Threading.SynchronizationContext>对象，以确定要封送到，该线程<xref:System.ServiceModel.CallbackBehaviorAttribute.ValidateMustUnderstand%2A>属性强制执行消息验证和<xref:System.ServiceModel.CallbackBehaviorAttribute.IncludeExceptionDetailInFaults%2A>属性以返回异常作为<xref:System.ServiceModel.FaultException>对象传递给服务以便进行调试。  
  
 [!code-csharp[CallbackBehaviorAttribute#3](../../../samples/snippets/csharp/VS_Snippets_CFX/callbackbehaviorattribute/cs/client.cs#3)]
 [!code-vb[CallbackBehaviorAttribute#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/callbackbehaviorattribute/vb/client.vb#3)]  
  
## <a name="using-callbackdebugbehavior-to-enable-the-flow-of-managed-exception-information"></a>使用 CallbackDebugBehavior 启用托管异常信息流  
 您可以启用托管的异常信息回流到服务，以便进行调试的设置将客户端回调对象中的流<xref:System.ServiceModel.Description.CallbackDebugBehavior.IncludeExceptionDetailInFaults%2A>属性设置为`true`以编程方式或从应用程序配置文件。  
  
 将托管异常信息返回到服务可能存在安全风险，因为异常详细信息会公开与内部客户端实现有关的信息，而未经授权的服务可能会使用这些信息。 此外，尽管<xref:System.ServiceModel.Description.CallbackDebugBehavior>也可以以编程方式设置属性，可以很容易忘记禁用<xref:System.ServiceModel.Description.CallbackDebugBehavior.IncludeExceptionDetailInFaults%2A>部署时。  
  
 由于涉及到一些安全问题，因此强烈建议您：  
  
-   使用应用程序配置文件设置的值<xref:System.ServiceModel.Description.CallbackDebugBehavior.IncludeExceptionDetailInFaults%2A>属性设置为`true`。  
  
-   仅在受控调试方案中才能这样做。  
  
 下面的代码示例演示一个客户端配置文件，该文件指示 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 从 SOAP 消息中的客户端回调对象返回托管异常信息。  
  
 <!-- TODO: review snippet reference [!code[SCA.CallbackContract#4](../../../samples/snippets/common/VS_Snippets_CFX/sca.callbackcontract/common/client.exe.config#4)]  -->
 <!-- TODO: review snippet reference [!code-csharp[SCA.CallbackContract#4](../../../samples/snippets/csharp/VS_Snippets_CFX/sca.callbackcontract/cs/client.exe.config#4)]  -->
 <!-- TODO: review snippet reference [!code-vb[SCA.CallbackContract#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/sca.callbackcontract/vb/client.exe.config#4)]  -->  
  
## <a name="using-the-clientviabehavior-behavior"></a>使用 ClientViaBehavior 行为  
 您可以使用<xref:System.ServiceModel.Description.ClientViaBehavior>行为，以指定应为其创建传输通道的统一资源标识符。 当直接网络目标不是消息的预期处理者时，可使用此行为。 当调用应用程序不需要知道最终目标时，或者当目标 `Via` 标头不是地址时，使用此行为可启用多跃点对话。  
  
## <a name="see-also"></a>另请参阅  
 [指定服务运行时行为](../../../docs/framework/wcf/specifying-service-run-time-behavior.md)