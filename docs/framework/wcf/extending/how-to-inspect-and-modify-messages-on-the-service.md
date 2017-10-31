---
title: "如何：检查和修改服务上的消息 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9c5b1cc7-84f3-45f8-9226-d59c278e8c42
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 如何：检查和修改服务上的消息
您可以检查或修改传入或传出消息[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]客户端通过实现<xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector?displayProperty=fullName>并将其插入服务运行时。 有关详细信息，请参阅[扩展调度程序](../../../../docs/framework/wcf/extending/extending-dispatchers.md)。 在服务上的等效功能为<xref:System.ServiceModel.Dispatcher.IClientMessageInspector?displayProperty=fullName>。  
  
### <a name="to-inspect-or-modify-messages"></a>检查或修改消息  
  
1.  实现<xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector?displayProperty=fullName>接口。  
  
2.  实现<xref:System.ServiceModel.Description.IServiceBehavior?displayProperty=fullName>， <xref:System.ServiceModel.Description.IEndpointBehavior?displayProperty=fullName>，或<xref:System.ServiceModel.Description.IContractBehavior?displayProperty=fullName>接口取决于您希望在其中轻松插入服务消息检查器的范围。  
  
3.  调用前，插入行为<xref:System.ServiceModel.ICommunicationObject.Open%2A?displayProperty=fullName>方法<xref:System.ServiceModel.ServiceHost?displayProperty=fullName>。 有关详细信息，请参阅[配置和扩展的运行时行为带有](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md)。  
  
## <a name="example"></a>示例  
 下面的代码示例按顺序演示以下各项：  
  
-   服务检查器实现。  
  
-   插入检查器的服务行为。  
  
-   在服务应用程序中加载和运行该行为的配置文件。  
  
 [!code-csharp[Interceptors#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/interceptors/cs/interceptors.cs#7)]
 [!code-vb[Interceptors#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/interceptors/vb/interceptors.vb#7)]  
  
 [!code-csharp[Interceptors#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/interceptors/cs/insertingbehaviors.cs#8)]
 [!code-vb[Interceptors#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/interceptors/vb/insertingbehaviors.vb#8)]  
  
 <!-- TODO: review snippet reference [!code[Interceptors#9](../../../../samples/snippets/common/VS_Snippets_CFX/interceptors/common/hostapplication.exe.config#9)]  -->
 <!-- TODO: review snippet reference [!code-csharp[Interceptors#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/interceptors/cs/hostapplication.exe.config#9)]  -->
 <!-- TODO: review snippet reference [!code-vb[Interceptors#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/interceptors/vb/hostapplication.exe.config#9)]  -->  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.ServiceModel.Dispatcher.IClientMessageInspector?displayProperty=fullName>   
 <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector?displayProperty=fullName>   
 [配置和扩展运行时使用行为](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md)