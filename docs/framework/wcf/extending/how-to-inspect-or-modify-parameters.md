---
title: "如何：检查或修改参数 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ab6c0ac7-aac4-45ba-93d6-a0e9afd1756f
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 如何：检查或修改参数
您可以检查或修改在上一次操作的传入或传出消息[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]客户端对象或[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]服务通过实现<xref:System.ServiceModel.Dispatcher.IParameterInspector?displayProperty=fullName>接口并将其插入客户端或服务运行时。 通常，操作行为用于为单个操作添加参数检查器；其他行为可以用于在更大范围内提供对运行库的方便访问。 有关详细信息，请参阅[扩展客户端](../../../../docs/framework/wcf/extending/extending-clients.md)和[扩展调度程序](../../../../docs/framework/wcf/extending/extending-dispatchers.md)。  
  
### <a name="inspecting-or-modifying-parameters"></a>检查或修改参数  
  
1.  实现<xref:System.ServiceModel.Dispatcher.IParameterInspector?displayProperty=fullName>接口。  
  
2.  实现<xref:System.ServiceModel.Description.IOperationBehavior?displayProperty=fullName>， <xref:System.ServiceModel.Description.IEndpointBehavior?displayProperty=fullName>， <xref:System.ServiceModel.Description.IServiceBehavior?displayProperty=fullName>或<xref:System.ServiceModel.Description.IContractBehavior?displayProperty=fullName> （取决于所需的作用域） 要将参数检查器添加到<xref:System.ServiceModel.Dispatcher.ClientOperation.ParameterInspectors%2A?displayProperty=fullName>或<xref:System.ServiceModel.Dispatcher.DispatchOperation.ParameterInspectors%2A?displayProperty=fullName>属性。  
  
3.  调用前，插入行为<xref:System.ServiceModel.ClientBase%601.Open%2A?displayProperty=fullName>或<xref:System.ServiceModel.ICommunicationObject.Open%2A?displayProperty=fullName>方法<xref:System.ServiceModel.ChannelFactory%601?displayProperty=fullName>。 有关详细信息，请参阅[配置和扩展的运行时行为带有](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md)。  
  
## <a name="example"></a>示例  
 下面的代码示例按顺序演示以下各项：  
  
-   参数检查器实现。  
  
-   插入参数检查器使用的行为实现<xref:System.ServiceModel.Description.IOperationBehavior?displayProperty=fullName>， <xref:System.ServiceModel.Description.IEndpointBehavior?displayProperty=fullName>，和一个<xref:System.ServiceModel.Description.IServiceBehavior?displayProperty=fullName>。  
  
-   配置文件，它在客户端应用程序中加载和运行终结点行为，以便在客户端上插入参数检查器。  
  
 [!code-csharp[Interceptors#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/interceptors/cs/interceptors.cs#4)]
 [!code-vb[Interceptors#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/interceptors/vb/interceptors.vb#4)]  
  
 [!code-csharp[Interceptors#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/interceptors/cs/insertingbehaviors.cs#5)]
 [!code-vb[Interceptors#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/interceptors/vb/insertingbehaviors.vb#5)]  
  
 <!-- TODO: review snippet reference [!code[Interceptors#3](../../../../samples/snippets/common/VS_Snippets_CFX/interceptors/common/client.exe.config#3)]  -->
 <!-- TODO: review snippet reference [!code-csharp[Interceptors#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/interceptors/cs/client.exe.config#3)]  -->
 <!-- TODO: review snippet reference [!code-vb[Interceptors#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/interceptors/vb/client.exe.config#3)]  -->  
  
## <a name="see-also"></a>另请参阅  
 [配置和扩展运行时使用行为](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md)